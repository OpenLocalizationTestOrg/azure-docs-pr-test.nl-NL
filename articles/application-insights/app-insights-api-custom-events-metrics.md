---
title: Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens | Microsoft Docs
description: Plaats een paar regels code in uw apparaat of een bureaublad-app, webpagina of service, gebruik bijhouden en analyseren van problemen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="63051-103">Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="63051-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="63051-104">Voeg een paar regels code in uw toepassing om erachter te komen wat gebruikers doen met het of om u te helpen bij het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="63051-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="63051-105">U kunt telemetrie verzenden van apparaat- en bureaublad-apps, webserver en webclients en webservers.</span><span class="sxs-lookup"><span data-stu-id="63051-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="63051-106">Gebruik de [Azure Application Insights](app-insights-overview.md) telemetrie-API voor het verzenden van aangepaste gebeurtenissen en metrische gegevens en uw eigen versies standaardtelemetrie core.</span><span class="sxs-lookup"><span data-stu-id="63051-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="63051-107">Deze API is de dezelfde API die gebruikmaken van de standaard Application Insights gegevens collectors.</span><span class="sxs-lookup"><span data-stu-id="63051-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="63051-108">API-overzicht</span><span class="sxs-lookup"><span data-stu-id="63051-108">API summary</span></span>
<span data-ttu-id="63051-109">De API is uniform op alle platforms, naast een paar kleine verschillen.</span><span class="sxs-lookup"><span data-stu-id="63051-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="63051-110">Methode</span><span class="sxs-lookup"><span data-stu-id="63051-110">Method</span></span> | <span data-ttu-id="63051-111">Gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="63051-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="63051-112">Pagina's, schermen, blades of formulieren.</span><span class="sxs-lookup"><span data-stu-id="63051-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="63051-113">Acties van gebruikers en andere gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="63051-113">User actions and other events.</span></span> <span data-ttu-id="63051-114">Gebruikt voor het gedrag van de gebruiker bijhouden of om prestaties te bewaken.</span><span class="sxs-lookup"><span data-stu-id="63051-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="63051-115">Prestatiemetingen zoals wachtrij lengten niet gerelateerd aan specifieke gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="63051-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="63051-116">Logboekregistratie uitzonderingen voor diagnose.</span><span class="sxs-lookup"><span data-stu-id="63051-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="63051-117">Traceren waarbij ze ten opzichte van andere gebeurtenissen optreden en stack-traces onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="63051-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="63051-118">De frequentie en duur van serveraanvragen voor prestatieanalyse logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="63051-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="63051-119">Diagnostische logboeken-berichten.</span><span class="sxs-lookup"><span data-stu-id="63051-119">Diagnostic log messages.</span></span> <span data-ttu-id="63051-120">U kunt ook de logboeken van derden vastleggen.</span><span class="sxs-lookup"><span data-stu-id="63051-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="63051-121">De duur en frequentie van aanroepen naar externe onderdelen die uw app afhankelijk van is logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="63051-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="63051-122">U kunt [eigenschappen en metrische gegevens koppelen](#properties) tot de meeste van deze aanroepen telemetrie.</span><span class="sxs-lookup"><span data-stu-id="63051-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="63051-123"><a name="prep"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="63051-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="63051-124">Als u nog een verwijzing op Application Insights-SDK hebt:</span><span class="sxs-lookup"><span data-stu-id="63051-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="63051-125">De Application Insights-SDK toevoegen aan uw project:</span><span class="sxs-lookup"><span data-stu-id="63051-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="63051-126">ASP.NET-project</span><span class="sxs-lookup"><span data-stu-id="63051-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="63051-127">Java-project</span><span class="sxs-lookup"><span data-stu-id="63051-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="63051-128">JavaScript in elke webpagina</span><span class="sxs-lookup"><span data-stu-id="63051-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="63051-129">In uw servercode apparaat of een webtoepassing omvatten:</span><span class="sxs-lookup"><span data-stu-id="63051-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="63051-130">*C#:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="63051-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="63051-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="63051-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="63051-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="63051-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="63051-133">Een exemplaar TelemetryClient maken</span><span class="sxs-lookup"><span data-stu-id="63051-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="63051-134">Maken van een exemplaar van `TelemetryClient` (behalve in JavaScript in webpagina's):</span><span class="sxs-lookup"><span data-stu-id="63051-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="63051-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="63051-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="63051-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="63051-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="63051-138">TelemetryClient is thread-safe.</span><span class="sxs-lookup"><span data-stu-id="63051-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="63051-139">Het is raadzaam om gebruik te maken van een instantie van TelemetryClient voor elke module van uw app.</span><span class="sxs-lookup"><span data-stu-id="63051-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="63051-140">Bijvoorbeeld: mogelijk hebt u één exemplaar van TelemetryClient in uw webservice voor het rapporteren van binnenkomende HTTP-aanvragen en andere in een klasse middleware rapport zakelijke logica gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="63051-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="63051-141">U kunt eigenschappen instellen, zoals `TelemetryClient.Context.User.Id` voor het bijhouden van gebruikers en sessies, of `TelemetryClient.Context.Device.Id` om de machine te bepalen.</span><span class="sxs-lookup"><span data-stu-id="63051-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="63051-142">Deze informatie is gekoppeld aan alle gebeurtenissen die door het exemplaar wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="63051-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="63051-143">TrackEvent</span></span>
<span data-ttu-id="63051-144">In Application Insights, een *aangepaste gebeurtenis* is van een gegevenspunt geldt dat u kunt weergeven in [Metrics Explorer](app-insights-metrics-explorer.md) als een verzamelde aantal en in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md) als afzonderlijke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="63051-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="63051-145">(Deze wordt niet verwant zijn aan de MVC- of andere framework 'gebeurtenissen'.)</span><span class="sxs-lookup"><span data-stu-id="63051-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="63051-146">Invoegen `TrackEvent` aanroepen in uw code te tellen van diverse gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="63051-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="63051-147">Hoe vaak gebruikers kiest voor een bepaalde functie, hoe vaak ze bepaalde doelen bereiken of zij mogelijk hoe vaak voor bepaalde soorten fouten.</span><span class="sxs-lookup"><span data-stu-id="63051-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="63051-148">Bijvoorbeeld in een gameapps een gebeurtenis wanneer een gebruiker het spel wins verzenden:</span><span class="sxs-lookup"><span data-stu-id="63051-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="63051-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="63051-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="63051-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="63051-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="63051-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="63051-153">Gebeurtenissen weergeven in de Microsoft Azure-portal</span><span class="sxs-lookup"><span data-stu-id="63051-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="63051-154">Open een aantal van uw gebeurtenissen vindt een [Metrics Explorer](app-insights-metrics-explorer.md) blade, Voeg een nieuwe grafiek toe en selecteer **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="63051-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Zie een aantal aangepaste gebeurtenissen](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="63051-156">Als u wilt vergelijken de aantallen voor verschillende gebeurtenissen, stelt u het grafiektype naar **raster**, and -groep met de gebeurtenisnaam:</span><span class="sxs-lookup"><span data-stu-id="63051-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Het grafiektype en groepering instellen](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="63051-158">Klik op het raster door de naam van een gebeurtenis om te zien van afzonderlijke exemplaren van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="63051-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="63051-159">Voor meer details - klikt u op elk exemplaar in de lijst.</span><span class="sxs-lookup"><span data-stu-id="63051-159">To see more detail - click any occurrence in the list.</span></span>

![Drillthrough-gebeurtenissen](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="63051-161">Als u wilt richten op specifieke gebeurtenissen in de zoekopdracht of Metrics Explorer, stelt u de blade-filter op de gebeurtenisnamen van de die u geïnteresseerd bent in:</span><span class="sxs-lookup"><span data-stu-id="63051-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Open Filters, vouw de naam van de gebeurtenis en selecteer een of meer waarden](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="63051-163">Aangepaste gebeurtenissen in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-163">Custom events in Analytics</span></span>

<span data-ttu-id="63051-164">De telemetrie is beschikbaar in de `customEvents` in tabel [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="63051-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="63051-165">Elke rij vertegenwoordigt een aanroep van `trackEvent(..)` in uw app.</span><span class="sxs-lookup"><span data-stu-id="63051-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="63051-166">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, de eigenschap itemCount geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="63051-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="63051-167">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen van trackEvent(), het proces steekproeven alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="63051-168">Als u het juiste aantal aangepaste gebeurtenissen, moet u daarom code gebruiken zoals `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="63051-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="63051-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="63051-169">TrackMetric</span></span>

<span data-ttu-id="63051-170">Application Insights kunnen metrische gegevens die niet zijn gekoppeld aan bepaalde gebeurtenissen van grafiekgebied.</span><span class="sxs-lookup"><span data-stu-id="63051-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="63051-171">U kan bijvoorbeeld een wachtrijlengte bewaken met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="63051-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="63051-172">Met metrische gegevens en de afzonderlijke metingen zijn van belang zijn kleiner dan de variaties en trends en dus statistische kolomdiagrammen zijn nuttig.</span><span class="sxs-lookup"><span data-stu-id="63051-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="63051-173">Om metrische gegevens naar Application Insights verzendt, kunt u de `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="63051-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="63051-174">Er zijn twee manieren een metriek verzenden:</span><span class="sxs-lookup"><span data-stu-id="63051-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="63051-175">Enkele waarde.</span><span class="sxs-lookup"><span data-stu-id="63051-175">Single value.</span></span> <span data-ttu-id="63051-176">Telkens wanneer u een meting in uw toepassing uitvoert, kunt u de overeenkomstige waarde verzenden naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="63051-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="63051-177">Bijvoorbeeld, wordt ervan uitgegaan dat u hebt een metriek met een beschrijving van het aantal items in een container.</span><span class="sxs-lookup"><span data-stu-id="63051-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="63051-178">U voor het eerst drie items in de container plaatsen en verwijder vervolgens twee items gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="63051-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="63051-179">Dienovereenkomstig, roept u `TrackMetric` tweemaal: de waarde eerst doorgeven `3` en vervolgens de waarde `-2`.</span><span class="sxs-lookup"><span data-stu-id="63051-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="63051-180">Application Insights worden beide waarden opgeslagen namens jou.</span><span class="sxs-lookup"><span data-stu-id="63051-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="63051-181">Aggregatie.</span><span class="sxs-lookup"><span data-stu-id="63051-181">Aggregation.</span></span> <span data-ttu-id="63051-182">Als u werkt met metrische gegevens, wordt elke meting zelden is van belang.</span><span class="sxs-lookup"><span data-stu-id="63051-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="63051-183">In plaats daarvan is een overzicht van wat er gebeurd gedurende een bepaalde periode is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="63051-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="63051-184">Dergelijke samenvatting heet _aggregatie_.</span><span class="sxs-lookup"><span data-stu-id="63051-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="63051-185">In het bovenstaande voorbeeld wordt de som van het cumulatieve metrische gegevens voor deze periode is `1` en het aantal van de metrische waarden is `2`.</span><span class="sxs-lookup"><span data-stu-id="63051-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="63051-186">Wanneer u de aggregatie-methode gebruikt, u alleen aanroepen `TrackMetric` eenmaal per periode en de verzamelde waarden te verzenden.</span><span class="sxs-lookup"><span data-stu-id="63051-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="63051-187">Dit is de aanbevolen aanpak omdat deze de kosten en prestaties overhead door minder gegevenspunten verzenden naar Application Insights tijdens het verzamelen van alle relevante gegevens nog steeds aanzienlijk kan verminderen.</span><span class="sxs-lookup"><span data-stu-id="63051-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="63051-188">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="63051-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="63051-189">Enkele waarden</span><span class="sxs-lookup"><span data-stu-id="63051-189">Single values</span></span>

<span data-ttu-id="63051-190">Metrische waarde voor een enkele verzenden:</span><span class="sxs-lookup"><span data-stu-id="63051-190">To send a single metric value:</span></span>

<span data-ttu-id="63051-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="63051-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="63051-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="63051-193">Samenvoegen van metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="63051-193">Aggregating metrics</span></span>

<span data-ttu-id="63051-194">Het is raadzaam met cumulatieve metrische gegevens voordat ze worden verzonden vanuit uw app of als u bandbreedte, kosten en prestaties te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="63051-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="63051-195">Hier volgt een voorbeeld van code verzamelen:</span><span class="sxs-lookup"><span data-stu-id="63051-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="63051-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="63051-197">Aangepaste metrische gegevens in Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="63051-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="63051-198">U kunt de resultaten, open Metrics Explorer en voeg een nieuwe grafiek toe.</span><span class="sxs-lookup"><span data-stu-id="63051-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="63051-199">De grafiek om weer te geven de metrische gegevens bewerken.</span><span class="sxs-lookup"><span data-stu-id="63051-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="63051-200">Uw aangepaste metrische gegevens kan enkele minuten worden weergegeven in de lijst met beschikbare metrische gegevens duren.</span><span class="sxs-lookup"><span data-stu-id="63051-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Voeg een nieuwe grafiek toe of Selecteer een grafiek en onder aangepast, selecteer uw metrische gegevens](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="63051-202">Aangepaste metrische gegevens in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="63051-203">De telemetrie is beschikbaar in de `customMetrics` in tabel [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="63051-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="63051-204">Elke rij vertegenwoordigt een aanroep van `trackMetric(..)` in uw app.</span><span class="sxs-lookup"><span data-stu-id="63051-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="63051-205">`valueSum`-Dit is de som van de metingen.</span><span class="sxs-lookup"><span data-stu-id="63051-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="63051-206">Als u de gemiddelde waarde, wordt gedeeld door `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="63051-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="63051-207">`valueCount`-Het aantal metingen die zijn samengevoegd in dit `trackMetric(..)` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="63051-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="63051-208">Paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="63051-208">Page views</span></span>
<span data-ttu-id="63051-209">In een app-apparaat of webpagina telemetrie van paginaweergaven standaard verzonden wanneer elke pagina of het scherm wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="63051-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="63051-210">Maar u kunt deze instelling wijzigen om bij te houden van paginaweergaven op aanvullende of verschillende tijdstippen.</span><span class="sxs-lookup"><span data-stu-id="63051-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="63051-211">Bijvoorbeeld in een app die wordt weergegeven voor tabbladen of blades, raadzaam om bij te houden van een pagina wanneer de gebruiker een nieuwe blade opent.</span><span class="sxs-lookup"><span data-stu-id="63051-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Gebruik lens op de blade overzicht](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="63051-213">Gebruikers- en sessiegegevens gegevens verzonden als eigenschappen samen met paginaweergaven, zodat de gebruikers- en sessiegegevens grafieken tot leven komen als er telemetrie van paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="63051-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="63051-214">Aangepaste paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="63051-214">Custom page views</span></span>
<span data-ttu-id="63051-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="63051-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="63051-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="63051-218">Als u meerdere tabbladen binnen andere HTML-pagina's hebt, kunt u de URL te opgeven:</span><span class="sxs-lookup"><span data-stu-id="63051-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="63051-219">Timing van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="63051-219">Timing page views</span></span>
<span data-ttu-id="63051-220">Standaard worden de tijden gerapporteerd als **laadtijd voor paginaweergave** worden gemeten vanaf de browser de aanvraag verzendt totdat de browser-gebeurtenis voor het laden van pagina wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="63051-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="63051-221">In plaats daarvan kunt u:</span><span class="sxs-lookup"><span data-stu-id="63051-221">Instead, you can either:</span></span>

* <span data-ttu-id="63051-222">Stel een expliciete duur de [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) aanroepen: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="63051-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="63051-223">Gebruik de paginaweergave timing aanroepen `startTrackPage` en `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="63051-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="63051-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="63051-225">...</span><span class="sxs-lookup"><span data-stu-id="63051-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="63051-226">De naam die u als de eerste parameter gebruikt wordt gekoppeld aan de aanroepen starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="63051-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="63051-227">Wordt standaard de naam van de huidige pagina.</span><span class="sxs-lookup"><span data-stu-id="63051-227">It defaults to the current page name.</span></span>

<span data-ttu-id="63051-228">De resulterende pagina load duur weergegeven in Metrics Explorer zijn afgeleid van het interval tussen de aanroepen starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="63051-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="63051-229">Het is aan u welke interval die u daadwerkelijk tijd.</span><span class="sxs-lookup"><span data-stu-id="63051-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="63051-230">Pagina telemetrie in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="63051-231">In [Analytics](app-insights-analytics.md) twee tabellen bevatten gegevens van de browser bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="63051-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="63051-232">De `pageViews` tabel bevat gegevens over de URL- en -titel</span><span class="sxs-lookup"><span data-stu-id="63051-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="63051-233">De `browserTimings` tabel bevat gegevens over de prestaties van de client, zoals de tijd voor de inkomende gegevens</span><span class="sxs-lookup"><span data-stu-id="63051-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="63051-234">Zoeken op hoe lang de browser nodig is om verschillende pagina's:</span><span class="sxs-lookup"><span data-stu-id="63051-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="63051-235">Voor detectie van de popularities van verschillende browsers:</span><span class="sxs-lookup"><span data-stu-id="63051-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="63051-236">Om te koppelen van paginaweergaven voor AJAX-aanroepen, aanmelden met afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="63051-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="63051-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="63051-237">TrackRequest</span></span>
<span data-ttu-id="63051-238">De SDK-server gebruikt TrackRequest HTTP-aanvragen moeten worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="63051-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="63051-239">U kunt deze zelf ook aanroepen als u verzoeken wilt simuleren in een context waarin er geen module van de web-service uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63051-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="63051-240">De aanbevolen manier om het verzenden van aanvraagtelemetrie is echter waar de aanvraag fungeert als een <a href="#operation-context">bewerking context</a>.</span><span class="sxs-lookup"><span data-stu-id="63051-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="63051-241">Bewerking context</span><span class="sxs-lookup"><span data-stu-id="63051-241">Operation context</span></span>
<span data-ttu-id="63051-242">U kunt telemetrie-items bij elkaar koppelen door te koppelen aan een algemene bewerking-ID.</span><span class="sxs-lookup"><span data-stu-id="63051-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="63051-243">De standaard-bijhouden module doet dit voor uitzonderingen en andere gebeurtenissen die worden verzonden tijdens het verwerken van een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="63051-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="63051-244">In [Search](app-insights-diagnostic-search.md) en [Analytics](app-insights-analytics.md), kunt u de ID gemakkelijk terugvinden alle gebeurtenissen die zijn gekoppeld aan de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="63051-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="63051-245">De eenvoudigste manier om in te stellen van de ID is het instellen van de context van een bewerking met behulp van dit patroon:</span><span class="sxs-lookup"><span data-stu-id="63051-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="63051-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="63051-247">Samen met het instellen van de context van een bewerking `StartOperation` maakt een telemetrie-item van het type dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="63051-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="63051-248">Het item telemetrie verzendt wanneer het verwijderen van de bewerking, of als u niet expliciet aanroepen `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="63051-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="63051-249">Als u `RequestTelemetry` als de telemetrie-type, de duur is ingesteld op het getimed interval tussen starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="63051-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="63051-250">Bewerking contexten kunnen niet worden genest.</span><span class="sxs-lookup"><span data-stu-id="63051-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="63051-251">Als er al een bewerking context bestaat, wordt de bijbehorende ID gekoppeld aan alle opgenomen items is, met inbegrip van het item dat is gemaakt met `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="63051-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="63051-252">In de zoekopdracht op de context van de bewerking gebruikt voor het maken de **verwante Items** lijst:</span><span class="sxs-lookup"><span data-stu-id="63051-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Verwante items](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="63051-254">Zie [toepassing-insights-aangepaste-bewerkingen-tracking.md] voor meer informatie over aangepaste bewerkingen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="63051-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="63051-255">Aanvragen in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-255">Requests in Analytics</span></span> 

<span data-ttu-id="63051-256">In [Application Insights Analytics](app-insights-analytics.md), weergeven van aanvragen in de `requests` tabel.</span><span class="sxs-lookup"><span data-stu-id="63051-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="63051-257">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, de eigenschap itemCount ziet een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="63051-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="63051-258">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen naar trackRequest() het proces steekproeven alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="63051-259">Als u een juiste aantal aanvragen en gemiddelde duur gesegmenteerd op aanvraag namen, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63051-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="63051-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="63051-260">TrackException</span></span>
<span data-ttu-id="63051-261">Uitzonderingen naar Application Insights verzenden:</span><span class="sxs-lookup"><span data-stu-id="63051-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="63051-262">Naar [tellen](app-insights-metrics-explorer.md), als een indicatie van de frequentie van een probleem.</span><span class="sxs-lookup"><span data-stu-id="63051-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="63051-263">Naar [onderzoeken van afzonderlijke exemplaren](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="63051-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="63051-264">De rapporten bevatten de stack-traces.</span><span class="sxs-lookup"><span data-stu-id="63051-264">The reports include the stack traces.</span></span>

<span data-ttu-id="63051-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="63051-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="63051-267">De SDK's catch veel uitzonderingen automatisch, dus u niet altijd hebt TrackException expliciet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="63051-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="63051-268">ASP.NET: [schrijven van code voor het onderscheppen](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="63051-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="63051-269">J2EE: [uitzonderingen worden aangetroffen, automatisch](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="63051-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="63051-270">JavaScript: Uitzonderingen worden automatisch aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="63051-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="63051-271">Als u uitschakelen van automatische verzameling wilt, moet u een regel toegevoegd aan het codefragment die u in uw webpagina's invoegt:</span><span class="sxs-lookup"><span data-stu-id="63051-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="63051-272">Uitzonderingen in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-272">Exceptions in Analytics</span></span>

<span data-ttu-id="63051-273">In [Application Insights Analytics](app-insights-analytics.md), uitzonderingen weergegeven in de `exceptions` tabel.</span><span class="sxs-lookup"><span data-stu-id="63051-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="63051-274">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, de `itemCount` eigenschap geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="63051-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="63051-275">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen naar trackException() het proces steekproeven alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="63051-276">Als u een juiste aantal uitzonderingen gesegmenteerd op type uitzondering, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63051-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="63051-277">De meeste informatie belangrijk stack al wordt geëxtraheerd in verschillende variabelen, maar u kunt ophalen uit elkaar de `details` structuur om meer te halen.</span><span class="sxs-lookup"><span data-stu-id="63051-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="63051-278">Aangezien deze structuur dynamisch is, moet u het resultaat dat het verwachte type converteren.</span><span class="sxs-lookup"><span data-stu-id="63051-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="63051-279">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63051-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="63051-280">Om te koppelen uitzonderingen met hun verwante aanvragen, gebruikt u een join:</span><span class="sxs-lookup"><span data-stu-id="63051-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="63051-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="63051-281">TrackTrace</span></span>
<span data-ttu-id="63051-282">Gebruik TrackTrace om u te helpen bij het analyseren van problemen door een spoor' breadcrumb' te sturen naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="63051-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="63051-283">U kunt segmenten van diagnostische gegevens verzenden en controleren ze op in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="63051-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="63051-284">[Meld u adapters](app-insights-asp-net-trace-logs.md) deze API gebruikt van derden om Logboeken te verzenden naar de portal.</span><span class="sxs-lookup"><span data-stu-id="63051-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="63051-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="63051-286">U kunt zoeken op de inhoud van het bericht, maar (in tegenstelling tot eigenschapswaarden) u kunt niet filteren op het.</span><span class="sxs-lookup"><span data-stu-id="63051-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="63051-287">De maximale grootte op `message` veel hoger is dan de limiet voor eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="63051-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="63051-288">U kunt relatief lange gegevens plaatsen in het bericht heeft als voordeel van TrackTrace.</span><span class="sxs-lookup"><span data-stu-id="63051-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="63051-289">U kunt bijvoorbeeld er postgegevens coderen.</span><span class="sxs-lookup"><span data-stu-id="63051-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="63051-290">U kunt bovendien een urgentieniveau toevoegen aan het bericht.</span><span class="sxs-lookup"><span data-stu-id="63051-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="63051-291">En net als andere telemetrie u eigenschapswaarden om u te helpen filter of zoeken naar verschillende sets van traceringen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="63051-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="63051-292">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63051-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="63051-293">In [Search](app-insights-diagnostic-search.md), u kunt eenvoudig filteren vervolgens alle berichten van een specifieke ernst die betrekking op een bepaalde database hebben.</span><span class="sxs-lookup"><span data-stu-id="63051-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="63051-294">Traceringen in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-294">Traces in Analytics</span></span>

<span data-ttu-id="63051-295">In [Application Insights Analytics](app-insights-analytics.md), aanroepen naar TrackTrace weergegeven in de `traces` tabel.</span><span class="sxs-lookup"><span data-stu-id="63051-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="63051-296">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, de eigenschap itemCount geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="63051-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="63051-297">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen naar `trackTrace()`, een van deze alleen in het proces steekproeven worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="63051-298">Als u het juiste aantal traceringsaanroepen, moet u daarom code zoals `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="63051-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="63051-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="63051-299">TrackDependency</span></span>
<span data-ttu-id="63051-300">Gebruik de TrackDependency-aanroep voor het bijhouden van de responstijden en het succespercentage van aanroepen naar externe code.</span><span class="sxs-lookup"><span data-stu-id="63051-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="63051-301">De resultaten worden weergegeven in de afhankelijkheidsgrafiek in de portal.</span><span class="sxs-lookup"><span data-stu-id="63051-301">The results appear in the dependency charts in the portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="63051-302">Houd er rekening mee dat de server SDK's bevatten een [afhankelijkheid module](app-insights-asp-net-dependencies.md) die worden gedetecteerd en bijgehouden bepaalde afhankelijkheidsaanroepen automatisch--bijvoorbeeld databases en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="63051-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="63051-303">U moet een agent installeren op uw server om te maken van de module werken.</span><span class="sxs-lookup"><span data-stu-id="63051-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="63051-304">U kunt deze aanroep gebruiken als u wilt bijhouden van de oproepen die de geautomatiseerde tracering niet catch- of als u niet wilt dat de agent te installeren.</span><span class="sxs-lookup"><span data-stu-id="63051-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="63051-305">Schakel uit de standaard afhankelijkheid bijhouden module bewerken [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) en verwijder de verwijzing naar `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="63051-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="63051-306">Afhankelijkheden in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-306">Dependencies in Analytics</span></span>

<span data-ttu-id="63051-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency belt weergeven de `dependencies` tabel.</span><span class="sxs-lookup"><span data-stu-id="63051-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="63051-308">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, de eigenschap itemCount geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="63051-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="63051-309">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen naar trackDependency() het proces steekproeven alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="63051-310">Als u een juiste aantal gesegmenteerd op doelonderdeel afhankelijkheden, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63051-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="63051-311">Om te koppelen afhankelijkheden met hun verwante aanvragen, gebruikt u een join:</span><span class="sxs-lookup"><span data-stu-id="63051-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="63051-312">Gegevens leegmaken</span><span class="sxs-lookup"><span data-stu-id="63051-312">Flushing data</span></span>
<span data-ttu-id="63051-313">Normaal gesproken verzendt de SDK op tijdstippen wilt minimaliseren, de gevolgen voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="63051-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="63051-314">Echter, in sommige gevallen u mogelijk wilt leegmaken van de buffer--bijvoorbeeld als u de SDK gebruikt in een toepassing die wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="63051-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="63051-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="63051-316">Houd er rekening mee dat de functie asynchroon is voor de [telemetrie-serverkanaal](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="63051-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="63051-317">Geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="63051-317">Authenticated users</span></span>
<span data-ttu-id="63051-318">In een web-app, worden gebruikers (standaard) geïdentificeerd door cookies.</span><span class="sxs-lookup"><span data-stu-id="63051-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="63051-319">Een gebruiker mogelijk meer dan één keer worden geteld als ze toegang krijgen tot uw app uit een andere computer of de browser, of als het verwijderen van cookies.</span><span class="sxs-lookup"><span data-stu-id="63051-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="63051-320">Als gebruikers zich bij uw app aanmelden, kunt u een meer nauwkeurige telling krijgen door de geverifieerde gebruiker-ID in te stellen in de browser-code:</span><span class="sxs-lookup"><span data-stu-id="63051-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="63051-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="63051-322">In een ASP.NET-webtoepassing MVC-toepassing, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63051-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="63051-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="63051-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="63051-324">Het is niet nodig om werkelijke van de gebruiker aanmelden namen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63051-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="63051-325">Alleen er moet een ID die uniek is voor die gebruiker.</span><span class="sxs-lookup"><span data-stu-id="63051-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="63051-326">Mag geen spaties of een van de tekens bevatten `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="63051-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="63051-327">De gebruikers-ID is ook in een sessiecookie ingesteld en verzonden naar de server.</span><span class="sxs-lookup"><span data-stu-id="63051-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="63051-328">Als de SDK-server is geïnstalleerd, wordt de geverifieerde gebruiker-ID verzonden als onderdeel van de contexteigenschappen van zowel client als server telemetrie.</span><span class="sxs-lookup"><span data-stu-id="63051-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="63051-329">Vervolgens kunt u filteren en zoekt u erop.</span><span class="sxs-lookup"><span data-stu-id="63051-329">You can then filter and search on it.</span></span>

<span data-ttu-id="63051-330">Als uw app gebruikers naar accounts groepen, kunt u ook een id voor het account (met de tekenbeperkingen voor dezelfde) doorgeven.</span><span class="sxs-lookup"><span data-stu-id="63051-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="63051-331">In [Metrics Explorer](app-insights-metrics-explorer.md), kunt u een diagram waarin telt **geverifieerde gebruikers,**, en **gebruikersaccounts**.</span><span class="sxs-lookup"><span data-stu-id="63051-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="63051-332">U kunt ook [search](app-insights-diagnostic-search.md) voor client gegevenspunten met specifieke gebruikersnamen en accounts.</span><span class="sxs-lookup"><span data-stu-id="63051-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="63051-333"><a name="properties"></a>Filteren, zoeken en segmenteren van uw gegevens met behulp van eigenschappen</span><span class="sxs-lookup"><span data-stu-id="63051-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="63051-334">U kunt eigenschappen en metingen koppelen aan uw gebeurtenissen (en ook met metrische gegevens en pagina weergaven, uitzonderingen en andere telemetriegegevens).</span><span class="sxs-lookup"><span data-stu-id="63051-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="63051-335">*Eigenschappen* tekenreekswaarden die u gebruiken kunt voor het filteren van uw telemetrie in de rapporten zijn.</span><span class="sxs-lookup"><span data-stu-id="63051-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="63051-336">Bijvoorbeeld, als uw app verschillende games biedt, kunt u de naam van het spel aan koppelen elke gebeurtenis zodat u kunt zien welke games populairder zijn.</span><span class="sxs-lookup"><span data-stu-id="63051-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="63051-337">Er is een limiet van 8192 op de string-lengte.</span><span class="sxs-lookup"><span data-stu-id="63051-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="63051-338">(Als u grote reeksen gegevens verzenden wilt, gebruikt u de bericht-parameter van [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="63051-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="63051-339">*Metrische gegevens* zijn numerieke waarden die kunnen worden weergegeven als geïllustreerd.</span><span class="sxs-lookup"><span data-stu-id="63051-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="63051-340">U wilt zien of er een geleidelijke toename van de scores die uw gamers bereiken.</span><span class="sxs-lookup"><span data-stu-id="63051-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="63051-341">De grafieken kunnen worden gesegmenteerd op de eigenschappen die worden verzonden met de gebeurtenis, zodat u kunt afzonderlijke ophalen of gestapeld grafieken voor verschillende games.</span><span class="sxs-lookup"><span data-stu-id="63051-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="63051-342">Ze moeten groter zijn dan of gelijk zijn aan 0 zijn voor metrische waarden moet correct worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63051-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="63051-343">Er zijn een aantal [beperkingen met betrekking tot het aantal eigenschappen en eigenschapswaarden metrische gegevens](#limits) die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63051-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="63051-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="63051-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="63051-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="63051-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="63051-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="63051-348">Zorgt niet voor logboekregistratie van persoonsgegevens in de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="63051-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="63051-349">*Als u metrische gegevens gebruikt*, Metrics Explorer openen en selecteer de metrische gegevens van de **aangepaste** groep:</span><span class="sxs-lookup"><span data-stu-id="63051-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Openen van Metrics Explorer, selecteert u de grafiek en selecteer de metriek](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="63051-351">Als uw metriek niet wordt weergegeven, of als de **aangepaste** kop niet het geval is, sluit de blade selectie en probeer het later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="63051-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="63051-352">Metrische gegevens kunt soms uur duren voordat de een aggregatie worden uitgevoerd via de pipeline.</span><span class="sxs-lookup"><span data-stu-id="63051-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="63051-353">*Als u de eigenschappen en metrische gegevens gebruikt*, de metriek segmenteren door de eigenschap:</span><span class="sxs-lookup"><span data-stu-id="63051-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Stel groeperen en selecteer vervolgens de eigenschap onder groeperen op](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="63051-355">*In Diagnostic Search*, kunt u de eigenschappen en metrische gegevens van afzonderlijke instanties van een gebeurtenis bekijken.</span><span class="sxs-lookup"><span data-stu-id="63051-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Selecteer een exemplaar en selecteer vervolgens '...'](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="63051-357">Gebruik de **Search** veld voor een overzicht van de gebeurtenis-instanties die een bepaalde eigenschappenwaarde hebben.</span><span class="sxs-lookup"><span data-stu-id="63051-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Typ een term in zoeken](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="63051-359">[Meer informatie over zoekopdracht expressies](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="63051-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="63051-360">Eigenschappen en metrische gegevens ook instellen</span><span class="sxs-lookup"><span data-stu-id="63051-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="63051-361">Als het is eenvoudiger, kunt u de parameters van een gebeurtenis in een afzonderlijk object verzamelen:</span><span class="sxs-lookup"><span data-stu-id="63051-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="63051-362">De hetzelfde exemplaar van de telemetrie-item niet hergebruiken (`event` in dit voorbeeld) Track*() meerdere keren aanroepen.</span><span class="sxs-lookup"><span data-stu-id="63051-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="63051-363">Dit kan leiden tot telemetrie met onjuiste configuratie worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="63051-364">Aangepaste metingen en eigenschappen in Analytics</span><span class="sxs-lookup"><span data-stu-id="63051-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="63051-365">In [Analytics](app-insights-analytics.md), eigenschappen en aangepaste metrische gegevens weergeven in de `customMeasurements` en `customDimensions` kenmerken van elke record telemetrie.</span><span class="sxs-lookup"><span data-stu-id="63051-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="63051-366">Bijvoorbeeld, als u een eigenschap genaamd 'spel' de aanvraagtelemetrie van uw hebt toegevoegd, deze query telt instanties van verschillende waarden van 'spel' en het gemiddelde van de aangepaste metrische 'score' weergeven:</span><span class="sxs-lookup"><span data-stu-id="63051-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="63051-367">U ziet dat:</span><span class="sxs-lookup"><span data-stu-id="63051-367">Notice that:</span></span>

* <span data-ttu-id="63051-368">Wanneer u een waarde van de customDimensions of customMeasurements JSON uitpakt, hieraan dynamische type, en zodat u dit casten `tostring` of `todouble`.</span><span class="sxs-lookup"><span data-stu-id="63051-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="63051-369">Rekening te houden met de mogelijkheid van [steekproeven](app-insights-sampling.md), moet u `sum(itemCount)`, niet `count()`.</span><span class="sxs-lookup"><span data-stu-id="63051-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="63051-370"><a name="timed"></a>Timing van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="63051-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="63051-371">Soms wilt u grafiek hoe lang het duurt om een actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="63051-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="63051-372">Bijvoorbeeld, u wilt mogelijk weten hoe lang gebruikers nemen op in een spel te overwegen.</span><span class="sxs-lookup"><span data-stu-id="63051-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="63051-373">Hiervoor kunt u de parameter meting.</span><span class="sxs-lookup"><span data-stu-id="63051-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="63051-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="63051-375"><a name="defaults"></a>Standaard-eigenschappen voor aangepaste telemetrie</span><span class="sxs-lookup"><span data-stu-id="63051-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="63051-376">Als u standaard eigenschapswaarden instellen voor een aantal aangepaste gebeurtenissen die u schrijft wilt, kunt u ze in een exemplaar van TelemetryClient instellen.</span><span class="sxs-lookup"><span data-stu-id="63051-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="63051-377">Deze zijn gekoppeld aan elk telemetrie-item dat wordt verzonden door de client.</span><span class="sxs-lookup"><span data-stu-id="63051-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="63051-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="63051-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="63051-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="63051-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="63051-381">Afzonderlijke telemetrie aanroepen kunnen u de standaardwaarden in hun woordenlijsten eigenschap overschrijven.</span><span class="sxs-lookup"><span data-stu-id="63051-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="63051-382">*Web voor JavaScript-clients*, [gebruik van JavaScript telemetrie initalisatiefuncties](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="63051-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="63051-383">*Eigenschappen toevoegen aan alle telemetrie*, met inbegrip van de gegevens van de standaardregel voor verzameling modules, [implementeren `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="63051-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="63051-384">Steekproef nemen en verwerken van telemetrie filteren</span><span class="sxs-lookup"><span data-stu-id="63051-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="63051-385">U kunt de code voor het verwerken van uw telemetrie voordat deze wordt verzonden van de SDK schrijven.</span><span class="sxs-lookup"><span data-stu-id="63051-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="63051-386">De verwerking omvat gegevens dat wordt verzonden door de standaard telemetrie-modules, zoals de verzameling van de HTTP-aanvragen en afhankelijkheid verzameling.</span><span class="sxs-lookup"><span data-stu-id="63051-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="63051-387">[Eigenschappen toevoegen](app-insights-api-filtering-sampling.md#add-properties) naar telemetrie door het implementeren van `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="63051-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="63051-388">U kunt bijvoorbeeld versienummers of berekende waarden toevoegen van andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="63051-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="63051-389">[Filteren](app-insights-api-filtering-sampling.md#filtering) kunt wijzigen of verwijderen van telemetrie voordat het wordt verzonden door de SDK door het implementeren van `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="63051-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="63051-390">U bepaalt wat wordt verzonden naar of verwijderd, maar u moet voor het effect op de metrische gegevens over uw account.</span><span class="sxs-lookup"><span data-stu-id="63051-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="63051-391">Afhankelijk van hoe u items negeren, kunt u de mogelijkheid om te navigeren tussen verwante items verliezen.</span><span class="sxs-lookup"><span data-stu-id="63051-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="63051-392">[Steekproef nemen](app-insights-api-filtering-sampling.md) is een ingepakte oplossing te verminderen de hoeveelheid gegevens die door uw app wordt verzonden naar de portal.</span><span class="sxs-lookup"><span data-stu-id="63051-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="63051-393">Hierbij wordt zonder de weergegeven metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="63051-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="63051-394">En zonder de mogelijkheid om te analyseren van problemen door te navigeren tussen verwante items zoals uitzonderingen, aanvragen en paginaweergaven beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="63051-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="63051-395">[Meer informatie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="63051-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="63051-396">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="63051-396">Disabling telemetry</span></span>
<span data-ttu-id="63051-397">Naar *dynamisch stoppen en starten* het verzamelen en verzenden van telemetrie:</span><span class="sxs-lookup"><span data-stu-id="63051-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="63051-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="63051-399">Naar *uitschakelen geselecteerde standaard collectors*--bijvoorbeeld, prestatiemeteritems, HTTP-aanvragen of afhankelijkheden--verwijderen of de relevante regels in uitcommentariëren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). U kunt dit bijvoorbeeld doen als u wilt de gegevens van uw eigen TrackRequest verzenden.</span><span class="sxs-lookup"><span data-stu-id="63051-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="63051-400"><a name="debug"></a>Modus voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="63051-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="63051-401">Tijdens de foutopsporing, is het nuttig om uw telemetrie afgehandeld via de pipeline, zodat u resultaten onmiddellijk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="63051-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="63051-402">U ook get extra berichten sturen die u helpen traceren problemen met de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="63051-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="63051-403">Schakel deze uit in productie, omdat dit kan uw app vertragen.</span><span class="sxs-lookup"><span data-stu-id="63051-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="63051-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="63051-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="63051-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="63051-406"><a name="ikey"></a>De instrumentatiesleutel voor de geselecteerde aangepaste telemetrie instellen</span><span class="sxs-lookup"><span data-stu-id="63051-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="63051-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="63051-408"><a name="dynamic-ikey"></a>Dynamische instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="63051-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="63051-409">Om te voorkomen dat de combinatie van telemetrie van ontwikkeling, testen en productieomgevingen, kunt u [afzonderlijke Application Insights-resources maken](app-insights-create-new-resource.md) en wijzigt u de sleutels, afhankelijk van de omgeving.</span><span class="sxs-lookup"><span data-stu-id="63051-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="63051-410">In plaats van de instrumentatiesleutel ophalen uit het configuratiebestand, kunt u dit instellen in uw code.</span><span class="sxs-lookup"><span data-stu-id="63051-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="63051-411">Stel de sleutel in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice:</span><span class="sxs-lookup"><span data-stu-id="63051-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="63051-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="63051-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="63051-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="63051-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="63051-414">In webpagina's, is het raadzaam om deze te stellen van de webserver status, in plaats van letterlijk coderen in het script.</span><span class="sxs-lookup"><span data-stu-id="63051-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="63051-415">Bijvoorbeeld in een webpagina in een ASP.NET-app gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="63051-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="63051-416">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="63051-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="63051-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="63051-417">TelemetryContext</span></span>
<span data-ttu-id="63051-418">TelemetryClient heeft een contexteigenschap die waarden bevat die samen met alle telemetriegegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="63051-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="63051-419">Normaal gesproken zijn ingesteld door de standaard telemetrie-modules, maar u kunt ook instellen ze zelf.</span><span class="sxs-lookup"><span data-stu-id="63051-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="63051-420">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63051-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="63051-421">Als u een van deze waarden zelf instellen, kunt u overwegen verwijderen van de betreffende regel uit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), zodat uw waarden en de standaard waarden niet veranderen.</span><span class="sxs-lookup"><span data-stu-id="63051-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="63051-422">**Onderdeel**: de app en de versie ervan.</span><span class="sxs-lookup"><span data-stu-id="63051-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="63051-423">**Apparaat**: gegevens over het apparaat waarop de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63051-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="63051-424">(In web-apps is dit de server of client-apparaat dat de telemetrie van wordt verzonden.)</span><span class="sxs-lookup"><span data-stu-id="63051-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="63051-425">**InstrumentationKey**: de Application Insights-resource in Azure waar de telemetrie worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63051-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="63051-426">Dit wordt gewoonlijk opgenomen in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="63051-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="63051-427">**Locatie**: de geografische locatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="63051-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="63051-428">**Bewerking**: In web-apps, de huidige HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="63051-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="63051-429">In andere typen Apps die kunt u dit instellen op gebeurtenissen groeperen samen.</span><span class="sxs-lookup"><span data-stu-id="63051-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="63051-430">**Id**: een gegenereerde waarde die verschillende gebeurtenissen, zodat wanneer u een gebeurtenis in Diagnostic Search inspecteert, u vindt verwante objecten.</span><span class="sxs-lookup"><span data-stu-id="63051-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="63051-431">**Naam**: een meestal de URL van de HTTP-aanvraag-id.</span><span class="sxs-lookup"><span data-stu-id="63051-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="63051-432">**SyntheticSource**: als dat niet null of leeg is, moet een tekenreeks die aangeeft dat de bron van de aanvraag is geïdentificeerd als een robot of web-test.</span><span class="sxs-lookup"><span data-stu-id="63051-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="63051-433">Standaard wordt het uitgesloten van berekeningen in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="63051-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="63051-434">**Eigenschappen**: eigenschappen die worden verzonden met alle telemetriegegevens.</span><span class="sxs-lookup"><span data-stu-id="63051-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="63051-435">Deze kan worden genegeerd in afzonderlijke bijhouden * aanroepen.</span><span class="sxs-lookup"><span data-stu-id="63051-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="63051-436">**Sessie**: de gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="63051-436">**Session**: The user's session.</span></span> <span data-ttu-id="63051-437">De ID wordt ingesteld op een gegenereerde waarde, die wordt gewijzigd wanneer de gebruiker niet actief is geweest even.</span><span class="sxs-lookup"><span data-stu-id="63051-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="63051-438">**Gebruiker**: gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="63051-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="63051-439">Limieten</span><span class="sxs-lookup"><span data-stu-id="63051-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="63051-440">Gebruiken om te voorkomen roept de frequentielimiet gegevens, [steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="63051-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="63051-441">Om te bepalen hoe lang gegevens wordt opgeslagen, Zie [bewaren van gegevens en privacy](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="63051-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="63051-442">Referentiedocumenten</span><span class="sxs-lookup"><span data-stu-id="63051-442">Reference docs</span></span>
* [<span data-ttu-id="63051-443">ASP.NET-verwijzing</span><span class="sxs-lookup"><span data-stu-id="63051-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="63051-444">Naslaginformatie over Java</span><span class="sxs-lookup"><span data-stu-id="63051-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="63051-445">Verwijzing in JavaScript</span><span class="sxs-lookup"><span data-stu-id="63051-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="63051-446">Android-SDK</span><span class="sxs-lookup"><span data-stu-id="63051-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="63051-447">iOS-SDK</span><span class="sxs-lookup"><span data-stu-id="63051-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="63051-448">SDK-code</span><span class="sxs-lookup"><span data-stu-id="63051-448">SDK code</span></span>
* [<span data-ttu-id="63051-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="63051-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="63051-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="63051-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="63051-451">Windows Server-pakketten</span><span class="sxs-lookup"><span data-stu-id="63051-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="63051-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="63051-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="63051-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="63051-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="63051-454">Alle platforms</span><span class="sxs-lookup"><span data-stu-id="63051-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="63051-455">Vragen</span><span class="sxs-lookup"><span data-stu-id="63051-455">Questions</span></span>
* <span data-ttu-id="63051-456">*Welke uitzonderingen's Track_() aanroepen weggooien*</span><span class="sxs-lookup"><span data-stu-id="63051-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="63051-457">Geen.</span><span class="sxs-lookup"><span data-stu-id="63051-457">None.</span></span> <span data-ttu-id="63051-458">U hoeft niet laten teruglopen ze in trycatch-componenten.</span><span class="sxs-lookup"><span data-stu-id="63051-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="63051-459">Als de SDK-problemen, wordt deze berichten aanmelden uitvoer van de console voor foutopsporing en--als de berichten via--in diagnostische gegevens doorzoeken ophalen.</span><span class="sxs-lookup"><span data-stu-id="63051-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="63051-460">*Is er een REST-API om gegevens te verkrijgen via de portal?*</span><span class="sxs-lookup"><span data-stu-id="63051-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="63051-461">Ja, de [data access-API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="63051-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="63051-462">Andere manieren om gegevens te extraheren, bijvoorbeeld [van analytische gegevens exporteren naar Power BI](app-insights-export-power-bi.md) en [continue export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="63051-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="63051-463"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63051-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="63051-464">Zoekopdracht gebeurtenissen en Logboeken</span><span class="sxs-lookup"><span data-stu-id="63051-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="63051-465">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="63051-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


