---
title: aaaIoT realtime-gegevensstromen en Azure Stream Analytics | Microsoft Docs
description: IoT-sensortags en -gegevensstromen met Stream Analytics en realtime-gegevensverwerking
keywords: IOT-oplossing, aan de slag met iot
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Aan de slag met Azure Stream Analytics tooprocess gegevens van IoT-apparaten
In deze zelfstudie leert u hoe toocreate logica toogather stream-verwerken van gegevens vanaf Internet der dingen (IoT)-apparaten. Gebruiken we een echte, Internet der dingen (IoT) gebruik case toodemonstrate hoe toobuild uw oplossing snel en economisch.

## <a name="prerequisites"></a>Vereisten
* [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/)
* Voorbeeldquery en gegevensbestanden die u kunt downloaden van [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Scenario
Contoso, een bedrijf in Hallo industriële automatisering ruimte is, heeft de fabricageproces volledig geautomatiseerd. Hallo-machines in dit bedrijf hebben sensoren die kunnen tekensetcodering gegevensstromen in realtime. In dit scenario wordt een werkvloerbeheerder realtime inzichten Hallo sensor gegevens toolook toohave wil voor patronen en acties uitvoeren op deze. Hallo Stream Analytics Query Language (SAQL) via Hallo sensor gegevens toofind interessante patronen van Hallo stroom inkomende gegevens zullen worden gebruikt.

Hier worden gegevens gegenereerd met een Texas Instrument Sensor Tag-apparaat.

![Texas Instruments Sensor Tag](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

Hallo-nettolading van het Hallo-gegevens is in JSON-indeling en ziet eruit als Hallo volgende:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

In een werkelijk scenario hebt u honderden van dit soort sensoren die gebeurtenissen als een stroom kunnen genereren. In het ideale geval een gateway-apparaat zou uitvoeren code toopush deze gebeurtenissen te[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) of [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/). Uw Stream Analytics-taak zou deze gebeurtenissen van Event Hubs voor opnemen en realtime-analyses query's uitvoeren op Hallo stromen. Vervolgens u Hallo resultaten tooone Hallo kan verzenden [uitvoer ondersteund](stream-analytics-define-outputs.md).

Voor het gebruiksgemak biedt deze introductiehandleiding een bestand met voorbeeldgegevens dat is verkregen uit echte Sensor Tag-apparaten. U kunt query's uitvoeren op Hallo voorbeeldgegevens en resultaten te zien. In volgende zelfstudies leert u hoe tooconnect uw taak tooinputs en uitvoer en deze toohello Azure-service te implementeren.

## <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken
1. In Hallo [Azure-portal](http://portal.azure.com), klikt u op het plusteken Hallo en typ vervolgens **STREAM ANALYTICS** in Hallo venster toohello rechts. Selecteer vervolgens **Stream Analytics-taak** in de lijst met resultaten Hallo.
   
    ![Een nieuwe Stream Analytics-taak maken](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Voer een unieke naam en controleer of Hallo-abonnement is Hallo juiste is voor uw project. Maak vervolgens een nieuwe resourcegroep of selecteer een bestaande in uw abonnement.
3. Selecteer een locatie voor uw taak. Voor de snelheid van verwerking en vermindering van de kosten in gegevensoverdracht selecteren Hallo wordt dezelfde locatie als de resourcegroep Hallo en beoogde storage-account aanbevolen.
   
    ![Details van het maken van een nieuwe Stream Analytics-taak](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > U maakt dit opslagaccount slechts één keer per regio. Deze opslag wordt gedeeld tussen alle Stream Analytics-taken die zijn gemaakt in deze regio.
   > 
   > 
4. Hallo vak tooplace Controleer uw taak op uw dashboard en klik vervolgens op **maken**.
   
    ![taak wordt gemaakt](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Er is een 'implementatie gestart...' hello rechtsboven van uw browservenster weergegeven. Snel verandert deze venster tooa voltooid zoals hieronder wordt weergegeven.
   
    ![taak wordt gemaakt](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Een Azure Stream Analytics-query maken
Nadat de taak is gemaakt van de tijd tooopen en build een query. Eenvoudig kunt u uw taak openen door te klikken op de tegel Hallo voor.

![Taaktegel](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

In Hallo **taak topologie** deelvenster te klikken op Hallo **QUERY** vak toogo toohello Query-Editor. Hallo **QUERY** editor kunt u tooenter een T-SQL-query die Hallo transformatie via Hallo inkomende gebeurtenisgegevens uitvoert.

![Queryvak](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Query: de onbewerkte gegevens archiveren
Hallo meest eenvoudige vorm van query is een Pass Through-query waarmee alle invoergegevens tooits aangewezen uitvoer archiveert. Hallo voorbeeldgegevensbestand van downloaden [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa locatie op de computer. 

1. Hallo-query uit Hallo PassThrough.txt bestand plakken. 
   
    ![Test invoerstroom](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Klik op Hallo drie punten volgende tooyour invoer en selecteer **voorbeeldgegevens uit bestand uploaden** vak.
   
    ![Test invoerstroom](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Een venster wordt geopend op Hallo rechts als gevolg hiervan, in het Selecteer Hallo Hallowereldasa InputStream.json gegevens vanaf de locatie van het gedownloade bestand en klik op **OK** Hallo Hallo deelvenster onderaan in.
   
    ![Test invoerstroom](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Klik vervolgens op Hallo **testen** stemmen in Hallo bovenste venster Hallo links en verwerken van uw testquery op Hallo voorbeeldgegevensset. Een venster wordt geopend hieronder uw query Hallo verwerken is voltooid.
   
    ![Testresultaten](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Query: Hallo gegevens filteren op basis van een voorwaarde
We gaan toofilter Hallo resultaten op basis van een voorwaarde. Willen we graag tooshow resultaten voor de gebeurtenissen die afkomstig zijn van 'sensorA'. Hallo-query is in Hallo Filtering.txt-bestand.

![Een gegevensstroom filteren](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Houd er rekening mee dat Hallo hoofdlettergevoelig query vergelijkt een string-waarde. Klik op Hallo **Test** stemmen opnieuw tooexecute Hallo query. Hallo-query moet 389 rijen van de 1860 gebeurtenissen worden geretourneerd.

![Tweede uitvoerresultaten van querytest](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Query: Een zakelijke werkstroom een waarschuwing tootrigger
We gaan onze query gedetailleerder maken. Voor elk type sensor, we wilt toomonitor gemiddelde temperatuur per 30 seconden venster en resultaten alleen weergegeven als Hallo gemiddelde temperatuur hoger dan 100 graden is. We zullen schrijven Hallo volgende query uitvoeren op en klik vervolgens op **Test** toosee Hallo resultaten. Hallo-query is in Hallo ThresholdAlerting.txt-bestand.

![30-secondenfilterquery](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

U ziet nu de resultaten nog maar 245 rijen en namen van sensoren bevatten waarbij Hallo gemiddelde temperatuur aangeven groter is dan 100. Deze query groepen Hallo stroom gebeurtenissen door **dspl**, namelijk Hallo sensornaam, meer dan een **Tumblingvenster** van 30 seconden. Tijdelijke query's moeten worden vermeld hoe we tijd tooprogress wilt. Met behulp van Hallo **TIMESTAMP BY** component, hebben we Hallo opgegeven **OUTPUTTIME** kolom tooassociate tijden met alle tijdelijke berekeningen. Voor gedetailleerde informatie leest u Hallo MSDN artikelen over [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing functies](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Query: detecteren van afwezigheid van gebeurtenissen
Hoe kunnen we van een query toofind een gebrek aan invoervelden schrijven? We vinden Hallo laatste keer dat een sensor gegevens verzonden en vervolgens geen gebeurtenissen voor Hallo volgende minuut verzonden heeft. Hallo-query is in Hallo AbsenseOfEvent.txt-bestand.

![Detecteren van afwezigheid van gebeurtenissen](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Hier gebruiken we een **LEFT OUTER** join toohello dezelfde gegevensstroom (self-join). Voor een **INNER**-join wordt alleen een resultaat geretourneerd wanneer een overeenkomst is gevonden.  Voor een **LEFT OUTER** join als een gebeurtenis van Hallo linkerkant Hallo join niet-overeenkomende is, een rij die NULL heeft voor alle kolommen van de rechterkant Hallo Hallo geretourneerd. Deze techniek is zeer nuttig toofind een afwezigheid van gebeurtenissen. Raadpleeg onze MSDN-documentatie voor meer informatie over [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).

## <a name="conclusion"></a>Conclusie
Hallo-doel van deze zelfstudie is toodemonstrate hoe toowrite verschillende Stream Analytics Query Language-query's en om te zien resulteert in het Hallo-browser. Maar dit slechts een begin. Met Stream Analytics hebt u nog veel meer mogelijkheden. Stream Analytics ondersteunt een groot aantal in- en uitgangen en kan zelfs gebruik functies die in Azure Machine Learning toomake het een krachtig hulpprogramma voor het analyseren van gegevensstromen. U kunt meer informatie over Stream Analytics tooexplore starten met behulp van onze [leeroverzicht](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Voor meer informatie over het toowrite query's Hallo artikel meer informatie over [veelvoorkomende querypatronen](stream-analytics-stream-analytics-query-patterns.md).

