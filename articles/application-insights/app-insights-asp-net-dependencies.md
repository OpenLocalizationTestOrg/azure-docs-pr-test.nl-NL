---
title: aaaDependency bijhouden in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="8fc06-103">Application Insights instellen: afhankelijkheid bijhouden</span><span class="sxs-lookup"><span data-stu-id="8fc06-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="8fc06-104">Een *afhankelijkheid* is een externe component die wordt aangeroepen door uw app.</span><span class="sxs-lookup"><span data-stu-id="8fc06-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="8fc06-105">Dit is doorgaans een service die is aangeroepen met behulp van HTTP, of een database of een bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="8fc06-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="8fc06-106">[Application Insights](app-insights-overview.md) maatregelen hoe lang de toepassing moet wachten voor afhankelijkheden en hoe vaak een afhankelijkheidsaanroep is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8fc06-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="8fc06-107">U kunt specifieke aanroepen te onderzoeken en koppelen toorequests en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![voorbeeldgrafieken](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="8fc06-109">Hallo out-of-the-box afhankelijkheidsmonitor rapporten momenteel aanroepen toothese typen afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="8fc06-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="8fc06-110">Server</span><span class="sxs-lookup"><span data-stu-id="8fc06-110">Server</span></span>
  * <span data-ttu-id="8fc06-111">SQL-databases</span><span class="sxs-lookup"><span data-stu-id="8fc06-111">SQL databases</span></span>
  * <span data-ttu-id="8fc06-112">ASP.NET-webtoepassingen en WCF-services die gebruikmaken van bindingen op basis van HTTP</span><span class="sxs-lookup"><span data-stu-id="8fc06-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="8fc06-113">Lokale of externe HTTP-aanroepen</span><span class="sxs-lookup"><span data-stu-id="8fc06-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="8fc06-114">Azure DB Cosmos, tabel, blob-opslag en wachtrij</span><span class="sxs-lookup"><span data-stu-id="8fc06-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="8fc06-115">Webpagina's</span><span class="sxs-lookup"><span data-stu-id="8fc06-115">Web pages</span></span>
  * <span data-ttu-id="8fc06-116">AJAX-aanroepen</span><span class="sxs-lookup"><span data-stu-id="8fc06-116">AJAX calls</span></span>

<span data-ttu-id="8fc06-117">Bewaking werkt met [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) rond geselecteerde methoden.</span><span class="sxs-lookup"><span data-stu-id="8fc06-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="8fc06-118">Prestatieoverhead is minimaal.</span><span class="sxs-lookup"><span data-stu-id="8fc06-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="8fc06-119">U kunt ook schrijven uw eigen SDK-aanroepen toomonitor andere afhankelijkheden, zowel in Hallo client en server code met Hallo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="8fc06-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="8fc06-120">Bewaking van afhankelijkheid ingesteld</span><span class="sxs-lookup"><span data-stu-id="8fc06-120">Set up dependency monitoring</span></span>
<span data-ttu-id="8fc06-121">Gedeeltelijke afhankelijkheidsgegevens worden automatisch verzameld door Hallo [Application Insights-SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="8fc06-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="8fc06-122">tooget volledige gegevens, installeren de desbetreffende agent Hallo voor Hallo host-server.</span><span class="sxs-lookup"><span data-stu-id="8fc06-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="8fc06-123">Platform</span><span class="sxs-lookup"><span data-stu-id="8fc06-123">Platform</span></span> | <span data-ttu-id="8fc06-124">Installeren</span><span class="sxs-lookup"><span data-stu-id="8fc06-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="8fc06-125">IIS-Server</span><span class="sxs-lookup"><span data-stu-id="8fc06-125">IIS Server</span></span> |<span data-ttu-id="8fc06-126">Beide [Status Monitor installeren op uw server](app-insights-monitor-performance-live-website-now.md) of [Upgrade van uw toepassing too.NET framework 4.6 of hoger](http://go.microsoft.com/fwlink/?LinkId=528259) en installeer Hallo [Application Insights-SDK](app-insights-asp-net.md) in uw app.</span><span class="sxs-lookup"><span data-stu-id="8fc06-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="8fc06-127">Azure Web App</span><span class="sxs-lookup"><span data-stu-id="8fc06-127">Azure Web App</span></span> |<span data-ttu-id="8fc06-128">In het Configuratiescherm voor web-app [Application Insights-blade open Hallo in uw web-app-Configuratiescherm](app-insights-azure-web-apps.md) en kies installeren als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8fc06-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="8fc06-129">Azure-Cloudservice</span><span class="sxs-lookup"><span data-stu-id="8fc06-129">Azure Cloud Service</span></span> |<span data-ttu-id="8fc06-130">[Gebruik opstarttaak](app-insights-cloudservices.md) of [installeren .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="8fc06-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="8fc06-131">Waar gegevens voor toofind-afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="8fc06-131">Where toofind dependency data</span></span>
* <span data-ttu-id="8fc06-132">[De toepassingstoewijzing](#application-map) visualiseren van afhankelijkheden tussen uw app en de aangrenzende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="8fc06-133">[Prestaties, browser en fout blades](#performance-and-blades) server afhankelijkheidsgegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8fc06-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="8fc06-134">[Blade browsers](#ajax-calls) AJAX-aanroepen vanuit de browsers van uw gebruikers bevat.</span><span class="sxs-lookup"><span data-stu-id="8fc06-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="8fc06-135">[Klik door vanuit traag of mislukte aanvragen](#diagnose-slow-requests) toocheck hun afhankelijkheidsaanroepen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="8fc06-136">[Analytics](#analytics) gebruikte tooquery afhankelijkheidsgegevens kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="8fc06-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="8fc06-137">Toepassingskaart</span><span class="sxs-lookup"><span data-stu-id="8fc06-137">Application Map</span></span>
<span data-ttu-id="8fc06-138">De toepassingstoewijzing fungeert als een visuele hulpmiddel toodiscovering afhankelijkheden tussen Hallo onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8fc06-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="8fc06-139">Deze wordt automatisch gegenereerd vanuit Hallo telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="8fc06-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="8fc06-140">Dit voorbeeld toont AJAX-aanroepen vanuit Hallo browser scripts en REST-aanroepen van Hallo server app-tootwo externe services.</span><span class="sxs-lookup"><span data-stu-id="8fc06-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Toepassingskaart](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="8fc06-142">**Navigeer in de vakken Hallo** toorelevant afhankelijkheid en andere grafieken.</span><span class="sxs-lookup"><span data-stu-id="8fc06-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="8fc06-143">**Pincode Hallo kaart** toohello [dashboard](app-insights-dashboards.md), wordt waar deze volledig functioneel.</span><span class="sxs-lookup"><span data-stu-id="8fc06-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="8fc06-144">[Meer informatie](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="8fc06-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="8fc06-145">Prestatie- en blades</span><span class="sxs-lookup"><span data-stu-id="8fc06-145">Performance and failure blades</span></span>
<span data-ttu-id="8fc06-146">de blade performance Hallo bevat Hallo duur van afhankelijkheidsaanroepen die zijn aangebracht door Hallo server app.</span><span class="sxs-lookup"><span data-stu-id="8fc06-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="8fc06-147">Er is een overzichtstabel en een tabel gesegmenteerd op aanroep.</span><span class="sxs-lookup"><span data-stu-id="8fc06-147">There's a summary chart and a table segmented by call.</span></span>

![Afhankelijkheid van de prestatiegrafieken-blade](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="8fc06-149">Klik in de samenvatting grafieken Hallo of Hallo tabel items toosearch onbewerkte instanties van deze aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Afhankelijkheid aanroep exemplaren](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="8fc06-151">**Foutaantallen** worden weergegeven op Hallo **fouten** blade.</span><span class="sxs-lookup"><span data-stu-id="8fc06-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="8fc06-152">Een mislukte is een retourcode die zich niet in Hallo bereik 200-399, of onbekend.</span><span class="sxs-lookup"><span data-stu-id="8fc06-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc06-153">**100% fouten?**</span><span class="sxs-lookup"><span data-stu-id="8fc06-153">**100% failures?**</span></span> <span data-ttu-id="8fc06-154">-Dit wordt waarschijnlijk geeft aan dat u alleen afhankelijkheidsgegevens van gedeeltelijke krijgt.</span><span class="sxs-lookup"><span data-stu-id="8fc06-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="8fc06-155">U moet te[afhankelijkheid bewaking van de juiste tooyour platform instellen](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="8fc06-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="8fc06-156">AJAX-aanroepen</span><span class="sxs-lookup"><span data-stu-id="8fc06-156">AJAX Calls</span></span>
<span data-ttu-id="8fc06-157">de blade Browsers Hallo toont Hallo duur en percentage mislukte AJAX-aanroepen van [JavaScript in uw webpagina's](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8fc06-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="8fc06-158">Deze worden weergegeven als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8fc06-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="8fc06-159"><a name="diagnosis"></a>Diagnose van trage aanvragen</span><span class="sxs-lookup"><span data-stu-id="8fc06-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="8fc06-160">Elke gebeurtenis van de aanvraag is gekoppeld aan afhankelijkheidsaanroepen hello, uitzonderingen en andere gebeurtenissen die worden bijgehouden, terwijl het verwerken van uw app Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8fc06-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="8fc06-161">Dus als bepaalde aanvragen onjuist uitvoert, kunt u vinden of dit is vanwege tooslow antwoorden van een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="8fc06-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="8fc06-162">We gaan een voorbeeld van die doorlopen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="8fc06-163">Tracering van aanvragen toodependencies</span><span class="sxs-lookup"><span data-stu-id="8fc06-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="8fc06-164">Open de blade Performance Hallo en bekijkt hello raster van aanvragen:</span><span class="sxs-lookup"><span data-stu-id="8fc06-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Lijst met aanvragen met gemiddelden en tellingen](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="8fc06-166">Hallo boven op een zeer lang duurt.</span><span class="sxs-lookup"><span data-stu-id="8fc06-166">hello top one is taking very long.</span></span> <span data-ttu-id="8fc06-167">Laten we zien als we vindt waarbij Hallo tijd is besteed.</span><span class="sxs-lookup"><span data-stu-id="8fc06-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="8fc06-168">Klik op die rij toosee afzonderlijke gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="8fc06-168">Click that row toosee individual request events:</span></span>

![Lijst van instanties van de aanvraag](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="8fc06-170">Klik op een langlopende exemplaar tooinspect deze nog verder en schuif naar beneden toohello externe afhankelijkheid aanroepen gerelateerde toothis aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8fc06-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Aanroepen tooRemote afhankelijkheden vinden, ongebruikelijke duur identificeren](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="8fc06-172">Het lijkt erop dat de meeste Hallo tijd onderhoud van die deze aanvraag is gespendeerd aan het gesprek tooa lokale service.</span><span class="sxs-lookup"><span data-stu-id="8fc06-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="8fc06-173">Meer informatie voor die rij tooget selecteren:</span><span class="sxs-lookup"><span data-stu-id="8fc06-173">Select that row tooget more information:</span></span>

![Klik op de link die externe afhankelijkheid tooidentify Hallo stackpad](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="8fc06-175">Lijkt erop dat dit is waar Hallo probleem is.</span><span class="sxs-lookup"><span data-stu-id="8fc06-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="8fc06-176">Wij Hallo probleem hebt nauwkeurige, dus nu we zojuist hebt toofind uit waarom die aanroep te lang duurt.</span><span class="sxs-lookup"><span data-stu-id="8fc06-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="8fc06-177">Aanvraag tijdlijn</span><span class="sxs-lookup"><span data-stu-id="8fc06-177">Request timeline</span></span>
<span data-ttu-id="8fc06-178">Er is geen afhankelijkheidsaanroep die is een bijzonder lange in andere gevallen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="8fc06-179">Maar door overschakelt naar de tijdlijnweergave toohello, kunnen we zien waar Hallo vertraging is opgetreden bij het verwerken van onze interne:</span><span class="sxs-lookup"><span data-stu-id="8fc06-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Aanroepen tooRemote afhankelijkheden vinden, ongebruikelijke duur identificeren](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="8fc06-181">Er lijkt toobe een gap big na het eerste afhankelijkheidsaanroep hello, zodat we onze toosee code moet bekijken waarom is.</span><span class="sxs-lookup"><span data-stu-id="8fc06-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="8fc06-182">Profiel van uw live site</span><span class="sxs-lookup"><span data-stu-id="8fc06-182">Profile your live site</span></span>

<span data-ttu-id="8fc06-183">Er is geen idee waar Hallo tijd gaat? Hallo [Application Insights profiler](app-insights-profiler.md) traceringen HTTP-live site tooyour aanroept en ziet u welke functies in uw code duurde Hallo langst.</span><span class="sxs-lookup"><span data-stu-id="8fc06-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="8fc06-184">Mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="8fc06-184">Failed requests</span></span>
<span data-ttu-id="8fc06-185">Mislukte aanvragen kunnen ook zijn gekoppeld aan toodependencies mislukte aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8fc06-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="8fc06-186">We kunnen opnieuw tootrack omlaag Hallo probleem doorklikken.</span><span class="sxs-lookup"><span data-stu-id="8fc06-186">Again, we can click through tootrack down hello problem.</span></span>

![Klik op Hallo mislukte aanvragen grafiek](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="8fc06-188">Klik op tooan exemplaar van een mislukte aanvraag en de bijbehorende gebeurtenissen bekijken.</span><span class="sxs-lookup"><span data-stu-id="8fc06-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Klik op een aanvraagtype, klikt u op Hallo tooget tooa verschillende instantieweergave van hetzelfde exemplaar hello, klikt u erop tooget uitzonderingsdetails.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="8fc06-190">Analytische gegevens</span><span class="sxs-lookup"><span data-stu-id="8fc06-190">Analytics</span></span>
<span data-ttu-id="8fc06-191">U kunt volgen afhankelijkheden in Hallo [querytaal van logboekanalyse](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="8fc06-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="8fc06-192">Hier volgen enkele voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8fc06-192">Here are some examples.</span></span>

* <span data-ttu-id="8fc06-193">Alle mislukte afhankelijkheidsaanroepen vinden:</span><span class="sxs-lookup"><span data-stu-id="8fc06-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="8fc06-194">AJAX-aanroepen vinden:</span><span class="sxs-lookup"><span data-stu-id="8fc06-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="8fc06-195">Afhankelijkheidsaanroepen verband met aanvragen zoeken:</span><span class="sxs-lookup"><span data-stu-id="8fc06-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="8fc06-196">Zoeken naar AJAX-aanroepen die zijn gekoppeld aan paginaweergaven:</span><span class="sxs-lookup"><span data-stu-id="8fc06-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="8fc06-197">Bijhouden van aangepaste afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="8fc06-197">Custom dependency tracking</span></span>
<span data-ttu-id="8fc06-198">Hallo standaard afhankelijkheid bijhouden module detecteert automatisch de externe afhankelijkheden, zoals databases en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="8fc06-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="8fc06-199">Maar u kunt een aantal extra onderdelen toobe behandeld in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="8fc06-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="8fc06-200">U kunt code schrijven waarmee afhankelijkheidsinformatie, verzendt met behulp van dezelfde Hallo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) dat wordt gebruikt door Hallo standaard modules.</span><span class="sxs-lookup"><span data-stu-id="8fc06-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="8fc06-201">Bijvoorbeeld, als u uw code met een assembly maken die u zelf niet schrijven, of u alle Hallo aanroepen tooit kan tijd, keren toofind uit wat de bijdrage tooyour antwoord maakt.</span><span class="sxs-lookup"><span data-stu-id="8fc06-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="8fc06-202">toohave deze gegevens weergegeven in de afhankelijkheidsgrafiek Hallo in Application Insights verzenden met behulp van `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="8fc06-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="8fc06-203">Als u tooswitch uit Hallo standaard afhankelijkheid bijhouden wilt, verwijdert u Hallo verwijzing tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="8fc06-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8fc06-204">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8fc06-204">Troubleshooting</span></span>
<span data-ttu-id="8fc06-205">*Afhankelijkheid geslaagd vlag altijd toont waar of ONWAAR.*</span><span class="sxs-lookup"><span data-stu-id="8fc06-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="8fc06-206">*SQL-query is niet volledig worden weergegeven.*</span><span class="sxs-lookup"><span data-stu-id="8fc06-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="8fc06-207">Meest recente versie van de toohello van Hallo SDK bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8fc06-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="8fc06-208">Als uw versie van .NET minder dan 4.6 is:</span><span class="sxs-lookup"><span data-stu-id="8fc06-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="8fc06-209">IIS-host: installeren [Application Insights-Agent](app-insights-monitor-performance-live-website-now.md) op Hallo-hostservers.</span><span class="sxs-lookup"><span data-stu-id="8fc06-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="8fc06-210">Azure-web-app: Open Application Insights tabblad Hallo web-app het Configuratiescherm en installeer Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8fc06-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="8fc06-211">Video</span><span class="sxs-lookup"><span data-stu-id="8fc06-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="8fc06-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fc06-212">Next steps</span></span>
* [<span data-ttu-id="8fc06-213">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="8fc06-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="8fc06-214">Gebruiker- en paginagegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="8fc06-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="8fc06-215">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="8fc06-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
