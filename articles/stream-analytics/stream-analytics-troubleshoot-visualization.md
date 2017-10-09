---
title: aaaVisualize en Stream Analytics-taken oplossen | Microsoft Docs
description: Meer informatie over hoe toovisualize een Stream Analytics-taak voor het oplossen van problemen met de Hallo diagnostics diagram functie selfservice pipeline.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualiseren en Stream Analytics-taken oplossen
In de Stream Analytics, net als bij andere technologieën cloud-gebaseerde is probleemoplossing het soms nodig toolook in waarom een taak geen levert uitvoer verwacht hello (of geen uitvoer eigenlijk). Daarom biedt Stream Analytics Hallo mogelijkheid voor het visualiseren van een streaming-taak. Dit is ook handig als een hulpmiddel voor het modelleren en Hallo side voordeel voor de documentatie van hun werk dat vereist is.

In Hallo visualisatie Configuratiescherm Hallo invoer is zichtbaar evenals Hallo-query wordt uitgevoerd en vervolgens alle Hallo uitvoerwaarden geconfigureerd. - Of configuratieproblemen problemen kunnen duidelijker en is ook handig toosee een visuele representatie van uw configuratie.

## <a name="using-hello-diagnosis-diagram-tool"></a>Het hulpprogramma voor Hallo diagnose diagram
Deze visualizer, klikt u op de knop 'Diagnose diagram' in Hallo tooaccess Hallo blade 'Instellingen' Hallo van Hallo Stream Analytics-taak.

![Stream-Analytics-Troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Alle invoer en uitvoer is kleurcode tooindicate Hallo huidige status van dit onderdeel, zoals hieronder wordt weergegeven.

![Stream-Analytics-Troubleshoot-visualization-Input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Wanneer Hallo gebruiker wil toolook op tussenliggende stappen toounderstand Hallo gegevensstroom querypatronen binnen een taak, biedt Hallo visualisatie hulpprogramma een weergave van Hallo uitsplitsing van Hallo query in de component stappen en Hallo stroom sequence. Te klikken op elke stap van de query, wordt de bijbehorende sectie Hallo in een query bewerken deelvenster zoals geïllustreerd weergeven. 

![Stream-Analytics-Troubleshoot-visualization-Intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

