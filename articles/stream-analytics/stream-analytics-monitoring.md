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
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="921e9-104">Bewaking van de Stream Analytics-taak begrijpen en hoe toomonitor query's</span><span class="sxs-lookup"><span data-stu-id="921e9-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="921e9-105">Inleiding: pagina Hallo-monitor</span><span class="sxs-lookup"><span data-stu-id="921e9-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="921e9-106">Hello Azure-portal beide surface prestatie metrische gegevens die kunnen worden gebruikt toomonitor en de prestaties van uw query en -taak oplossen.</span><span class="sxs-lookup"><span data-stu-id="921e9-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="921e9-107">toosee deze metrische gegevens, bladeren toohello Stream Analytics-taak u geïnteresseerd bent in de metrische gegevens voor weergave Hallo zien **bewaking** sectie op de pagina overzicht Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e9-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Bewaking van de koppeling](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="921e9-109">Hallo-venster wordt weergegeven, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="921e9-109">hello window will appear as shown:</span></span>

![Bewakingstaak Dashboard](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="921e9-111">Metrische gegevens beschikbaar voor Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="921e9-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="921e9-112">Gegevens</span><span class="sxs-lookup"><span data-stu-id="921e9-112">Metric</span></span>                 | <span data-ttu-id="921e9-113">Definitie</span><span class="sxs-lookup"><span data-stu-id="921e9-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="921e9-114">SU % gebruik</span><span class="sxs-lookup"><span data-stu-id="921e9-114">SU % Utilization</span></span>       | <span data-ttu-id="921e9-115">Hallo-gebruik van Hallo Streaming-eenheid toegewezen tooa taak Hallo Scale tabblad in het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="921e9-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="921e9-116">Hierboven, wordt hoge kans dat de verwerking van gebeurtenissen kan worden vertraagd of gestopt Bezig met het of moet deze indicator 80% bereiken.</span><span class="sxs-lookup"><span data-stu-id="921e9-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="921e9-117">Invoervelden</span><span class="sxs-lookup"><span data-stu-id="921e9-117">Input Events</span></span>           | <span data-ttu-id="921e9-118">De hoeveelheid gegevens die door Hallo Stream Analytics-taak in het aantal gebeurtenissen dat is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="921e9-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="921e9-119">Dit kan zijn gebruikte toovalidate dat gebeurtenissen toohello invoerbron worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="921e9-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="921e9-120">Uitvoergebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="921e9-120">Output Events</span></span>          | <span data-ttu-id="921e9-121">De hoeveelheid gegevens die door Hallo Stream Analytics-taak toohello uitvoerdoel, in aantal gebeurtenissen dat is verzonden.</span><span class="sxs-lookup"><span data-stu-id="921e9-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="921e9-122">Out-van-Order-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="921e9-122">Out-of-Order Events</span></span>    | <span data-ttu-id="921e9-123">Het aantal gebeurtenissen ontvangen volgorde die zijn verwijderd of een aangepaste tijdstempel, op basis van Hallo gebeurtenis ordening beleid gegeven.</span><span class="sxs-lookup"><span data-stu-id="921e9-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="921e9-124">Dit kan worden beïnvloed door het Hallo-configuratie van Hallo tolerantieperiode geplaatst Out instelling.</span><span class="sxs-lookup"><span data-stu-id="921e9-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="921e9-125">Conversie van fouten</span><span class="sxs-lookup"><span data-stu-id="921e9-125">Data Conversion Errors</span></span> | <span data-ttu-id="921e9-126">Het aantal gegevens conversiefouten die door een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="921e9-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="921e9-127">Runtime-fouten</span><span class="sxs-lookup"><span data-stu-id="921e9-127">Runtime Errors</span></span>         | <span data-ttu-id="921e9-128">Totaal aantal Hallo van fouten die tijdens het uitvoeren van een Stream Analytics-taak optreden.</span><span class="sxs-lookup"><span data-stu-id="921e9-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="921e9-129">Laat invoervelden</span><span class="sxs-lookup"><span data-stu-id="921e9-129">Late Input Events</span></span>      | <span data-ttu-id="921e9-130">Aantal gebeurtenissen dat binnenkomt laat vanuit Hallo-bron die ofwel verwijderd of hun timestamp is aangepast, op basis van Hallo gebeurtenis ordening beleidsconfiguratie van Hallo laat tolerantieperiode instelling.</span><span class="sxs-lookup"><span data-stu-id="921e9-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="921e9-131">Aanvragen van functie</span><span class="sxs-lookup"><span data-stu-id="921e9-131">Function Requests</span></span>      | <span data-ttu-id="921e9-132">Het aantal aanroepen toohello Azure Machine Learning-functie (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="921e9-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="921e9-133">Mislukte functie aanvragen</span><span class="sxs-lookup"><span data-stu-id="921e9-133">Failed Function Requests</span></span> | <span data-ttu-id="921e9-134">Het aantal mislukte Azure Machine Learning-functieaanroepen (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="921e9-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="921e9-135">Gebeurtenissen voor de functie</span><span class="sxs-lookup"><span data-stu-id="921e9-135">Function Events</span></span>        | <span data-ttu-id="921e9-136">Aantal gebeurtenissen verzonden toohello Azure Machine Learning-functie (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="921e9-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="921e9-137">Invoergebeurtenis Bytes</span><span class="sxs-lookup"><span data-stu-id="921e9-137">Input Event Bytes</span></span>      | <span data-ttu-id="921e9-138">De hoeveelheid gegevens die zijn ontvangen door Hallo Stream Analytics-taak, in bytes.</span><span class="sxs-lookup"><span data-stu-id="921e9-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="921e9-139">Dit kan zijn gebruikte toovalidate dat gebeurtenissen toohello invoerbron worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="921e9-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="921e9-140">Bewaking aanpassen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="921e9-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="921e9-141">U kunt Hallo type diagram, metrische gegevens weergegeven, aanpassen en tijdsbereik in instellingen voor Hallo grafiek bewerken.</span><span class="sxs-lookup"><span data-stu-id="921e9-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="921e9-142">Zie voor meer informatie [hoe tooCustomize bewaking](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="921e9-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Query-tijd van de Monitor-grafiek](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="921e9-144">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="921e9-144">Get help</span></span>
<span data-ttu-id="921e9-145">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="921e9-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="921e9-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="921e9-146">Next steps</span></span>
* [<span data-ttu-id="921e9-147">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="921e9-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="921e9-148">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="921e9-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="921e9-149">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="921e9-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="921e9-150">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="921e9-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="921e9-151">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="921e9-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

