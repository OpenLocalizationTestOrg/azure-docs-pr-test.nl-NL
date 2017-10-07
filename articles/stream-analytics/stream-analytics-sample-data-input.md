---
title: AAA steekproeven invoer in Azure Stream Analytics | Microsoft Docs
description: Speldenpunt problemen bij het oplossen van Stream Analytics-taken.
keywords: invoer, invoer steekproeven oplossen
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="badfa-104">Azure Stream Analytics invoer-stream steekproeven</span><span class="sxs-lookup"><span data-stu-id="badfa-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="badfa-105">U kunt steekproef nemen invoer gebeurtenissen die afkomstig zijn van een bestand en het testen van query's in Hallo portal zonder toostart of stoppen van een taak met behulp van Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="badfa-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="badfa-106">Uw query testen</span><span class="sxs-lookup"><span data-stu-id="badfa-106">Testing your query</span></span>

<span data-ttu-id="badfa-107">Open in Hallo Stream Analytics-taak detailvenster Hallo **Query-editor** blade door te klikken op de querynaam Hallo onder **Query**.</span><span class="sxs-lookup"><span data-stu-id="badfa-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="badfa-108">(In ons voorbeeldscenario omdat nog geen query is gemaakt, klikt u op Hallo **combinatie** tijdelijke aanduiding.)</span><span class="sxs-lookup"><span data-stu-id="badfa-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![Hallo Stream Analytics query-editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="badfa-110">Net als in de vorige release Hallo Hallo uitgebreide editor blade voor het maken van uw query weergegeven.</span><span class="sxs-lookup"><span data-stu-id="badfa-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="badfa-111">Nu Hallo blade is bijgewerkt met een nieuwe linkerdeelvenster die toont Hallo in- en uitgangen die worden gebruikt door query Hallo en gedefinieerd voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="badfa-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![Hallo Stream Analytics query-editor invoer en uitvoer van lijsten](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="badfa-113">Ook wordt weergegeven, zijn een extra invoer en uitvoer, die niet zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="badfa-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="badfa-114">Ze afkomstig zijn van het nieuwe querysjabloon hello, beginnend met.</span><span class="sxs-lookup"><span data-stu-id="badfa-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="badfa-115">Ze te wijzigen of zelfs verdwijnen helemaal, zoals u Hallo query bewerken.</span><span class="sxs-lookup"><span data-stu-id="badfa-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="badfa-116">U kunt deze gewoon negeren nu.</span><span class="sxs-lookup"><span data-stu-id="badfa-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="badfa-117">tootest met voorbeeldgegevens voor invoer met de rechtermuisknop op een van uw invoer en selecteer vervolgens **voorbeeldgegevens uit bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="badfa-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Hallo Stream Analytics query-editor uploaden voorbeeldgegevens uit bestandsopdracht](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="badfa-119">Nadat het Hallo uploaden is voltooid, klikt u op **Test** tootest deze query op Hallo voorbeeldgegevens u zojuist hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="badfa-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![knop voor Hallo Stream Analytics query-editor testen](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="badfa-121">Als u toosave hello testuitvoer voor later gebruik wilt, worden Hallo resultaten van de query wordt weergegeven in Hallo browser met een koppeling toohello downloadresultaten.</span><span class="sxs-lookup"><span data-stu-id="badfa-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="badfa-122">U kunt nu eenvoudig en iteratief pas uw query en testen herhaaldelijk toosee hoe Hallo uitvoer verandert.</span><span class="sxs-lookup"><span data-stu-id="badfa-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Voorbeelduitvoer van stream Analytics query-editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="badfa-124">In de Hallo voorafgaand aan de installatiekopie, is een tweede uitvoer toegevoegd, aangeroepen **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="badfa-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="badfa-125">Wanneer u meerdere uitgangen in een query gebruikt, kunt u zien Hallo resultaten voor elke uitvoer afzonderlijk en schakelen tussen deze twee.</span><span class="sxs-lookup"><span data-stu-id="badfa-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="badfa-126">Nadat u tevreden met Hallo resultaten bent, kunt u uw query opslaan, uw taak starten, terug zitten en bekijkt hello magie van Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="badfa-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="badfa-127">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="badfa-127">Get help</span></span>

<span data-ttu-id="badfa-128">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="badfa-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="badfa-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="badfa-129">Next steps</span></span>
* [<span data-ttu-id="badfa-130">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="badfa-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="badfa-131">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="badfa-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="badfa-132">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="badfa-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="badfa-133">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="badfa-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="badfa-134">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="badfa-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
