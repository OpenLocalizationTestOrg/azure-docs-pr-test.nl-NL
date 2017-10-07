---
title: aaaAzure Application Insights telemetrie Data Model - Metric telemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor metrische telemetrie
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="4a21e-103">Metrische telemetrie: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4a21e-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="4a21e-104">Er zijn twee soorten metrische telemetrie ondersteund door [Application Insights](app-insights-overview.md): enkele meting en vooraf samengevoegde metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="4a21e-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="4a21e-105">Meting is alleen een naam en waarde.</span><span class="sxs-lookup"><span data-stu-id="4a21e-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="4a21e-106">Vooraf samengevoegde metrische gegevens geeft de minimale en maximale waarde van Hallo metriek in hello aggregatie-interval en de standaarddeviatie van deze.</span><span class="sxs-lookup"><span data-stu-id="4a21e-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="4a21e-107">Vooraf samengevoegde metrische telemetrie wordt ervan uitgegaan dat aggregatie-periode is 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="4a21e-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="4a21e-108">Er zijn verschillende bekende metrische namen ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4a21e-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="4a21e-109">Metrische gegevens voor systeem- en prestatiemeteritems:</span><span class="sxs-lookup"><span data-stu-id="4a21e-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="4a21e-110">**.NET-naam**</span><span class="sxs-lookup"><span data-stu-id="4a21e-110">**.NET name**</span></span>             | <span data-ttu-id="4a21e-111">**Platform agnostisch naam**</span><span class="sxs-lookup"><span data-stu-id="4a21e-111">**Platform agnostic name**</span></span> | <span data-ttu-id="4a21e-112">**De naam van de REST-API**</span><span class="sxs-lookup"><span data-stu-id="4a21e-112">**REST API name**</span></span> | <span data-ttu-id="4a21e-113">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="4a21e-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="4a21e-114">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-114">Work in progress...</span></span> | [<span data-ttu-id="4a21e-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="4a21e-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="4a21e-116">totale aantal CPU</span><span class="sxs-lookup"><span data-stu-id="4a21e-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="4a21e-117">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-117">Work in progress...</span></span> | [<span data-ttu-id="4a21e-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="4a21e-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="4a21e-119">geheugen beschikbaar op de schijf</span><span class="sxs-lookup"><span data-stu-id="4a21e-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="4a21e-120">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-120">Work in progress...</span></span> | [<span data-ttu-id="4a21e-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="4a21e-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="4a21e-122">CPU van Hallo proces Hallo-toepassing te hosten</span><span class="sxs-lookup"><span data-stu-id="4a21e-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="4a21e-123">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-123">Work in progress...</span></span> | [<span data-ttu-id="4a21e-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="4a21e-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="4a21e-125">geheugen dat wordt gebruikt door Hallo proces Hallo-toepassing te hosten</span><span class="sxs-lookup"><span data-stu-id="4a21e-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="4a21e-126">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-126">Work in progress...</span></span> | [<span data-ttu-id="4a21e-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4a21e-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="4a21e-128">het aantal i/o-bewerkingen wordt uitgevoerd door proces Hallo-toepassing te hosten</span><span class="sxs-lookup"><span data-stu-id="4a21e-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="4a21e-129">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-129">Work in progress...</span></span> | [<span data-ttu-id="4a21e-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4a21e-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="4a21e-131">aantal aanvragen dat is verwerkt door toepassing</span><span class="sxs-lookup"><span data-stu-id="4a21e-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="4a21e-132">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-132">Work in progress...</span></span> | [<span data-ttu-id="4a21e-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4a21e-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="4a21e-134">aantal uitzonderingen worden veroorzaakt door toepassing</span><span class="sxs-lookup"><span data-stu-id="4a21e-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="4a21e-135">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-135">Work in progress...</span></span> | [<span data-ttu-id="4a21e-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="4a21e-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="4a21e-137">Gemiddeld aantal aanvragen uitvoeringstijd</span><span class="sxs-lookup"><span data-stu-id="4a21e-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="4a21e-138">Werk in uitvoering...</span><span class="sxs-lookup"><span data-stu-id="4a21e-138">Work in progress...</span></span> | [<span data-ttu-id="4a21e-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="4a21e-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="4a21e-140">het aantal aanvragen dat wacht op verwerking in een wachtrij Hallo</span><span class="sxs-lookup"><span data-stu-id="4a21e-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="4a21e-141">Naam</span><span class="sxs-lookup"><span data-stu-id="4a21e-141">Name</span></span>

<span data-ttu-id="4a21e-142">Naam van Hallo metrische gegevens van de gewenste toosee in Application Insights-portal en de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="4a21e-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="4a21e-143">Waarde</span><span class="sxs-lookup"><span data-stu-id="4a21e-143">Value</span></span>

<span data-ttu-id="4a21e-144">Enkelvoudige waarde voor de meting.</span><span class="sxs-lookup"><span data-stu-id="4a21e-144">Single value for measurement.</span></span> <span data-ttu-id="4a21e-145">De som van de afzonderlijke metingen voor Hallo aggregatie.</span><span class="sxs-lookup"><span data-stu-id="4a21e-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="4a21e-146">Count</span><span class="sxs-lookup"><span data-stu-id="4a21e-146">Count</span></span>

<span data-ttu-id="4a21e-147">Metrische gewicht van Hallo metrische gegevens geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="4a21e-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="4a21e-148">Mag niet worden ingesteld voor een meting.</span><span class="sxs-lookup"><span data-stu-id="4a21e-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="4a21e-149">Min</span><span class="sxs-lookup"><span data-stu-id="4a21e-149">Min</span></span>

<span data-ttu-id="4a21e-150">De minimumwaarde van Hallo metrische gegevens geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="4a21e-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="4a21e-151">Mag niet worden ingesteld voor een meting.</span><span class="sxs-lookup"><span data-stu-id="4a21e-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="4a21e-152">Max.</span><span class="sxs-lookup"><span data-stu-id="4a21e-152">Max</span></span>

<span data-ttu-id="4a21e-153">Maximumwaarde van Hallo metrische gegevens geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="4a21e-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="4a21e-154">Mag niet worden ingesteld voor een meting.</span><span class="sxs-lookup"><span data-stu-id="4a21e-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="4a21e-155">Standaarddeviatie</span><span class="sxs-lookup"><span data-stu-id="4a21e-155">Standard deviation</span></span>

<span data-ttu-id="4a21e-156">De standaarddeviatie van Hallo metrische gegevens geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="4a21e-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="4a21e-157">Mag niet worden ingesteld voor een meting.</span><span class="sxs-lookup"><span data-stu-id="4a21e-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4a21e-158">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="4a21e-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="4a21e-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a21e-159">Next steps</span></span>

- <span data-ttu-id="4a21e-160">Meer informatie over hoe toouse [Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="4a21e-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="4a21e-161">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="4a21e-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4a21e-162">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4a21e-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
