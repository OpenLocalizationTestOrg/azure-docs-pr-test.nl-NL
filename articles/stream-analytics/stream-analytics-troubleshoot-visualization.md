---
title: Visualiseren en Stream Analytics-taken oplossen | Microsoft Docs
description: Ontdek hoe u een pijplijn Stream Analytics-taak voor self-service het oplossen van problemen met de functie voor het diagram van diagnostische gegevens te visualiseren.
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
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="502e3-103">Visualiseren en Stream Analytics-taken oplossen</span><span class="sxs-lookup"><span data-stu-id="502e3-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="502e3-104">In de Stream Analytics, net als bij andere technologieën cloud-gebaseerde is probleemoplossing soms nodig te onderzoeken waarom een taak geen levert de verwachte uitvoer (of eigenlijk uitvoer).</span><span class="sxs-lookup"><span data-stu-id="502e3-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="502e3-105">Daarom biedt Stream Analytics de mogelijkheid voor het visualiseren van een streaming-taak.</span><span class="sxs-lookup"><span data-stu-id="502e3-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="502e3-106">Dit is ook handig als een hulpmiddel voor het modelleren en heeft het voordeel aan clientzijde voor deze vereisen documentatie van hun werk.</span><span class="sxs-lookup"><span data-stu-id="502e3-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="502e3-107">De invoer is in het deelvenster visualisatie zichtbaar evenals de query wordt uitgevoerd en vervolgens alle de uitvoer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="502e3-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="502e3-108">- Of configuratieproblemen problemen kunnen duidelijker en kan ook handig om te zien van een visuele representatie van uw configuratie zijn.</span><span class="sxs-lookup"><span data-stu-id="502e3-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="502e3-109">Hulpprogramma voor het diagnose diagram</span><span class="sxs-lookup"><span data-stu-id="502e3-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="502e3-110">Voor toegang tot deze visualizer, klikt u op de knop 'Diagnose diagram' op de blade 'Instellingen' van de van de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="502e3-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![Stream-Analytics-Troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="502e3-112">Alle invoer en uitvoer is kleurcode om aan te geven van de huidige status van dit onderdeel, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="502e3-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="502e3-114">Wanneer de gebruiker wil om te kijken naar tussenliggende querystappen om te begrijpen van het patroon van de gegevensstroom binnen een taak, biedt het hulpprogramma visualisatie een weergave van de uitsplitsing van de query in de bijbehorende stappen onderdeel en de volgorde van de stroom.</span><span class="sxs-lookup"><span data-stu-id="502e3-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="502e3-115">Op elke stap van de query te klikken, wordt de bijbehorende sectie in een query bewerken deelvenster zoals wordt geïllustreerd weergeven.</span><span class="sxs-lookup"><span data-stu-id="502e3-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![Stream-Analytics-Troubleshoot-visualization-Intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="502e3-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="502e3-117">Next steps</span></span>
* [<span data-ttu-id="502e3-118">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502e3-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="502e3-119">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502e3-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="502e3-120">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="502e3-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="502e3-121">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="502e3-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="502e3-122">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="502e3-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

