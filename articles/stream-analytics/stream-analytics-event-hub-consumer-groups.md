---
title: Azure Stream Analytics aaaDebug met event hub-ontvangers | Microsoft Docs
description: Aanbevolen procedures voor het overwegen van Event Hubs consumer-groepen in de Stream Analytics-taken opvragen.
keywords: limiet van Event hub, klantengroep
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Fouten opsporen in Azure Stream Analytics met event hub-ontvangers

U kunt Azure Event Hubs in Azure Stream Analytics tooingest of uitvoer gegevens uit een taak. Is een best practice voor het gebruik van Event Hubs toouse meerdere consumergroepen, tooensure taak schaalbaarheid. Een reden hiervoor is dat het aantal lezers in Stream Analytics-taak voor een specifieke invoer Hallo Hallo betrekking heeft op Hallo aantal lezers in een enkel consumergroep. Hallo exacte aantal ontvangers is gebaseerd op interne implementatiedetails voor Hallo scale-out topologie logica. Hallo aantal ontvangers is extern niet toegankelijk. het aantal lezers Hallo kunt wijzigen tijdens het Hallo taak starten of tijdens upgrades van de taak.

> [!NOTE]
> Wanneer het aantal lezers Hallo gewijzigd tijdens de upgrade van een taak, worden waarschuwingen voor tijdelijke tooaudit Logboeken geschreven. Stream Analytics-taken worden automatisch herstellen van deze problemen van voorbijgaande aard.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Het aantal lezers per partitie overschrijdt de limiet van vijf Event Hubs

Scenario's in welke Hallo het aantal lezers per partitie Hallo Event Hubs limiet van vijf overschrijdt zijn Hallo volgende:

* Meerdere SELECT-instructies: als u meerdere SELECT-instructies die te verwijzen**dezelfde** event hub-invoer, elke SELECT-instructie zorgt ervoor dat een nieuwe ontvanger toobe gemaakt.
* UNION: Wanneer u een UNION gebruikt, is het mogelijk toohave meerdere invoerwaarden die toohello verwijzen **dezelfde** event hub- en groep.
* SELF-join: Wanneer u een SELF JOIN-bewerking gebruikt, is het mogelijk toorefer toohello **dezelfde** event hub meerdere keren.

## <a name="solution"></a>Oplossing

Hallo kunnen volgende best practices verminderen in welke Hallo het aantal lezers per partitie Hallo Event Hubs limiet van vijf overschrijdt scenario's.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Uw query splitsen in meerdere stappen met behulp van een WITH-component

de component WITH Hallo Hiermee geeft u een tijdelijk benoemde resultatenset die kan worden verwezen door een FROM-component in Hallo-query. U definieert Hallo WITH-clausule in Hallo uitvoering bereik van één SELECT-instructie.

Bijvoorbeeld, in plaats van deze query:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Gebruik deze query:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Zorg ervoor dat de invoer toodifferent consumergroepen binden

Voor query's waarin drie of meer invoerwaarden verbonden toohello zijn dezelfde Event Hubs consumer groep, maakt u afzonderlijke consumer-groepen. U moet hiervoor Hallo maken van aanvullende Stream Analytics-invoer.


## <a name="get-help"></a>Help opvragen
Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooStream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor stream Analytics query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)
