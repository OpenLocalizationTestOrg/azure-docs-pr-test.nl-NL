---
title: aaaLive metrische gegevensstroom met aangepaste metrische gegevens en diagnostische gegevens in Azure Application Insights | Microsoft Docs
description: Bewaken van uw web-app in realtime met aangepaste metrische gegevens en onderzoeken van problemen met een live feed fouten, traceringen en gebeurtenissen.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="44d3c-103">Livestream metrische gegevens: De Monitor & spoor met een latentie van 1 seconde</span><span class="sxs-lookup"><span data-stu-id="44d3c-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="44d3c-104">Hallo kloppen in de race hart van uw webtoepassing live, in productie-test met behulp van livestream metrische gegevens van [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44d3c-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="44d3c-105">Selecteer en metrische gegevens en prestaties tellers toowatch in real-time, zonder eventuele verstoringen tooyour service filteren.</span><span class="sxs-lookup"><span data-stu-id="44d3c-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="44d3c-106">Inspecteer de stack-traces van voorbeeld kan aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="44d3c-107">Samen met [Profiler](app-insights-profiler.md), [momentopname foutopsporingsprogramma](app-insights-snapshot-debugger.md), en [prestatietests](app-insights-monitor-web-app-availability.md#performance-tests), metrische gegevens livestream biedt een krachtige en niet-Invasief diagnostisch hulpprogramma van uw live web site.</span><span class="sxs-lookup"><span data-stu-id="44d3c-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="44d3c-108">U kunt met livestream metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="44d3c-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="44d3c-109">Valideren van een oplossing, terwijl deze wordt uitgebracht, prestaties en mislukte aantallen volgen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="44d3c-110">Bekijkt hello effect van belasting te testen en problemen diagnosticeren live.</span><span class="sxs-lookup"><span data-stu-id="44d3c-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="44d3c-111">Zich richten op bepaalde test sessies of bekende problemen door te selecteren en filteren Hallo metrische gegevens die u wilt dat toowatch filteren.</span><span class="sxs-lookup"><span data-stu-id="44d3c-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="44d3c-112">Uitzondering traceringen meteen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="44d3c-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="44d3c-113">Experiment met filters toofind Hallo meest relevante KPI's.</span><span class="sxs-lookup"><span data-stu-id="44d3c-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="44d3c-114">Alle vensters prestaties meteritem live bewaken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="44d3c-115">Zoek een server die problemen ondervindt, en eenvoudig alle Hallo KPI/live feed toojust filteren die server.</span><span class="sxs-lookup"><span data-stu-id="44d3c-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="44d3c-116">[![Live video van de gegevensstroom van de metrische](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="44d3c-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="44d3c-117">Metrische gegevens livestream is momenteel beschikbaar op lokale met ASP.NET-apps of in Hallo Cloud.</span><span class="sxs-lookup"><span data-stu-id="44d3c-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="44d3c-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="44d3c-118">Get started</span></span>

1. <span data-ttu-id="44d3c-119">Als u nog niet hebt [Application Insights geïnstalleerd](app-insights-asp-net.md) in uw ASP.NET-web-app of [app voor Windows server](app-insights-windows-services.md), doet u dat nu.</span><span class="sxs-lookup"><span data-stu-id="44d3c-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="44d3c-120">**Meest recente versie van de update toohello** van Hallo Application Insights-pakket.</span><span class="sxs-lookup"><span data-stu-id="44d3c-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="44d3c-121">In Visual Studio met de rechtermuisknop op uw project en kies **beheren Nuget-pakketten**.</span><span class="sxs-lookup"><span data-stu-id="44d3c-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="44d3c-122">Open Hallo **Updates** tabblad selectievakje **Include prerelease**, en selecteer alle Hallo Microsoft.ApplicationInsights.* pakketten.</span><span class="sxs-lookup"><span data-stu-id="44d3c-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="44d3c-123">Implementeer uw app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="44d3c-123">Redeploy your app.</span></span>

3. <span data-ttu-id="44d3c-124">In Hallo [Azure-portal](https://portal.azure.com)Hallo Application Insights-resource voor uw app openen en open vervolgens Live Stream.</span><span class="sxs-lookup"><span data-stu-id="44d3c-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="44d3c-125">[Beveiligde Hallo besturingskanaal](#secure-the-control-channel) als u mogelijk gevoelige gegevens zoals klantnamen in filters.</span><span class="sxs-lookup"><span data-stu-id="44d3c-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Klik op Hallo overzichtsblade Live Stream](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="44d3c-127">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="44d3c-127">No data?</span></span> <span data-ttu-id="44d3c-128">Controleer de firewall van uw server</span><span class="sxs-lookup"><span data-stu-id="44d3c-128">Check your server firewall</span></span>

<span data-ttu-id="44d3c-129">Controleer Hallo [uitgaande poorten voor de metrische gegevens livestream](app-insights-ip-addresses.md#outgoing-ports) zijn geopend in de firewall van uw servers Hallo.</span><span class="sxs-lookup"><span data-stu-id="44d3c-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="44d3c-130">Hoe verschilt livestream metrische gegevens van Metrics Explorer en Analytics?</span><span class="sxs-lookup"><span data-stu-id="44d3c-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="44d3c-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="44d3c-131">Live Stream</span></span> | <span data-ttu-id="44d3c-132">Metrics Explorer en analyses</span><span class="sxs-lookup"><span data-stu-id="44d3c-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="44d3c-133">Latentie</span><span class="sxs-lookup"><span data-stu-id="44d3c-133">Latency</span></span>|<span data-ttu-id="44d3c-134">Gegevens die worden weergegeven binnen één seconde</span><span class="sxs-lookup"><span data-stu-id="44d3c-134">Data displayed within one second</span></span>|<span data-ttu-id="44d3c-135">Geaggregeerd in minuten</span><span class="sxs-lookup"><span data-stu-id="44d3c-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="44d3c-136">Er geen bewaarperiode</span><span class="sxs-lookup"><span data-stu-id="44d3c-136">No retention</span></span>|<span data-ttu-id="44d3c-137">Gegevens zich blijft voordoen terwijl deze op Hallo grafiek en vervolgens wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="44d3c-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="44d3c-138">Gegevens bewaard gedurende 90 dagen</span><span class="sxs-lookup"><span data-stu-id="44d3c-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="44d3c-139">Op aanvraag</span><span class="sxs-lookup"><span data-stu-id="44d3c-139">On demand</span></span>|<span data-ttu-id="44d3c-140">Gegevens gestreamd tijdens het openen van Live metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="44d3c-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="44d3c-141">Gegevens worden verzonden wanneer Hallo SDK is geïnstalleerd en ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="44d3c-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="44d3c-142">Gratis</span><span class="sxs-lookup"><span data-stu-id="44d3c-142">Free</span></span>|<span data-ttu-id="44d3c-143">Er zijn geen kosten voor Live Stream gegevens</span><span class="sxs-lookup"><span data-stu-id="44d3c-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="44d3c-144">Onderwerpnaam te[prijzen](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="44d3c-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="44d3c-145">Steekproeven</span><span class="sxs-lookup"><span data-stu-id="44d3c-145">Sampling</span></span>|<span data-ttu-id="44d3c-146">Alle geselecteerde metrische gegevens en prestatiemeteritems worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="44d3c-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="44d3c-147">Fouten en stack-traces steekproeven worden genomen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="44d3c-148">TelemetryProcessors worden niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="44d3c-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="44d3c-149">Mogelijk zijn gebeurtenissen [door actieve](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="44d3c-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="44d3c-150">Besturingskanaal</span><span class="sxs-lookup"><span data-stu-id="44d3c-150">Control channel</span></span>|<span data-ttu-id="44d3c-151">Filter besturingselement signalen verzonden toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="44d3c-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="44d3c-152">We raden u [secure dit kanaal](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="44d3c-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="44d3c-153">Communicatie kan niet worden teruggedraaid, toohello portal</span><span class="sxs-lookup"><span data-stu-id="44d3c-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="44d3c-154">Selecteer en metrische gegevens over uw filteren</span><span class="sxs-lookup"><span data-stu-id="44d3c-154">Select and filter your metrics</span></span>

<span data-ttu-id="44d3c-155">(Beschikbaar op klassieke ASP.NET-apps met Hallo nieuwste SDK.)</span><span class="sxs-lookup"><span data-stu-id="44d3c-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="44d3c-156">U kunt aangepaste KPI live bewaken door willekeurige filters zijn toegepast op alle telemetrie voor Application Insights van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="44d3c-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="44d3c-157">Klik op Hallo filterbesturingselement waarin wordt weergegeven wanneer u muis van Hallo grafieken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="44d3c-158">Hallo volgende grafiek met het uitzetten van een aangepaste aanvraag aantal KPI met filters op de URL en de duur van de kenmerken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="44d3c-159">Filters Hello stroom Preview sectie ziet u een live feed telemetrie die overeenkomt met de Hallo criteria die u hebt opgegeven op elk punt in tijd valideren.</span><span class="sxs-lookup"><span data-stu-id="44d3c-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![Aangepaste aanvraag KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="44d3c-161">U kunt een andere waarde dan het aantal bewaken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="44d3c-162">Hallo-opties, is afhankelijk van Hallo type stream, wat erop kan telemetrie voor Application Insights: aanvragen, afhankelijkheden, uitzonderingen, traceringen, gebeurtenissen of metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="44d3c-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="44d3c-163">Het kan ook uw eigen [aangepaste meting](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="44d3c-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opties voor](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="44d3c-165">Bovendien tooApplication Insights telemetry, u kunt ook bewaken Windows-prestatiemeteritem door selecteren die uit Hallo stroom opties, en het Hallo-naam van het prestatiemeteritem Hallo leveren.</span><span class="sxs-lookup"><span data-stu-id="44d3c-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="44d3c-166">Live metrische gegevens worden samengevoegd op twee punten: lokaal op elke server en klik vervolgens op alle servers.</span><span class="sxs-lookup"><span data-stu-id="44d3c-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="44d3c-167">U kunt Hallo standaard op door een andere opties selecteren in Hallo respectieve vervolgkeuzelijsten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="44d3c-168">Voorbeeld telemetrie: Aangepaste Live diagnostische gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="44d3c-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="44d3c-169">Standaard ziet live feed Hallo van gebeurtenissen u voorbeelden van mislukte aanvragen en afhankelijkheidsaanroepen, uitzonderingen, gebeurtenissen en traceringen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="44d3c-170">Klik op Hallo pictogram toosee Hallo toegepast filtercriteria op elk gewenst moment in de tijd.</span><span class="sxs-lookup"><span data-stu-id="44d3c-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Standaard live feed](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="44d3c-172">Als met metrische gegevens, kunt u elke willekeurige criteria tooany Hallo Application Insights telemetrie typen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="44d3c-173">In dit voorbeeld selecteren we, traceringen en gebeurtenissen voor mislukte aanvragen voor specifieke.</span><span class="sxs-lookup"><span data-stu-id="44d3c-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="44d3c-174">Er worden ook alle uitzonderingen en fouten van afhankelijkheid selecteren.</span><span class="sxs-lookup"><span data-stu-id="44d3c-174">We are also selecting all exceptions and dependency failures.</span></span>

![Aangepaste live feed](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="44d3c-176">Opmerking: Op dit moment voor de criteria voor op basis van een bericht van uitzondering gebruiken buitenste uitzondering het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="44d3c-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="44d3c-177">In het voorgaande voorbeeld Hallo toofilter uit Hallo onschadelijk uitzondering met het InnerException-bericht (volgt hello "<--' scheidingsteken)"Hallo-client is verbroken."</span><span class="sxs-lookup"><span data-stu-id="44d3c-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="44d3c-178">Gebruik een bericht bevat niet-'Fout bij het lezen van de aanvraaginhoud' criteria.</span><span class="sxs-lookup"><span data-stu-id="44d3c-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="44d3c-179">Zie de details van de Hallo van een item in Hallo feed live door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="44d3c-180">U kunt onderbreken Hallo feed door te klikken op **onderbreken** gewoon omlaag schuiven, of op een item te klikken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="44d3c-181">Live feed wordt hervat nadat u schuift in back toohello top of door te klikken op Hallo teller van items die zijn verzameld tijdens het programma is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="44d3c-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Steekproef live fouten](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="44d3c-183">Filteren op server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="44d3c-183">Filter by server instance</span></span>

<span data-ttu-id="44d3c-184">Als u een bepaalde server rolinstantie toomonitor wilt, kunt u filteren op de server.</span><span class="sxs-lookup"><span data-stu-id="44d3c-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Steekproef live fouten](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="44d3c-186">SDK-vereisten</span><span class="sxs-lookup"><span data-stu-id="44d3c-186">SDK Requirements</span></span>
<span data-ttu-id="44d3c-187">Aangepaste metrische gegevens livestream is beschikbaar met versie 2.4.0-beta2 of nieuwere van [Application Insights-SDK voor web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="44d3c-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="44d3c-188">Houd er rekening mee tooselect 'Prerelease opnemen' optie uit de NuGet-Pakketbeheer.</span><span class="sxs-lookup"><span data-stu-id="44d3c-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="44d3c-189">Hallo-besturingskanaal beveiligen</span><span class="sxs-lookup"><span data-stu-id="44d3c-189">Secure hello control channel</span></span>
<span data-ttu-id="44d3c-190">Hallo aangepaste filters criteria die u opgeeft worden verzonden back toohello Live metrische gegevens onderdeel Hallo Application Insights-SDK.</span><span class="sxs-lookup"><span data-stu-id="44d3c-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="44d3c-191">Hallo filters kunnen mogelijk vertrouwelijke gegevens zoals customerIDs bevatten.</span><span class="sxs-lookup"><span data-stu-id="44d3c-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="44d3c-192">U kunt beveiligen met een geheime sleutel van de API bovendien toohello instrumentatiesleutel Hallo-kanaal.</span><span class="sxs-lookup"><span data-stu-id="44d3c-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="44d3c-193">Maak een API-sleutel</span><span class="sxs-lookup"><span data-stu-id="44d3c-193">Create an API Key</span></span>

![Api-sleutel maken](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="44d3c-195">API-sleutel tooConfiguration toevoegen</span><span class="sxs-lookup"><span data-stu-id="44d3c-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="44d3c-196">Voeg Hallo AuthenticationApiKey toohello QuickPulseTelemetryModule in Hallo applicationinsights.config-bestand:</span><span class="sxs-lookup"><span data-stu-id="44d3c-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="44d3c-197">Of in code wordt ingesteld op Hallo QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="44d3c-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="44d3c-198">Als u kent en vertrouwt dat alle gekoppelde servers hello, kunt u aangepaste filters Hallo zonder Hallo geverifieerde kanaal proberen.</span><span class="sxs-lookup"><span data-stu-id="44d3c-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="44d3c-199">Deze optie is beschikbaar voor zes maanden.</span><span class="sxs-lookup"><span data-stu-id="44d3c-199">This option is available for six months.</span></span> <span data-ttu-id="44d3c-200">Met deze overschrijving is vereist eenmaal elke nieuwe sessie of als een nieuwe server online is.</span><span class="sxs-lookup"><span data-stu-id="44d3c-200">This override is required once every new session, or when a new server comes online.</span></span>

![Live metrische gegevens Auth-opties](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="44d3c-202">Het is raadzaam dat u Hallo geverifieerde kanaal instellen voordat u een potentieel gevoelige informatie, zoals CustomerID in Hallo filtercriteria invoert.</span><span class="sxs-lookup"><span data-stu-id="44d3c-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="44d3c-203">Een test prestatiebelasting genereren</span><span class="sxs-lookup"><span data-stu-id="44d3c-203">Generating a performance test load</span></span>

<span data-ttu-id="44d3c-204">Als u wilt dat toowatch Hallo effect van een werklast verhogen, gebruik Hallo prestatietest blade.</span><span class="sxs-lookup"><span data-stu-id="44d3c-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="44d3c-205">Het simuleert aanvragen van een aantal gelijktijdige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="44d3c-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="44d3c-206">Beide 'handmatig 'tests uit te voeren (ping-tests) van één URL of uit te voeren een [WebTest met meerdere stappen prestatietest](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (in hello dezelfde manier als voor een beschikbaarheid testen) te uploaden.</span><span class="sxs-lookup"><span data-stu-id="44d3c-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="44d3c-207">Nadat u de prestatietest Hallo hebt gemaakt, opent u Hallo test en Hallo Live Stream blade in afzonderlijke vensters.</span><span class="sxs-lookup"><span data-stu-id="44d3c-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="44d3c-208">U kunt zien wanneer Hallo in de wachtrij prestaties test start en Bekijk live stream op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="44d3c-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="44d3c-209">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="44d3c-209">Troubleshooting</span></span>

<span data-ttu-id="44d3c-210">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="44d3c-210">No data?</span></span> <span data-ttu-id="44d3c-211">Als uw toepassing bevindt zich in een beveiligd netwerk: metrische gegevens Stream Live maakt gebruik van een ander IP-adressen dan andere telemetrie voor Application Insights.</span><span class="sxs-lookup"><span data-stu-id="44d3c-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="44d3c-212">Zorg ervoor dat [die IP-adressen](app-insights-ip-addresses.md) zijn geopend in uw firewall.</span><span class="sxs-lookup"><span data-stu-id="44d3c-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="44d3c-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44d3c-213">Next steps</span></span>
* [<span data-ttu-id="44d3c-214">Gebruik met Application Insights controleren</span><span class="sxs-lookup"><span data-stu-id="44d3c-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="44d3c-215">Met behulp van diagnostische gegevens doorzoeken</span><span class="sxs-lookup"><span data-stu-id="44d3c-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="44d3c-216">Profiler</span><span class="sxs-lookup"><span data-stu-id="44d3c-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="44d3c-217">Momentopname-foutopsporingsprogramma</span><span class="sxs-lookup"><span data-stu-id="44d3c-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
