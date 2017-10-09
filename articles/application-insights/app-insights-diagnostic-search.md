---
title: aaaUsing zoeken in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="ca2b0-103">Met behulp van zoeken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="ca2b0-103">Using Search in Application Insights</span></span>
<span data-ttu-id="ca2b0-104">Search is een functie van [Application Insights](app-insights-overview.md) gebruiken toofind en verkennen afzonderlijke telemetrie-items, zoals uitzonderingen, paginaweergaven of web-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="ca2b0-105">En u kunt bekijken logboektraceringen en gebeurtenissen die u hebt gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="ca2b0-106">(Voor complexere query's over uw gegevens, gebruikt u [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="ca2b0-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="ca2b0-107">Waar ziet u zoeken?</span><span class="sxs-lookup"><span data-stu-id="ca2b0-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="ca2b0-108">In hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ca2b0-108">In hello Azure portal</span></span>
<span data-ttu-id="ca2b0-109">U kunt diagnostische gegevens doorzoeken expliciet openen vanuit Hallo Application Insights overzichtsblade van uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="ca2b0-111">Ook wordt geopend wanneer u klikt op via bepaalde grafieken en raster artikelen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="ca2b0-112">De filters zijn in dit geval vooraf toofocus ingesteld op Hallo type item dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="ca2b0-113">Bijvoorbeeld: op de overzichtsblade hello, er is een staafdiagram van aanvragen die zijn geclassificeerd door reactietijd.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="ca2b0-114">Klik op via een bereik prestaties toosee een lijst met afzonderlijke aanvragen in dat bereik responstijd:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Klik in de aanvraag-prestaties](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="ca2b0-116">Hallo-hoofdtekst van Diagnostic Search is een lijst van telemetrie-items - serveraanvragen pagina weergaven en aangepaste gebeurtenissen die u hebt gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="ca2b0-117">Boven aan de lijst Hallo is Hallo een overzichtstabel weergegeven aantal gebeurtenissen gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="ca2b0-118">Klik op Vernieuwen tooget nieuwe gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="ca2b0-119">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca2b0-119">In Visual Studio</span></span>

<span data-ttu-id="ca2b0-120">In Visual Studio is er ook een venster Application Insights zoeken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="ca2b0-121">Dit is vooral handig voor het weergeven van telemetriegebeurtenissen die worden gegenereerd door Hallo-toepassing die u fouten opspoort.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="ca2b0-122">Maar Hallo gebeurtenissen verzameld van uw gepubliceerde app op Hallo Azure-portal ook kan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="ca2b0-123">Hallo zoekvenster openen in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-123">Open hello Search window in Visual Studio:</span></span>

![Visual Studio Application Insights zoeken openen](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="ca2b0-125">Hallo zoekvenster heeft functies vergelijkbare toohello web-portal:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-125">hello Search window has features similar toohello web portal:</span></span>

![Venster van Visual Studio Application Insights zoeken](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="ca2b0-127">Hallo bijhouden bewerking tabblad is beschikbaar wanneer u een aanvraag of een paginaweergave opent.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="ca2b0-128">Een ' bewerking ' is een reeks gebeurtenissen die is gekoppeld aan tooa één pagina of de aanvraag voor weergave.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="ca2b0-129">Bijvoorbeeld, afhankelijkheidsaanroepen, uitzonderingen, traceerlogboeken en aangepaste gebeurtenissen mogelijk deel uit van een enkele bewerking.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="ca2b0-130">Hallo bijhouden bewerking tabblad toont Hallo grafisch timing en duur van deze gebeurtenissen in de relatie toohello aanvraag of pagina.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="ca2b0-131">Afzonderlijke items te inspecteren</span><span class="sxs-lookup"><span data-stu-id="ca2b0-131">Inspect individual items</span></span>
<span data-ttu-id="ca2b0-132">Selecteer alle telemetrie-item toosee sleutelvelden en verwante items.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="ca2b0-133">Als u wilt dat toosee Hallo volledige set van velden, klikt u op '...'.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Klik op Nieuw werkitem, Hallo-velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="ca2b0-135">Typen gebeurtenissen filteren</span><span class="sxs-lookup"><span data-stu-id="ca2b0-135">Filter event types</span></span>
<span data-ttu-id="ca2b0-136">Open de blade filteren Hallo en kies Hallo gebeurtenis typt u toosee wilt.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="ca2b0-137">(Als u later toorestore Hallo filters waarmee u Hallo blade geopend wilt, klikt u op opnieuw instellen.)</span><span class="sxs-lookup"><span data-stu-id="ca2b0-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Filter kiest en selecteert u de typen telemetrie](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="ca2b0-139">Hallo gebeurtenistypen zijn:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-139">hello event types are:</span></span>

* <span data-ttu-id="ca2b0-140">**Tracering** - [diagnostische logboeken](app-insights-asp-net-trace-logs.md) inclusief TrackTrace, log4Net, NLog en System.Diagnostic.Trace aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="ca2b0-141">**Aanvraag** -HTTP-aanvragen ontvangen door de server-toepassing, met inbegrip van pagina's, scripts, afbeeldingen, Stijlbestanden en gegevens.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="ca2b0-142">Deze gebeurtenissen zijn gebruikte toocreate Hallo aanvraag en -antwoord overzichtsgrafieken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="ca2b0-143">**Paginaweergave** - [telemetrie verzonden door de webclient Hallo](app-insights-javascript.md), toocreate pagina view-rapporten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="ca2b0-144">**Aangepaste gebeurtenis** : als u aanroepen tooTrackEvent() ingevoegd in de volgorde te[gebruik controleren](app-insights-api-custom-events-metrics.md), kunt u deze hier zoeken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="ca2b0-145">**Uitzondering** : niet-onderschepte [uitzonderingen in Hallo server](app-insights-asp-net-exceptions.md), die u zich aanmeldt met TrackException() en.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="ca2b0-146">**Afhankelijkheid** - [aanroepen vanuit de servertoepassing](app-insights-asp-net-dependencies.md) tooother services zoals databases of REST-API's en AJAX-aanroepen vanuit uw [clientcode](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="ca2b0-147">**Beschikbaarheid** -resultaten van [beschikbaarheidstests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="ca2b0-148">Filteren op eigenschapswaarden</span><span class="sxs-lookup"><span data-stu-id="ca2b0-148">Filter on property values</span></span>
<span data-ttu-id="ca2b0-149">U kunt gebeurtenissen op Hallo waarden van de eigenschappen op te filteren.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="ca2b0-150">Hallo beschikbare eigenschappen, is afhankelijk van Hallo-gebeurtenistypen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="ca2b0-151">Bijvoorbeeld aanvragen met een specifieke antwoordcode pikken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-151">For example, pick out requests with a specific response code.</span></span> 

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="ca2b0-153">Er zijn geen waarden van een bepaalde eigenschap kiezen heeft Hallo hetzelfde effect als het kiezen van alle waarden.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="ca2b0-154">Het verandert filter voor die eigenschap uit.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="ca2b0-155">Beperk uw zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="ca2b0-155">Narrow your search</span></span>
<span data-ttu-id="ca2b0-156">Kennisgeving die Hallo telt toohello rechts van de filterwaarden Hallo weergeven hoeveel exemplaren er in de huidige gefilterde set Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="ca2b0-157">In dit voorbeeld is het wissen dat die Hallo rapportkoptekst/werknemers aanvraag resulteert in de meeste Hallo '500'-fouten:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="ca2b0-159">Zoeken naar gebeurtenissen met de Hallo dezelfde eigenschap</span><span class="sxs-lookup"><span data-stu-id="ca2b0-159">Find events with hello same property</span></span>
<span data-ttu-id="ca2b0-160">Zoeken naar alle Hallo items Hallo dezelfde waarde van eigenschap:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-160">Find all hello items with hello same property value:</span></span>

![Met de rechtermuisknop op een eigenschap](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="ca2b0-162">Hallo zoekgegevens</span><span class="sxs-lookup"><span data-stu-id="ca2b0-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="ca2b0-163">toowrite meer complexe query's, open [ **Analytics** ](app-insights-analytics-tour.md) vanaf de bovenkant Hallo van Hallo Search-blade.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="ca2b0-164">U kunt voorwaarden in een van de eigenschapswaarden Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="ca2b0-165">Dit is vooral handig als u hebt geschreven [aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md) met eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="ca2b0-166">U kunt een tijdsbereik als zoekopdrachten via een korter bereik zijn sneller tooset.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="ca2b0-168">Zoeken naar volledige woorden, niet subtekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="ca2b0-169">Aanhalingstekens tooenclose speciale tekens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="ca2b0-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ca2b0-170">string</span></span> | <span data-ttu-id="ca2b0-171">is *niet* gevonden door</span><span class="sxs-lookup"><span data-stu-id="ca2b0-171">is *not* found by</span></span> | <span data-ttu-id="ca2b0-172">maar deze worden gevonden</span><span class="sxs-lookup"><span data-stu-id="ca2b0-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca2b0-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="ca2b0-173">HomeController.About</span></span> |<span data-ttu-id="ca2b0-174">thuis</span><span class="sxs-lookup"><span data-stu-id="ca2b0-174">home</span></span><br/><span data-ttu-id="ca2b0-175">Domeincontroller</span><span class="sxs-lookup"><span data-stu-id="ca2b0-175">controller</span></span><br/><span data-ttu-id="ca2b0-176">out</span><span class="sxs-lookup"><span data-stu-id="ca2b0-176">out</span></span> | <span data-ttu-id="ca2b0-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="ca2b0-177">homecontroller</span></span><br/><span data-ttu-id="ca2b0-178">over</span><span class="sxs-lookup"><span data-stu-id="ca2b0-178">about</span></span><br/><span data-ttu-id="ca2b0-179">'homecontroller.about'</span><span class="sxs-lookup"><span data-stu-id="ca2b0-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="ca2b0-180">Verenigde Staten</span><span class="sxs-lookup"><span data-stu-id="ca2b0-180">United States</span></span>|<span data-ttu-id="ca2b0-181">UNI</span><span class="sxs-lookup"><span data-stu-id="ca2b0-181">Uni</span></span><br/><span data-ttu-id="ca2b0-182">Ted</span><span class="sxs-lookup"><span data-stu-id="ca2b0-182">ted</span></span>|<span data-ttu-id="ca2b0-183">Verenigd</span><span class="sxs-lookup"><span data-stu-id="ca2b0-183">united</span></span><br/><span data-ttu-id="ca2b0-184">statussen</span><span class="sxs-lookup"><span data-stu-id="ca2b0-184">states</span></span><br/><span data-ttu-id="ca2b0-185">Verenigde Staten en</span><span class="sxs-lookup"><span data-stu-id="ca2b0-185">united AND states</span></span><br/><span data-ttu-id="ca2b0-186">'Verenigde Staten'</span><span class="sxs-lookup"><span data-stu-id="ca2b0-186">"united states"</span></span>

<span data-ttu-id="ca2b0-187">Hier volgen Hallo zoeken expressies die u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="ca2b0-188">Voorbeeldquery</span><span class="sxs-lookup"><span data-stu-id="ca2b0-188">Sample query</span></span> | <span data-ttu-id="ca2b0-189">Effect</span><span class="sxs-lookup"><span data-stu-id="ca2b0-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="ca2b0-190">Alle gebeurtenissen in Hallo tijdsbereik waarvan de velden Hallo-word "apple bevatten" zoeken</span><span class="sxs-lookup"><span data-stu-id="ca2b0-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="ca2b0-191">Zoeken naar gebeurtenissen die beide woorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-191">Find events that contain both words.</span></span> <span data-ttu-id="ca2b0-192">Gebruik kapitaal 'en', niet 'en'.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="ca2b0-193">Gebeurtenissen die beide woord bevatten zoeken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-193">Find events that contain either word.</span></span> <span data-ttu-id="ca2b0-194">Gebruik 'Of', niet "of".</span><span class="sxs-lookup"><span data-stu-id="ca2b0-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="ca2b0-195">Korte vorm.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="ca2b0-196">Gebeurtenissen die bevatten van één woord, maar niet Hallo andere zoeken.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="ca2b0-197">Steekproeven</span><span class="sxs-lookup"><span data-stu-id="ca2b0-197">Sampling</span></span>
<span data-ttu-id="ca2b0-198">Als uw app veel telemetrie genereert (en u Hallo ASP.NET-SDK-versie 2.0.0-beta3 of hoger), Hallo adaptieve steekproeven module vermindert automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="ca2b0-199">Gebeurtenissen die zijn echter gerelateerde toohello dezelfde aanvraag zijn geselecteerd of gedeselecteerd als groep, zodat u tussen gerelateerde gebeurtenissen kunt navigeren.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="ca2b0-200">[Meer informatie over steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="ca2b0-201">Werkitem maken</span><span class="sxs-lookup"><span data-stu-id="ca2b0-201">Create work item</span></span>
<span data-ttu-id="ca2b0-202">U kunt een bug in GitHub of Visual Studio Team Services maken met de Hallo details van elk telemetrie-item.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Klik op Nieuw werkitem, Hallo-velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="ca2b0-204">Hallo eerste keer dat u dit doet, tooconfigure wordt u gevraagd een koppeling tooyour Team Services-account en project.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Hallo-URL van uw Team Services-server en de naam van het Project Hallo vullen en op autoriseren](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="ca2b0-206">(U kunt ook Hallo-koppeling configureren op Hallo werkitems blade.)</span><span class="sxs-lookup"><span data-stu-id="ca2b0-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="ca2b0-207">Uw zoekopdracht opslaan</span><span class="sxs-lookup"><span data-stu-id="ca2b0-207">Save your search</span></span>
<span data-ttu-id="ca2b0-208">Als u alle gewenste Hallo filters hebt ingesteld, kunt u Hallo zoeken als favoriet opslaan.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="ca2b0-209">Als u in een organisatie-account werkt, kunt u kiezen of tooshare met andere teamleden.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Klik op de favoriet en klik op Opslaan Hallo naam instellen](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="ca2b0-211">toosee hello zoeken opnieuw **Ga toohello overzichtsblade** en Favorieten openen:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Tegel Favorieten](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="ca2b0-213">Als u met relatief tijdsbereik opgeslagen, is heropend blade Hallo Hallo meest recente gegevens.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="ca2b0-214">Als u met absoluut tijdsbereik opgeslagen, ziet u Hallo dezelfde gegevens elke keer.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="ca2b0-215">(Als 'Relatieve' niet beschikbaar als u wilt dat een favoriet toosave, tijdsbereik in Hallo-header op en een periode op die een aangepast bereik niet instellen.)</span><span class="sxs-lookup"><span data-stu-id="ca2b0-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="ca2b0-216">Meer telemetrie tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="ca2b0-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="ca2b0-217">In toevoeging toohello out-of-the-box-telemetrie is verzonden door de Application Insights-SDK, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ca2b0-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="ca2b0-218">Logboektraceringen van uw favoriete framework voor logboekregistratie in vastleggen [.NET](app-insights-asp-net-trace-logs.md) of [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="ca2b0-219">Dit betekent dat u kunt uw logboektraceringen doorzoeken en ze te correleren met paginaweergaven, uitzonderingen en andere gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="ca2b0-220">[Schrijven van code](app-insights-api-custom-events-metrics.md) toosend aangepaste gebeurtenissen, paginaweergaven en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="ca2b0-221">[Meer informatie over hoe toosend registreert en aangepaste telemetrie tooApplication Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="ca2b0-222"><a name="questions"></a>MET Q & A</span><span class="sxs-lookup"><span data-stu-id="ca2b0-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="ca2b0-223"><a name="limits"></a>Hoeveel gegevens behouden blijven?</span><span class="sxs-lookup"><span data-stu-id="ca2b0-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="ca2b0-224">Zie Hallo [limieten samenvatting](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="ca2b0-225">Hoe kan ik postgegevens zien in mijn serveraanvragen?</span><span class="sxs-lookup"><span data-stu-id="ca2b0-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="ca2b0-226">Er geen Hallo postgegevens automatisch wordt geregistreerd, maar u kunt [TrackTrace of logboek aanroepen](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b0-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="ca2b0-227">Hallo postgegevens in Hallo-bericht parameter geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="ca2b0-228">U kunt niet filteren op het Hallo-bericht in Hallo dezelfde manier kunt u filteren op eigenschappen, maar de maximale grootte Hallo is langer.</span><span class="sxs-lookup"><span data-stu-id="ca2b0-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="ca2b0-229">Video</span><span class="sxs-lookup"><span data-stu-id="ca2b0-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="ca2b0-230"><a name="add"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca2b0-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="ca2b0-231">Schrijven van complexe query's in Analytics</span><span class="sxs-lookup"><span data-stu-id="ca2b0-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="ca2b0-232">Logboeken en aangepaste telemetrie tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="ca2b0-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="ca2b0-233">Beschikbaarheid en reactiesnelheid tests instellen</span><span class="sxs-lookup"><span data-stu-id="ca2b0-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="ca2b0-234">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ca2b0-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
