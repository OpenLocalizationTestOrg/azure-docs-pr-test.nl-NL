---
title: Afhankelijkheid bijhouden in Azure Application Insights | Microsoft Docs
description: Analyseer het gebruik, de beschikbaarheid en de prestaties van uw on-premises webtoepassing of Microsoft Azure-webtoepassing met Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="91d17-103">Application Insights instellen: afhankelijkheid bijhouden</span><span class="sxs-lookup"><span data-stu-id="91d17-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="91d17-104">Een *afhankelijkheid* is een externe component die wordt aangeroepen door uw app.</span><span class="sxs-lookup"><span data-stu-id="91d17-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="91d17-105">Dit is doorgaans een service die is aangeroepen met behulp van HTTP, of een database of een bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="91d17-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="91d17-106">[Application Insights](app-insights-overview.md) maatregelen hoe lang de toepassing moet wachten voor afhankelijkheden en hoe vaak een afhankelijkheidsaanroep is mislukt.</span><span class="sxs-lookup"><span data-stu-id="91d17-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="91d17-107">U kunt specifieke aanroepen te onderzoeken en koppelen aan aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="91d17-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![voorbeeldgrafieken](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="91d17-109">De afhankelijkheidsmonitor voor out-of-the-box rapporten momenteel aanroepen naar deze typen afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="91d17-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="91d17-110">Server</span><span class="sxs-lookup"><span data-stu-id="91d17-110">Server</span></span>
  * <span data-ttu-id="91d17-111">SQL-databases</span><span class="sxs-lookup"><span data-stu-id="91d17-111">SQL databases</span></span>
  * <span data-ttu-id="91d17-112">ASP.NET-webtoepassingen en WCF-services die gebruikmaken van bindingen op basis van HTTP</span><span class="sxs-lookup"><span data-stu-id="91d17-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="91d17-113">Lokale of externe HTTP-aanroepen</span><span class="sxs-lookup"><span data-stu-id="91d17-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="91d17-114">Azure DB Cosmos, tabel, blob-opslag en wachtrij</span><span class="sxs-lookup"><span data-stu-id="91d17-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="91d17-115">Webpagina's</span><span class="sxs-lookup"><span data-stu-id="91d17-115">Web pages</span></span>
  * <span data-ttu-id="91d17-116">AJAX-aanroepen</span><span class="sxs-lookup"><span data-stu-id="91d17-116">AJAX calls</span></span>

<span data-ttu-id="91d17-117">Bewaking werkt met [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) rond geselecteerde methoden.</span><span class="sxs-lookup"><span data-stu-id="91d17-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="91d17-118">Prestatieoverhead is minimaal.</span><span class="sxs-lookup"><span data-stu-id="91d17-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="91d17-119">U kunt ook uw eigen SDK-aanroepen voor het bewaken van andere afhankelijkheden, zowel op de client en server-code schrijven met behulp van de [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="91d17-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="91d17-120">Bewaking van afhankelijkheid ingesteld</span><span class="sxs-lookup"><span data-stu-id="91d17-120">Set up dependency monitoring</span></span>
<span data-ttu-id="91d17-121">Gedeeltelijke afhankelijkheidsgegevens worden verzameld, automatisch door de [Application Insights-SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="91d17-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="91d17-122">Als u alle gegevens, installeert u de desbetreffende agent voor de hostserver.</span><span class="sxs-lookup"><span data-stu-id="91d17-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="91d17-123">Platform</span><span class="sxs-lookup"><span data-stu-id="91d17-123">Platform</span></span> | <span data-ttu-id="91d17-124">Installeren</span><span class="sxs-lookup"><span data-stu-id="91d17-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="91d17-125">IIS-Server</span><span class="sxs-lookup"><span data-stu-id="91d17-125">IIS Server</span></span> |<span data-ttu-id="91d17-126">Beide [Status Monitor installeren op uw server](app-insights-monitor-performance-live-website-now.md) of [Upgrade van uw toepassing naar .NET framework 4.6 of hoger](http://go.microsoft.com/fwlink/?LinkId=528259) en installeer de [Application Insights-SDK](app-insights-asp-net.md) in uw app.</span><span class="sxs-lookup"><span data-stu-id="91d17-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="91d17-127">Azure Web App</span><span class="sxs-lookup"><span data-stu-id="91d17-127">Azure Web App</span></span> |<span data-ttu-id="91d17-128">In het Configuratiescherm voor web-app [de Application Insights-blade geopend in het Configuratiescherm van de web-app](app-insights-azure-web-apps.md) en kies installeren als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="91d17-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="91d17-129">Azure-Cloudservice</span><span class="sxs-lookup"><span data-stu-id="91d17-129">Azure Cloud Service</span></span> |<span data-ttu-id="91d17-130">[Gebruik opstarttaak](app-insights-cloudservices.md) of [installeren .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="91d17-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="91d17-131">Waar vind ik afhankelijkheidsgegevens</span><span class="sxs-lookup"><span data-stu-id="91d17-131">Where to find dependency data</span></span>
* <span data-ttu-id="91d17-132">[De toepassingstoewijzing](#application-map) visualiseren van afhankelijkheden tussen uw app en de aangrenzende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="91d17-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="91d17-133">[Prestaties, browser en fout blades](#performance-and-blades) server afhankelijkheidsgegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="91d17-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="91d17-134">[Blade browsers](#ajax-calls) AJAX-aanroepen vanuit de browsers van uw gebruikers bevat.</span><span class="sxs-lookup"><span data-stu-id="91d17-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="91d17-135">[Klik door vanuit traag of mislukte aanvragen](#diagnose-slow-requests) aanroepen om te controleren van de afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="91d17-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="91d17-136">[Analytics](#analytics) kan worden gebruikt om gegevens van de afhankelijkheid opvragen.</span><span class="sxs-lookup"><span data-stu-id="91d17-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="91d17-137">Toepassingskaart</span><span class="sxs-lookup"><span data-stu-id="91d17-137">Application Map</span></span>
<span data-ttu-id="91d17-138">De toepassingstoewijzing fungeert als een visuele hulpmiddel voor het detecteren van afhankelijkheden tussen de onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="91d17-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="91d17-139">Deze wordt automatisch gegenereerd vanuit de telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="91d17-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="91d17-140">Dit voorbeeld toont AJAX-aanroepen vanuit de browser-scripts en het aanroepen van de REST van de server-app voor twee externe services.</span><span class="sxs-lookup"><span data-stu-id="91d17-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Toepassingskaart](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="91d17-142">**Navigeer in de vakken** relevante afhankelijkheid en andere grafieken.</span><span class="sxs-lookup"><span data-stu-id="91d17-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="91d17-143">**De kaart vastmaken** naar de [dashboard](app-insights-dashboards.md), wordt waar deze volledig functioneel.</span><span class="sxs-lookup"><span data-stu-id="91d17-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="91d17-144">[Meer informatie](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="91d17-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="91d17-145">Prestatie- en blades</span><span class="sxs-lookup"><span data-stu-id="91d17-145">Performance and failure blades</span></span>
<span data-ttu-id="91d17-146">De blade performance toont de duur van afhankelijkheidsaanroepen die door de server-app.</span><span class="sxs-lookup"><span data-stu-id="91d17-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="91d17-147">Er is een overzichtstabel en een tabel gesegmenteerd op aanroep.</span><span class="sxs-lookup"><span data-stu-id="91d17-147">There's a summary chart and a table segmented by call.</span></span>

![Afhankelijkheid van de prestatiegrafieken-blade](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="91d17-149">Klik in de samenvatting grafieken of de tabelitems om te zoeken onbewerkte instanties van deze aanroepen.</span><span class="sxs-lookup"><span data-stu-id="91d17-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Afhankelijkheid aanroep exemplaren](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="91d17-151">**Foutaantallen** worden weergegeven op de **fouten** blade.</span><span class="sxs-lookup"><span data-stu-id="91d17-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="91d17-152">Een mislukte is een retourcode die zich niet in het bereik 200-399, of een onbekend.</span><span class="sxs-lookup"><span data-stu-id="91d17-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="91d17-153">**100% fouten?**</span><span class="sxs-lookup"><span data-stu-id="91d17-153">**100% failures?**</span></span> <span data-ttu-id="91d17-154">-Dit wordt waarschijnlijk geeft aan dat u alleen afhankelijkheidsgegevens van gedeeltelijke krijgt.</span><span class="sxs-lookup"><span data-stu-id="91d17-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="91d17-155">U moet [instellen van de bewaking van afhankelijkheid geschikt is voor uw platform](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="91d17-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="91d17-156">AJAX-aanroepen</span><span class="sxs-lookup"><span data-stu-id="91d17-156">AJAX Calls</span></span>
<span data-ttu-id="91d17-157">De blade Browsers toont de duur en mislukt de frequentie van AJAX-aanroepen vanuit [JavaScript in uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="91d17-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="91d17-158">Deze worden weergegeven als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="91d17-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="91d17-159"><a name="diagnosis"></a>Diagnose van trage aanvragen</span><span class="sxs-lookup"><span data-stu-id="91d17-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="91d17-160">Elke gebeurtenis van de aanvraag is gekoppeld aan het aanroepen van afhankelijkheden, uitzonderingen en andere gebeurtenissen die worden bijgehouden, terwijl de aanvraag is verwerkt door uw app.</span><span class="sxs-lookup"><span data-stu-id="91d17-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="91d17-161">Dus als bepaalde aanvragen onjuist uitvoert, kunt u vinden of deze is als gevolg van trage reacties van een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="91d17-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="91d17-162">We gaan een voorbeeld van die doorlopen.</span><span class="sxs-lookup"><span data-stu-id="91d17-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="91d17-163">Tracering van aanvragen naar afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="91d17-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="91d17-164">Open de blade Performance en bekijk het raster van aanvragen:</span><span class="sxs-lookup"><span data-stu-id="91d17-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Lijst met aanvragen met gemiddelden en tellingen](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="91d17-166">De bovenste een duurt zeer lang.</span><span class="sxs-lookup"><span data-stu-id="91d17-166">The top one is taking very long.</span></span> <span data-ttu-id="91d17-167">Laten we zien als we vindt waarbij de tijd is besteed.</span><span class="sxs-lookup"><span data-stu-id="91d17-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="91d17-168">Klik op die rij om afzonderlijke aanvraag gebeurtenissen te bekijken:</span><span class="sxs-lookup"><span data-stu-id="91d17-168">Click that row to see individual request events:</span></span>

![Lijst van instanties van de aanvraag](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="91d17-170">Klik op een willekeurig exemplaar langlopende om verdere inspecteren en schuif omlaag naar de externe afhankelijkheidsaanroepen die betrekking hebben op deze aanvraag:</span><span class="sxs-lookup"><span data-stu-id="91d17-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Vinden van aanroepen naar externe afhankelijkheden, het identificeren van ongebruikelijke duur](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="91d17-172">Het lijkt erop dat de meeste van de tijd van onderhoud van deze aanvraag is die is doorgebracht in een aanroep van een lokale service.</span><span class="sxs-lookup"><span data-stu-id="91d17-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="91d17-173">Selecteer die rij voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="91d17-173">Select that row to get more information:</span></span>

![Deze externe afhankelijkheid voor het identificeren van de stackpad doorklikken](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="91d17-175">Lijkt erop dat dit is waar het probleem is.</span><span class="sxs-lookup"><span data-stu-id="91d17-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="91d17-176">We het probleem hebt nauwkeurige, dus nu we zojuist hebt om erachter te komen waarom die aanroep te lang duurt.</span><span class="sxs-lookup"><span data-stu-id="91d17-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="91d17-177">Aanvraag tijdlijn</span><span class="sxs-lookup"><span data-stu-id="91d17-177">Request timeline</span></span>
<span data-ttu-id="91d17-178">Er is geen afhankelijkheidsaanroep die is een bijzonder lange in andere gevallen.</span><span class="sxs-lookup"><span data-stu-id="91d17-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="91d17-179">Maar door het overschakelen naar de tijdlijnweergave, kunnen we zien waar de vertraging is opgetreden bij het verwerken van onze interne:</span><span class="sxs-lookup"><span data-stu-id="91d17-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Vinden van aanroepen naar externe afhankelijkheden, het identificeren van ongebruikelijke duur](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="91d17-181">Er lijkt een gap big nadat de eerste afhankelijkheid aangeroepen, zodat we onze code om te zien waarom moet kijken.</span><span class="sxs-lookup"><span data-stu-id="91d17-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="91d17-182">Profiel van uw live site</span><span class="sxs-lookup"><span data-stu-id="91d17-182">Profile your live site</span></span>

<span data-ttu-id="91d17-183">Er is geen idee waar de tijd gaat?</span><span class="sxs-lookup"><span data-stu-id="91d17-183">No idea where the time goes?</span></span> <span data-ttu-id="91d17-184">De [Application Insights profiler](app-insights-profiler.md) traceringen HTTP-aanroepen naar uw live site en ziet u welke functies in uw code het langst heeft geduurd.</span><span class="sxs-lookup"><span data-stu-id="91d17-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="91d17-185">Mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="91d17-185">Failed requests</span></span>
<span data-ttu-id="91d17-186">Mislukte aanvragen kunnen ook zijn gekoppeld aan de mislukte aanroepen naar afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="91d17-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="91d17-187">We kunnen opnieuw in en klik in voor het opsporen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="91d17-187">Again, we can click through to track down the problem.</span></span>

![Klik op de grafiek mislukte aanvragen](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="91d17-189">Klik verder naar een exemplaar van een mislukte aanvraag en bekijk de bijbehorende gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="91d17-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Klik op een aanvraag met het type, het exemplaar voor ophalen naar een andere weergave van hetzelfde exemplaar, klikt u erop om details van uitzondering.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="91d17-191">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="91d17-191">Analytics</span></span>
<span data-ttu-id="91d17-192">U kunt volgen afhankelijkheden in de [querytaal van logboekanalyse](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="91d17-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="91d17-193">Hier volgen enkele voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="91d17-193">Here are some examples.</span></span>

* <span data-ttu-id="91d17-194">Alle mislukte afhankelijkheidsaanroepen vinden:</span><span class="sxs-lookup"><span data-stu-id="91d17-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="91d17-195">AJAX-aanroepen vinden:</span><span class="sxs-lookup"><span data-stu-id="91d17-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="91d17-196">Afhankelijkheidsaanroepen verband met aanvragen zoeken:</span><span class="sxs-lookup"><span data-stu-id="91d17-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="91d17-197">Zoeken naar AJAX-aanroepen die zijn gekoppeld aan paginaweergaven:</span><span class="sxs-lookup"><span data-stu-id="91d17-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="91d17-198">Bijhouden van aangepaste afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="91d17-198">Custom dependency tracking</span></span>
<span data-ttu-id="91d17-199">De standaard afhankelijkheid bijhouden module detecteert automatisch de externe afhankelijkheden, zoals databases en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="91d17-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="91d17-200">Maar u kunt een aantal extra onderdelen op dezelfde manier worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="91d17-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="91d17-201">Kunt u code schrijven waarmee afhankelijkheidsinformatie, worden verzonden met behulp van dezelfde [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) dat wordt gebruikt door de standard-modules.</span><span class="sxs-lookup"><span data-stu-id="91d17-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="91d17-202">Als u uw code met een assembly die u zelf niet schrijven maken, kan u bijvoorbeeld alle aanroepen, om erachter te komen welke bijdrage hiervan in uw reactietijden tijd.</span><span class="sxs-lookup"><span data-stu-id="91d17-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="91d17-203">Als u deze gegevens weergegeven in de afhankelijkheidsgrafiek in Application Insights, verzenden met behulp van `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="91d17-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="91d17-204">Als u de standaard afhankelijkheid bijhouden module uitschakelen wilt, verwijdert u de verwijzing naar DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="91d17-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="91d17-205">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="91d17-205">Troubleshooting</span></span>
<span data-ttu-id="91d17-206">*Afhankelijkheid geslaagd vlag altijd toont waar of ONWAAR.*</span><span class="sxs-lookup"><span data-stu-id="91d17-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="91d17-207">*SQL-query is niet volledig worden weergegeven.*</span><span class="sxs-lookup"><span data-stu-id="91d17-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="91d17-208">Voer een upgrade naar de nieuwste versie van de SDK.</span><span class="sxs-lookup"><span data-stu-id="91d17-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="91d17-209">Als uw versie van .NET minder dan 4.6 is:</span><span class="sxs-lookup"><span data-stu-id="91d17-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="91d17-210">IIS-host: installeren [Application Insights-Agent](app-insights-monitor-performance-live-website-now.md) op de host-servers.</span><span class="sxs-lookup"><span data-stu-id="91d17-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="91d17-211">Azure-web-app: Open Application Insights tabblad in het Configuratiescherm van de web-app en installeer Application Insights.</span><span class="sxs-lookup"><span data-stu-id="91d17-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="91d17-212">Video</span><span class="sxs-lookup"><span data-stu-id="91d17-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="91d17-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91d17-213">Next steps</span></span>
* [<span data-ttu-id="91d17-214">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="91d17-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="91d17-215">Gebruiker- en paginagegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="91d17-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="91d17-216">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="91d17-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
