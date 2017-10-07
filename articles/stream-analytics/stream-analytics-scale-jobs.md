---
title: aaaScale Stream Analytics-taken tooincrease doorvoer | Microsoft Docs
description: Meer informatie over hoe tooscale Stream Analytics-taken op invoer partities configureren, Hallo querydefinitie afstemmen en instellen van taak streaming-eenheden.
keywords: gegevens streaming afstemmen analytics streaming gegevensverwerking,
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Scale Azure Stream Analytics-taken tooincrease stroom gegevensverwerking doorvoer
Dit artikel laat zien hoe tootune een Stream Analytics query tooincrease doorvoer voor Streaming Analytics-taken. U leert hoe tooscale Stream Analytics taken door invoer partities configureren en berekenen en het instellen van taak afstemmen Hallo analytics querydefinitie *streamingeenheden* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Wat zijn de onderdelen van een Stream Analytics-taak Hallo?
De definitie van een Stream Analytics-taak bevat invoer, een query- en uitvoer. Invoer is waar Hallo taak leest Hallo-gegevensstroom uit. Hallo query is gebruikte tootransform Hallo gegevens invoerstroom en Hallo uitvoer is waar Hallo taak Hallo taak resultaten verzendt.  

Een taak vereist ten minste één invoerbron voor het streamen van gegevens. Hallo kan invoerbron van de gegevensstroom worden opgeslagen in een Azure event hub of in Azure blob-opslag. Zie voor meer informatie [inleiding tooAzure Stream Analytics](stream-analytics-introduction.md) en [aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partities in event hubs en Azure-opslag
Schalen van een Stream Analytics-taak maakt gebruik van partities in Hallo invoer of uitvoer. Hiermee kunt die u gegevens in op basis van een partitiesleutel subsets verdelen partitioneren. Een proces dat Hallo-gegevens (zoals een Streaming Analytics-taak verbruikt) kunt gebruiken en het schrijven van verschillende partities parallel verhoogt de doorvoer. Wanneer u met Streaming Analytics werkt, kunt u profiteren van partitionering in event hubs en in de Blob-opslag. 

Zie voor meer informatie over partities Hallo artikelen te volgen:

* [Overzicht van Event Hubs-functies](../event-hubs/event-hubs-features.md#partitions)
* [Partitioneren van gegevens](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Streaming-eenheden (SUs)
Streaming-eenheden (SUs) vertegenwoordigen Hallo bronnen en rekenkracht die vereist zijn in volgorde van tooexecute een Azure Stream Analytics-taak. SUs bieden een manier toodescribe Hallo relatieve gebeurtenisverwerking capaciteit op basis van een gecombineerde meting van CPU, geheugen, en lezen en schrijven tarieven. Elke SU overeenkomt met tooroughly 1 MB per seconde van doorvoer. 

Hoeveel SUs kiezen zijn vereist voor een bepaalde taak is afhankelijk van Hallo partitieconfiguratie voor Hallo invoer en gedefinieerd voor de taak Hallo Hallo-query. U kunt selecteren van tooyour quotum in SUs voor een taak. Elk Azure-abonnement heeft standaard een quotum van up too50 SUs voor alle Hallo analytics-taken in een specifieke regio. tooincrease SUs voor uw abonnementen buiten dit quotum, neem contact op met [Microsoft Support](http://support.microsoft.com). Geldige waarden voor SUs per taak zijn 1, 3, 6, en omhoog in stappen van 6.

## <a name="embarrassingly-parallel-jobs"></a>Perfect parallelle taken
Een *perfect parallelle* taak is de meest schaalbare scenario Hallo we in Azure Stream Analytics hebben. Deze verbinding maakt met één partitie van Hallo invoer tooone exemplaar van Hallo query tooone partitie van Hallo uitvoer. Deze parallelle uitvoering heeft Hallo volgens de vereisten:

1. Als uw query logica is afhankelijk van Hallo sleutel wordt verwerkt door Hallo query dezelfde exemplaar, moet u ervoor zorgen dat het Hallo-gebeurtenissen toohello gaan dezelfde partitie van uw invoer. Voor event hubs, dit betekent dat de gebeurtenisgegevens Hallo moet Hallo **PartitionKey** waarde ingesteld. U kunt ook de gepartitioneerde afzenders gebruiken. Voor blob-opslag, betekent dit dat dat Hallo gebeurtenissen toohello worden verzonden dezelfde partitie map. Als uw query logica vereist geen Hallo sleutel toobe verwerkt door Hallo dezelfde exemplaar opvragen, kunt u deze vereiste negeren. Een voorbeeld van deze logica is een eenvoudige select-project-filter-query.  

2. Zodra het Hallo-gegevens worden verspreid Hallo invoer zijde, moet u ervoor zorgen dat uw query is gepartitioneerd. Hiervoor moet u toouse **Partition By** in alle Hallo stappen. Meerdere stappen zijn toegestaan, maar ze alle moeten worden gepartitioneerd door Hallo dezelfde sleutel. Op dit moment Hallo partitiesleutel te moet worden ingesteld**PartitionId** om Hallo taak toobe volledig parallelle.  

3. Alleen event hubs en blob-opslag ondersteund gepartitioneerde uitvoer. Event hub-uitvoer, moet u configureren Hallo partitie sleutel toobe **PartitionId**. Voor blob storage-uitvoer hebt u geen toodo alles.  

4. het aantal invoer partities Hallo moet gelijk zijn aan Hallo aantal partities van de uitvoer. BLOB storage uitvoer ondersteunt momenteel geen partities. Maar dat is geen probleem, omdat deze Hallo partitieschema van Hallo upstream-query. Hier volgen voorbeelden van waarden van partitie waarmee een volledig parallelle taak:  

   * 8 event hub invoer partities en 8 event hub uitvoer partities
   * 8 event hub invoer partities en uitvoer van blob-opslag  
   * 8 blob storage invoer partities en uitvoer van blob-opslag  
   * 8 blob-opslag invoer partities en 8 uitvoer partities van de event hub  

Hallo volgende secties worden enkele voorbeeldscenario's die perfect parallelle zijn.

### <a name="simple-query"></a>Eenvoudige query

* Invoer: Event hub, met 8 partities
* Uitvoer: Event hub, met 8 partities

Query:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Deze query is een eenvoudige filter. We hebben daarom tooworry over partitioneren Hallo invoer die toohello event hub worden verzonden. U ziet dat Hallo-query bevat **partitie door PartitionId**, zodat deze voldoet aan vereiste #2 van eerder. Hallo-uitvoer moet tooconfigure Hallo event hub-uitvoer in Hallo taak toohave Hallo partitie sleutelset te**PartitionId**. Een laatste controle is toomake ervoor dat het aantal invoer partities Hallo gelijk toohello aantal partities van de uitvoer.

### <a name="query-with-a-grouping-key"></a>Query's uitvoeren met een groeperingssleutel

* Invoer: Event hub, met 8 partities
* Uitvoer: Blob-opslag

Query:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Deze query heeft een groeperingssleutel. Daarom Hallo dezelfde sleutel behoeften toobe door Hallo dezelfde query exemplaar, wat betekent dat gebeurtenissen moeten worden verzonden toohello event hub in een gepartitioneerde wijze verwerkt. Maar welke sleutel moet worden gebruikt? **PartitionId** een concept taak logica. Hallo sleutel daadwerkelijk belangrijk voor ons is **TollBoothId**, dus Hallo **PartitionKey** waarde Hallo gebeurtenisgegevens moet **TollBoothId**. We dit doen in Hallo query door **Partition By** te**PartitionId**. Omdat Hallo uitvoer blobopslag, moeten we niet tooworry over het configureren van een waarde voor de partitiesleutel, volgens de vereiste #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Meerdere stappen query met een groeperingssleutel
* Invoer: Event hub, met 8 partities
* Uitvoer: Event hub-instantie met 8 partities

Query:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Deze query heeft een groeperingssleutel, zodat dezelfde sleutel behoeften toobe verwerkt door Hallo Hallo hetzelfde exemplaar van de query. We kunnen gebruiken dezelfde strategie zoals in het vorige voorbeeld Hallo Hallo. In dit geval heeft Hallo query meerdere stappen. Elke stap heeft **partitie door PartitionId**? Ja, dus Hallo query voldaan aan de vereiste #3. Hallo-uitvoer moet tooset Hallo partitiesleutel te**PartitionId**, zoals eerder besproken. Ook ziet u dat er Hallo hetzelfde aantal partities als Hallo-invoer.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Voorbeeldscenario's die zijn *niet* perfect parallelle

In de vorige sectie hello bleek we enkele perfect parallelle scenario's. In deze sectie bespreken we scenario's die niet voldoen aan vereisten toobe alle Hallo perfect parallelle. 

### <a name="mismatched-partition-count"></a>Aantal niet-overeenkomende partities
* Invoer: Event hub, met 8 partities
* Uitvoer: Event hub met 32 partities

In dit geval wordt het maakt niet uit welke Hallo-query is. Als Hallo invoer partitie aantal komt niet overeen met de Hallo uitvoer partitie count, Hallo topologie niet perfect parallelle.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Geen gebruikmaakt van event hubs of blob-opslag als uitvoer
* Invoer: Event hub, met 8 partities
* Uitvoer: Power BI

Power BI-uitvoer ondersteunt momenteel geen partitioneren. Dit scenario is daarom niet perfect parallelle.

### <a name="multi-step-query-with-different-partition-by-values"></a>De query meerdere stappen met verschillende waarden voor Partition By
* Invoer: Event hub, met 8 partities
* Uitvoer: Event hub, met 8 partities

Query:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Zoals u ziet, gebruikmaakt van de tweede stap Hallo **TollBoothId** als partitiesleutel Hallo. Deze stap is dezelfde niet Hallo als eerste stap hello, en daarom vereist ons toodo een willekeurige volgorde. 

Hallo voorgaande voorbeelden ziet u enkele Stream Analytics-taken die een perfect parallelle topologie te voldoen (of niet). Als die in overeenstemming zijn, hebben ze Hallo mogelijkheden voor maximale schaal. Voor taken die niet voldoen aan een van deze profielen schalen richtlijnen beschikbaar in toekomstige zijn updates. Op dit moment gebruiken Hallo algemene richtlijnen in Hallo uit te voeren.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Hallo maximale streaming-eenheden van een taak berekenen
Totaal aantal streaming-eenheden die kunnen worden gebruikt door een Stream Analytics-taak Hallo is afhankelijk van Hallo aantal stappen in Hallo query gedefinieerd voor het Hallo-taak en Hallo aantal partities voor elke stap.

### <a name="steps-in-a-query"></a>De stappen in een query
Een query kan één of meerdere stappen hebben. Elke stap bestaat uit een subquery die zijn gedefinieerd door Hallo **WITH** sleutelwoord. Hallo-query die buiten Hallo **WITH** sleutelwoord (slechts één query) ook wordt beschouwd als een stap, zoals Hallo **Selecteer** instructie in de volgende query Hallo:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Deze query bestaat uit twee stappen.

> [!NOTE]
> Deze query wordt later in Hallo artikel nader besproken.
>  

### <a name="partition-a-step"></a>Een stap partitioneren
Een stap partitioneren vereist Hallo volgende voorwaarden:

* de invoerbron Hallo moet worden gepartitioneerd. 
* Hallo **Selecteer** -instructie van Hallo query moet lezen van een gepartitioneerde invoerbron.
* Hallo query binnen Hallo stap Hallo moet hebben **Partition By** sleutelwoord.

Wanneer een query is gepartitioneerd, Hallo invoervelden zijn verwerkt en geaggregeerde in afzonderlijke partitiegroepen en uitvoer gebeurtenissen worden gegenereerd voor elk van de groepen Hallo. Als u een gecombineerde aggregaat wilt, moet u een tweede stap niet-gepartitioneerde tooaggregate maken.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Hallo max streaming-eenheden voor een taak berekenen
Alle niet-gepartitioneerde stappen kunnen samen opschalen toosix streaming-eenheden (SUs) voor een Stream Analytics-taak. SUs tooadd, een stap moeten worden gepartitioneerd. Elke partitie kan zes SUs hebben.

<table border="1">
<tr><th>Query’s uitvoeren</th><th>Maximale SUs voor Hallo-taak</th></td>

<tr><td>
<ul>
<li>Hallo-query bevat één stap.</li>
<li>Hallo stap niet is gepartitioneerd.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Hallo invoergegevens stream is gepartitioneerd met 3.</li>
<li>Hallo-query bevat één stap.</li>
<li>Hallo stap is gepartitioneerd.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>Hallo-query bevat twee stappen.</li>
<li>Geen van de stappen Hallo is gepartitioneerd.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Hallo invoergegevens stream is gepartitioneerd met 3.</li>
<li>Hallo-query bevat twee stappen. Hallo invoer stap is gepartitioneerd en Hallo tweede stap bestaat niet.</li>
<li>Hallo <strong>Selecteer</strong> instructie leest uit Hallo gepartitioneerd invoer.</li>
</ul>
</td>
<td>24 (18 voor gepartitioneerde stappen) + 6 voor niet-gepartitioneerde stappen</td></tr>
</table>

### <a name="examples-of-scaling"></a>Voorbeelden van schaal

Hallo berekent volgende query Hallo aantal auto's binnen een drie minuten een gratis-station met drie tollbooths doorlopen. Deze query kan worden uitgebreid toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

meer toouse SUs voor Hallo query, zowel de stroom inkomende gegevens Hallo en Hallo query moet worden gepartitioneerd. Omdat Hallo gegevensstroom partitie is too3 ingesteld, kan hello volgende gewijzigde query worden uitgebreid too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Wanneer een query is gepartitioneerd, worden de invoervelden Hallo verwerkt en geaggregeerd in een afzonderlijke partitiegroepen. Uitvoergebeurtenissen worden ook gegenereerd voor elk van Hallo groepen. Partitioneren kan leiden tot enige onverwachte resultaten hello **GROUP BY** veld is niet de partitiesleutel Hallo in Hallo invoergegevens stroom. Bijvoorbeeld, Hallo **TollBoothId** veld in de vorige query Hallo is niet de partitiesleutel Hallo van **Input1**. Hallo-resultaat is dat Hallo gegevens van tolhuisje #1 in meerdere partities kunnen worden verspreid.

Elk Hallo **Input1** partities afzonderlijk wordt verwerkt door de Stream Analytics. Als gevolg hiervan Hallo meerdere records van het Hallo auto aantal voor dezelfde tolhuisje in Hallo dezelfde tumblingvenster wordt gemaakt. Als de invoer partitiesleutel Hallo kan niet worden gewijzigd, kan dit probleem worden opgelost door een niet-partitie stap, zoals in het volgende voorbeeld Hallo toe te voegen:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Deze query kan worden geschaald too24 SUs.

> [!NOTE]
> Als u van twee streams samenvoegen, ervoor zorgen dat Hallo stromen worden gepartitioneerd met de partitiesleutel Hallo van Hallo kolom toocreate Hallo joins te gebruiken. Controleer ook of u hebt Hallo hetzelfde aantal partities in beide stromen.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Configureren van de Stream Analytics streaming-eenheden

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Vinden in de lijst met resources Hallo Hallo Stream Analytics-taak dat u wilt dat tooscale en het open.
3. Taak in Hallo blade onder **configureren**, klikt u op **Scale**.

    ![Azure Stream Analytics-taak Portalconfiguratie][img.stream.analytics.preview.portal.settings.scale]

4. Gebruik Hallo schuifregelaar tooset Hallo SUs voor Hallo-taak. U ziet dat u beperkte toospecific SU-instellingen.


## <a name="monitor-job-performance"></a>Prestaties van de taak controleren
Hello Azure-portal kunt u Hallo doorvoer van een taak volgen:

![Azure Stream Analytics-taken voor monitor][img.stream.analytics.monitor.job]

Hallo verwacht doorvoer van Hallo werkbelasting berekenen. Als Hallo doorvoer kleiner is dan verwacht, Hallo invoer partitie afstemmen, Hallo query afstemmen en SUs tooyour taak toevoegen.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Stream Analytics-doorvoer op grote schaal visualiseren: Hallo frambozen Pi scenario
toohelp die u begrijpt hoe de Stream Analytics-taken schalen, hebben we een experiment op basis van de invoer van een apparaat frambozen Pi uitgevoerd. Dit experiment laat ons zien Hallo effect op de doorvoer van meerdere streaming-eenheden en partities.

In dit scenario wordt met Hallo apparaat sensor gegevens (clients) tooan event hub verzendt. Streaming Analytics Hallo gegevens verwerkt en verzendt een waarschuwing of -statistieken als een output tooanother event hub. 

Hallo-client verzendt sensorgegevens in JSON-indeling. Hallo gegevensuitvoer is ook in JSON-indeling. Hallo gegevens ziet er als volgt:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Hallo na query is gebruikt toosend een waarschuwing wanneer een licht is uitgeschakeld:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Meting doorvoer

In deze context is doorvoer Hallo hoeveelheid invoergegevens verwerkt door de Stream Analytics in een vaste hoeveelheid tijd. (We gemeten voor 10 minuten.) invoergegevens tooachieve Hallo best verwerking doorvoer voor hello, beide Hallo gegevensstroom invoer en Hallo query zijn gepartitioneerd. We opgenomen **COUNT()** in Hallo query toomeasure hoeveel invoervelden zijn verwerkt. toomake ervoor Hallo-taak is gewoon wacht niet invoervelden toocome, elke partitie van Hallo invoer event hub is vooraf geladen met ongeveer 300 MB met invoergegevens.

Hallo toont volgende tabel Hallo resultaten die hebt gezien wanneer we het aantal streaming-eenheden Hallo verhoogd en de overeenkomstige partitie Hallo in event hubs telt.  

<table border="1">
<tr><th>Invoer partities</th><th>Uitvoer partities</th><th>Streamingeenheden</th><th>Volgehouden doorvoer
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4.06 MB/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8.06 MB/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38.32 MB/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172.67 MB/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454.27 MB/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609.69 MB/s</td>
</tr>
</table>

En hello volgende grafiek ziet u een visualisatie van Hallo relatie tussen SUs en doorvoer.

![IMG.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

