---
title: aaaApplication Insights-API voor aangepaste gebeurtenissen en metrische gegevens | Microsoft Docs
description: Invoegen van een paar regels code in het gebruik van uw apparaat of bureaublad-app, een webpagina of service, tootrack en onderzoeken van problemen.
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
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="c7ca9-103">Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c7ca9-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="c7ca9-104">Een paar regels code in uw toepassing toofind uit wat gebruikers met het doen invoegen of toohelp vaststellen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="c7ca9-105">U kunt telemetrie verzenden van apparaat- en bureaublad-apps, webserver en webclients en webservers.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="c7ca9-106">Gebruik Hallo [Azure Application Insights](app-insights-overview.md) telemetrie-API toosend aangepaste gebeurtenissen en metrische gegevens en uw eigen versies standaardtelemetrie core.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="c7ca9-107">Deze API is Hallo dezelfde API die Hallo standaard Application Insights gegevens collectors gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="c7ca9-108">API-overzicht</span><span class="sxs-lookup"><span data-stu-id="c7ca9-108">API summary</span></span>
<span data-ttu-id="c7ca9-109">Hallo API is uniform op alle platforms, naast een paar kleine verschillen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="c7ca9-110">Methode</span><span class="sxs-lookup"><span data-stu-id="c7ca9-110">Method</span></span> | <span data-ttu-id="c7ca9-111">Gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="c7ca9-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="c7ca9-112">Pagina's, schermen, blades of formulieren.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="c7ca9-113">Acties van gebruikers en andere gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-113">User actions and other events.</span></span> <span data-ttu-id="c7ca9-114">Tootrack gebruiker gedrag of toomonitor prestaties gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="c7ca9-115">Prestatiemetingen zoals wachtrij lengten niet gerelateerd toospecific gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="c7ca9-116">Logboekregistratie uitzonderingen voor diagnose.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="c7ca9-117">Traceren waarin ze in de relatie tooother gebeurtenissen optreden en stack-traces onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="c7ca9-118">Logboekregistratie Hallo frequentie en duur van serveraanvragen voor analyse van prestaties.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="c7ca9-119">Diagnostische logboeken-berichten.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-119">Diagnostic log messages.</span></span> <span data-ttu-id="c7ca9-120">U kunt ook de logboeken van derden vastleggen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="c7ca9-121">Logboekregistratie Hallo duur en frequentie van aanroepen tooexternal onderdelen die afhankelijk van uw app.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="c7ca9-122">U kunt [eigenschappen en metrische gegevens koppelen](#properties) toomost telemetrie aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="c7ca9-123"><a name="prep"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c7ca9-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="c7ca9-124">Als u nog een verwijzing op Application Insights-SDK hebt:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="c7ca9-125">Hallo Application Insights-SDK tooyour project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="c7ca9-126">ASP.NET-project</span><span class="sxs-lookup"><span data-stu-id="c7ca9-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="c7ca9-127">Java-project</span><span class="sxs-lookup"><span data-stu-id="c7ca9-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="c7ca9-128">JavaScript in elke webpagina</span><span class="sxs-lookup"><span data-stu-id="c7ca9-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="c7ca9-129">In uw servercode apparaat of een webtoepassing omvatten:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="c7ca9-130">*C#:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="c7ca9-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="c7ca9-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="c7ca9-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="c7ca9-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="c7ca9-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="c7ca9-133">Een exemplaar TelemetryClient maken</span><span class="sxs-lookup"><span data-stu-id="c7ca9-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="c7ca9-134">Maken van een exemplaar van `TelemetryClient` (behalve in JavaScript in webpagina's):</span><span class="sxs-lookup"><span data-stu-id="c7ca9-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="c7ca9-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="c7ca9-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="c7ca9-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="c7ca9-138">TelemetryClient is thread-safe.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="c7ca9-139">Het is raadzaam om gebruik te maken van een instantie van TelemetryClient voor elke module van uw app.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="c7ca9-140">Bijvoorbeeld: mogelijk hebt u één exemplaar van TelemetryClient in uw web-service tooreport binnenkomende HTTP-aanvragen en andere in een middleware klasse tooreport zakelijke logica gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="c7ca9-141">U kunt eigenschappen instellen, zoals `TelemetryClient.Context.User.Id` tootrack gebruikers en sessies, of `TelemetryClient.Context.Device.Id` tooidentify Hallo machine.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="c7ca9-142">Deze informatie is aangesloten tooall gebeurtenissen die Hallo exemplaar verzendt.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="c7ca9-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="c7ca9-143">TrackEvent</span></span>
<span data-ttu-id="c7ca9-144">In Application Insights, een *aangepaste gebeurtenis* is van een gegevenspunt geldt dat u kunt weergeven in [Metrics Explorer](app-insights-metrics-explorer.md) als een verzamelde aantal en in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md) als afzonderlijke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="c7ca9-145">(Niet verwant tooMVC of andere framework 'gebeurtenissen'.)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="c7ca9-146">Invoegen `TrackEvent` roept in uw code toocount diverse gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="c7ca9-147">Hoe vaak gebruikers kiest voor een bepaalde functie, hoe vaak ze bepaalde doelen bereiken of zij mogelijk hoe vaak voor bepaalde soorten fouten.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="c7ca9-148">Bijvoorbeeld in een gameapps een gebeurtenis wanneer een gebruiker wins Hallo game verzenden:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="c7ca9-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="c7ca9-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="c7ca9-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="c7ca9-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="c7ca9-153">De gebeurtenissen in Microsoft Azure-portal Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="c7ca9-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="c7ca9-154">toosee een aantal van uw gebeurtenissen, open een [Metrics Explorer](app-insights-metrics-explorer.md) blade, Voeg een nieuwe grafiek toe en selecteer **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Zie een aantal aangepaste gebeurtenissen](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="c7ca9-156">toocompare hello tellingen van verschillende gebeurtenissen ingesteld Hallo grafiektype te**raster**, and -groep met de gebeurtenisnaam:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Hallo grafiektype en groepering instellen](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="c7ca9-158">Klik op Hallo raster in een gebeurtenis naam toosee afzonderlijke exemplaren van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="c7ca9-159">toosee specifieke - klikt u op elk exemplaar in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-159">toosee more detail - click any occurrence in hello list.</span></span>

![Drillthrough-Hallo-gebeurtenissen](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="c7ca9-161">toofocus van specifieke gebeurtenissen in de zoekopdracht of Metrics Explorer set Hallo blade filter toohello gebeurtenisnamen die u geïnteresseerd bent in:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Open Filters, vouw de naam van de gebeurtenis en selecteer een of meer waarden](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="c7ca9-163">Aangepaste gebeurtenissen in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-163">Custom events in Analytics</span></span>

<span data-ttu-id="c7ca9-164">Hallo telemetrie is beschikbaar in Hallo `customEvents` in tabel [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="c7ca9-165">Elke rij vertegenwoordigt een gesprek te`trackEvent(..)` in uw app.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="c7ca9-166">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="c7ca9-167">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackEvent(), Hallo steekproeven proces alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="c7ca9-168">tooget het juiste aantal aangepaste gebeurtenissen, moet u daarom code gebruiken zoals `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="c7ca9-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="c7ca9-169">TrackMetric</span></span>

<span data-ttu-id="c7ca9-170">Application Insights kunnen metrische gegevens die niet aangesloten tooparticular gebeurtenissen zijn van grafiekgebied.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="c7ca9-171">U kan bijvoorbeeld een wachtrijlengte bewaken met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="c7ca9-172">Hallo afzonderlijke metingen zijn minder interessant dan Hallo variaties en trends met metrische gegevens, en dus statistische kolomdiagrammen zijn nuttig.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="c7ca9-173">In order toosend metrische gegevens tooApplication inzichten, kunt u Hallo `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="c7ca9-174">Er zijn twee manieren toosend metric:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="c7ca9-175">Enkele waarde.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-175">Single value.</span></span> <span data-ttu-id="c7ca9-176">Telkens wanneer u een meting in uw toepassing uitvoert, verzendt u overeenkomende waarde Hallo tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="c7ca9-177">Bijvoorbeeld, wordt ervan uitgegaan dat u hebt een metriek Hallo aantal items in een container te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="c7ca9-178">U voor het eerst drie items in Hallo container geplaatst en verwijder vervolgens twee items gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="c7ca9-179">Dienovereenkomstig, roept u `TrackMetric` tweemaal: eerst doorgegeven waarde Hallo `3` en vervolgens Hallo waarde `-2`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="c7ca9-180">Application Insights worden beide waarden opgeslagen namens jou.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="c7ca9-181">Aggregatie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-181">Aggregation.</span></span> <span data-ttu-id="c7ca9-182">Als u werkt met metrische gegevens, wordt elke meting zelden is van belang.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="c7ca9-183">In plaats daarvan is een overzicht van wat er gebeurd gedurende een bepaalde periode is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="c7ca9-184">Dergelijke samenvatting heet _aggregatie_.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="c7ca9-185">Hallo hierboven voorbeeld Hallo cumulatieve metrische som gedurende deze periode is `1` en Hallo Hallo metrische waarden aantal `2`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="c7ca9-186">Wanneer u Hallo aggregatie benadering, u alleen aanroepen `TrackMetric` eenmaal per periode en verzenden Hallo geaggregeerde tijdwaarden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="c7ca9-187">Dit is Hallo aanbevolen benadering omdat Hallo kosten aantasten kan en prestaties van de overhead door minder gegevens te verzenden tooApplication Insights, punten tijdens het verzamelen van nog steeds alle relevante informatie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="c7ca9-188">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="c7ca9-189">Enkele waarden</span><span class="sxs-lookup"><span data-stu-id="c7ca9-189">Single values</span></span>

<span data-ttu-id="c7ca9-190">toosend metrische waarde voor een enkele:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-190">toosend a single metric value:</span></span>

<span data-ttu-id="c7ca9-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="c7ca9-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="c7ca9-193">Samenvoegen van metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c7ca9-193">Aggregating metrics</span></span>

<span data-ttu-id="c7ca9-194">Het verdient aanbeveling tooaggregate metrische gegevens voordat ze worden verzonden vanuit uw app, tooreduce bandbreedte, kosten en tooimprove prestaties.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="c7ca9-195">Hier volgt een voorbeeld van code verzamelen:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="c7ca9-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-196">*C#*</span></span>

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
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
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
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="c7ca9-197">Aangepaste metrische gegevens in Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="c7ca9-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="c7ca9-198">toosee hello resultaten Metrics Explorer openen en een nieuwe grafiek toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="c7ca9-199">Hallo grafiek tooshow uw metriek bewerken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-200">Uw aangepaste metric duurt enkele minuten tooappear in Hallo lijst met beschikbare metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Voeg een nieuwe grafiek toe of Selecteer een grafiek en onder aangepast, selecteer uw metrische gegevens](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="c7ca9-202">Aangepaste metrische gegevens in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="c7ca9-203">Hallo telemetrie is beschikbaar in Hallo `customMetrics` in tabel [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="c7ca9-204">Elke rij vertegenwoordigt een gesprek te`trackMetric(..)` in uw app.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="c7ca9-205">`valueSum`-Dit is de som Hallo Hallo metingen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="c7ca9-206">tooget hello gemiddelde waarde delen door `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="c7ca9-207">`valueCount`-aantal van de metingen die zijn samengevoegd in dit Hallo `trackMetric(..)` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="c7ca9-208">Paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="c7ca9-208">Page views</span></span>
<span data-ttu-id="c7ca9-209">In een app-apparaat of webpagina telemetrie van paginaweergaven standaard verzonden wanneer elke pagina of het scherm wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="c7ca9-210">Maar u kunt deze paginaweergaven tootrack wijzigen op aanvullende of verschillende tijdstippen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="c7ca9-211">Bijvoorbeeld in een app die wordt weergegeven voor tabbladen of blades, kunt u een pagina tootrack wanneer Hallo gebruiker een nieuwe blade opent.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Gebruik lens op de blade overzicht](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="c7ca9-213">Gebruikers- en sessiegegevens gegevens verzonden zoals eigenschappen samen met paginaweergaven, zodat gebruikers- en sessiegegevens grafieken tot leven komen als er telemetrie van paginaweergaven Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="c7ca9-214">Aangepaste paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="c7ca9-214">Custom page views</span></span>
<span data-ttu-id="c7ca9-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="c7ca9-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="c7ca9-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="c7ca9-218">Als u meerdere tabbladen binnen andere HTML-pagina's hebt, kunt u Hallo-URL te opgeven:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="c7ca9-219">Timing van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="c7ca9-219">Timing page views</span></span>
<span data-ttu-id="c7ca9-220">Standaard Hallo keren gerapporteerd als **laadtijd voor paginaweergave** worden gemeten vanuit de browser Hallo Hallo-aanvraag verzendt totdat van de browser van het Hallo-gebeurtenis voor het laden van pagina wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="c7ca9-221">In plaats daarvan kunt u:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-221">Instead, you can either:</span></span>

* <span data-ttu-id="c7ca9-222">Instellen van een expliciete duur in Hallo [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) aanroepen: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="c7ca9-223">Hallo pagina weergave timing aanroepen gebruiken `startTrackPage` en `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="c7ca9-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="c7ca9-225">...</span><span class="sxs-lookup"><span data-stu-id="c7ca9-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="c7ca9-226">Hallo naam die u gebruikt als de eerste parameter Hallo Hallo start koppelt en stop de aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="c7ca9-227">Wordt standaard de naam van toohello huidige pagina.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="c7ca9-228">Hallo resulterende laadtijd weergegeven in Metrics Explorer duur zijn afgeleid van hello-interval tussen Hallo starten en stoppen van aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="c7ca9-229">Is tooyou welke interval die u daadwerkelijk tijd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="c7ca9-230">Pagina telemetrie in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="c7ca9-231">In [Analytics](app-insights-analytics.md) twee tabellen bevatten gegevens van de browser bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="c7ca9-232">Hallo `pageViews` tabel bevat gegevens over de URL- en titel Hallo</span><span class="sxs-lookup"><span data-stu-id="c7ca9-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="c7ca9-233">Hallo `browserTimings` tabel bevat gegevens over de prestaties van de client, zoals Hallo tijd tooprocess Hallo binnenkomende gegevens</span><span class="sxs-lookup"><span data-stu-id="c7ca9-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="c7ca9-234">toofind hoe lang Hallo browser duurt tooprocess verschillende pagina's:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="c7ca9-235">toodiscover hello popularities van verschillende browsers:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="c7ca9-236">aanmelden bij tooassociate pagina weergaven tooAJAX aanroepen met afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="c7ca9-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="c7ca9-237">TrackRequest</span></span>
<span data-ttu-id="c7ca9-238">Hallo server SDK gebruikt TrackRequest toolog HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="c7ca9-239">U kunt deze zelf ook aanroepen als u wilt dat toosimulate aanvragen in een context waarin er geen Hallo web service-module die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="c7ca9-240">Hallo wordt echter aanbevolen manier toosend aanvraagtelemetrie is waar Hallo aanvraag fungeert als een <a href="#operation-context">bewerking context</a>.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="c7ca9-241">Bewerking context</span><span class="sxs-lookup"><span data-stu-id="c7ca9-241">Operation context</span></span>
<span data-ttu-id="c7ca9-242">U kunt telemetrie-items bij elkaar koppelen door het koppelen van toothem een algemene bewerking-ID.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="c7ca9-243">Hallo standaard aanvraag bijhouden module doet dit voor uitzonderingen en andere gebeurtenissen die worden verzonden tijdens het verwerken van een HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="c7ca9-244">In [Search](app-insights-diagnostic-search.md) en [Analytics](app-insights-analytics.md), kunt u Hallo ID tooeasily zoeken naar alle gebeurtenissen die zijn gekoppeld aan het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="c7ca9-245">Hallo gemakkelijkste manier tooset Hallo-ID is tooset de context van een bewerking met behulp van dit patroon:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="c7ca9-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="c7ca9-247">Samen met het instellen van de context van een bewerking `StartOperation` maakt een telemetrie-item van het Hallo-type dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="c7ca9-248">Het Hallo telemetrie item verzendt wanneer buitengebruikstelling Hallo opnieuw, of als u niet expliciet aanroepen `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="c7ca9-249">Als u `RequestTelemetry` als Hallo telemetrie type, de duur is een time-out opgetreden toohello interval tussen starten en stoppen is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="c7ca9-250">Bewerking contexten kunnen niet worden genest.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="c7ca9-251">Als er al een bewerking context bestaat, wordt de bijbehorende ID gekoppeld aan alle Hallo opgenomen items is, inclusief Hallo item dat is gemaakt met `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="c7ca9-252">In de zoekopdracht op Hallo bewerking context is gebruikte toocreate Hallo **verwante Items** lijst:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Verwante items](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="c7ca9-254">Zie [toepassing-insights-aangepaste-bewerkingen-tracking.md] voor meer informatie over aangepaste bewerkingen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="c7ca9-255">Aanvragen in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-255">Requests in Analytics</span></span> 

<span data-ttu-id="c7ca9-256">In [Application Insights Analytics](app-insights-analytics.md), weergeven van aanvragen in Hallo `requests` tabel.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="c7ca9-257">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount eigenschap ziet een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="c7ca9-258">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackRequest(), Hallo steekproeven proces alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="c7ca9-259">tooget het juiste aantal aanvragen en de gemiddelde duur gesegmenteerd op aanvraag namen, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="c7ca9-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="c7ca9-260">TrackException</span></span>
<span data-ttu-id="c7ca9-261">Uitzonderingen tooApplication Insights verzenden:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="c7ca9-262">te[tellen](app-insights-metrics-explorer.md), als een indicatie van Hallo frequentie van een probleem.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="c7ca9-263">te[onderzoeken van afzonderlijke exemplaren](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="c7ca9-264">Hallo-rapporten bevatten Hallo stack-traces.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="c7ca9-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="c7ca9-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="c7ca9-267">Hallo-SDK's catch veel uitzonderingen automatisch, dus u niet altijd toocall TrackException expliciet hebt.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="c7ca9-268">ASP.NET: [code schrijven toocatch uitzonderingen](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="c7ca9-269">J2EE: [uitzonderingen worden aangetroffen, automatisch](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="c7ca9-270">JavaScript: Uitzonderingen worden automatisch aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="c7ca9-271">Als u toodisable automatische verzameling wilt, voegt u een regel toohello codefragment waarmee u in uw webpagina's invoegen:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="c7ca9-272">Uitzonderingen in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-272">Exceptions in Analytics</span></span>

<span data-ttu-id="c7ca9-273">In [Application Insights Analytics](app-insights-analytics.md), uitzonderingen weergegeven in Hallo `exceptions` tabel.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="c7ca9-274">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, hello `itemCount` eigenschap geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="c7ca9-275">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackException(), Hallo steekproeven proces alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="c7ca9-276">tooget het juiste aantal uitzonderingen gesegmenteerd op type uitzondering, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="c7ca9-277">De meeste van belangrijke informatie over de stack al wordt geëxtraheerd in verschillende variabelen, maar u kunt pull-elkaar Hallo Hallo `details` structuur tooget meer.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="c7ca9-278">Aangezien deze structuur dynamisch is, moet u uitbrengt Hallo toohello resultaattype die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="c7ca9-279">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="c7ca9-280">tooassociate uitzonderingen met hun verwante aanvragen, gebruikt u een join:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="c7ca9-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="c7ca9-281">TrackTrace</span></span>
<span data-ttu-id="c7ca9-282">Gebruik TrackTrace toohelp analyseren van problemen door een 'breadcrumb audittrail' tooApplication Insights verzenden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="c7ca9-283">U kunt segmenten van diagnostische gegevens verzenden en controleren ze op in [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="c7ca9-284">[Meld u adapters](app-insights-asp-net-trace-logs.md) deze API toosend van derden logboeken toohello portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="c7ca9-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="c7ca9-286">U kunt zoeken op de inhoud van het bericht, maar (in tegenstelling tot eigenschapswaarden) u kunt niet filteren op het.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="c7ca9-287">de maximumgrootte Hallo op `message` veel hoger is dan de limiet Hallo op Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="c7ca9-288">U kunt relatief lange gegevens plaatsen in het Hallo-bericht heeft als voordeel van TrackTrace.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="c7ca9-289">U kunt bijvoorbeeld er postgegevens coderen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="c7ca9-290">Bovendien kunt u een bericht van ernst niveau tooyour toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="c7ca9-291">En net als andere telemetrie u eigenschap waarden toohelp die u filteren of zoeken naar verschillende sets van traceringen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="c7ca9-292">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="c7ca9-293">In [Search](app-insights-diagnostic-search.md), u kunt eenvoudig filteren vervolgens alle Hallo-berichten van een bepaalde ernstniveau worden weergegeven die betrekking tooa bepaalde database hebben.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="c7ca9-294">Traceringen in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-294">Traces in Analytics</span></span>

<span data-ttu-id="c7ca9-295">In [Application Insights Analytics](app-insights-analytics.md), belt tooTrackTrace weergeven in Hallo `traces` tabel.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="c7ca9-296">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="c7ca9-297">Voor een voorbeeld itemCount == 10 betekent dat van 10 te aanroepen`trackTrace()`, Hallo steekproeven proces verzonden slechts één van beide.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="c7ca9-298">het juiste aantal traceringsaanroepen tooget, moet u daarom code zoals `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="c7ca9-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="c7ca9-299">TrackDependency</span></span>
<span data-ttu-id="c7ca9-300">Gebruik Hallo TrackDependency aanroepen tootrack Hallo responstijden en het succespercentage van aanroepen tooan externe stuk code.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="c7ca9-301">Hallo-resultaten verschijnen in de afhankelijkheidsgrafiek Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-301">hello results appear in hello dependency charts in hello portal.</span></span>

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

<span data-ttu-id="c7ca9-302">Houd er rekening mee dat Hallo server SDK's bevatten een [afhankelijkheid module](app-insights-asp-net-dependencies.md) die worden gedetecteerd en bepaalde afhankelijkheidsaanroepen automatisch--bijgehouden bijvoorbeeld toodatabases en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="c7ca9-303">U hebt tooinstall een agent op uw server toomake Hallo module werken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="c7ca9-304">U kunt deze aanroep gebruiken als u wilt dat tootrack aanroepen die geautomatiseerde bijhouden Hallo niet catch- of als u niet wilt tooinstall Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="c7ca9-305">tooturn uitschakelen Hallo standaard afhankelijkheid bijhouden module bewerken [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) en Hallo verwijzing te verwijderen`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="c7ca9-306">Afhankelijkheden in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-306">Dependencies in Analytics</span></span>

<span data-ttu-id="c7ca9-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency aanroepen weergegeven in Hallo `dependencies` tabel.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="c7ca9-308">Als [steekproeven](app-insights-sampling.md) is uitgevoerd, Hallo itemCount-eigenschap geeft een waarde groter dan 1.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="c7ca9-309">Voor een voorbeeld itemCount == 10 betekent dat van 10 aanroepen tootrackDependency(), Hallo steekproeven proces alleen één van beide verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="c7ca9-310">tooget het juiste aantal afhankelijkheden gesegmenteerd op target-component, zoals code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="c7ca9-311">tooassociate afhankelijkheden met hun verwante aanvragen, gebruikt u een join:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="c7ca9-312">Gegevens leegmaken</span><span class="sxs-lookup"><span data-stu-id="c7ca9-312">Flushing data</span></span>
<span data-ttu-id="c7ca9-313">Normaal gesproken verzendt Hallo SDK op tijdstippen toominimize Hallo impact op Hallo gebruiker gekozen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="c7ca9-314">In sommige gevallen wilt u echter mogelijk tooflush Hallo buffer--bijvoorbeeld, als u gebruikmaakt van Hallo SDK in een toepassing die wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="c7ca9-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="c7ca9-316">Houd er rekening mee dat Hallo functie asynchrone voor Hallo [telemetrie-serverkanaal](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="c7ca9-317">Geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="c7ca9-317">Authenticated users</span></span>
<span data-ttu-id="c7ca9-318">In een web-app, worden gebruikers (standaard) geïdentificeerd door cookies.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="c7ca9-319">Een gebruiker mogelijk meer dan één keer worden geteld als ze toegang krijgen tot uw app uit een andere computer of de browser, of als het verwijderen van cookies.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="c7ca9-320">Als gebruikers zich tooyour app, kunt u een meer nauwkeurige telling krijgen Hallo geverifieerde gebruikers-ID door in te stellen Hallo browser code:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="c7ca9-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="c7ca9-322">In een ASP.NET-webtoepassing MVC-toepassing, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="c7ca9-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="c7ca9-324">Het is niet nodig toouse Hallo werkelijke aanmelden gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="c7ca9-325">Alleen heeft toobe een ID die unieke toothat gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="c7ca9-326">Mag geen spaties of Hallo tekens bevatten `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="c7ca9-327">Hallo gebruikers-ID is ook in een sessiecookie ingesteld en toohello server verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="c7ca9-328">Als Hallo server SDK is geïnstalleerd, geverifieerd Hallo gebruiker-ID wordt verzonden als onderdeel van Hallo contexteigenschappen van zowel client als server telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="c7ca9-329">Vervolgens kunt u filteren en zoekt u erop.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-329">You can then filter and search on it.</span></span>

<span data-ttu-id="c7ca9-330">Als uw app gebruikers naar accounts groepen, kunt u ook een id voor Hallo account doorgeven (Hello teken dezelfde beperkingen).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="c7ca9-331">In [Metrics Explorer](app-insights-metrics-explorer.md), kunt u een diagram waarin telt **geverifieerde gebruikers,**, en **gebruikersaccounts**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="c7ca9-332">U kunt ook [search](app-insights-diagnostic-search.md) voor client gegevenspunten met specifieke gebruikersnamen en accounts.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="c7ca9-333"><a name="properties"></a>Filteren, zoeken en segmenteren van uw gegevens met behulp van eigenschappen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="c7ca9-334">U kunt de eigenschappen en metingen tooyour gebeurtenissen (en ook toometrics, paginaweergaven, uitzonderingen en andere telemetriegegevens) koppelen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="c7ca9-335">*Eigenschappen* waarmee u toofilter uw telemetrie in gebruiksrapporten Hallo kunt tekenreekswaarden zijn.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="c7ca9-336">Bijvoorbeeld, als uw app verschillende games biedt, kunt u koppelen Hallo-naam van Hallo game tooeach gebeurtenis zodat u kunt zien welke games populairder zijn.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="c7ca9-337">Er is een limiet van 8192 op Hallo string-lengte.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="c7ca9-338">(Als u toosend grote reeksen gegevens wilt, gebruikt u Hallo-bericht parameter van [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="c7ca9-339">*Metrische gegevens* zijn numerieke waarden die kunnen worden weergegeven als geïllustreerd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="c7ca9-340">Bijvoorbeeld, kunt u toosee als er een geleidelijke toename van Hallo scores die uw gamers bereiken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="c7ca9-341">Hallo grafieken kunnen worden gesegmenteerd op Hallo scheiden van de eigenschappen die worden verzonden met Hallo gebeurtenis, zodat u kunt ophalen of gestapelde grafieken voor verschillende games.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="c7ca9-342">Voor metrische waarden toobe juist weergegeven, moeten ze too0 groter dan of gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="c7ca9-343">Er zijn een aantal [limieten op Hallo aantal eigenschappen en eigenschapswaarden metrische gegevens](#limits) die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="c7ca9-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-344">*JavaScript*</span></span>

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


<span data-ttu-id="c7ca9-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="c7ca9-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="c7ca9-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="c7ca9-348">Wees voorzichtig niet toolog persoonlijk herleidbare informatie in de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="c7ca9-349">*Als u metrische gegevens gebruikt*, opent u Metrics Explorer en selecteer Hallo metric in Hallo **aangepaste** groep:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Open van Metrics Explorer, selecteer Hallo grafiek, en selecteer Hallo metrische gegevens](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="c7ca9-351">Als uw metriek niet wordt weergegeven, of als hello **aangepaste** kop niet het geval is, sluit Hallo selectie blade en probeer het later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="c7ca9-352">Metrische gegevens kan soms een uur duren toobe via Hallo pipeline geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="c7ca9-353">*Als u de eigenschappen en metrische gegevens gebruikt*, Hallo metriek segmenteren door Hallo-eigenschap:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Ingesteld groeperen en selecteer vervolgens de eigenschap Hallo onder groeperen op](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="c7ca9-355">*In Diagnostic Search*, kunt u Hallo eigenschappen en metrische gegevens van afzonderlijke instanties van een gebeurtenis bekijken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Selecteer een exemplaar en selecteer vervolgens '...'](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="c7ca9-357">Gebruik Hallo **Search** veld toosee gebeurtenis instanties die een bepaalde eigenschappenwaarde hebben.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Typ een term in zoeken](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="c7ca9-359">[Meer informatie over zoekopdracht expressies](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="c7ca9-360">Andere manier tooset eigenschappen en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c7ca9-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="c7ca9-361">Als het is eenvoudiger, kunt u Hallo parameters van een gebeurtenis in een afzonderlijk object verzamelen:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="c7ca9-362">Hallo niet gebruiken hetzelfde exemplaar van de telemetrie-item (`event` in dit voorbeeld) toocall Track*() meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="c7ca9-363">Dit kan leiden tot telemetrie toobe verzonden met een onjuiste configuratie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="c7ca9-364">Aangepaste metingen en eigenschappen in Analytics</span><span class="sxs-lookup"><span data-stu-id="c7ca9-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="c7ca9-365">In [Analytics](app-insights-analytics.md), eigenschappen en aangepaste metrische gegevens weergeven in Hallo `customMeasurements` en `customDimensions` kenmerken van elke record telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="c7ca9-366">Bijvoorbeeld, als u een eigenschap genaamd 'spel' tooyour aanvraagtelemetrie hebt toegevoegd, deze query telt Hallo instanties van verschillende waarden van 'spel' en gemiddelde Hallo Hallo aangepaste metrische 'score' weergeven:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="c7ca9-367">U ziet dat:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-367">Notice that:</span></span>

* <span data-ttu-id="c7ca9-368">Wanneer u een waarde van Hallo customDimensions of customMeasurements JSON uitpakt, hieraan dynamische type, en zodat u dit casten `tostring` of `todouble`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="c7ca9-369">account van de mogelijkheid Hallo van tootake [steekproeven](app-insights-sampling.md), moet u `sum(itemCount)`, niet `count()`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="c7ca9-370"><a name="timed"></a>Timing van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="c7ca9-371">Soms wilt u toochart hoe lang het duurt tooperform een actie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="c7ca9-372">U kunt bijvoorbeeld tooknow hoe lang gebruikers tooconsider opties worden in een spel.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="c7ca9-373">Hiervoor kunt u Hallo meting parameter.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="c7ca9-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="c7ca9-375"><a name="defaults"></a>Standaard-eigenschappen voor aangepaste telemetrie</span><span class="sxs-lookup"><span data-stu-id="c7ca9-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="c7ca9-376">Als u tooset eigenschap standaardwaarden voor een aantal aangepaste gebeurtenissen Hallo die u schrijft wilt, kunt u ze in een exemplaar van TelemetryClient instellen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="c7ca9-377">Ze zijn aangesloten tooevery telemetrie-item dat wordt verzonden door de client.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="c7ca9-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="c7ca9-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="c7ca9-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="c7ca9-381">Afzonderlijke telemetrie aanroepen kunnen Hallo standaardwaarden in hun woordenlijsten eigenschap te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="c7ca9-382">*Web voor JavaScript-clients*, [gebruik van JavaScript telemetrie initalisatiefuncties](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="c7ca9-383">*tooadd eigenschappen tooall telemetrie*, met inbegrip van gegevens van de standaardregel voor verzameling modules, Hallo [implementeren `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="c7ca9-384">Steekproef nemen en verwerken van telemetrie filteren</span><span class="sxs-lookup"><span data-stu-id="c7ca9-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="c7ca9-385">U kunt code tooprocess uw telemetrie schrijven voordat deze wordt verzonden van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="c7ca9-386">Hallo verwerking omvat gegevens dat wordt verzonden door Hallo standaard telemetrie modules, zoals de verzameling van de HTTP-aanvragen en afhankelijkheid verzameling.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="c7ca9-387">[Eigenschappen toevoegen](app-insights-api-filtering-sampling.md#add-properties) tootelemetry door het implementeren van `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="c7ca9-388">U kunt bijvoorbeeld versienummers of berekende waarden toevoegen van andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="c7ca9-389">[Filteren](app-insights-api-filtering-sampling.md#filtering) kunt wijzigen of verwijderen van telemetrie voordat het wordt verzonden door Hallo SDK door het implementeren van `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="c7ca9-390">U bepaalt wat wordt verzonden naar of verwijderd, maar u tooaccount voor Hallo effect op uw metrische gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="c7ca9-391">Afhankelijk van hoe u items negeren, kunt u Hallo mogelijkheid toonavigate tussen verwante items verliezen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="c7ca9-392">[Steekproef nemen](app-insights-api-filtering-sampling.md) is een volume verpakte oplossing tooreduce Hallo van gegevens die worden verzonden vanuit uw app toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="c7ca9-393">Dit gebeurt zonder Hallo weergegeven metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="c7ca9-394">En zonder die betrekking hebben op uw mogelijkheid toodiagnose problemen door te navigeren tussen verwante items zoals uitzonderingen, aanvragen en paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="c7ca9-395">[Meer informatie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="c7ca9-396">Telemetrie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-396">Disabling telemetry</span></span>
<span data-ttu-id="c7ca9-397">te*dynamisch stoppen en starten* Hallo verzamelen en verzenden van telemetrie:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="c7ca9-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="c7ca9-399">te*uitschakelen geselecteerde standaard collectors*--bijvoorbeeld, prestatiemeteritems, HTTP-aanvragen of afhankelijkheden--verwijderen of Hallo relevante regels in uitcommentariëren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). U kunt dit bijvoorbeeld doen als u uw eigen gegevens TrackRequest toosend wilt.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="c7ca9-400"><a name="debug"></a>Modus voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c7ca9-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="c7ca9-401">Tijdens de foutopsporing, is het nuttig toohave uw telemetrie doorgegeven Hallo pipeline, direct zodat u resultaten onmiddellijk kunt zien.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="c7ca9-402">U ook get extra berichten sturen die u helpen traceren problemen met Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="c7ca9-403">Schakel deze uit in productie, omdat dit kan uw app vertragen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="c7ca9-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="c7ca9-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="c7ca9-406"><a name="ikey"></a>De instrumentatiesleutel Hallo voor de geselecteerde aangepaste telemetrie instellen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="c7ca9-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="c7ca9-408"><a name="dynamic-ikey"></a>Dynamische instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="c7ca9-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="c7ca9-409">tooavoid combinatie van telemetrie van ontwikkeling, testen en productieomgevingen, kunt u [afzonderlijke Application Insights-resources maken](app-insights-create-new-resource.md) en wijzigt u de sleutels, afhankelijk van het Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="c7ca9-410">In plaats van het Hallo-instrumentatiesleutel ophalen uit het Hallo-configuratiebestand en kunt u dit instellen in uw code.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="c7ca9-411">Hallo-sleutel in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice ingesteld:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="c7ca9-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="c7ca9-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="c7ca9-414">In webpagina's, kunt u tooset op Hallo van de webserver status, in plaats van letterlijk coderen in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="c7ca9-415">Bijvoorbeeld in een webpagina in een ASP.NET-app gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="c7ca9-416">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="c7ca9-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="c7ca9-417">TelemetryContext</span></span>
<span data-ttu-id="c7ca9-418">TelemetryClient heeft een contexteigenschap die waarden bevat die samen met alle telemetriegegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="c7ca9-419">Normaal gesproken zijn ingesteld door Hallo standaard telemetrie modules, maar u kunt ook instellen ze zelf.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="c7ca9-420">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="c7ca9-421">Als u een van deze waarden zelf, overweeg te verwijderen van de betreffende regel Hallo van [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), zodat uw en Hallo standaard waarden niet veranderen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="c7ca9-422">**Onderdeel**: Hallo-app en de versie ervan.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="c7ca9-423">**Apparaat**: gegevens over het Hallo-apparaat waarop Hallo-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="c7ca9-424">(In web-apps is dit Hallo-server of client-apparaat dat Hallo telemetrie is verzonden vanaf.)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="c7ca9-425">**InstrumentationKey**: Hallo Application Insights-resource in Azure waar Hallo telemetrie worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="c7ca9-426">Dit wordt gewoonlijk opgenomen in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="c7ca9-427">**Locatie**: Hallo geografische locatie van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="c7ca9-428">**Bewerking**: Hallo In web-apps, huidige HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="c7ca9-429">In andere typen Apps kunt u deze gebeurtenissen toogroup samen instellen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="c7ca9-430">**Id**: een gegenereerde waarde die verschillende gebeurtenissen, zodat wanneer u een gebeurtenis in Diagnostic Search inspecteert, u vindt verwante objecten.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="c7ca9-431">**Naam**: een meestal Hallo URL van Hallo HTTP-aanvraag-id.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="c7ca9-432">**SyntheticSource**: als niet null of leeg is, een tekenreeks die of Hallo het bronbestand van Hallo-aanvraag aangeeft is geïdentificeerd als een robot of web-test.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="c7ca9-433">Standaard wordt het uitgesloten van berekeningen in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="c7ca9-434">**Eigenschappen**: eigenschappen die worden verzonden met alle telemetriegegevens.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="c7ca9-435">Deze kan worden genegeerd in afzonderlijke bijhouden * aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="c7ca9-436">**Sessie**: Hallo gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-436">**Session**: hello user's session.</span></span> <span data-ttu-id="c7ca9-437">Hallo-ID is gegenereerd tooa waarde, die wordt gewijzigd wanneer het Hallo-gebruiker niet actief is geweest even ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="c7ca9-438">**Gebruiker**: gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="c7ca9-439">Limieten</span><span class="sxs-lookup"><span data-stu-id="c7ca9-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="c7ca9-440">Hallo limiet, gebruik roept tooavoid [steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="c7ca9-441">toodetermine hoe lang gegevens worden bewaard raadpleegt [bewaren van gegevens en privacy](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="c7ca9-442">Referentiedocumenten</span><span class="sxs-lookup"><span data-stu-id="c7ca9-442">Reference docs</span></span>
* [<span data-ttu-id="c7ca9-443">ASP.NET-verwijzing</span><span class="sxs-lookup"><span data-stu-id="c7ca9-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="c7ca9-444">Naslaginformatie over Java</span><span class="sxs-lookup"><span data-stu-id="c7ca9-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="c7ca9-445">Verwijzing in JavaScript</span><span class="sxs-lookup"><span data-stu-id="c7ca9-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="c7ca9-446">Android-SDK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="c7ca9-447">iOS-SDK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="c7ca9-448">SDK-code</span><span class="sxs-lookup"><span data-stu-id="c7ca9-448">SDK code</span></span>
* [<span data-ttu-id="c7ca9-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="c7ca9-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="c7ca9-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="c7ca9-451">Windows Server-pakketten</span><span class="sxs-lookup"><span data-stu-id="c7ca9-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="c7ca9-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="c7ca9-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="c7ca9-454">Alle platforms</span><span class="sxs-lookup"><span data-stu-id="c7ca9-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="c7ca9-455">Vragen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-455">Questions</span></span>
* <span data-ttu-id="c7ca9-456">*Welke uitzonderingen's Track_() aanroepen weggooien*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="c7ca9-457">Geen.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-457">None.</span></span> <span data-ttu-id="c7ca9-458">U hoeft niet toowrap ze in trycatch-componenten.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="c7ca9-459">Als er problemen Hallo SDK, wordt deze berichten aanmelden Hallo foutopsporing console-uitvoer en--als hello berichten ophalen via--in diagnostische gegevens doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="c7ca9-460">*Is er een REST-API tooget gegevens vanuit de portal Hallo?*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="c7ca9-461">Ja, Hallo [data access-API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="c7ca9-462">Andere manieren tooextract gegevens omvatten [exporteren vanuit Analytics tooPower BI](app-insights-export-power-bi.md) en [continue export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="c7ca9-463"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="c7ca9-464">Zoekopdracht gebeurtenissen en Logboeken</span><span class="sxs-lookup"><span data-stu-id="c7ca9-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="c7ca9-465">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="c7ca9-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


