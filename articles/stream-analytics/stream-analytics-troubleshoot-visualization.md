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
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="54f5f-103">Visualiseren en Stream Analytics-taken oplossen</span><span class="sxs-lookup"><span data-stu-id="54f5f-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="54f5f-104">In de Stream Analytics, net als bij andere technologieën cloud-gebaseerde is probleemoplossing het soms nodig toolook in waarom een taak geen levert uitvoer verwacht hello (of geen uitvoer eigenlijk).</span><span class="sxs-lookup"><span data-stu-id="54f5f-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="54f5f-105">Daarom biedt Stream Analytics Hallo mogelijkheid voor het visualiseren van een streaming-taak.</span><span class="sxs-lookup"><span data-stu-id="54f5f-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="54f5f-106">Dit is ook handig als een hulpmiddel voor het modelleren en Hallo side voordeel voor de documentatie van hun werk dat vereist is.</span><span class="sxs-lookup"><span data-stu-id="54f5f-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="54f5f-107">In Hallo visualisatie Configuratiescherm Hallo invoer is zichtbaar evenals Hallo-query wordt uitgevoerd en vervolgens alle Hallo uitvoerwaarden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="54f5f-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="54f5f-108">- Of configuratieproblemen problemen kunnen duidelijker en is ook handig toosee een visuele representatie van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="54f5f-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="54f5f-109">Het hulpprogramma voor Hallo diagnose diagram</span><span class="sxs-lookup"><span data-stu-id="54f5f-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="54f5f-110">Deze visualizer, klikt u op de knop 'Diagnose diagram' in Hallo tooaccess Hallo blade 'Instellingen' Hallo van Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="54f5f-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![Stream-Analytics-Troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="54f5f-112">Alle invoer en uitvoer is kleurcode tooindicate Hallo huidige status van dit onderdeel, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="54f5f-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="54f5f-114">Wanneer Hallo gebruiker wil toolook op tussenliggende stappen toounderstand Hallo gegevensstroom querypatronen binnen een taak, biedt Hallo visualisatie hulpprogramma een weergave van Hallo uitsplitsing van Hallo query in de component stappen en Hallo stroom sequence.</span><span class="sxs-lookup"><span data-stu-id="54f5f-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="54f5f-115">Te klikken op elke stap van de query, wordt de bijbehorende sectie Hallo in een query bewerken deelvenster zoals geïllustreerd weergeven.</span><span class="sxs-lookup"><span data-stu-id="54f5f-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![Stream-Analytics-Troubleshoot-visualization-Intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="54f5f-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54f5f-117">Next steps</span></span>
* [<span data-ttu-id="54f5f-118">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54f5f-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="54f5f-119">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54f5f-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="54f5f-120">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="54f5f-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="54f5f-121">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="54f5f-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="54f5f-122">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="54f5f-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

