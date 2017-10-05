---
title: Met de zoekfunctie in Azure Application Insights | Microsoft Docs
description: Zoeken en filteren onbewerkte telemetrie verzonden door uw web-app.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e2d12f807756b778a64920b12a66fba184a99844
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="009ac-103">Met behulp van zoeken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="009ac-103">Using Search in Application Insights</span></span>
<span data-ttu-id="009ac-104">Search is een functie van [Application Insights](app-insights-overview.md) waarmee u kunt vinden en verkennen afzonderlijke telemetrie-items, zoals uitzonderingen, paginaweergaven of web-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="009ac-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="009ac-105">En u kunt bekijken logboektraceringen en gebeurtenissen die u hebt gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="009ac-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="009ac-106">(Voor complexere query's over uw gegevens, gebruikt u [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="009ac-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="009ac-107">Waar ziet u zoeken?</span><span class="sxs-lookup"><span data-stu-id="009ac-107">Where do you see Search?</span></span>
### <a name="in-the-azure-portal"></a><span data-ttu-id="009ac-108">In de Azure portal</span><span class="sxs-lookup"><span data-stu-id="009ac-108">In the Azure portal</span></span>
<span data-ttu-id="009ac-109">U kunt diagnostische gegevens doorzoeken expliciet openen vanuit de Application Insights-overzichtsblade van uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="009ac-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span></span>

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="009ac-111">Ook wordt geopend wanneer u klikt op via bepaalde grafieken en raster artikelen.</span><span class="sxs-lookup"><span data-stu-id="009ac-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="009ac-112">In dit geval zijn de filters vooraf ingesteld te concentreren op het type item dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="009ac-112">In this case, its filters are pre-set to focus on the type of item you selected.</span></span> 

<span data-ttu-id="009ac-113">Bijvoorbeeld: op de overzichtsblade er is een staafdiagram van aanvragen die zijn geclassificeerd door reactietijd.</span><span class="sxs-lookup"><span data-stu-id="009ac-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="009ac-114">Klik op door een prestatiebereik voor een overzicht van afzonderlijke aanvragen in die periode antwoord:</span><span class="sxs-lookup"><span data-stu-id="009ac-114">Click through a performance range to see a list of individual requests in that response time range:</span></span>

![Klik in de aanvraag-prestaties](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="009ac-116">De hoofdtekst van Diagnostic Search is een lijst van telemetrie-items - serveraanvragen pagina weergaven en aangepaste gebeurtenissen die u hebt gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="009ac-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="009ac-117">Boven aan de lijst is een overzichtstabel weergegeven aantal gebeurtenissen gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="009ac-117">At the top of the list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="009ac-118">Klik op Vernieuwen om nieuwe gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="009ac-118">Click Refresh to get new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="009ac-119">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="009ac-119">In Visual Studio</span></span>

<span data-ttu-id="009ac-120">In Visual Studio is er ook een venster Application Insights zoeken.</span><span class="sxs-lookup"><span data-stu-id="009ac-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="009ac-121">Dit is vooral handig voor het weergeven van telemetriegebeurtenissen die worden gegenereerd door de toepassing die u fouten opspoort.</span><span class="sxs-lookup"><span data-stu-id="009ac-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span></span> <span data-ttu-id="009ac-122">Maar kan ook worden weergegeven waarop de gebeurtenissen verzameld van uw gepubliceerde app op de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="009ac-122">But it can also show the events collected from your published app at the Azure portal.</span></span>

<span data-ttu-id="009ac-123">Het venster zoeken openen in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="009ac-123">Open the Search window in Visual Studio:</span></span>

![Visual Studio Application Insights zoeken openen](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="009ac-125">Het venster zoeken bevat functies die vergelijkbaar is met de web-portal:</span><span class="sxs-lookup"><span data-stu-id="009ac-125">The Search window has features similar to the web portal:</span></span>

![Venster van Visual Studio Application Insights zoeken](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="009ac-127">Het tabblad bijhouden bewerking is alleen beschikbaar wanneer u een aanvraag of een paginaweergave opent.</span><span class="sxs-lookup"><span data-stu-id="009ac-127">The Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="009ac-128">Een ' bewerking ' is een reeks gebeurtenissen die is gekoppeld aan op een afzonderlijke weergave van de aanvraag of pagina.</span><span class="sxs-lookup"><span data-stu-id="009ac-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span></span> <span data-ttu-id="009ac-129">Bijvoorbeeld, afhankelijkheidsaanroepen, uitzonderingen, traceerlogboeken en aangepaste gebeurtenissen mogelijk deel uit van een enkele bewerking.</span><span class="sxs-lookup"><span data-stu-id="009ac-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="009ac-130">Het tabblad bijhouden bewerking worden grafisch weergegeven de timing en duur van deze gebeurtenissen ten opzichte van de weergave van de aanvraag of pagina.</span><span class="sxs-lookup"><span data-stu-id="009ac-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="009ac-131">Afzonderlijke items te inspecteren</span><span class="sxs-lookup"><span data-stu-id="009ac-131">Inspect individual items</span></span>
<span data-ttu-id="009ac-132">Selecteer een telemetrie-item voor een overzicht van de velden voor sleutels en verwante items.</span><span class="sxs-lookup"><span data-stu-id="009ac-132">Select any telemetry item to see key fields and related items.</span></span> <span data-ttu-id="009ac-133">Als u zien van de volledige set van velden wilt, klikt u op '...'.</span><span class="sxs-lookup"><span data-stu-id="009ac-133">If you want to see the full set of fields, click "...".</span></span> 

![Klik op Nieuw werkitem, de velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="009ac-135">Typen gebeurtenissen filteren</span><span class="sxs-lookup"><span data-stu-id="009ac-135">Filter event types</span></span>
<span data-ttu-id="009ac-136">Open de blade filteren en kiest u de typen gebeurtenissen die u wilt zien.</span><span class="sxs-lookup"><span data-stu-id="009ac-136">Open the Filter blade and choose the event types you want to see.</span></span> <span data-ttu-id="009ac-137">(Als u later herstellen van de filters waarmee u de blade geopend wilt, klikt u op opnieuw instellen.)</span><span class="sxs-lookup"><span data-stu-id="009ac-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span></span>

![Filter kiest en selecteert u de typen telemetrie](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="009ac-139">De gebeurtenistypen zijn:</span><span class="sxs-lookup"><span data-stu-id="009ac-139">The event types are:</span></span>

* <span data-ttu-id="009ac-140">**Tracering** - [diagnostische logboeken](app-insights-asp-net-trace-logs.md) inclusief TrackTrace, log4Net, NLog en System.Diagnostic.Trace aanroepen.</span><span class="sxs-lookup"><span data-stu-id="009ac-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="009ac-141">**Aanvraag** -HTTP-aanvragen ontvangen door de server-toepassing, met inbegrip van pagina's, scripts, afbeeldingen, Stijlbestanden en gegevens.</span><span class="sxs-lookup"><span data-stu-id="009ac-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="009ac-142">Deze gebeurtenissen worden gebruikt voor het maken van de aanvraag en antwoord overzichtsgrafieken.</span><span class="sxs-lookup"><span data-stu-id="009ac-142">These events are used to create the request and response overview charts.</span></span>
* <span data-ttu-id="009ac-143">**Paginaweergave** - [telemetrie verzonden door de webclient](app-insights-javascript.md)pagina view-rapporten maken die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="009ac-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span></span> 
* <span data-ttu-id="009ac-144">**Aangepaste gebeurtenis** : als u het aanroepen van TrackEvent() om ingevoegd [gebruik controleren](app-insights-api-custom-events-metrics.md), kunt u deze hier zoeken.</span><span class="sxs-lookup"><span data-stu-id="009ac-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="009ac-145">**Uitzondering** : niet-onderschepte [uitzonderingen in de server](app-insights-asp-net-exceptions.md), die u zich aanmeldt met TrackException() en.</span><span class="sxs-lookup"><span data-stu-id="009ac-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="009ac-146">**Afhankelijkheid** - [aanroepen vanuit de servertoepassing](app-insights-asp-net-dependencies.md) met andere services zoals REST-API's of databases en AJAX-aanroepen van uw [clientcode](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="009ac-147">**Beschikbaarheid** -resultaten van [beschikbaarheidstests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="009ac-148">Filteren op eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="009ac-148">Filter on property values</span></span>
<span data-ttu-id="009ac-149">Gebeurtenissen van de waarden van de eigenschappen kunt u filteren.</span><span class="sxs-lookup"><span data-stu-id="009ac-149">You can filter events on the values of their properties.</span></span> <span data-ttu-id="009ac-150">De beschikbare eigenschappen, is afhankelijk van de typen gebeurtenissen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="009ac-150">The available properties depend on the event types you selected.</span></span> 

<span data-ttu-id="009ac-151">Bijvoorbeeld aanvragen met een specifieke antwoordcode pikken.</span><span class="sxs-lookup"><span data-stu-id="009ac-151">For example, pick out requests with a specific response code.</span></span> 

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="009ac-153">Er zijn geen waarden van een bepaalde eigenschap kiezen heeft hetzelfde effect als het kiezen van alle waarden.</span><span class="sxs-lookup"><span data-stu-id="009ac-153">Choosing no values of a particular property has the same effect as choosing all values.</span></span> <span data-ttu-id="009ac-154">Het verandert filter voor die eigenschap uit.</span><span class="sxs-lookup"><span data-stu-id="009ac-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="009ac-155">Beperk uw zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="009ac-155">Narrow your search</span></span>
<span data-ttu-id="009ac-156">U ziet dat het aantal rechts van de filterwaarden hoeveel exemplaren er in de huidige set gefilterde worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="009ac-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span></span> 

<span data-ttu-id="009ac-157">In dit voorbeeld is duidelijk dat de 'rapportkoptekst/werknemers' resultaten in de meeste van de '500' fouten aanvragen:</span><span class="sxs-lookup"><span data-stu-id="009ac-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span></span>

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-the-same-property"></a><span data-ttu-id="009ac-159">Gebeurtenissen met dezelfde eigenschap vinden</span><span class="sxs-lookup"><span data-stu-id="009ac-159">Find events with the same property</span></span>
<span data-ttu-id="009ac-160">Alle items met dezelfde waarde voor de eigenschap zoeken:</span><span class="sxs-lookup"><span data-stu-id="009ac-160">Find all the items with the same property value:</span></span>

![Met de rechtermuisknop op een eigenschap](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-the-data"></a><span data-ttu-id="009ac-162">Gegevens op te zoeken</span><span class="sxs-lookup"><span data-stu-id="009ac-162">Search the data</span></span>

> [!NOTE]
> <span data-ttu-id="009ac-163">Voor het schrijven van complexe query's, open [ **Analytics** ](app-insights-analytics-tour.md) vanaf de bovenkant van de Search-blade.</span><span class="sxs-lookup"><span data-stu-id="009ac-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span></span>
> 

<span data-ttu-id="009ac-164">U kunt zoeken naar de voorwaarden in een van de eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="009ac-164">You can search for terms in any of the property values.</span></span> <span data-ttu-id="009ac-165">Dit is vooral handig als u hebt geschreven [aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md) met eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="009ac-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="009ac-166">Het is raadzaam een bereik, zoekopdrachten over een kortere bereik zijn sneller tijd in te stellen.</span><span class="sxs-lookup"><span data-stu-id="009ac-166">You might want to set a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="009ac-168">Zoeken naar volledige woorden, niet subtekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="009ac-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="009ac-169">Aanhalingstekens moet u speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="009ac-169">Use quotation marks to enclose special characters.</span></span>

| <span data-ttu-id="009ac-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="009ac-170">string</span></span> | <span data-ttu-id="009ac-171">is *niet* gevonden door</span><span class="sxs-lookup"><span data-stu-id="009ac-171">is *not* found by</span></span> | <span data-ttu-id="009ac-172">maar deze worden gevonden</span><span class="sxs-lookup"><span data-stu-id="009ac-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="009ac-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="009ac-173">HomeController.About</span></span> |<span data-ttu-id="009ac-174">thuis</span><span class="sxs-lookup"><span data-stu-id="009ac-174">home</span></span><br/><span data-ttu-id="009ac-175">Domeincontroller</span><span class="sxs-lookup"><span data-stu-id="009ac-175">controller</span></span><br/><span data-ttu-id="009ac-176">out</span><span class="sxs-lookup"><span data-stu-id="009ac-176">out</span></span> | <span data-ttu-id="009ac-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="009ac-177">homecontroller</span></span><br/><span data-ttu-id="009ac-178">over</span><span class="sxs-lookup"><span data-stu-id="009ac-178">about</span></span><br/><span data-ttu-id="009ac-179">'homecontroller.about'</span><span class="sxs-lookup"><span data-stu-id="009ac-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="009ac-180">Verenigde Staten</span><span class="sxs-lookup"><span data-stu-id="009ac-180">United States</span></span>|<span data-ttu-id="009ac-181">UNI</span><span class="sxs-lookup"><span data-stu-id="009ac-181">Uni</span></span><br/><span data-ttu-id="009ac-182">Ted</span><span class="sxs-lookup"><span data-stu-id="009ac-182">ted</span></span>|<span data-ttu-id="009ac-183">Verenigd</span><span class="sxs-lookup"><span data-stu-id="009ac-183">united</span></span><br/><span data-ttu-id="009ac-184">statussen</span><span class="sxs-lookup"><span data-stu-id="009ac-184">states</span></span><br/><span data-ttu-id="009ac-185">Verenigde Staten en</span><span class="sxs-lookup"><span data-stu-id="009ac-185">united AND states</span></span><br/><span data-ttu-id="009ac-186">'Verenigde Staten'</span><span class="sxs-lookup"><span data-stu-id="009ac-186">"united states"</span></span>

<span data-ttu-id="009ac-187">Hier volgen de search-expressies die u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="009ac-187">Here are the search expressions you can use:</span></span>

| <span data-ttu-id="009ac-188">Voorbeeldquery</span><span class="sxs-lookup"><span data-stu-id="009ac-188">Sample query</span></span> | <span data-ttu-id="009ac-189">Effect</span><span class="sxs-lookup"><span data-stu-id="009ac-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="009ac-190">Alle gebeurtenissen in het tijdsbereik waarvan de velden het woord "apple bevatten" zoeken</span><span class="sxs-lookup"><span data-stu-id="009ac-190">Find all events in the time range whose fields include the word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="009ac-191">Zoeken naar gebeurtenissen die beide woorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="009ac-191">Find events that contain both words.</span></span> <span data-ttu-id="009ac-192">Gebruik kapitaal 'en', niet 'en'.</span><span class="sxs-lookup"><span data-stu-id="009ac-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="009ac-193">Gebeurtenissen die beide woord bevatten zoeken.</span><span class="sxs-lookup"><span data-stu-id="009ac-193">Find events that contain either word.</span></span> <span data-ttu-id="009ac-194">Gebruik 'Of', niet "of".</span><span class="sxs-lookup"><span data-stu-id="009ac-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="009ac-195">Korte vorm.</span><span class="sxs-lookup"><span data-stu-id="009ac-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="009ac-196">Gebeurtenissen die bevatten van één woord en niet op andere zoeken.</span><span class="sxs-lookup"><span data-stu-id="009ac-196">Find events that contain one word but not the other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="009ac-197">Steekproeven</span><span class="sxs-lookup"><span data-stu-id="009ac-197">Sampling</span></span>
<span data-ttu-id="009ac-198">Als uw app veel telemetrie genereert (en u gebruikt de ASP.NET-SDK-versie 2.0.0-beta3 of hoger), de module adaptieve steekproeven beperkt automatisch het volume dat wordt verzonden naar de portal door te sturen alleen een representatieve fractie van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="009ac-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="009ac-199">Gebeurtenissen die betrekking op dezelfde aanvraag hebben kunnen echter zijn geselecteerd of gedeselecteerd als groep, zodat u tussen gerelateerde gebeurtenissen kunt navigeren.</span><span class="sxs-lookup"><span data-stu-id="009ac-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="009ac-200">[Meer informatie over steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="009ac-201">Werkitem maken</span><span class="sxs-lookup"><span data-stu-id="009ac-201">Create work item</span></span>
<span data-ttu-id="009ac-202">U kunt een bug in GitHub of Visual Studio Team Services maken met de details van elk telemetrie-item.</span><span class="sxs-lookup"><span data-stu-id="009ac-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span></span> 

![Klik op Nieuw werkitem, de velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="009ac-204">De eerste keer dat u dit doet, wordt u gevraagd een koppeling naar uw Team Services-account en het project te configureren.</span><span class="sxs-lookup"><span data-stu-id="009ac-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span></span>

![Vult u de URL van uw Team Services-server en de naam van het Project en klik op autoriseren](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="009ac-206">(U kunt ook de koppeling configureren op de blade werkitems.)</span><span class="sxs-lookup"><span data-stu-id="009ac-206">(You can also configure the link on the Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="009ac-207">Uw zoekopdracht opslaan</span><span class="sxs-lookup"><span data-stu-id="009ac-207">Save your search</span></span>
<span data-ttu-id="009ac-208">Als u de gewenste filters hebt ingesteld, kunt u de zoekopdracht als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="009ac-208">When you've set all the filters you want, you can save the search as a favorite.</span></span> <span data-ttu-id="009ac-209">Als u in een organisatie-account werkt, kunt u kiezen of u wilt delen met andere teamleden.</span><span class="sxs-lookup"><span data-stu-id="009ac-209">If you work in an organizational account, you can choose whether to share it with other team members.</span></span>

![Klik op favoriet, instellen van de naam en klik op Opslaan](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="009ac-211">Om te zien van de zoekopdracht opnieuw **gaat u naar de overzichtsblade** en Favorieten openen:</span><span class="sxs-lookup"><span data-stu-id="009ac-211">To see the search again, **go to the overview blade** and open Favorites:</span></span>

![Tegel Favorieten](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="009ac-213">Als u met relatief tijdsbereik opgeslagen, heeft de heropend blade de meest recente gegevens.</span><span class="sxs-lookup"><span data-stu-id="009ac-213">If you saved with Relative time range, the re-opened blade has the latest data.</span></span> <span data-ttu-id="009ac-214">Als u met absoluut tijdsbereik opgeslagen, ziet u dezelfde gegevens elke keer.</span><span class="sxs-lookup"><span data-stu-id="009ac-214">If you saved with Absolute time range, you see the same data every time.</span></span> <span data-ttu-id="009ac-215">(Als 'Relatieve' niet beschikbaar wanneer u wilt een favoriet opslaan, tijdsbereik in de header op en een periode op die een aangepast bereik niet instellen.)</span><span class="sxs-lookup"><span data-stu-id="009ac-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-to-application-insights"></a><span data-ttu-id="009ac-216">Meer telemetrie verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="009ac-216">Send more telemetry to Application Insights</span></span>
<span data-ttu-id="009ac-217">Naast de out-of-the-box-telemetrie verzonden door de Application Insights-SDK, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="009ac-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="009ac-218">Logboektraceringen van uw favoriete framework voor logboekregistratie in vastleggen [.NET](app-insights-asp-net-trace-logs.md) of [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="009ac-219">Dit betekent dat u kunt uw logboektraceringen doorzoeken en ze te correleren met paginaweergaven, uitzonderingen en andere gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="009ac-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="009ac-220">[Schrijven van code](app-insights-api-custom-events-metrics.md) om aangepaste gebeurtenissen, paginaweergaven en uitzonderingen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="009ac-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="009ac-221">[Ontdek hoe logboeken en aangepaste telemetrie verzendt naar Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="009ac-222"><a name="questions"></a>MET Q & A</span><span class="sxs-lookup"><span data-stu-id="009ac-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="009ac-223"><a name="limits"></a>Hoeveel gegevens behouden blijven?</span><span class="sxs-lookup"><span data-stu-id="009ac-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="009ac-224">Zie de [limieten samenvatting](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="009ac-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="009ac-225">Hoe kan ik postgegevens zien in mijn serveraanvragen?</span><span class="sxs-lookup"><span data-stu-id="009ac-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="009ac-226">Er wordt de POST-gegevens niet automatisch geregistreerd, maar u kunt [TrackTrace of logboek aanroepen](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="009ac-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="009ac-227">Plaats de POST-gegevens in de bericht-parameter.</span><span class="sxs-lookup"><span data-stu-id="009ac-227">Put the POST data in the message parameter.</span></span> <span data-ttu-id="009ac-228">U kunt niet filteren op het bericht op dezelfde manier die u op Eigenschappen filteren kunt, maar de maximale grootte is langer.</span><span class="sxs-lookup"><span data-stu-id="009ac-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="009ac-229">Video</span><span class="sxs-lookup"><span data-stu-id="009ac-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="009ac-230"><a name="add"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="009ac-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="009ac-231">Schrijven van complexe query's in Analytics</span><span class="sxs-lookup"><span data-stu-id="009ac-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="009ac-232">Logboeken en aangepaste telemetrie verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="009ac-232">Send logs and custom telemetry to Application Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="009ac-233">Beschikbaarheid en reactiesnelheid tests instellen</span><span class="sxs-lookup"><span data-stu-id="009ac-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="009ac-234">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="009ac-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
