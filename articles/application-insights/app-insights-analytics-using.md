---
title: aaaUsing Analytics - Hallo krachtige zoekfunctie van Azure Application Insights | Microsoft Docs
description: 'Met behulp van Hallo Analytics, Hallo diagnostische gegevens doorzoeken krachtige hulpprogramma van Application Insights. '
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="b4330-103">Door middel van analyses in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b4330-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="b4330-104">[Analytics](app-insights-analytics.md) is Hallo krachtige zoekfunctie van [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4330-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b4330-105">Deze pagina's worden de Log Analytics query language beschreven.</span><span class="sxs-lookup"><span data-stu-id="b4330-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="b4330-106">**[Hallo inleidende video bekijken](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="b4330-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="b4330-107">**[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet nog gegevens tooApplication Insights verzendt.</span><span class="sxs-lookup"><span data-stu-id="b4330-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="b4330-108">Open Analytics</span><span class="sxs-lookup"><span data-stu-id="b4330-108">Open Analytics</span></span>
<span data-ttu-id="b4330-109">Klik op Analytics van uw app thuis resource in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4330-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="b4330-111">Hallo inline-zelfstudie hebt u enkele ideeën over wat u kunt doen.</span><span class="sxs-lookup"><span data-stu-id="b4330-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="b4330-112">Er is een [hier uitgebreider rondleiding](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="b4330-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="b4330-113">Uw telemetrie query</span><span class="sxs-lookup"><span data-stu-id="b4330-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="b4330-114">Een query schrijven</span><span class="sxs-lookup"><span data-stu-id="b4330-114">Write a query</span></span>
![Schema weergeven](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="b4330-116">Beginnen met de namen van elk van de vermelde aan de linkerkant Hallo Hallo-tabellen hello (of Hallo [bereik](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) of [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span><span class="sxs-lookup"><span data-stu-id="b4330-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="b4330-117">Gebruik `|` toocreate een pijplijn met [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="b4330-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="b4330-118">IntelliSense vraagt u met de Hallo operators en Hallo expressie-elementen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4330-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="b4330-119">Klik op het informatiepictogram hello (of druk op CTRL + SPATIEBALK) tooget een langere beschrijving en voorbeelden van hoe toouse elk element.</span><span class="sxs-lookup"><span data-stu-id="b4330-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="b4330-120">Zie Hallo [Analytics taal rondleiding](app-insights-analytics-tour.md) en [taalreferentie](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b4330-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="b4330-121">Een query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b4330-121">Run a query</span></span>
![Een query uit te voeren](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="b4330-123">U kunt één regeleinden gebruiken in een query.</span><span class="sxs-lookup"><span data-stu-id="b4330-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="b4330-124">Plaats de cursor Hallo binnen of aan Hallo einde van de gewenste toorun Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="b4330-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="b4330-125">Controleer de tijdsbereik Hallo van uw query.</span><span class="sxs-lookup"><span data-stu-id="b4330-125">Check hello time range of your query.</span></span> <span data-ttu-id="b4330-126">(U kunt deze wijzigen of deze door uw eigen overschrijven [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) -component in uw query.)</span><span class="sxs-lookup"><span data-stu-id="b4330-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="b4330-127">Klik op Go toorun Hallo query.</span><span class="sxs-lookup"><span data-stu-id="b4330-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="b4330-128">Lege regels niet in uw query worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b4330-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="b4330-129">U kunt meerdere gescheiden query's in één query tabblad houden door deze te scheiden met een lege regels.</span><span class="sxs-lookup"><span data-stu-id="b4330-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="b4330-130">Alleen Hallo query's met de Hallo cursor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4330-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="b4330-131">Een query opslaan</span><span class="sxs-lookup"><span data-stu-id="b4330-131">Save a query</span></span>
![Opslaan van een query](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="b4330-133">Hallo huidige query-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="b4330-133">Save hello current query file.</span></span>
2. <span data-ttu-id="b4330-134">Open een opgeslagen query-bestand.</span><span class="sxs-lookup"><span data-stu-id="b4330-134">Open a saved query file.</span></span>
3. <span data-ttu-id="b4330-135">Maak een nieuwe querybestand.</span><span class="sxs-lookup"><span data-stu-id="b4330-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="b4330-136">Zie Hallo-details</span><span class="sxs-lookup"><span data-stu-id="b4330-136">See hello details</span></span>
<span data-ttu-id="b4330-137">De volledige lijst met eigenschappen voor elke rij in Hallo resultaten toosee uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="b4330-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="b4330-138">U kunt verder uitbreiden in elke eigenschap die is bijvoorbeeld een gestructureerde waarde -, aangepaste dimensies of Hallo stack aanbieding in een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="b4330-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Vouw een rij](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="b4330-140">Hallo resultaten ordenen</span><span class="sxs-lookup"><span data-stu-id="b4330-140">Arrange hello results</span></span>
<span data-ttu-id="b4330-141">U kunt sorteren, filteren, pagineren en groep Hallo resultaten van uw query.</span><span class="sxs-lookup"><span data-stu-id="b4330-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="b4330-142">Sorteren, groeperen en filteren in de browser Hallo niet Voer de query opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="b4330-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="b4330-143">Ze alleen Hallo resultaten die zijn geretourneerd door de laatste query opnieuw te rangschikken.</span><span class="sxs-lookup"><span data-stu-id="b4330-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="b4330-144">tooperform deze taken in het Hallo-server voordat Hallo resultaten worden geretourneerd, schrijft u uw query met Hallo [sorteren](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [samenvatten](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) en [waar](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span><span class="sxs-lookup"><span data-stu-id="b4330-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="b4330-145">Hallo-kolommen die u wilt kiezen zoals toosee, sleept u kolom headers toorearrange en formaat kolommen te slepen.</span><span class="sxs-lookup"><span data-stu-id="b4330-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Kolommen rangschikken](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="b4330-147">Items sorteren en filteren</span><span class="sxs-lookup"><span data-stu-id="b4330-147">Sort and filter items</span></span>
<span data-ttu-id="b4330-148">Uw resultaten sorteren door te klikken op Hallo hoofd van een kolom.</span><span class="sxs-lookup"><span data-stu-id="b4330-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="b4330-149">Klik opnieuw toosort Hallo andere manier en klikt u op een derde keer toorevert toohello oorspronkelijke ordening geretourneerd door de query.</span><span class="sxs-lookup"><span data-stu-id="b4330-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="b4330-150">Gebruik Hallo pictogram toonarrow uw zoekopdracht filteren.</span><span class="sxs-lookup"><span data-stu-id="b4330-150">Use hello filter icon toonarrow your search.</span></span>

![Kolommen sorteren en filteren](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="b4330-152">Items groeperen</span><span class="sxs-lookup"><span data-stu-id="b4330-152">Group items</span></span>
<span data-ttu-id="b4330-153">toosort groeperen door meer dan een kolom te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4330-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="b4330-154">Deze eerst inschakelen en sleep de kolomkoppen in Hallo ruimte boven Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b4330-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Groep](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="b4330-156">Ontbreken er bepaalde resultaten?</span><span class="sxs-lookup"><span data-stu-id="b4330-156">Missing some results?</span></span>

<span data-ttu-id="b4330-157">Als u denkt dat u alle verwachte Hallo-resultaten niet ziet, moet u er een aantal mogelijke redenen zijn.</span><span class="sxs-lookup"><span data-stu-id="b4330-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="b4330-158">**Filter tijdsbereik**.</span><span class="sxs-lookup"><span data-stu-id="b4330-158">**Time range filter**.</span></span> <span data-ttu-id="b4330-159">Standaard worden alleen er resultaten van Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="b4330-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="b4330-160">Er is een automatische filter dat verkleint Hallo bereik van de resultaten die zijn opgehaald uit de brontabellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4330-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="b4330-161">U kunt echter wijzigen Hallo tijdsbereik filteren met behulp van de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4330-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="b4330-162">Of u kunt automatische bereik Hallo vervangen door uw eigen [ `where  ... timestamp ...` component](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) in uw query.</span><span class="sxs-lookup"><span data-stu-id="b4330-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="b4330-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b4330-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="b4330-164">**Resultaten limiet**.</span><span class="sxs-lookup"><span data-stu-id="b4330-164">**Results limit**.</span></span> <span data-ttu-id="b4330-165">Er is een limiet van ongeveer 10 k rijen op Hallo resultaten geretourneerd door het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="b4330-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="b4330-166">Een waarschuwing bevat als u gaan Hallo overschreden.</span><span class="sxs-lookup"><span data-stu-id="b4330-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="b4330-167">Als dat gebeurt, sorteren van de resultaten in de tabel Hallo won't altijd u alle Hallo werkelijke eerste of laatste resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="b4330-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="b4330-168">Het is raadzaam om tooavoid roept Hallo limiet.</span><span class="sxs-lookup"><span data-stu-id="b4330-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="b4330-169">Filter tijdsbereik hello gebruiken, of gebruik operators, zoals:</span><span class="sxs-lookup"><span data-stu-id="b4330-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="b4330-170">Top 100 volgens de timestamp</span><span class="sxs-lookup"><span data-stu-id="b4330-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="b4330-171">100 duren</span><span class="sxs-lookup"><span data-stu-id="b4330-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="b4330-172">samenvatten</span><span class="sxs-lookup"><span data-stu-id="b4330-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="b4330-173">waar tijdstempel > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="b4330-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="b4330-174">(Meer dan 10 k rijen wilt?</span><span class="sxs-lookup"><span data-stu-id="b4330-174">(Want more than 10k rows?</span></span> <span data-ttu-id="b4330-175">Overweeg het gebruik van [continue Export](app-insights-export-telemetry.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="b4330-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="b4330-176">Analytics is ontworpen voor analyse, in plaats van onbewerkte gegevens op te halen.)</span><span class="sxs-lookup"><span data-stu-id="b4330-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="b4330-177">Diagrammen</span><span class="sxs-lookup"><span data-stu-id="b4330-177">Diagrams</span></span>
<span data-ttu-id="b4330-178">Hallo type diagram dat u wilt selecteren:</span><span class="sxs-lookup"><span data-stu-id="b4330-178">Select hello type of diagram you'd like:</span></span>

![Selecteer een diagramtype](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="b4330-180">Als u meerdere kolommen van de juiste typen Hallo hebt, kunt u Hallo x en y-as en een kolom met de dimensies toosplit Hallo resultaten op.</span><span class="sxs-lookup"><span data-stu-id="b4330-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="b4330-181">Standaard resultaten in eerste instantie worden weergegeven als een tabel, en u Hallo diagram handmatig selecteren.</span><span class="sxs-lookup"><span data-stu-id="b4330-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="b4330-182">Maar u kunt Hallo [renderen richtlijn](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) aan Hallo einde van een query tooselect een diagram.</span><span class="sxs-lookup"><span data-stu-id="b4330-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="b4330-183">Analytics diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="b4330-183">Analytics diagnostics</span></span>


<span data-ttu-id="b4330-184">Op een timechart als er een plotselinge piek of de stap in uw gegevens, ziet u mogelijk een gemarkeerde punt op Hallo lijn.</span><span class="sxs-lookup"><span data-stu-id="b4330-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="b4330-185">Hiermee wordt aangegeven dat Analytics Diagnostics een combinatie van eigenschappen die Hallo plotselinge verandering uitfilteren is geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="b4330-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="b4330-186">Klik op Hallo punt tooget meer informatie over het Hallo-filter en toosee Hallo gefilterde versie.</span><span class="sxs-lookup"><span data-stu-id="b4330-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="b4330-187">Hiermee kunt u bepalen welke veroorzaakt Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b4330-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="b4330-188">Meer informatie over diagnostische gegevens Analytics</span><span class="sxs-lookup"><span data-stu-id="b4330-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Analytics diagnostische gegevens](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="b4330-190">Pincode toodashboard</span><span class="sxs-lookup"><span data-stu-id="b4330-190">Pin toodashboard</span></span>
<span data-ttu-id="b4330-191">U kunt vastmaken een diagram of tabel tooone van uw [dashboards gedeeld](app-insights-dashboards.md) -Hallo pincode klikt u op.</span><span class="sxs-lookup"><span data-stu-id="b4330-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="b4330-192">(U moet mogelijk te[upgrade pakket de prijzen van uw app](app-insights-pricing.md) tooturn over deze functie.)</span><span class="sxs-lookup"><span data-stu-id="b4330-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Klik op Hallo pincode](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="b4330-194">Dit betekent dat, wanneer u een dashboard toohelp u Hallo prestaties of het gebruik van uw webservices bewaken samenstellen, u erg complexe analyse naast Hallo andere metrische gegevens opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="b4330-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="b4330-195">Als er vier of minder kolommen, kunt u een tabel toohello-dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="b4330-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="b4330-196">Alleen Hallo bovenste zeven rijen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b4330-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="b4330-197">Dashboard vernieuwen</span><span class="sxs-lookup"><span data-stu-id="b4330-197">Dashboard refresh</span></span>
<span data-ttu-id="b4330-198">Hallo grafiek vastgemaakt toohello dashboard wordt automatisch vernieuwd door Hallo query opnieuw ongeveer elk uur wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4330-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="b4330-199">U kunt ook klikken op de knop Vernieuwen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4330-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="b4330-200">Automatische vereenvoudigen</span><span class="sxs-lookup"><span data-stu-id="b4330-200">Automatic simplifications</span></span>

<span data-ttu-id="b4330-201">Bepaalde vereenvoudigen zijn toegepaste tooa grafiek wanneer u deze tooa dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="b4330-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="b4330-202">**Tijd van de beperking:** query's zijn automatisch beperkt toohello afgelopen 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="b4330-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="b4330-203">Hallo effect is Hallo dezelfde als de query bevat `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="b4330-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="b4330-204">**Aantal beperking bin:** als u een grafiek die een groot aantal afzonderlijke opslaglocaties (meestal een staafdiagram weergeven heeft) minder ingevuld opslaglocaties automatisch gegroepeerd in een enkele 'anderen' hello opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="b4330-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="b4330-205">Bijvoorbeeld: deze query:</span><span class="sxs-lookup"><span data-stu-id="b4330-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="b4330-206">Analytics weergegeven als volgt:</span><span class="sxs-lookup"><span data-stu-id="b4330-206">looks like this in Analytics:</span></span>

![Grafiek met lange staart](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="b4330-208">maar wanneer u deze tooa dashboard vastmaken als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="b4330-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Grafiek met beperkte opslaglocaties](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="b4330-210">TooExcel exporteren</span><span class="sxs-lookup"><span data-stu-id="b4330-210">Export tooExcel</span></span>
<span data-ttu-id="b4330-211">Nadat u een query uitvoert hebt, kunt u een CSV-bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="b4330-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="b4330-212">Klik op **exporteren, Excel**.</span><span class="sxs-lookup"><span data-stu-id="b4330-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="b4330-213">TooPower BI exporteren</span><span class="sxs-lookup"><span data-stu-id="b4330-213">Export tooPower BI</span></span>
<span data-ttu-id="b4330-214">Hallo cursor plaatsen in een query en kies **exporteren, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="b4330-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Exporteren van Analytics tooPower BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="b4330-216">U uitvoeren Hallo query in Power BI.</span><span class="sxs-lookup"><span data-stu-id="b4330-216">You run hello query in Power BI.</span></span> <span data-ttu-id="b4330-217">U kunt deze toorefresh, instellen op een planning.</span><span class="sxs-lookup"><span data-stu-id="b4330-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="b4330-218">U kunt dashboards die samenbrengen van gegevens uit een groot aantal bronnen maken met Power BI.</span><span class="sxs-lookup"><span data-stu-id="b4330-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="b4330-219">Meer informatie over export tooPower BI</span><span class="sxs-lookup"><span data-stu-id="b4330-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="b4330-220">Dieptekoppeling</span><span class="sxs-lookup"><span data-stu-id="b4330-220">Deep link</span></span>

<span data-ttu-id="b4330-221">Een koppeling onder **uitvoer, koppeling van de Share** kunt u tooanother gebruiker verzenden.</span><span class="sxs-lookup"><span data-stu-id="b4330-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="b4330-222">Opgegeven Hallo gebruiker heeft [toegang tooyour resourcegroep](app-insights-resources-roles-access-control.md), Hallo query wordt geopend in Hallo Analytics gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b4330-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="b4330-223">(In Hallo-koppeling Hallo querytekst wordt weergegeven na '? q = ' gzip gecomprimeerd en base 64-codering.</span><span class="sxs-lookup"><span data-stu-id="b4330-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="b4330-224">U kunt code toogenerate dieptekoppelingen schrijven toousers op te geven.</span><span class="sxs-lookup"><span data-stu-id="b4330-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="b4330-225">Hallo wordt echter aanbevolen manier toorun Analytics van code is via Hallo [REST-API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="b4330-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="b4330-226">Automatisering</span><span class="sxs-lookup"><span data-stu-id="b4330-226">Automation</span></span>

<span data-ttu-id="b4330-227">Gebruik Hallo [REST-API van Data Access](https://dev.applicationinsights.io/) toorun analysequery's.</span><span class="sxs-lookup"><span data-stu-id="b4330-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="b4330-228">[Bijvoorbeeld](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (met PowerShell):</span><span class="sxs-lookup"><span data-stu-id="b4330-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="b4330-229">In tegenstelling tot Hallo Analytics UI, geeft Hallo REST-API tijdstempel beperking tooyour query's niet automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b4330-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="b4330-230">Houd er rekening mee tooadd uw eigen where-component, tooavoid grote antwoorden ophalen.</span><span class="sxs-lookup"><span data-stu-id="b4330-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="b4330-231">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="b4330-231">Import data</span></span>

<span data-ttu-id="b4330-232">U kunt gegevens importeren uit een CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="b4330-232">You can import data from a CSV file.</span></span> <span data-ttu-id="b4330-233">Standaardgebruik zijn tooimport statische gegevens die u kunt deelnemen aan met tabellen uit uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="b4330-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="b4330-234">Als de geverifieerde gebruikers worden geïdentificeerd in uw telemetrie met een alias of een verborgen-id, kunt u bijvoorbeeld een tabel die is toegewezen aliassen tooreal namen importeren.</span><span class="sxs-lookup"><span data-stu-id="b4330-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="b4330-235">Door een join op Hallo-aanvraagtelemetrie uitvoert, kunt u gebruikers identificeren met hun echte namen in Hallo Analytics-rapporten.</span><span class="sxs-lookup"><span data-stu-id="b4330-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="b4330-236">Het gegevensschema van uw definiëren</span><span class="sxs-lookup"><span data-stu-id="b4330-236">Define your data schema</span></span>

1. <span data-ttu-id="b4330-237">Klik op **instellingen** (op linksboven) en vervolgens **gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="b4330-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="b4330-238">Toevoegen van een gegevensbron, Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="b4330-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="b4330-239">U bent toosupply gevraagd een steekproef van Hallo gegevens, die ten minste tien rijen bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4330-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="b4330-240">Corrigeer Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="b4330-240">You then correct hello schema.</span></span>

<span data-ttu-id="b4330-241">Hiermee definieert u een gegevensbron, klikt u vervolgens u kunt afzonderlijke tabellen tooimport gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4330-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="b4330-242">Een tabel importeren</span><span class="sxs-lookup"><span data-stu-id="b4330-242">Import a table</span></span>

1. <span data-ttu-id="b4330-243">Definitie van de gegevensbron uit de lijst Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="b4330-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="b4330-244">Klik op 'Uploaden' en volg Hallo instructies tooupload Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b4330-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="b4330-245">Hiervoor moet een aanroep tooa REST-API en het is daarom gemakkelijk tooautomate.</span><span class="sxs-lookup"><span data-stu-id="b4330-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="b4330-246">De tabel is nu beschikbaar voor gebruik in Analytics query's.</span><span class="sxs-lookup"><span data-stu-id="b4330-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="b4330-247">Deze wordt weergegeven in Analytics</span><span class="sxs-lookup"><span data-stu-id="b4330-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="b4330-248">Gebruik tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="b4330-248">Use hello table</span></span>

<span data-ttu-id="b4330-249">Stel de definitie van de gegevensbron wordt aangeroepen `usermap`, en dat er twee velden `realName` en `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="b4330-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="b4330-250">Hallo `requests` tabel heeft ook een veld met de naam `user_AuthenticatedId`, zodat u eenvoudig toojoin ze:</span><span class="sxs-lookup"><span data-stu-id="b4330-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="b4330-251">Hallo resulterende tabel van aanvragen is een extra kolom `realName`.</span><span class="sxs-lookup"><span data-stu-id="b4330-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="b4330-252">Importeren uit LogStash</span><span class="sxs-lookup"><span data-stu-id="b4330-252">Import from LogStash</span></span>

<span data-ttu-id="b4330-253">Als u [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), kunt u Analytics tooquery uw Logboeken.</span><span class="sxs-lookup"><span data-stu-id="b4330-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="b4330-254">Gebruik Hallo [invoegtoepassing die gegevens doorgesluisd naar Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="b4330-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="b4330-255">Video</span><span class="sxs-lookup"><span data-stu-id="b4330-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

