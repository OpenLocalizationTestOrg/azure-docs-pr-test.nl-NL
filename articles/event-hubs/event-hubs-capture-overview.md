---
title: aaaOverview van het vastleggen van Azure Event Hubs | Microsoft Docs
description: Vastleggen van telemetriegegevens met Event Hubs vastleggen
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Azure Event Hubs vastleggen

Vastleggen van Azure Event Hubs kunt u tooautomatically afleveren Hallo gegevensstromen in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) of [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account van uw keuze, hello flexibiliteit toegevoegd voor het opgeven van een interval van tijd of grootte. Het instellen van het vastleggen is snel, zijn er geen administratieve kosten toorun en deze schaalt automatisch met Event Hubs [doorvoereenheden](event-hubs-features.md#capacity). Vastleggen van Event Hubs is Hallo gemakkelijkste manier tooload gegevensstromen in Azure, en kunt u toofocus op gegevensverwerking in plaats van op het opnemen van gegevens.

Vastleggen van Event Hubs kunt u realtime tooprocess en pijplijnen op basis van batch op Hallo dezelfde stroom. Dit betekent dat u kunt oplossingen bouwt die groeien met uw behoeften gedurende een bepaalde periode. Of u bij het bouwen van batch-systemen vandaag nog met het oog op toekomstige realtime verwerking of u wilt dat tooadd een efficiënte koude pad tooan bestaande realtime-oplossing, is het vastleggen van Event Hubs werken met gegevensstromen eenvoudiger.

## <a name="how-event-hubs-capture-works"></a>Event Hubs vastleggen werking

Event Hubs is een duurzame buffer tijd bewaren voor telemetrie inkomend, vergelijkbare tooa gedistribueerde logboek. Hallo sleutel tooscaling in Event Hubs is Hallo [gepartitioneerde consumer model](event-hubs-features.md#partitions). Elke partitie is een onafhankelijke segment van gegevens en onafhankelijk is verbruikt. Na verloop van tijd die deze gegevens van jaar uitschakelen op basis van Hallo configureerbare bewaarperiode. Als gevolg hiervan een bepaalde gebeurtenis hub nooit ' te vol raakt. "

U toospecify vastleggen van Event Hubs worden kunt uw eigen Azure Blob storage-account en een container of een Azure Data Lake Store-account, de gebruikte toostore Hallo vastgelegd gegevens. Deze accounts kunnen zich in Hallo dezelfde regio als uw event hub of in een andere regio, toohello flexibiliteit van Event Hubs vastleggen Hallo-functie toe te voegen.

Gegevensopname is geschreven in [Apache Avro] [ Apache Avro] indeling: een compact, snelle, binaire indeling die uitgebreide gegevensstructuren inlineschema biedt. Deze indeling wordt veel gebruikt in de Hadoop-ecosysteem hello, Stream Analytics en Azure Data Factory. Meer informatie over het werken met Avro vindt verderop in dit artikel.

### <a name="capture-windowing"></a>Windowing vastleggen

Vastleggen van Event Hubs kunnen tooset van een venster toocontrol vast te leggen. Dit venster is een minimale grootte en de configuratie van de tijd met een 'eerste WINS-beleid,' wat betekent dat Hallo eerste trigger is aangetroffen, wordt een capture-bewerking. Als u hebt een vijftien minuten, 100 MB venster vastleggen en 1 MB per seconde Hallo grootte venster triggers voordat Hallo tijdvenster. Elke partitie afzonderlijk vastgelegd en schrijft een voltooide blok-blob gelijktijdig Hallo met vastleggen, met de naam van Hallo tijd op welke Hallo vastleggen interval is opgetreden. Hallo opslag naamconventie is als volgt:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Toothroughput eenheden schalen

Event Hubs-verkeer wordt beheerd door [doorvoereenheden](event-hubs-features.md#capacity). Eén doorvoereenheid kunt 1 MB per seconde of 1000 gebeurtenissen per seconde van inkomende en twee keer de omvang van uitgaande gegevens. Standaard Event Hubs kunnen worden geconfigureerd met 1-20 doorvoereenheden en u kunt meer aanschaffen bij een quotum verhogen [ondersteuningsaanvraag][support request]. Gebruik dat buiten uw aangeschafte doorvoereenheden wordt beperkt. Event Hubs vastleggen kopieert gegevens rechtstreeks vanuit Hallo interne Event Hubs opslag voor het overslaan van doorvoer eenheid uitgaande quota en opslaan van uw uitgaande voor andere lezers verwerking zoals Stream Analytics of Spark.

Na de configuratie vastleggen van Event Hubs wordt automatisch uitgevoerd wanneer u uw eerste gebeurtenis verzenden en wordt hervat. toomake het eenvoudiger voor de downstreamverwerking-tooknow die Hallo-proces werkt, Event Hubs lege bestanden schrijft wanneer er geen gegevens zijn. Deze procedure biedt een voorspelbare uitgebracht en de markering die kan worden ingevoerd uw batch-processors.

## <a name="setting-up-event-hubs-capture"></a>Instellen van het vastleggen van Event Hubs

U kunt vastleggen configureren tijdens het Hallo event hub maken met behulp van Hallo [Azure-portal](https://portal.azure.com), of met behulp van Azure Resource Manager-sjablonen. Zie voor meer informatie Hallo artikelen te volgen:

- [Inschakelen van Event Hubs vastleggen met behulp van hello Azure-portal](event-hubs-capture-enable-through-portal.md)
- [Maken van een naamruimte Event Hubs met een event hub en vastleggen met behulp van een Azure Resource Manager-sjabloon inschakelen](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Hallo vastgelegd bestanden verkennen en werken met Avro

Vastleggen van Event Hubs maakt bestanden in de Avro-indeling die is opgegeven op het tijdvenster Hallo geconfigureerd. U kunt deze bestanden weergeven in een hulpprogramma zoals [Azure Opslagverkenner][Azure Storage Explorer]. U kunt downloaden Hallo bestanden lokaal toowork erop.

Hallo-bestanden die zijn geproduceerd door het vastleggen van Event Hubs hebben Hallo Avro-schema te volgen:

![][3]

Een eenvoudige manier tooexplore Avro-bestanden worden met behulp van Hallo [Avro extra] [ Avro Tools] jar van Apache. Na het downloaden van dit jar, ziet u door het uitvoeren van de volgende opdracht Hallo Hallo-schema van een specifiek Avro-bestand:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Met deze opdracht retourneert

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

U kunt ook gebruik van hulpprogramma's voor Avro tooconvert hello tooJSON indeling en andere bewerkingen uitvoeren.

tooperform meer geavanceerde verwerken, downloaden en installeren van Avro voor uw keuze van platform. Hallo er bij uitvoering van dit artikel, zijn implementaties beschikbaar voor C, C++, C\#, Java, NodeJS, Perl, PHP, Python en Ruby.

Apache Avro is voltooid aan de slag-handleidingen voor [Java] [ Java] en [Python][Python]. U kunt ook lezen Hallo [aan de slag met Event Hubs vastleggen](event-hubs-capture-python.md) artikel.

## <a name="how-event-hubs-capture-is-charged"></a>Hoe Event Hubs vastleggen wordt in rekening gebracht

Vastleggen van Event Hubs wordt gemeten op dezelfde manier toothroughput eenheden: als een per uur kosten. Hallo kosten is rechtstreeks evenredig toohello getal voor Hallo naamruimte aangeschafte doorvoereenheden. Als doorvoereenheden worden verhoogd of verlaagd, worden de meters Event Hubs vastleggen verhogen en tooprovide die overeenkomt met de prestaties afnemen. Hallo meters optreden in combinatie. Zie voor prijsinformatie, [prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Volgende stappen

Vastleggen van Event Hubs zijn Hallo gemakkelijkste manier tooget gegevens in Azure. Met Azure Data Lake en Azure Data Factory Azure HDInsight kunt u batchverwerking uitvoeren en andere analyses met behulp van bekende hulpprogramma's en platforms van uw keuze op elke schaal moet u.

U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Aan de slag verzenden en ontvangen van gebeurtenissen](event-hubs-dotnet-framework-getstarted-send.md)
* Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][sample application that uses Event Hubs]
* [Event Hubs-overzicht][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
