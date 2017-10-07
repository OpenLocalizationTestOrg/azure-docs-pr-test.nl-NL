---
title: Bewaking van Stream Analytics-taak aaaUnderstanding | Microsoft Docs
description: Informatie over Stream Analytics-taak controleren
keywords: query-monitor
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Bewaking van de Stream Analytics-taak begrijpen en hoe toomonitor query's

## <a name="introduction-hello-monitor-page"></a>Inleiding: pagina Hallo-monitor
Hello Azure-portal beide surface prestatie metrische gegevens die kunnen worden gebruikt toomonitor en de prestaties van uw query en -taak oplossen. toosee deze metrische gegevens, bladeren toohello Stream Analytics-taak u geïnteresseerd bent in de metrische gegevens voor weergave Hallo zien **bewaking** sectie op de pagina overzicht Hallo.  

![Bewaking van de koppeling](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

Hallo-venster wordt weergegeven, zoals wordt weergegeven:

![Bewakingstaak Dashboard](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Metrische gegevens beschikbaar voor Stream Analytics
| Gegevens                 | Definitie                               |
| ---------------------- | ---------------------------------------- |
| SU % gebruik       | Hallo-gebruik van Hallo Streaming-eenheid toegewezen tooa taak Hallo Scale tabblad in het Hallo-taak. Hierboven, wordt hoge kans dat de verwerking van gebeurtenissen kan worden vertraagd of gestopt Bezig met het of moet deze indicator 80% bereiken. |
| Invoervelden           | De hoeveelheid gegevens die door Hallo Stream Analytics-taak in het aantal gebeurtenissen dat is ontvangen. Dit kan zijn gebruikte toovalidate dat gebeurtenissen toohello invoerbron worden verzonden. |
| Uitvoergebeurtenissen          | De hoeveelheid gegevens die door Hallo Stream Analytics-taak toohello uitvoerdoel, in aantal gebeurtenissen dat is verzonden. |
| Out-van-Order-gebeurtenissen    | Het aantal gebeurtenissen ontvangen volgorde die zijn verwijderd of een aangepaste tijdstempel, op basis van Hallo gebeurtenis ordening beleid gegeven. Dit kan worden beïnvloed door het Hallo-configuratie van Hallo tolerantieperiode geplaatst Out instelling. |
| Conversie van fouten | Het aantal gegevens conversiefouten die door een Stream Analytics-taak. |
| Runtime-fouten         | Totaal aantal Hallo van fouten die tijdens het uitvoeren van een Stream Analytics-taak optreden. |
| Laat invoervelden      | Aantal gebeurtenissen dat binnenkomt laat vanuit Hallo-bron die ofwel verwijderd of hun timestamp is aangepast, op basis van Hallo gebeurtenis ordening beleidsconfiguratie van Hallo laat tolerantieperiode instelling. |
| Aanvragen van functie      | Het aantal aanroepen toohello Azure Machine Learning-functie (indien aanwezig). |
| Mislukte functie aanvragen | Het aantal mislukte Azure Machine Learning-functieaanroepen (indien aanwezig). |
| Gebeurtenissen voor de functie        | Aantal gebeurtenissen verzonden toohello Azure Machine Learning-functie (indien aanwezig). |
| Invoergebeurtenis Bytes      | De hoeveelheid gegevens die zijn ontvangen door Hallo Stream Analytics-taak, in bytes. Dit kan zijn gebruikte toovalidate dat gebeurtenissen toohello invoerbron worden verzonden. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Bewaking aanpassen in hello Azure-portal
U kunt Hallo type diagram, metrische gegevens weergegeven, aanpassen en tijdsbereik in instellingen voor Hallo grafiek bewerken. Zie voor meer informatie [hoe tooCustomize bewaking](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Query-tijd van de Monitor-grafiek](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

