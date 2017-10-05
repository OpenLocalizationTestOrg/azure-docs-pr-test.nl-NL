---
title: Azure Stream Analytics gegevensgestuurde foutopsporing met behulp van het diagram taak | Microsoft Docs
description: De Stream Analytics-taak oplossen met behulp van de taak diagram en metrische gegevens.
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="c6bdf-103">Gegevensgestuurde foutopsporing met behulp van de taak-diagram</span><span class="sxs-lookup"><span data-stu-id="c6bdf-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="c6bdf-104">Diagram van de taak op de **bewaking** blade in de Azure portal kunt u uw pijplijn taak visualiseren.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="c6bdf-105">Deze bevat invoer, uitvoer en querystappen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="c6bdf-106">Het diagram taak kunt u de metrische gegevens voor elke stap sneller isoleren van de bron van een probleem opgetreden bij het oplossen van problemen onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="c6bdf-107">Met behulp van de taak-diagram</span><span class="sxs-lookup"><span data-stu-id="c6bdf-107">Using the job diagram</span></span>

<span data-ttu-id="c6bdf-108">In de Azure portal, terwijl in een Stream Analytics-taak onder **ondersteuning + probleemoplossing**, selecteer **taak diagram**:</span><span class="sxs-lookup"><span data-stu-id="c6bdf-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagram van de taak met metrische gegevens - locatie](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="c6bdf-110">Elke stap van de query voor een overzicht van de bijbehorende sectie in een query deelvenster bewerken te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="c6bdf-111">Een grafiek metrische gegevens voor de stap wordt weergegeven in een onderste deelvenster op de pagina.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Diagram van de taak met metrische gegevens - basic taak](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="c6bdf-113">Overzicht van de partities van de invoer Azure Event Hubs, selecteer **...**</span><span class="sxs-lookup"><span data-stu-id="c6bdf-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="c6bdf-114">Een contextmenu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-114">A context menu appears.</span></span> <span data-ttu-id="c6bdf-115">U kunt ook de invoer fusie zien.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-115">You also can see the input merger.</span></span>

![Diagram van de taak met metrische gegevens - partitie uitbreiden](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="c6bdf-117">Overzicht van de metrische grafiek voor slechts één partitie, selecteer het knooppunt partitie.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="c6bdf-118">De metrische gegevens worden aan de onderkant van de pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-118">The metrics are shown at the bottom of the page.</span></span>

![Diagram van de taak met metrische gegevens - meer metrische gegevens](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="c6bdf-120">Overzicht van de grafiek metrische gegevens voor een fusie, selecteer het knooppunt fusie.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="c6bdf-121">Het volgende diagram ziet u dat er geen gebeurtenissen zijn verwijderd of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-121">The following chart shows that no events were dropped or adjusted.</span></span>

![Diagram van de taak met metrische gegevens - raster](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="c6bdf-123">Voor de details van de metrische waarde en de tijd, wijst u de grafiek.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-123">To see the details of the metric value and time, point to the chart.</span></span>

![Taak diagram met metrische gegevens: houd de muisaanwijzer](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="c6bdf-125">Problemen oplossen met behulp van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c6bdf-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="c6bdf-126">De **QueryLastProcessedTime** metriek geeft aan wanneer de gegevens voor het ontvangen van een specifieke stap.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="c6bdf-127">Door te kijken naar de topologie, kunt u achterwaarts werken vanuit de uitvoer-processor om te zien welke stap is niet ontvangen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="c6bdf-128">Als een stap niet van gegevens ophalen is, gaat u naar de stap query net vóór.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="c6bdf-129">Controleer of de vorige stap van de query heeft een tijdvenster en als voldoende tijd is verstreken voor deze gegevens uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="c6bdf-130">(Let op dat moment windows zijn uitgelijnd op het uur.)</span><span class="sxs-lookup"><span data-stu-id="c6bdf-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="c6bdf-131">Als de vorige stap van de query een invoer-processor is, gebruiken de invoer metrische gegevens om te beantwoord de volgende gerichte vragen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="c6bdf-132">Ze kunnen u helpen bepalen of een taak is ophalen van gegevens uit de invoerbronnen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="c6bdf-133">Controleer elke partitie als de query gepartitioneerd is.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="c6bdf-134">Hoeveel gegevens wordt gelezen?</span><span class="sxs-lookup"><span data-stu-id="c6bdf-134">How much data is being read?</span></span>

*   <span data-ttu-id="c6bdf-135">**InputEventsSourcesTotal** is het aantal eenheden lezen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="c6bdf-136">Bijvoorbeeld, het aantal blobs.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="c6bdf-137">**InputEventsTotal** is het aantal gebeurtenissen dat is gelezen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="c6bdf-138">Deze metrische waarde is beschikbaar per partitie.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="c6bdf-139">**InputEventsInBytesTotal** is het aantal bytes dat is gelezen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="c6bdf-140">**InputEventsLastArrivalTime** is bijgewerkt met de tijd van elke ontvangen gebeurtenis in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="c6bdf-141">Is tijd vooruitgang?</span><span class="sxs-lookup"><span data-stu-id="c6bdf-141">Is time moving forward?</span></span> <span data-ttu-id="c6bdf-142">Als feitelijke gebeurtenissen worden gelezen, kan interpunctie niet worden verleend.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="c6bdf-143">**InputEventsLastPunctuationTime** geeft aan wanneer er interpunctie is gegenereerd om ervoor te zorgen dat de tijd vooruit blijft lopen.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="c6bdf-144">Als interpunctie niet wordt verleend, kan gegevensstroom ophalen geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="c6bdf-145">Zijn er fouten in de invoer?</span><span class="sxs-lookup"><span data-stu-id="c6bdf-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="c6bdf-146">**InputEventsEventDataNullTotal** is een aantal van gebeurtenissen die null-gegevens.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="c6bdf-147">**InputEventsSerializerErrorsTotal** is het aantal gebeurtenissen dat kan niet correct worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="c6bdf-148">**InputEventsDegradedTotal** is een aantal van gebeurtenissen die een probleem gehad andere dan met deserialisatie.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="c6bdf-149">Worden gebeurtenissen verwijderd of aangepast?</span><span class="sxs-lookup"><span data-stu-id="c6bdf-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="c6bdf-150">**InputEventsEarlyTotal** is het aantal gebeurtenissen die u een tijdstempel van de toepassing voordat de bovengrens hebt.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="c6bdf-151">**InputEventsLateTotal** is het aantal gebeurtenissen die gedurende de tijdstempel van een toepassing na de bovengrens hebben.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="c6bdf-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is het aantal gebeurtenissen verwijderd voordat de begintijd van de taak.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="c6bdf-153">We dalen achter bij het lezen van gegevens?</span><span class="sxs-lookup"><span data-stu-id="c6bdf-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="c6bdf-154">**InputEventsSourcesBackloggedTotal** vertelt u hoeveel meer berichten moeten worden gelezen voor Event Hubs en Azure IoT Hub-invoer.</span><span class="sxs-lookup"><span data-stu-id="c6bdf-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="c6bdf-155">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="c6bdf-155">Get help</span></span>
<span data-ttu-id="c6bdf-156">Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c6bdf-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6bdf-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6bdf-157">Next steps</span></span>
* [<span data-ttu-id="c6bdf-158">Inleiding tot Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c6bdf-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c6bdf-159">Aan de slag met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c6bdf-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c6bdf-160">Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="c6bdf-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c6bdf-161">Naslaggids voor stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="c6bdf-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c6bdf-162">Stream Analytics management REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="c6bdf-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
