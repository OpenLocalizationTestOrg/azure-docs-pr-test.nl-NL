---
title: voor gebeurtenisverwerking aaaReal tijd met de verwerking van de Stream Analytics-gebeurtenis | Microsoft Docs
description: Meer informatie over hoe een set van Azure-services kan samenwerken voor het inschakelen van de verwerking van realtime-gebeurtenissen en analyses.
keywords: realtime verwerking, verwerking van gebeurtenissen, referentiearchitectuur
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Verwijzen naar architectuur: realtime-gebeurtenissen verwerken met Microsoft Azure Stream Analytics
Hallo referentiearchitectuur voor realtime-gebeurtenissen verwerken met Azure Stream Analytics is beoogde tooprovide een algemene blauwdruk voor het implementeren van een realtime platform als een service (PaaS) stroom verwerken met Microsoft Azure.

## <a name="summary"></a>Samenvatting
Traditioneel zijn analytics-oplossingen gebaseerd op mogelijkheden, zoals ETL (extract, transform, load) en datawarehousing, waarbij gegevens opgeslagen voorafgaande tooanalysis is. Veranderende vereisten, met inbegrip van meer snel binnenkomende gegevens, worden deze bestaande model toohello limiet worden gepusht. Hallo mogelijkheid tooanalyze gegevens binnen zwevend streams voorafgaande toostorage is een oplossing en terwijl het is niet een nieuwe mogelijkheid, Hallo-methode niet algemeen is vastgesteld over alle bedrijfstak verticalen. 

Microsoft Azure biedt een uitgebreide catalogus analytics-technologieën die u kunnen ondersteunen een matrix van de oplossing voor verschillende scenario's en vereisten. Selecteren welke toodeploy Azure-services voor een oplossing voor end-to-end kan lastig Hallo breedte van de offerings gegeven. Dit artikel is ontworpen toodescribe Hallo mogelijkheden en interoperabiliteit van Hallo verschillende Azure-services die ondersteuning bieden voor een gebeurtenis streaming-oplossing. Hierin wordt uitgelegd aantal Hallo scenario's waarin klanten van dit type benadering profiteren kunnen.

## <a name="contents"></a>Inhoud
* Managementsamenvatting
* Inleiding tooReal tijd Analytics
* Toegevoegde waarde van realtime-gegevens in Azure
* Algemene scenario's voor realtime-analyses
* Architectuur en onderdelen
  * Gegevensbronnen
  * Gegevensintegratie laag
  * Realtime-analyses laag
  * Data Storage-laag
  * Presentatie / laag-verbruik
* Conclusie

**Auteur:** Jeroen Feddersen, Solution Architect Datacenter Insights van uitmuntende Microsoft Corporation

**Gepubliceerd:** januari 2015

**Revisie:** 1.0

**Download:** [realtime-gebeurtenissen verwerken met Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

