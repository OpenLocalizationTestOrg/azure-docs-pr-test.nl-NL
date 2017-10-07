---
title: AAA Azure Stream Analytics gegevensgestuurde foutopsporing met behulp van Hallo taak diagram | Microsoft Docs
description: De Stream Analytics-taak oplossen met behulp van Hallo taak diagram en metrische gegevens.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Gegevensgestuurde foutopsporing met behulp van Hallo taak diagram

Hallo taak diagram op Hallo **bewaking** blade in hello Azure-portal kunt u uw pijplijn taak visualiseren. Deze bevat invoer, uitvoer en querystappen. U kunt Hallo taak diagram tooexamine Hallo metrische gegevens voor elke stap, toomore isoleren snel Hallo bron van een probleem opgetreden bij het oplossen van problemen.

## <a name="using-hello-job-diagram"></a>Met behulp van Hallo taak diagram

In hello Azure-portal, terwijl in een Stream Analytics-taak onder **ondersteuning + probleemoplossing**, selecteer **taak diagram**:

![Diagram van de taak met metrische gegevens - locatie](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Selecteer elke stap toosee Hallo overeenkomende gedeelte query in een query deelvenster bewerken. Een metriek grafiek voor Hallo stap wordt weergegeven in een onderste deelvenster op Hallo pagina.

![Diagram van de taak met metrische gegevens - basic taak](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Selecteer toosee Hallo partities van hello Azure Event Hubs-invoer, **...** Een contextmenu wordt weergegeven. U kunt ook Hallo invoer fusie zien.

![Diagram van de taak met metrische gegevens - partitie uitbreiden](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

toosee hello metrische grafiek voor slechts één partitie, selecteer Hallo partitie knooppunt. Hallo metrische gegevens worden weergegeven onder Hallo van Hallo pagina.

![Diagram van de taak met metrische gegevens - meer metrische gegevens](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

toosee hello grafiek metrische gegevens voor een fusie, selecteer Hallo fusie knooppunt. Hallo volgende diagram ziet u dat er geen gebeurtenissen zijn verwijderd of gewijzigd.

![Diagram van de taak met metrische gegevens - raster](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

details van de toosee Hallo Hallo metrische waarde en de tijd, punt toohello grafiek.

![Taak diagram met metrische gegevens: houd de muisaanwijzer](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Problemen oplossen met behulp van de metrische gegevens

Hallo **QueryLastProcessedTime** metriek geeft aan wanneer de gegevens voor het ontvangen van een specifieke stap. Door te kijken Hallo-topologie, kunt u achterwaarts werken van Hallo uitvoer processor toosee stap niet van gegevens ontvangen is. Als een stap niet van gegevens ophalen is, gaat u toohello query stap net vóór. Controleer of hello voorgaande query stap heeft een tijdvenster en of u voldoende tijd is verstreken voor toooutput gegevens. (Let op dat moment windows uitgelijnde toohello uur zijn.)
 
Als hello voorgaande query stap een invoer-processor, gericht gebruik Hallo invoer metrische gegevens toohelp antwoord Hallo volgende vragen. Ze kunnen u helpen bepalen of een taak is ophalen van gegevens uit de invoerbronnen. Als het Hallo-query is gepartitioneerd, controleert u elke partitie.
 
### <a name="how-much-data-is-being-read"></a>Hoeveel gegevens wordt gelezen?

*   **InputEventsSourcesTotal** is het aantal eenheden lezen Hallo. Bijvoorbeeld, Hallo aantal blobs.
*   **InputEventsTotal** is Hallo aantal gebeurtenissen dat is gelezen. Deze metrische waarde is beschikbaar per partitie.
*   **InputEventsInBytesTotal** Hallo aantal gelezen bytes is.
*   **InputEventsLastArrivalTime** is bijgewerkt met de tijd van elke ontvangen gebeurtenis in de wachtrij.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Is tijd vooruitgang? Als feitelijke gebeurtenissen worden gelezen, kan interpunctie niet worden verleend.

*   **InputEventsLastPunctuationTime** geeft aan wanneer een interpunctie tookeep tijd verplaatsen is uitgegeven doorsturen. Als interpunctie niet wordt verleend, kan gegevensstroom ophalen geblokkeerd.
 
### <a name="are-there-any-errors-in-hello-input"></a>Zijn er fouten in de Hallo invoer?

*   **InputEventsEventDataNullTotal** is een aantal van gebeurtenissen die null-gegevens.
*   **InputEventsSerializerErrorsTotal** is het aantal gebeurtenissen dat kan niet correct worden gedeserialiseerd.
*   **InputEventsDegradedTotal** is een aantal van gebeurtenissen die een probleem gehad andere dan met deserialisatie.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Worden gebeurtenissen verwijderd of aangepast?

*   **InputEventsEarlyTotal** is Hallo aantal gebeurtenissen die een tijdstempel van de toepassing voordat de bovengrens Hallo hebben.
*   **InputEventsLateTotal** is het aantal gebeurtenissen die gedurende de tijdstempel van een toepassing na de bovengrens Hallo hebben Hallo.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** Hallo aantal gebeurtenissen verwijderd voordat de begintijd van taak Hallo is.
 
### <a name="are-we-falling-behind-in-reading-data"></a>We dalen achter bij het lezen van gegevens?

*   **InputEventsSourcesBackloggedTotal** wordt aangegeven hoeveel meer berichten toobe moeten lezen voor Event Hubs en Azure IoT Hub-invoer.


## <a name="get-help"></a>Help opvragen
Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooStream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor stream Analytics query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics management REST API-referentiemateriaal](https://msdn.microsoft.com/library/azure/dn835031.aspx)
