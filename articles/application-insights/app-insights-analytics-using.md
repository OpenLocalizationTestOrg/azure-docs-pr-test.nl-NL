---
title: Met Analytics - een krachtige zoekprogramma van Azure Application Insights | Microsoft Docs
description: 'Met behulp van de Analytics, het hulpprogramma krachtige diagnostische gegevens doorzoeken van de Application Insights. '
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
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="f0bd7-103">Door middel van analyses in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0bd7-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="f0bd7-104">[Analytics](app-insights-analytics.md) is de functie krachtige zoeken van [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f0bd7-105">Deze pagina's worden de Log Analytics query language beschreven.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="f0bd7-106">**[Bekijk de video inleidende](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="f0bd7-107">**[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet van gegevens naar Application Insights nog verzenden.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="f0bd7-108">Open Analytics</span><span class="sxs-lookup"><span data-stu-id="f0bd7-108">Open Analytics</span></span>
<span data-ttu-id="f0bd7-109">Klik op Analytics van uw app thuis resource in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="f0bd7-111">De inline-zelfstudie hebt u enkele ideeën over wat u kunt doen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="f0bd7-112">Er is een [hier uitgebreider rondleiding](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="f0bd7-113">Uw telemetrie query</span><span class="sxs-lookup"><span data-stu-id="f0bd7-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="f0bd7-114">Een query schrijven</span><span class="sxs-lookup"><span data-stu-id="f0bd7-114">Write a query</span></span>
![Schema weergeven](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="f0bd7-116">Beginnen met de namen van elk van de tabellen die aan de linkerkant worden vermeld (of de [bereik](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) of [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="f0bd7-117">Gebruik `|` voor het maken van een pijplijn van [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="f0bd7-118">IntelliSense vraagt u met de operators en de expressie-elementen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="f0bd7-119">Klik op het informatiepictogram (of druk op CTRL + SPATIEBALK) om op te halen van een langere beschrijving en voorbeelden van het gebruik van elk element.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="f0bd7-120">Zie de [Analytics taal rondleiding](app-insights-analytics-tour.md) en [taalreferentie](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="f0bd7-121">Een query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-121">Run a query</span></span>
![Een query uit te voeren](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="f0bd7-123">U kunt één regeleinden gebruiken in een query.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="f0bd7-124">Plaats de cursor in- of aan het einde van de query die u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="f0bd7-125">Controleer het tijdsbereik van uw query.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-125">Check the time range of your query.</span></span> <span data-ttu-id="f0bd7-126">(U kunt deze wijzigen of deze door uw eigen overschrijven [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) -component in uw query.)</span><span class="sxs-lookup"><span data-stu-id="f0bd7-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="f0bd7-127">Klik op naar de query wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="f0bd7-128">Lege regels niet in uw query worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="f0bd7-129">U kunt meerdere gescheiden query's in één query tabblad houden door deze te scheiden met een lege regels.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="f0bd7-130">Alleen de query met de cursor wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="f0bd7-131">Een query opslaan</span><span class="sxs-lookup"><span data-stu-id="f0bd7-131">Save a query</span></span>
![Opslaan van een query](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="f0bd7-133">Sla het huidige querybestand.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-133">Save the current query file.</span></span>
2. <span data-ttu-id="f0bd7-134">Open een opgeslagen query-bestand.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-134">Open a saved query file.</span></span>
3. <span data-ttu-id="f0bd7-135">Maak een nieuwe querybestand.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="f0bd7-136">Bekijk de details</span><span class="sxs-lookup"><span data-stu-id="f0bd7-136">See the details</span></span>
<span data-ttu-id="f0bd7-137">Vouw een rij in de resultaten om te zien van de volledige lijst met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="f0bd7-138">U kunt verder uitbreiden in elke eigenschap die is bijvoorbeeld een gestructureerde waarde -, aangepaste dimensies of de stack aanbieding in een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Vouw een rij](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="f0bd7-140">De resultaten ordenen</span><span class="sxs-lookup"><span data-stu-id="f0bd7-140">Arrange the results</span></span>
<span data-ttu-id="f0bd7-141">U kunt sorteren, filteren, pagineren en de resultaten van uw query te groeperen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="f0bd7-142">Sorteren, groeperen en filteren in de browser niet Voer de query opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="f0bd7-143">Ze alleen de resultaten die zijn geretourneerd door de laatste query opnieuw te rangschikken.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="f0bd7-144">Om deze taken in de server uitvoeren voordat u de resultaten worden geretourneerd, schrijft u uw query met de [sorteren](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [samenvatten](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) en [waar](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="f0bd7-145">Kies de kolommen die u wilt bekijken, sleept u de kolomkoppen om te rangschikken en kolombreedtes te slepen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Kolommen rangschikken](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="f0bd7-147">Items sorteren en filteren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-147">Sort and filter items</span></span>
<span data-ttu-id="f0bd7-148">Uw resultaten sorteren door te klikken op de kop van een kolom.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="f0bd7-149">Klik op opnieuw als u wilt sorteren van de andere manier en klikt u op een derde tijdstip terugkeren naar de oorspronkelijke ordening geretourneerd door de query.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="f0bd7-150">Gebruik het filterpictogram in de zoekactie.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-150">Use the filter icon to narrow your search.</span></span>

![Kolommen sorteren en filteren](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="f0bd7-152">Items groeperen</span><span class="sxs-lookup"><span data-stu-id="f0bd7-152">Group items</span></span>
<span data-ttu-id="f0bd7-153">Gebruik op meer dan een kolom wilt sorteren, groeperen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="f0bd7-154">Deze eerst inschakelen en sleep de kolomkoppen in de ruimte boven de tabel.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Groep](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="f0bd7-156">Ontbreken er bepaalde resultaten?</span><span class="sxs-lookup"><span data-stu-id="f0bd7-156">Missing some results?</span></span>

<span data-ttu-id="f0bd7-157">Als u denkt dat u niet de verwachte resultaten ziet, moet u er een aantal mogelijke redenen zijn.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="f0bd7-158">**Filter tijdsbereik**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-158">**Time range filter**.</span></span> <span data-ttu-id="f0bd7-159">Standaard worden alleen resultaten weergegeven in de afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="f0bd7-160">Er is een automatische filter dat het bereik van de resultaten die zijn opgehaald uit de brontabellen beperkt.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="f0bd7-161">U kunt echter het tijdsbereik wijzigen filteren met behulp van de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="f0bd7-162">Of u kunt het automatische bereik vervangen door uw eigen [ `where  ... timestamp ...` component](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) in uw query.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="f0bd7-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="f0bd7-164">**Resultaten limiet**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-164">**Results limit**.</span></span> <span data-ttu-id="f0bd7-165">Er is een limiet van ongeveer 10 kB rijen op de resultaten van de portal.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="f0bd7-166">Ziet u een waarschuwing als u gaan dan de limiet.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="f0bd7-167">Als dat gebeurt, won't sorteren van de resultaten in de tabel altijd weergeven u alle werkelijke eerste of laatste resultaten.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="f0bd7-168">Het is raadzaam om te voorkomen dat roept de limiet.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="f0bd7-169">Het filter tijdsbereik gebruiken, of gebruik operators, zoals:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="f0bd7-170">Top 100 volgens de timestamp</span><span class="sxs-lookup"><span data-stu-id="f0bd7-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="f0bd7-171">100 duren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="f0bd7-172">samenvatten</span><span class="sxs-lookup"><span data-stu-id="f0bd7-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="f0bd7-173">waar tijdstempel > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="f0bd7-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="f0bd7-174">(Meer dan 10 k rijen wilt?</span><span class="sxs-lookup"><span data-stu-id="f0bd7-174">(Want more than 10k rows?</span></span> <span data-ttu-id="f0bd7-175">Overweeg het gebruik van [continue Export](app-insights-export-telemetry.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="f0bd7-176">Analytics is ontworpen voor analyse, in plaats van onbewerkte gegevens op te halen.)</span><span class="sxs-lookup"><span data-stu-id="f0bd7-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="f0bd7-177">Diagrammen</span><span class="sxs-lookup"><span data-stu-id="f0bd7-177">Diagrams</span></span>
<span data-ttu-id="f0bd7-178">Selecteer het type diagram dat u wilt dat:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-178">Select the type of diagram you'd like:</span></span>

![Selecteer een diagramtype](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="f0bd7-180">Als u meerdere kolommen van de juiste typen hebt, kunt u de x en y-as en een kolom van dimensies scheiden van de resultaten op.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="f0bd7-181">Standaard resultaten in eerste instantie worden weergegeven als een tabel, en u handmatig het diagram selecteren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="f0bd7-182">Maar u kunt de [renderen richtlijn](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) aan het einde van een query naar een diagram selecteren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="f0bd7-183">Analytics diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="f0bd7-183">Analytics diagnostics</span></span>


<span data-ttu-id="f0bd7-184">Op een timechart als er een plotselinge piek of de stap in uw gegevens, ziet u mogelijk een gemarkeerd punt op de regel.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="f0bd7-185">Hiermee wordt aangegeven dat een combinatie van eigenschappen die de onverwachte wijziging uitfilteren is geïdentificeerd door Analytics diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="f0bd7-186">Klik op het punt om meer details op het filter en de gefilterde versie te zien.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="f0bd7-187">Hiermee kunt u bepalen wat de oorzaak van de wijziging.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="f0bd7-188">Meer informatie over diagnostische gegevens Analytics</span><span class="sxs-lookup"><span data-stu-id="f0bd7-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Analytics diagnostische gegevens](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="f0bd7-190">Vastmaken aan dashboard</span><span class="sxs-lookup"><span data-stu-id="f0bd7-190">Pin to dashboard</span></span>
<span data-ttu-id="f0bd7-191">U kunt vastmaken een diagram of de tabel op een van uw [dashboards gedeeld](app-insights-dashboards.md) -Klik op de pincode.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="f0bd7-192">(Mogelijk moet u [upgrade pakket de prijzen van uw app](app-insights-pricing.md) voor deze functie inschakelen.)</span><span class="sxs-lookup"><span data-stu-id="f0bd7-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Klik op de pincode](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="f0bd7-194">Dit betekent dat, wanneer u een dashboard om te controleren van de prestaties of het gebruik van uw webservices samenstellen, u erg complexe analyse naast de andere metrische gegevens opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="f0bd7-195">Als er vier of minder kolommen, kunt u een tabel aan het dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="f0bd7-196">Alleen de bovenste zeven rijen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="f0bd7-197">Dashboard vernieuwen</span><span class="sxs-lookup"><span data-stu-id="f0bd7-197">Dashboard refresh</span></span>
<span data-ttu-id="f0bd7-198">De grafiek vastgemaakt aan het dashboard wordt automatisch vernieuwd door de query opnieuw ongeveer elk uur wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="f0bd7-199">U kunt ook klikken op de knop vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="f0bd7-200">Automatische vereenvoudigen</span><span class="sxs-lookup"><span data-stu-id="f0bd7-200">Automatic simplifications</span></span>

<span data-ttu-id="f0bd7-201">Bepaalde vereenvoudigen worden toegepast op een grafiek wanneer u het vastmaken aan een dashboard.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="f0bd7-202">**Tijd van de beperking:** query's zijn automatisch beperkt tot de afgelopen 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="f0bd7-203">Het effect is hetzelfde als wanneer de query bevat `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="f0bd7-204">**Aantal beperking bin:** als u een grafiek met een groot aantal afzonderlijke opslaglocaties (meestal een staafdiagram) wordt weergegeven, de minder ingevuld opslaglocaties automatisch gegroepeerd in één bin 'anderen'.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="f0bd7-205">Bijvoorbeeld: deze query:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="f0bd7-206">Analytics weergegeven als volgt:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-206">looks like this in Analytics:</span></span>

![Grafiek met lange staart](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="f0bd7-208">maar wanneer u deze aan een dashboard vastmaken, als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Grafiek met beperkte opslaglocaties](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="f0bd7-210">Exporteren naar Excel</span><span class="sxs-lookup"><span data-stu-id="f0bd7-210">Export to Excel</span></span>
<span data-ttu-id="f0bd7-211">Nadat u een query uitvoert hebt, kunt u een CSV-bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="f0bd7-212">Klik op **exporteren, Excel**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="f0bd7-213">Exporteren naar Power BI</span><span class="sxs-lookup"><span data-stu-id="f0bd7-213">Export to Power BI</span></span>
<span data-ttu-id="f0bd7-214">Plaats de cursor in een query en kies **exporteren, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Exporteren van analytische gegevens met Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="f0bd7-216">U voert de query in Power BI.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-216">You run the query in Power BI.</span></span> <span data-ttu-id="f0bd7-217">U kunt dit instellen als volgens een schema vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="f0bd7-218">U kunt dashboards die samenbrengen van gegevens uit een groot aantal bronnen maken met Power BI.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="f0bd7-219">Meer informatie over het exporteren naar Power BI</span><span class="sxs-lookup"><span data-stu-id="f0bd7-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="f0bd7-220">Dieptekoppeling</span><span class="sxs-lookup"><span data-stu-id="f0bd7-220">Deep link</span></span>

<span data-ttu-id="f0bd7-221">Een koppeling onder **uitvoer, koppeling van de Share** die u kunt zenden naar een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="f0bd7-222">Mits de gebruiker heeft [toegang tot uw resourcegroep](app-insights-resources-roles-access-control.md), de query wordt geopend in de gebruikersinterface Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="f0bd7-223">(In de koppeling tekst van de query wordt weergegeven na '? q = ' gzip gecomprimeerd en base 64-codering.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="f0bd7-224">U kunt de code voor het genereren van dieptekoppelingen die u aan gebruikers biedt schrijven.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="f0bd7-225">De aanbevolen manier om het uitvoeren van analyses van code is echter met behulp van de [REST-API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="f0bd7-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="f0bd7-226">Automatisering</span><span class="sxs-lookup"><span data-stu-id="f0bd7-226">Automation</span></span>

<span data-ttu-id="f0bd7-227">Gebruik de [REST-API van Data Access](https://dev.applicationinsights.io/) Analytics query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="f0bd7-228">[Bijvoorbeeld](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (met PowerShell):</span><span class="sxs-lookup"><span data-stu-id="f0bd7-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="f0bd7-229">In tegenstelling tot de gebruikersinterface van Analytics, wordt de REST-API niet automatisch toegevoegd een timestamp-beperking aan de query's.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="f0bd7-230">Vergeet niet uw eigen where-component, om te voorkomen dat grote antwoorden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="f0bd7-231">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-231">Import data</span></span>

<span data-ttu-id="f0bd7-232">U kunt gegevens importeren uit een CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-232">You can import data from a CSV file.</span></span> <span data-ttu-id="f0bd7-233">Een gemiddelde gebruiksduur is om statische gegevens die u kunt deelnemen aan met tabellen uit uw telemetrie te importeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="f0bd7-234">Als de geverifieerde gebruikers worden geïdentificeerd in uw telemetrie met een alias of een verborgen-id, kunt u bijvoorbeeld een tabel die is toegewezen aliassen aan echte namen importeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="f0bd7-235">Door het uitvoeren van een join voor de aanvraagtelemetrie, kunt u gebruikers identificeren met hun echte naam in de Analytics-rapporten.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="f0bd7-236">Het gegevensschema van uw definiëren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-236">Define your data schema</span></span>

1. <span data-ttu-id="f0bd7-237">Klik op **instellingen** (op linksboven) en vervolgens **gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="f0bd7-238">Toevoegen van een gegevensbron, de instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="f0bd7-239">U wordt gevraagd om op te geven van een steekproef van de gegevens die moet ten minste tien rijen bevatten.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="f0bd7-240">U kunt het schema corrigeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-240">You then correct the schema.</span></span>

<span data-ttu-id="f0bd7-241">Hiermee definieert u een gegevensbron, waarin u vervolgens kunt afzonderlijke tabellen importeren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="f0bd7-242">Een tabel importeren</span><span class="sxs-lookup"><span data-stu-id="f0bd7-242">Import a table</span></span>

1. <span data-ttu-id="f0bd7-243">Open de definitie van de gegevensbron uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="f0bd7-244">Klik op 'Uploaden' en volg de instructies voor het uploaden van de tabel.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="f0bd7-245">Hiervoor moet een aanroep van een REST-API en het is daarom gemakkelijk te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="f0bd7-246">De tabel is nu beschikbaar voor gebruik in Analytics query's.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="f0bd7-247">Deze wordt weergegeven in Analytics</span><span class="sxs-lookup"><span data-stu-id="f0bd7-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="f0bd7-248">Gebruik de tabel</span><span class="sxs-lookup"><span data-stu-id="f0bd7-248">Use the table</span></span>

<span data-ttu-id="f0bd7-249">Stel de definitie van de gegevensbron wordt aangeroepen `usermap`, en dat er twee velden `realName` en `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="f0bd7-250">De `requests` tabel heeft ook een veld met de naam `user_AuthenticatedId`, zodat u gemakkelijk te koppelen:</span><span class="sxs-lookup"><span data-stu-id="f0bd7-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="f0bd7-251">De resulterende tabel van aanvragen is een extra kolom `realName`.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="f0bd7-252">Importeren uit LogStash</span><span class="sxs-lookup"><span data-stu-id="f0bd7-252">Import from LogStash</span></span>

<span data-ttu-id="f0bd7-253">Als u [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), kunt u Analytics query uitvoeren op uw Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f0bd7-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="f0bd7-254">Gebruik de [invoegtoepassing die gegevens doorgesluisd naar Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="f0bd7-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="f0bd7-255">Video</span><span class="sxs-lookup"><span data-stu-id="f0bd7-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

