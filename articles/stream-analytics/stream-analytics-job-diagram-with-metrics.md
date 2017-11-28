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
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="303e1-103">Gegevensgestuurde foutopsporing met behulp van Hallo taak diagram</span><span class="sxs-lookup"><span data-stu-id="303e1-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="303e1-104">Hallo taak diagram op Hallo **bewaking** blade in hello Azure-portal kunt u uw pijplijn taak visualiseren.</span><span class="sxs-lookup"><span data-stu-id="303e1-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="303e1-105">Deze bevat invoer, uitvoer en querystappen.</span><span class="sxs-lookup"><span data-stu-id="303e1-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="303e1-106">U kunt Hallo taak diagram tooexamine Hallo metrische gegevens voor elke stap, toomore isoleren snel Hallo bron van een probleem opgetreden bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="303e1-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="303e1-107">Met behulp van Hallo taak diagram</span><span class="sxs-lookup"><span data-stu-id="303e1-107">Using hello job diagram</span></span>

<span data-ttu-id="303e1-108">In hello Azure-portal, terwijl in een Stream Analytics-taak onder **ondersteuning + probleemoplossing**, selecteer **taak diagram**:</span><span class="sxs-lookup"><span data-stu-id="303e1-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagram van de taak met metrische gegevens - locatie](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="303e1-110">Selecteer elke stap toosee Hallo overeenkomende gedeelte query in een query deelvenster bewerken.</span><span class="sxs-lookup"><span data-stu-id="303e1-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="303e1-111">Een metriek grafiek voor Hallo stap wordt weergegeven in een onderste deelvenster op Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="303e1-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagram van de taak met metrische gegevens - basic taak](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="303e1-113">Selecteer toosee Hallo partities van hello Azure Event Hubs-invoer, **...**</span><span class="sxs-lookup"><span data-stu-id="303e1-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="303e1-114">Een contextmenu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="303e1-114">A context menu appears.</span></span> <span data-ttu-id="303e1-115">U kunt ook Hallo invoer fusie zien.</span><span class="sxs-lookup"><span data-stu-id="303e1-115">You also can see hello input merger.</span></span>

![Diagram van de taak met metrische gegevens - partitie uitbreiden](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="303e1-117">toosee hello metrische grafiek voor slechts één partitie, selecteer Hallo partitie knooppunt.</span><span class="sxs-lookup"><span data-stu-id="303e1-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="303e1-118">Hallo metrische gegevens worden weergegeven onder Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="303e1-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagram van de taak met metrische gegevens - meer metrische gegevens](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="303e1-120">toosee hello grafiek metrische gegevens voor een fusie, selecteer Hallo fusie knooppunt.</span><span class="sxs-lookup"><span data-stu-id="303e1-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="303e1-121">Hallo volgende diagram ziet u dat er geen gebeurtenissen zijn verwijderd of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="303e1-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagram van de taak met metrische gegevens - raster](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="303e1-123">details van de toosee Hallo Hallo metrische waarde en de tijd, punt toohello grafiek.</span><span class="sxs-lookup"><span data-stu-id="303e1-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Taak diagram met metrische gegevens: houd de muisaanwijzer](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="303e1-125">Problemen oplossen met behulp van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="303e1-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="303e1-126">Hallo **QueryLastProcessedTime** metriek geeft aan wanneer de gegevens voor het ontvangen van een specifieke stap.</span><span class="sxs-lookup"><span data-stu-id="303e1-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="303e1-127">Door te kijken Hallo-topologie, kunt u achterwaarts werken van Hallo uitvoer processor toosee stap niet van gegevens ontvangen is.</span><span class="sxs-lookup"><span data-stu-id="303e1-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="303e1-128">Als een stap niet van gegevens ophalen is, gaat u toohello query stap net vóór.</span><span class="sxs-lookup"><span data-stu-id="303e1-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="303e1-129">Controleer of hello voorgaande query stap heeft een tijdvenster en of u voldoende tijd is verstreken voor toooutput gegevens.</span><span class="sxs-lookup"><span data-stu-id="303e1-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="303e1-130">(Let op dat moment windows uitgelijnde toohello uur zijn.)</span><span class="sxs-lookup"><span data-stu-id="303e1-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="303e1-131">Als hello voorgaande query stap een invoer-processor, gericht gebruik Hallo invoer metrische gegevens toohelp antwoord Hallo volgende vragen.</span><span class="sxs-lookup"><span data-stu-id="303e1-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="303e1-132">Ze kunnen u helpen bepalen of een taak is ophalen van gegevens uit de invoerbronnen.</span><span class="sxs-lookup"><span data-stu-id="303e1-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="303e1-133">Als het Hallo-query is gepartitioneerd, controleert u elke partitie.</span><span class="sxs-lookup"><span data-stu-id="303e1-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="303e1-134">Hoeveel gegevens wordt gelezen?</span><span class="sxs-lookup"><span data-stu-id="303e1-134">How much data is being read?</span></span>

*   <span data-ttu-id="303e1-135">**InputEventsSourcesTotal** is het aantal eenheden lezen Hallo.</span><span class="sxs-lookup"><span data-stu-id="303e1-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="303e1-136">Bijvoorbeeld, Hallo aantal blobs.</span><span class="sxs-lookup"><span data-stu-id="303e1-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="303e1-137">**InputEventsTotal** is Hallo aantal gebeurtenissen dat is gelezen.</span><span class="sxs-lookup"><span data-stu-id="303e1-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="303e1-138">Deze metrische waarde is beschikbaar per partitie.</span><span class="sxs-lookup"><span data-stu-id="303e1-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="303e1-139">**InputEventsInBytesTotal** Hallo aantal gelezen bytes is.</span><span class="sxs-lookup"><span data-stu-id="303e1-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="303e1-140">**InputEventsLastArrivalTime** is bijgewerkt met de tijd van elke ontvangen gebeurtenis in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="303e1-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="303e1-141">Is tijd vooruitgang?</span><span class="sxs-lookup"><span data-stu-id="303e1-141">Is time moving forward?</span></span> <span data-ttu-id="303e1-142">Als feitelijke gebeurtenissen worden gelezen, kan interpunctie niet worden verleend.</span><span class="sxs-lookup"><span data-stu-id="303e1-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="303e1-143">**InputEventsLastPunctuationTime** geeft aan wanneer een interpunctie tookeep tijd verplaatsen is uitgegeven doorsturen.</span><span class="sxs-lookup"><span data-stu-id="303e1-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="303e1-144">Als interpunctie niet wordt verleend, kan gegevensstroom ophalen geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="303e1-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="303e1-145">Zijn er fouten in de Hallo invoer?</span><span class="sxs-lookup"><span data-stu-id="303e1-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="303e1-146">**InputEventsEventDataNullTotal** is een aantal van gebeurtenissen die null-gegevens.</span><span class="sxs-lookup"><span data-stu-id="303e1-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="303e1-147">**InputEventsSerializerErrorsTotal** is het aantal gebeurtenissen dat kan niet correct worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="303e1-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="303e1-148">**InputEventsDegradedTotal** is een aantal van gebeurtenissen die een probleem gehad andere dan met deserialisatie.</span><span class="sxs-lookup"><span data-stu-id="303e1-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="303e1-149">Worden gebeurtenissen verwijderd of aangepast?</span><span class="sxs-lookup"><span data-stu-id="303e1-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="303e1-150">**InputEventsEarlyTotal** is Hallo aantal gebeurtenissen die een tijdstempel van de toepassing voordat de bovengrens Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="303e1-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="303e1-151">**InputEventsLateTotal** is het aantal gebeurtenissen die gedurende de tijdstempel van een toepassing na de bovengrens Hallo hebben Hallo.</span><span class="sxs-lookup"><span data-stu-id="303e1-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="303e1-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** Hallo aantal gebeurtenissen verwijderd voordat de begintijd van taak Hallo is.</span><span class="sxs-lookup"><span data-stu-id="303e1-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="303e1-153">We dalen achter bij het lezen van gegevens?</span><span class="sxs-lookup"><span data-stu-id="303e1-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="303e1-154">**InputEventsSourcesBackloggedTotal** wordt aangegeven hoeveel meer berichten toobe moeten lezen voor Event Hubs en Azure IoT Hub-invoer.</span><span class="sxs-lookup"><span data-stu-id="303e1-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="303e1-155">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="303e1-155">Get help</span></span>
<span data-ttu-id="303e1-156">Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="303e1-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="303e1-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="303e1-157">Next steps</span></span>
* [<span data-ttu-id="303e1-158">Inleiding tooStream Analytics</span><span class="sxs-lookup"><span data-stu-id="303e1-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="303e1-159">Aan de slag met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="303e1-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="303e1-160">Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="303e1-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="303e1-161">Naslaggids voor stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="303e1-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="303e1-162">Stream Analytics management REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="303e1-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
