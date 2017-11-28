---
title: aaaIntroduction tooStream Analytics-vensterfuncties | Microsoft Docs
description: Meer informatie over drie vensterfuncties Hallo in Stream Analytics (tumbling, hopping, Verschuivend).
keywords: venster Verschuivend venster venster hopping tumbling
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="ad9ee-104">Inleiding tooStream Analytics-vensterfuncties</span><span class="sxs-lookup"><span data-stu-id="ad9ee-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="ad9ee-105">In veel realtime streaming-scenario's, is het nodig tooperform bewerkingen alleen op de gegevens in de tijdelijke windows hello.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="ad9ee-106">Systeemeigen ondersteuning voor windowing functies is een belangrijke functie van Azure Stream Analytics die Hallo naald op de productiviteit van ontwikkelaars verplaatst in complexe stroom verwerking taken ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="ad9ee-107">Stream Analytics biedt ontwikkelaars toouse [ **Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) en [ **schuifregelaar** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform tijdelijke bewerkingen op het streamen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="ad9ee-108">Hierbij moet worden opgemerkt dat alle [venster](https://msdn.microsoft.com/library/dn835019.aspx) operations uitvoerresultaten op Hallo **end** van Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="ad9ee-109">Hallo-uitvoer van Hallo-venster worden één gebeurtenis op basis van Hallo statistische functie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="ad9ee-110">Hallo-gebeurtenis heeft Hallo tijdstempel van Hallo einde van Hallo-venster en alle functies van het venster met een vaste lengte zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="ad9ee-111">Ten slotte het is belangrijk toonote die alle functies van het venster moeten worden gebruikt in een [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) component.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Stream Analytics venster werkt concepten](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="ad9ee-113">Tumblingvenster</span><span class="sxs-lookup"><span data-stu-id="ad9ee-113">Tumbling Window</span></span>
<span data-ttu-id="ad9ee-114">Daling vensterfuncties gebruikte toosegment zijn een gegevensstroom in segmenten van verschillende tijd en uitvoeren van een functie hiertegen, zoals Hallo in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="ad9ee-115">de belangrijkste differentiators Hallo van een tumblingvenster zijn dat ze herhalen, elkaar niet overlappen en een gebeurtenis kan niet toomore dan één tumblingvenster behoren.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Stream Analytics-vensterfuncties tumbling intro](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="ad9ee-117">Hoppingvenster</span><span class="sxs-lookup"><span data-stu-id="ad9ee-117">Hopping Window</span></span>
<span data-ttu-id="ad9ee-118">Hopping venster functies hop doorsturen door een vaste periode.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="ad9ee-119">Eenvoudig toothink hiervan als daling vensters die elkaar overlappen kunnen, kan het zijn zodat gebeurtenissen deel van toomore dan Hopping venster resultaat ingesteld uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="ad9ee-120">toomake een venster Hopping Hallo dezelfde als een tumblingvenster geeft een eenvoudig hello hop grootte toobe Hallo dezelfde als Hallo venstergrootte.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Stream Analytics-vensterfuncties hopping intro](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="ad9ee-122">Sliding Window</span><span class="sxs-lookup"><span data-stu-id="ad9ee-122">Sliding Window</span></span>
<span data-ttu-id="ad9ee-123">Verschuivende vensterfuncties, in tegenstelling tot Tumbling of windows, Hopping produceren uitvoer **alleen** wanneer een gebeurtenis zich voordoet.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="ad9ee-124">Elk venster zijn ten minste één gebeurtenis en Hallo venster continu verplaatst doorsturen door een € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="ad9ee-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="ad9ee-125">Net als Windows Hopping kunnen gebeurtenissen toomore dan één venster Verschuivend behoren.</span><span class="sxs-lookup"><span data-stu-id="ad9ee-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Stream Analytics-vensterfuncties Verschuivend intro](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="ad9ee-127">Help opvragen bij vensterfuncties</span><span class="sxs-lookup"><span data-stu-id="ad9ee-127">Getting help with Window functions</span></span>
<span data-ttu-id="ad9ee-128">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="ad9ee-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad9ee-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad9ee-129">Next steps</span></span>
* [<span data-ttu-id="ad9ee-130">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ad9ee-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ad9ee-131">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ad9ee-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ad9ee-132">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="ad9ee-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ad9ee-133">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="ad9ee-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ad9ee-134">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="ad9ee-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

