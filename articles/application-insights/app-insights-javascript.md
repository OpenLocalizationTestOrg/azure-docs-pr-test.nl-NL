---
title: Azure Application Insights voor JavaScript-web-apps | Microsoft Docs
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
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="e4a9d-104">Application Insights voor webpagina’s</span><span class="sxs-lookup"><span data-stu-id="e4a9d-104">Application Insights for web pages</span></span>
<span data-ttu-id="e4a9d-105">Krijg inzicht in de prestaties en het gebruik van uw webpagina's of app.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="e4a9d-106">Wanneer u [Application Insights](app-insights-overview.md) toevoegt aan uw paginascript, krijgt u de beschikking over allerlei gegevens, zoals de tijden voor het laden van pagina’s en AJAX-aanroepen, tellingen en details van browseruitzonderingen en AJAX-fouten, evenals de aantallen gebruikers en sessies.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="e4a9d-107">Al deze gegevens kunnen worden gesegmenteerd op pagina, clientbesturingssysteem en browserversie, geografische locatie en andere dimensies.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="e4a9d-108">U kunt waarschuwingen instellen voor foutaantallen of het langzaam laden van de pagina.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="e4a9d-109">En door het invoegen van trace-aanroepen in JavaScript-code, kunt u bijhouden hoe de verschillende functies van uw webpaginatoepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="e4a9d-110">Application Insights kan met elke webpagina worden gebruikt. Het enige wat u hiervoor hoeft te doen, is een klein stukje JavaScript toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="e4a9d-111">Als de webservice [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) is, kunt u telemetrie van uw server en clients integreren.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Open de resource van uw app in portal.azure.com en klik op Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="e4a9d-113">U hebt een abonnement op [Microsoft Azure](https://azure.com) nodig.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="e4a9d-114">Als uw team een organisatie-abonnement heeft, vraagt u de eigenaar om uw Microsoft-account hieraan toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="e4a9d-115">Ontwikkeling en kleinschalig gebruik kosten u niets.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="e4a9d-116">Application Insights instellen voor uw webpagina</span><span class="sxs-lookup"><span data-stu-id="e4a9d-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="e4a9d-117">Voeg als volgt het codefragment van de loader toe aan uw webpagina's.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="e4a9d-118">Een Application Insights-resource openen of maken</span><span class="sxs-lookup"><span data-stu-id="e4a9d-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="e4a9d-119">In de Application Insights-resource worden gegevens over de prestaties en het gebruik van uw pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="e4a9d-120">Meld u aan bij de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e4a9d-121">Als u bewaking voor de serverkant van uw app al hebt ingesteld, hebt u al een resource:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Kies Bladeren, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="e4a9d-123">Als u nog geen resource hebt, maakt u er een:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-123">If you don't have one, create it:</span></span>

![Kies Nieuw, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="e4a9d-125">*Heb u op dit moment vragen?*</span><span class="sxs-lookup"><span data-stu-id="e4a9d-125">*Questions already?*</span></span> <span data-ttu-id="e4a9d-126">[Meer over het maken van een resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="e4a9d-127">Het SDK-script toevoegen aan uw app of webpagina's</span><span class="sxs-lookup"><span data-stu-id="e4a9d-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="e4a9d-128">Haal het script voor webpagina's op in Snel starten:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-128">In Quick Start, get the script for web pages:</span></span>

![Kies op de overzichtsblade van uw app de optie Snel starten, Code ophalen voor het bewaken van mijn webpagina’s.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="e4a9d-131">Voeg het script in vlak vóór de `</head>`-tag op elke pagina die u wilt volgen. Als uw website een basispagina heeft, kunt u daar het script plaatsen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="e4a9d-132">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-132">For example:</span></span>

* <span data-ttu-id="e4a9d-133">In een ASP.NET-MVC-project plaatst u het in `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="e4a9d-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="e4a9d-134">Op een SharePoint-site opent u in het Configuratiescherm [Site-instellingen / basispagina](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="e4a9d-135">Het script bevat de instrumentatiesleutel die de gegevens naar uw Application Insights-resource stuurt.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="e4a9d-136">([Nadere uitleg over het script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="e4a9d-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="e4a9d-137">*(Als u een bekend webpaginaframework gebruikt, is het een goed idee om op zoek te gaan naar een geschikte Application Insights-adapter. Er is bijvoorbeeld een [AngularJS-module](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="e4a9d-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="e4a9d-138">Gedetailleerde configuratie</span><span class="sxs-lookup"><span data-stu-id="e4a9d-138">Detailed configuration</span></span>
<span data-ttu-id="e4a9d-139">U kunt diverse [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) instellen. In de meeste gevallen is dat echter niet nodig.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="e4a9d-140">U kunt bijvoorbeeld het aantal Ajax-aanroepen dat per paginaweergave wordt gerapporteerd beperken of deze rapportering uitschakelen (om verkeer te beperken).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="e4a9d-141">Of u kunt de foutopsporingsmodus zo instellen dat telemetrie snel via de pijplijn wordt verzameld zonder deze telemetrie in een batch op te nemen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="e4a9d-142">Voor het instellen van deze parameters zoekt u deze regel in het codefragment en voegt u hierna meer items toe, gescheiden door komma's:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="e4a9d-143">De [beschikbare parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) zijn:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="e4a9d-144"><a name="run"></a>Uw app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e4a9d-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="e4a9d-145">Voer uw web-app uit, gebruik deze een tijdje om telemetrie te genereren en wacht een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="e4a9d-146">U kunt de app zelf op uw ontwikkelcomputer uitvoeren met behulp van de **F5**-toets, maar u kunt de app ook publiceren en door gebruikers laten uitproberen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="e4a9d-147">Als u de telemetrie wilt controleren die door een web-app naar Application Insights wordt verzonden, gebruikt u de foutopsporingsprogramma's van de browser (in veel browsers opent u deze met **F12**).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="e4a9d-148">Gegevens worden verzonden naar dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="e4a9d-149">Gegevens over uw browserprestaties verkennen</span><span class="sxs-lookup"><span data-stu-id="e4a9d-149">Explore your browser performance data</span></span>
<span data-ttu-id="e4a9d-150">Open de blade Browsers om cumulatieve prestatiegegevens weer te geven van de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![Open de resource van uw app in portal.azure.com en klik op Instellingen, Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="e4a9d-152">*Zijn er nog geen gegevens? Klik boven aan de pagina op **Vernieuwen**. Ziet u nog steeds niets? Raadpleeg [Probleemoplossing](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="e4a9d-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="e4a9d-153">De blade Browser is een [Metrics Explorer-blade](app-insights-metrics-explorer.md) met vooraf ingestelde filters en grafiekselecties.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="e4a9d-154">U kunt het tijdbereik, de filters en configuratie van de grafiek bewerken, en desgewenst het resultaat als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="e4a9d-155">Klik op **Standaardwaarden herstellen** om de oorspronkelijke bladeconfiguratie terug te zetten.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="e4a9d-156">Laadprestaties van de pagina</span><span class="sxs-lookup"><span data-stu-id="e4a9d-156">Page load performance</span></span>
<span data-ttu-id="e4a9d-157">Bovenaan staat een grafieksegment met laadtijden van pagina’s.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="e4a9d-158">De totale hoogte van de grafiek geeft de gemiddelde tijd aan die nodig is voor het laden en weergeven van pagina's van uw app in de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="e4a9d-159">De tijd wordt gemeten vanaf het moment dat de browser de eerste HTTP-aanvraag verzendt tot het moment dat alle synchrone gebeurtenissen tijdens het laden zijn verwerkt, met inbegrip van indeling en uitgevoerde scripts.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="e4a9d-160">Asynchrone taken, zoals het laden van de webonderdelen van AJAX-aanroepen, zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="e4a9d-161">De grafiek segmenteert de totale laadtijd van de pagina in de [standaardtijdsinstellingen gedefinieerd door W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="e4a9d-162">De *netwerkverbindingstijd* is vaak lager dan u verwacht, omdat het een gemiddelde betreft op basis van alle aanvragen van de browser aan de server.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="e4a9d-163">Veel afzonderlijke aanvragen hebben een verbindingstijd van 0, omdat er al een actieve verbinding met de server bestaat.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="e4a9d-164">Worden pagina’s traag geladen?</span><span class="sxs-lookup"><span data-stu-id="e4a9d-164">Slow loading?</span></span>
<span data-ttu-id="e4a9d-165">Het traag laden van pagina is voor uw gebruikers een belangrijke bron van ergernis.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="e4a9d-166">Als de grafiek aangeeft dat pagina’s traag worden geladen, is het eenvoudig om wat diagnostisch onderzoek uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="e4a9d-167">De grafiek toont de gemiddelde paginalaadtijd in uw app.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="e4a9d-168">Als u wilt weten of het probleem zich beperkt tot bepaalde pagina's, kijkt u een stukje lager op de blade. Daar ziet u een raster dat gesegmenteerd is op pagina-URL:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="e4a9d-169">Let op het aantal paginaweergaven en de standaarddeviatie.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="e4a9d-170">Als het aantal pagina's zeer laag is, hebben gebruikers er niet veel last van.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="e4a9d-171">Een hoge standaarddeviatie (vergelijkbaar met het gemiddelde) geeft aan dat er grote verschillen bestaan tussen de afzonderlijke metingen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="e4a9d-172">**Zoom in op een URL en een paginaweergave.**</span><span class="sxs-lookup"><span data-stu-id="e4a9d-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="e4a9d-173">Klik op een paginanaam om een blade weer te geven met browsergrafieken die zijn gefilterd op die ene URL. Klik vervolgens op een exemplaar van een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="e4a9d-174">Klik op `...` voor een volledige lijst met eigenschappen voor de betreffende gebeurtenis of controleer de AJAX-aanroepen en gerelateerde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="e4a9d-175">Trage AJAX-aanroepen zijn van invloed op de algemene laadtijd van pagina’s als beide synchroon gebeuren.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="e4a9d-176">Gerelateerde gebeurtenissen omvatten serveraanvragen voor dezelfde URL (als u op uw webserver Application Insights hebt ingesteld).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="e4a9d-177">**Paginaprestaties over langere tijd.**</span><span class="sxs-lookup"><span data-stu-id="e4a9d-177">**Page performance over time.**</span></span> <span data-ttu-id="e4a9d-178">Wijzig op de blade Browsers het raster met paginalaadtijden in een lijndiagram om na te gaan of er op bepaalde tijden pieken waren:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Op de kop van het raster klikken en een nieuw grafiektype selecteren](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="e4a9d-180">**Segmenteer op andere dimensies.**</span><span class="sxs-lookup"><span data-stu-id="e4a9d-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="e4a9d-181">Mogelijk laden uw pagina's trager in een bepaalde browser, in een bepaald clientbesturingssysteem of op bepaalde gebruikerslocaties.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="e4a9d-182">Voeg een nieuwe grafiek toe en experimenteer met de dimensie **Groeperen op**.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="e4a9d-183">AJAX-prestaties</span><span class="sxs-lookup"><span data-stu-id="e4a9d-183">AJAX Performance</span></span>
<span data-ttu-id="e4a9d-184">Zorg ervoor dat eventuele AJAX-aanroepen op uw webpagina's goed worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="e4a9d-185">Ze worden vaak gebruikt voor het asynchroon vullen van onderdelen van uw pagina.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="e4a9d-186">Hoewel de algemene pagina waarschijnlijk onmiddellijk laadt, kunnen uw gebruikers zich gaan ergeren doordat ze steeds moeten wachten op ladende paginaonderdelen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="e4a9d-187">AJAX-oproepen vanuit uw webpagina worden op de blade Browsers weergegeven als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="e4a9d-188">In het bovenste gedeelte van de blade ziet u samenvattingsgrafieken:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="e4a9d-189">en verder naar beneden gedetailleerde rasters:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="e4a9d-190">Klik op een rij voor specifieke informatie.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="e4a9d-191">Als u het filter Browsers op de blade verwijdert, worden zowel de server als de AJAX-afhankelijkheden opgenomen in deze grafieken.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="e4a9d-192">Klik op Standaardwaarden herstellen om het filter opnieuw te configureren.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="e4a9d-193">**Als u wilt inzoomen op mislukte AJAX-aanroepen**, bladert u omlaag naar het raster met afhankelijkheidsfouten en klikt u vervolgens op een rij om specifieke exemplaren weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="e4a9d-194">Klik op `...` voor de volledige telemetrie voor een AJAX-aanroep.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="e4a9d-195">Zijn er geen AJAX-aanroepen gemeld?</span><span class="sxs-lookup"><span data-stu-id="e4a9d-195">No Ajax calls reported?</span></span>
<span data-ttu-id="e4a9d-196">AJAX-aanroepen zijn HTTP-/HTTPS-aanroepen vanuit het script van de webpagina.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="e4a9d-197">Als u constateert dat deze niet worden gerapporteerd, gaat u na of het codefragment niet de [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` of `maxAjaxCallsPerView` instelt.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="e4a9d-198">Browseruitzonderingen</span><span class="sxs-lookup"><span data-stu-id="e4a9d-198">Browser exceptions</span></span>
<span data-ttu-id="e4a9d-199">Op de blade Browsers ziet u een grafiek met samenvattingen van uitzonderingen en lager op de blade een raster met typen uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="e4a9d-200">Als u constateert dat er geen browseruitzonderingen worden gerapporteerd, gaat u na of het codefragment niet de [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking` instelt.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="e4a9d-201">De afzonderlijke paginaweergavegebeurtenissen inspecteren</span><span class="sxs-lookup"><span data-stu-id="e4a9d-201">Inspect individual page view events</span></span>

<span data-ttu-id="e4a9d-202">Meestal wordt telemetrie van paginaweergaven geanalyseerd door Application Insights en ziet u alleen cumulatieve rapporten, het gemiddelde van alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="e4a9d-203">Maar voor foutopsporing kunt u ook zoeken op afzonderlijke paginaweergavegebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="e4a9d-204">Stel op de blade Diagnostische gegevens doorzoeken de optie Filters in op Paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="e4a9d-205">Selecteer een gebeurtenis om deze gedetailleerder te bekijken.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-205">Select any event to see more detail.</span></span> <span data-ttu-id="e4a9d-206">Klik op de pagina met details op '...' om nog meer details weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="e4a9d-207">Als u [Zoeken](app-insights-diagnostic-search.md) gebruikt, zorg er dan voor dat u zoekt op volledige woorden. 'About' vindt u bijvoorbeeld niet met 'Abou' of met 'bout'.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="e4a9d-208">U kunt ook de krachtige [querytaal van Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) gebruiken om paginaweergaven te doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="e4a9d-209">Eigenschappen van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="e4a9d-209">Page view properties</span></span>
* <span data-ttu-id="e4a9d-210">**Duur van paginaweergave**</span><span class="sxs-lookup"><span data-stu-id="e4a9d-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="e4a9d-211">Standaard is dit de tijd voor het laden van de pagina, van clientverzoek tot het moment dat de pagina volledig is laden (inclusief hulpbestanden, maar uitgezonderd asynchrone taken zoals AJAX-aanroepen).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="e4a9d-212">Als u `overridePageViewDuration` instelt in de [paginaconfiguratie](#detailed-configuration), is de duur van de paginaweergave het interval tussen de clientaanvraag en het uitvoeren van de eerste `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="e4a9d-213">Als u trackPageView na de initialisatie van het script hebt verplaatst vanaf de normale positie, wordt er een andere waarde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="e4a9d-214">Als `overridePageViewDuration` is ingesteld en er een duurargument is opgegeven in de `trackPageView()`-aanroep, wordt in plaats daarvan de waarde van het argument gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="e4a9d-215">Aangepast telling van het aantal paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="e4a9d-215">Custom page counts</span></span>
<span data-ttu-id="e4a9d-216">Standaard wordt er een paginaweergave geteld telkens wanneer er in de clientbrowser een nieuwe pagina wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="e4a9d-217">Maar desgewenst kunt u ook aanvullende paginaweergaven tellen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-217">But you might want to count additional page views.</span></span> <span data-ttu-id="e4a9d-218">Op een pagina kan bijvoorbeeld de inhoud worden weergegeven in tabbladen en u wilt een paginaweergave tellen wanneer de gebruiker naar een ander tabblad gaat.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="e4a9d-219">Of JavaScript-code op de pagina laadt nieuwe inhoud zonder de browser-URL te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="e4a9d-220">Ga als volgt te werk om op het betreffende punt in uw clientcode een JavaScript-aanroep in te voegen:</span><span class="sxs-lookup"><span data-stu-id="e4a9d-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="e4a9d-221">De naam van de pagina mag dezelfde tekens als een URL bevatten, maar alles na '#' of '?' wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="e4a9d-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="e4a9d-222">Gebruik bijhouden</span><span class="sxs-lookup"><span data-stu-id="e4a9d-222">Usage tracking</span></span>
<span data-ttu-id="e4a9d-223">Wilt u weten wat gebruikers met uw app doen?</span><span class="sxs-lookup"><span data-stu-id="e4a9d-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="e4a9d-224">Meer informatie over het bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="e4a9d-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="e4a9d-225">[Meer informatie over de API voor aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e4a9d-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="e4a9d-226"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="e4a9d-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="e4a9d-227"><a name="next"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4a9d-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="e4a9d-228">Bijhouden van gebruik</span><span class="sxs-lookup"><span data-stu-id="e4a9d-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="e4a9d-229">Aangepaste gebeurtenissen en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="e4a9d-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="e4a9d-230">Bouwen-meten-leren</span><span class="sxs-lookup"><span data-stu-id="e4a9d-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

