---
title: aaaAzure Application Insights voor JavaScript web-apps | Microsoft Docs
description: Verzamel tellingen van het aantal paginaweergaven en sessies, webclientgegevens en gebruikspatronen. Detecteer uitzonderingen en prestatieproblemen in JavaScript-webpagina's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="45729-104">Application Insights voor webpagina’s</span><span class="sxs-lookup"><span data-stu-id="45729-104">Application Insights for web pages</span></span>
<span data-ttu-id="45729-105">Lees over Hallo prestaties en het gebruik van uw webpagina's of app.</span><span class="sxs-lookup"><span data-stu-id="45729-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="45729-106">Als u [Application Insights](app-insights-overview.md) tooyour pagina script, krijgt u de tijdsinstellingen van pagina's en AJAX-aanroepen, tellingen en details van browseruitzonderingen en AJAX-fouten, evenals gebruikers en aantallen sessie.</span><span class="sxs-lookup"><span data-stu-id="45729-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="45729-107">Al deze gegevens kunnen worden gesegmenteerd op pagina, clientbesturingssysteem en browserversie, geografische locatie en andere dimensies.</span><span class="sxs-lookup"><span data-stu-id="45729-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="45729-108">U kunt waarschuwingen instellen voor foutaantallen of het langzaam laden van de pagina.</span><span class="sxs-lookup"><span data-stu-id="45729-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="45729-109">En door het invoegen van traceringsaanroepen in uw JavaScript-code, kunt u bijhouden hoe verschillende functies van uw webpagina-toepassing hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="45729-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="45729-110">Application Insights kan met elke webpagina worden gebruikt. Het enige wat u hiervoor hoeft te doen, is een klein stukje JavaScript toevoegen.</span><span class="sxs-lookup"><span data-stu-id="45729-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="45729-111">Als de webservice [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) is, kunt u telemetrie van uw server en clients integreren.</span><span class="sxs-lookup"><span data-stu-id="45729-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Open de resource van uw app in portal.azure.com en klik op Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="45729-113">U hebt een abonnement te[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="45729-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="45729-114">Als uw team een organisatie-abonnement heeft, vraagt u Hallo eigenaar tooadd uw tooit Microsoft-Account.</span><span class="sxs-lookup"><span data-stu-id="45729-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="45729-115">Ontwikkeling en kleinschalig gebruik kosten u niets.</span><span class="sxs-lookup"><span data-stu-id="45729-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="45729-116">Application Insights instellen voor uw webpagina</span><span class="sxs-lookup"><span data-stu-id="45729-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="45729-117">Hallo loader code codefragment tooyour webpagina's, als volgt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="45729-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="45729-118">Een Application Insights-resource openen of maken</span><span class="sxs-lookup"><span data-stu-id="45729-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="45729-119">Hallo Application Insights-resource worden gegevens over de prestaties en het gebruik van uw pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="45729-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="45729-120">Meld u aan bij de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45729-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="45729-121">Als u al een controle voor de serverzijde Hallo van uw app ingesteld, hebt u al een resource:</span><span class="sxs-lookup"><span data-stu-id="45729-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Kies Bladeren, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="45729-123">Als u nog geen resource hebt, maakt u er een:</span><span class="sxs-lookup"><span data-stu-id="45729-123">If you don't have one, create it:</span></span>

![Kies Nieuw, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="45729-125">*Heb u op dit moment vragen?*</span><span class="sxs-lookup"><span data-stu-id="45729-125">*Questions already?*</span></span> <span data-ttu-id="45729-126">[Meer over het maken van een resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="45729-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="45729-127">Hallo SDK script tooyour app of webpagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="45729-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="45729-128">Haal Hallo script voor webpagina's in Snel starten:</span><span class="sxs-lookup"><span data-stu-id="45729-128">In Quick Start, get hello script for web pages:</span></span>

![Op de overzichtsblade van uw app, kiest u snel starten, kunt u code toomonitor mijn webpagina's.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="45729-131">Voeg Hallo script net vóór Hallo `</head>` tag van elke pagina die u wilt tootrack.</span><span class="sxs-lookup"><span data-stu-id="45729-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="45729-132">Als uw website een basispagina heeft, kunt u er Hallo script plaatsen.</span><span class="sxs-lookup"><span data-stu-id="45729-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="45729-133">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="45729-133">For example:</span></span>

* <span data-ttu-id="45729-134">In een ASP.NET-MVC-project plaatst u het in `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="45729-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="45729-135">Open in een SharePoint-site op Hallo van het Configuratiescherm, [Site-instellingen / basispagina](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="45729-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="45729-136">Hallo-script bevat de instrumentatiesleutel Hallo waarin wordt verwezen Hallo gegevens tooyour Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="45729-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="45729-137">([Nadere uitleg van Hallo-script. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="45729-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="45729-138">*(Als u een bekend webpaginaframework gebruikt, is het een goed idee om op zoek te gaan naar een geschikte Application Insights-adapter. Er is bijvoorbeeld een [AngularJS-module](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="45729-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="45729-139">Gedetailleerde configuratie</span><span class="sxs-lookup"><span data-stu-id="45729-139">Detailed configuration</span></span>
<span data-ttu-id="45729-140">U kunt diverse [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) instellen. In de meeste gevallen is dat echter niet nodig.</span><span class="sxs-lookup"><span data-stu-id="45729-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="45729-141">U kunt bijvoorbeeld uitschakelen of beperken Hallo aantal Ajax-aanroepen per paginaweergave (tooreduce verkeer) gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="45729-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="45729-142">Of u kunt de foutopsporing modus toohave telemetrie verplaatsen snel via Hallo pipeline instellen zonder in batch worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="45729-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="45729-143">tooset deze parameters zoekt u deze regel in het codefragment Hallo en meer door komma's gescheiden items toevoegen nadat deze:</span><span class="sxs-lookup"><span data-stu-id="45729-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="45729-144">Hallo [beschikbare parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) omvatten:</span><span class="sxs-lookup"><span data-stu-id="45729-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="45729-145"><a name="run"></a>Uw app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="45729-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="45729-146">Uw web-app uitvoeren, gebruiken een tijdens toogenerate Telemetrie en wacht een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="45729-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="45729-147">U kunt uitvoeren met behulp van Hallo **F5** sleutel op uw ontwikkelcomputer of publiceren en door gebruikers laten uitproberen aan.</span><span class="sxs-lookup"><span data-stu-id="45729-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="45729-148">Als u toocheck Hallo telemetrie wilt dat een web-app tooApplication Insights verzendt, gebruikt u de foutopsporingsprogramma's van de browser (**F12** in veel browsers).</span><span class="sxs-lookup"><span data-stu-id="45729-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="45729-149">Gegevens worden toodc.services.visualstudio.com verzonden.</span><span class="sxs-lookup"><span data-stu-id="45729-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="45729-150">Gegevens over uw browserprestaties verkennen</span><span class="sxs-lookup"><span data-stu-id="45729-150">Explore your browser performance data</span></span>
<span data-ttu-id="45729-151">Open Hallo Browser blade tooshow geaggregeerd prestatiegegevens van de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45729-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![Open de resource van uw app in portal.azure.com en klik op Instellingen, Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="45729-153">*Zijn er nog geen gegevens? Klik op **vernieuwen** bovenaan Hallo Hallo pagina. Ziet u nog steeds niets? Raadpleeg [Probleemoplossing](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="45729-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="45729-154">Hallo Browser blade is een [Metrics Explorer-blade](app-insights-metrics-explorer.md) met vooraf ingestelde filters en grafiekselecties.</span><span class="sxs-lookup"><span data-stu-id="45729-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="45729-155">U kunt het tijdsbereik hello, filters en configuratie van de grafiek bewerken als u wilt en Hallo resultaat als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="45729-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="45729-156">Klik op **standaardwaarden herstellen** tooget back toohello oorspronkelijke bladeconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="45729-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="45729-157">Laadprestaties van de pagina</span><span class="sxs-lookup"><span data-stu-id="45729-157">Page load performance</span></span>
<span data-ttu-id="45729-158">Hallo is top een grafieksegment met laadtijden van pagina's.</span><span class="sxs-lookup"><span data-stu-id="45729-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="45729-159">totale hoogte van de grafiek Hallo Hallo vertegenwoordigt Hallo gemiddelde tijd tooload en weergave van pagina's van uw app in browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45729-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="45729-160">Hallo tijd wordt gemeten vanaf wanneer Hallo browser Hallo eerste HTTP-aanvraag tot alle synchrone load gebeurtenissen zijn verwerkt verzendt, met inbegrip van indeling en de scripts uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45729-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="45729-161">Asynchrone taken, zoals het laden van de webonderdelen van AJAX-aanroepen, zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="45729-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="45729-162">Hallo grafiek segmenteert Hallo totale paginalaadtijd in Hallo [standaardtijdsinstellingen gedefinieerd door W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="45729-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="45729-163">Houd er rekening mee dat Hallo *netwerk verbinden* is vaak lager dan u verwacht, omdat het is een gemiddelde over alle aanvragen van Hallo browser toohello-server.</span><span class="sxs-lookup"><span data-stu-id="45729-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="45729-164">Veel afzonderlijke aanvragen hebben een verbindingstijd van 0, omdat er al een actieve verbinding toohello-server.</span><span class="sxs-lookup"><span data-stu-id="45729-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="45729-165">Worden pagina’s traag geladen?</span><span class="sxs-lookup"><span data-stu-id="45729-165">Slow loading?</span></span>
<span data-ttu-id="45729-166">Het traag laden van pagina is voor uw gebruikers een belangrijke bron van ergernis.</span><span class="sxs-lookup"><span data-stu-id="45729-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="45729-167">Als het Hallo-grafiek aangeeft dat pagina traag worden geladen, is het eenvoudig toodo wat diagnostisch onderzoek.</span><span class="sxs-lookup"><span data-stu-id="45729-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="45729-168">Hallo diagram toont Hallo gemiddelde paginalaadtijd in uw app.</span><span class="sxs-lookup"><span data-stu-id="45729-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="45729-169">toosee als Hallo probleem zich beperkt tooparticular pagina's, uiterlijk verder omlaag Hallo blade, waarbij er een raster gesegmenteerd op pagina-URL:</span><span class="sxs-lookup"><span data-stu-id="45729-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="45729-170">U ziet Hallo aantal paginaweergaven en de standaarddeviatie.</span><span class="sxs-lookup"><span data-stu-id="45729-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="45729-171">Als het Hallo-aantal pagina's zeer laag is, klikt u vervolgens Hallo probleem is niet dat gebruikers ondervonden veel.</span><span class="sxs-lookup"><span data-stu-id="45729-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="45729-172">Een hoge standaarddeviatie (vergelijkbaar toohello gemiddelde) geeft aan dat er grote verschillen bestaan tussen de afzonderlijke metingen.</span><span class="sxs-lookup"><span data-stu-id="45729-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="45729-173">**Zoom in op een URL en een paginaweergave.**</span><span class="sxs-lookup"><span data-stu-id="45729-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="45729-174">Klik op elke pagina naam toosee een blade van de browser grafieken gefilterde alleen toothat URL; en vervolgens op een exemplaar van een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="45729-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="45729-175">Klik op `...` voor een volledige lijst met eigenschappen voor die gebeurtenis of Controleer Hallo Ajax-aanroepen en gerelateerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="45729-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="45729-176">Trage Ajax-aanroepen Hallo van invloed zijn op de algemene laadtijd van pagina als beide synchroon gebeuren.</span><span class="sxs-lookup"><span data-stu-id="45729-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="45729-177">Gerelateerde gebeurtenissen omvatten serveraanvragen voor Hallo dezelfde URL (als u Application Insights hebt ingesteld op uw webserver).</span><span class="sxs-lookup"><span data-stu-id="45729-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="45729-178">**Paginaprestaties over langere tijd.**</span><span class="sxs-lookup"><span data-stu-id="45729-178">**Page performance over time.**</span></span> <span data-ttu-id="45729-179">Wijzigen terug op de blade Browsers Hallo Hallo laadtijd voor paginaweergave raster in een grafiek regel toosee als er pieken op bepaalde tijden:</span><span class="sxs-lookup"><span data-stu-id="45729-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Klik op Hallo-head van Hallo raster en een nieuw grafiektype selecteren](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="45729-181">**Segmenteer op andere dimensies.**</span><span class="sxs-lookup"><span data-stu-id="45729-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="45729-182">Uw pagina's mogelijk langzamer tooload op een bepaalde browser, clientbesturingssysteem of gebruiker plaats?</span><span class="sxs-lookup"><span data-stu-id="45729-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="45729-183">Voeg een nieuwe grafiek toe en Experimenteer met Hallo **Group by** dimensie.</span><span class="sxs-lookup"><span data-stu-id="45729-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="45729-184">AJAX-prestaties</span><span class="sxs-lookup"><span data-stu-id="45729-184">AJAX Performance</span></span>
<span data-ttu-id="45729-185">Zorg ervoor dat eventuele AJAX-aanroepen op uw webpagina's goed worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="45729-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="45729-186">Ze zijn vaak gebruikte toofill onderdelen van uw pagina asynchroon.</span><span class="sxs-lookup"><span data-stu-id="45729-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="45729-187">Hoewel hello algemene pagina onmiddellijk laadt waarschijnlijk, uw gebruikers zich gaan ergeren doordat ze steeds op lege webonderdelen, wachten op gegevens tooappear bevat.</span><span class="sxs-lookup"><span data-stu-id="45729-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="45729-188">AJAX-aanroepen vanuit uw webpagina worden weergegeven op de blade Browsers Hallo als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="45729-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="45729-189">Samenvattingsgrafieken in Hallo bovenste gedeelte van de blade Hallo:</span><span class="sxs-lookup"><span data-stu-id="45729-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="45729-190">en verder naar beneden gedetailleerde rasters:</span><span class="sxs-lookup"><span data-stu-id="45729-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="45729-191">Klik op een rij voor specifieke informatie.</span><span class="sxs-lookup"><span data-stu-id="45729-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="45729-192">Als u een filter voor Hallo-Browsers op Hallo blade verwijdert, worden zowel de server als de AJAX-afhankelijkheden opgenomen in deze grafieken.</span><span class="sxs-lookup"><span data-stu-id="45729-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="45729-193">Klik op standaardinstellingen herstellen tooreconfigure Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="45729-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="45729-194">**toodrill in mislukte Ajax-aanroepen** Schuif naar beneden toohello met afhankelijkheidsfouten en klik vervolgens op een specifieke rij toosee-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="45729-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="45729-195">Klik op `...` voor Hallo volledige telemetrie voor een Ajax-aanroep.</span><span class="sxs-lookup"><span data-stu-id="45729-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="45729-196">Zijn er geen AJAX-aanroepen gemeld?</span><span class="sxs-lookup"><span data-stu-id="45729-196">No Ajax calls reported?</span></span>
<span data-ttu-id="45729-197">AJAX-aanroepen zijn HTTP/HTTPS-aanroepen vanuit Hallo-script van de webpagina.</span><span class="sxs-lookup"><span data-stu-id="45729-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="45729-198">Als u ze gerapporteerd niet ziet, controleert u dat codefragment Hallo Hallo niet ingesteld `disableAjaxTracking` of `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="45729-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="45729-199">Browseruitzonderingen</span><span class="sxs-lookup"><span data-stu-id="45729-199">Browser exceptions</span></span>
<span data-ttu-id="45729-200">Op de blade Browsers hello wordt een grafiek met samenvattingen uitzonderingen en een raster met typen uitzonderingen lager Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="45729-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="45729-201">Als er geen browseruitzonderingen gerapporteerd, controleert die codefragment Hallo Hallo niet ingesteld `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="45729-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="45729-202">De afzonderlijke paginaweergavegebeurtenissen inspecteren</span><span class="sxs-lookup"><span data-stu-id="45729-202">Inspect individual page view events</span></span>

<span data-ttu-id="45729-203">Meestal wordt telemetrie van paginaweergaven geanalyseerd door Application Insights en ziet u alleen cumulatieve rapporten, het gemiddelde van alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45729-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="45729-204">Maar voor foutopsporing kunt u ook zoeken op afzonderlijke paginaweergavegebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="45729-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="45729-205">Hallo diagnostische gegevens doorzoeken blade ingesteld Filters tooPage weergeven.</span><span class="sxs-lookup"><span data-stu-id="45729-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="45729-206">Selecteer een gebeurtenis toosee meer details.</span><span class="sxs-lookup"><span data-stu-id="45729-206">Select any event toosee more detail.</span></span> <span data-ttu-id="45729-207">Klik in Hallo pagina met details op '...' toosee nog meer details.</span><span class="sxs-lookup"><span data-stu-id="45729-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="45729-208">Als u [Search](app-insights-diagnostic-search.md), aankondiging dat u volledige woorden toomatch hebt: 'Abou' of 'bout' komen niet overeen met 'About'.</span><span class="sxs-lookup"><span data-stu-id="45729-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="45729-209">U kunt ook Hallo krachtige [querytaal van logboekanalyse](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="45729-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="45729-210">Eigenschappen van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="45729-210">Page view properties</span></span>
* <span data-ttu-id="45729-211">**Duur van paginaweergave**</span><span class="sxs-lookup"><span data-stu-id="45729-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="45729-212">Standaard Hallo keer dat er vergt tooload Hallo pagina, van de client aanvraag toofull laden (inclusief hulpbestanden, maar uitgezonderd asynchrone taken zoals Ajax-aanroepen).</span><span class="sxs-lookup"><span data-stu-id="45729-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="45729-213">Als u instelt `overridePageViewDuration` in Hallo [paginaconfiguratie](#detailed-configuration), eerst interval tussen client aanvraag tooexecution Hallo Hallo `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="45729-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="45729-214">Als u trackPageView vanaf de normale positie na de initialisatie van Hallo script hello verplaatst, wordt een andere waarde weer.</span><span class="sxs-lookup"><span data-stu-id="45729-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="45729-215">Als `overridePageViewDuration` is ingesteld en een duurargument is opgegeven in Hallo `trackPageView()` aanroep, Hallo argumentwaarde in plaats daarvan wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="45729-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="45729-216">Aangepast telling van het aantal paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="45729-216">Custom page counts</span></span>
<span data-ttu-id="45729-217">Het aantal pagina's wordt standaard elke keer dat een nieuwe pagina wordt geladen in de browser Hallo van client.</span><span class="sxs-lookup"><span data-stu-id="45729-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="45729-218">Maar u kunt de aanvullende paginaweergaven toocount.</span><span class="sxs-lookup"><span data-stu-id="45729-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="45729-219">Bijvoorbeeld, een pagina kan de inhoud worden weergegeven in tabbladen en u wilt toocount een pagina wanneer de gebruiker Hallo tabbladen overschakelt.</span><span class="sxs-lookup"><span data-stu-id="45729-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="45729-220">Of JavaScript-code in Hallo pagina laadt nieuwe inhoud zonder Hallo browser URL.</span><span class="sxs-lookup"><span data-stu-id="45729-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="45729-221">Invoegen Hallo betreffende punt in uw clientcode een JavaScript-aanroep als volgt:</span><span class="sxs-lookup"><span data-stu-id="45729-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="45729-222">naam van de pagina Hallo mag dezelfde tekens als een URL, maar alles na '#' hello of '? ' wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="45729-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="45729-223">Gebruik bijhouden</span><span class="sxs-lookup"><span data-stu-id="45729-223">Usage tracking</span></span>
<span data-ttu-id="45729-224">Wilt u toofind uit wat gebruikers met uw app doen?</span><span class="sxs-lookup"><span data-stu-id="45729-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="45729-225">Meer informatie over het bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="45729-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="45729-226">[Meer informatie over de API voor aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="45729-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="45729-227"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="45729-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="45729-228"><a name="next"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45729-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="45729-229">Bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="45729-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="45729-230">Aangepaste gebeurtenissen en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="45729-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="45729-231">Bouwen-meten-leren</span><span class="sxs-lookup"><span data-stu-id="45729-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

