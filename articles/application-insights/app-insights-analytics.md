---
title: Analytics - een krachtige zoekprogramma van Azure Application Insights | Microsoft Docs
description: 'Overzicht van Analytics, het hulpprogramma krachtige diagnostische gegevens doorzoeken van de Application Insights. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="8ca36-103">Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ca36-103">Analytics in Application Insights</span></span>
<span data-ttu-id="8ca36-104">[Analytics](app-insights-analytics.md) is de functie krachtige zoeken van [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ca36-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8ca36-105">Deze pagina's worden de Log Analytics query language beschreven.</span><span class="sxs-lookup"><span data-stu-id="8ca36-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="8ca36-106">**[Bekijk de video inleidende](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="8ca36-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="8ca36-107">**[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet van gegevens naar Application Insights nog verzenden.</span><span class="sxs-lookup"><span data-stu-id="8ca36-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="8ca36-108">**[SQL-gebruikers cheats blad](https://aka.ms/sql-analytics)**  zet de meest voorkomende idioms.</span><span class="sxs-lookup"><span data-stu-id="8ca36-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="8ca36-109">**[Taalreferentie](app-insights-analytics-reference.md)**  informatie over het gebruik van alle andere van krachtige functies van de querytaal logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="8ca36-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="8ca36-110">Query's in Analytics</span><span class="sxs-lookup"><span data-stu-id="8ca36-110">Queries in Analytics</span></span>
<span data-ttu-id="8ca36-111">Een typische query is een *bron* tabel gevolgd door een reeks *operators* gescheiden door `|`.</span><span class="sxs-lookup"><span data-stu-id="8ca36-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="8ca36-112">Bijvoorbeeld, we willen weten welk tijdstip van de dag de burgers van Hyderabad de web-app probeert.</span><span class="sxs-lookup"><span data-stu-id="8ca36-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="8ca36-113">En hoewel we er, gaan we kijken welke resultaatcodes voor HTTP-aanvragen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8ca36-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="8ca36-114">We tellen afzonderlijke client-IP-adressen, ze groeperen per uur van de dag gedurende de afgelopen 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="8ca36-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="8ca36-115">Als u resultaten buiten de voorgaande 24 uur, 'tijdstempel' expliciet opnemen in uw query of gebruik de vervolgkeuzelijst tijd bereik.</span><span class="sxs-lookup"><span data-stu-id="8ca36-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="8ca36-116">We gaan de resultaten bij het kiezen van de resultaten van verschillende reactiecodes stapelen presentatie staafdiagram weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8ca36-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Kies staafdiagram, x en y-as en segmentering](./media/app-insights-analytics/020.png)

<span data-ttu-id="8ca36-118">Lijkt erop dat de app op lunchpauze en insluiten-tijd in Hyderabad populairste is.</span><span class="sxs-lookup"><span data-stu-id="8ca36-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="8ca36-119">(En gaan we deze 500 codes).</span><span class="sxs-lookup"><span data-stu-id="8ca36-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="8ca36-120">Er zijn ook krachtige statistische bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="8ca36-120">There are also powerful statistical operations:</span></span>

![Resultaten van statistische query](./media/app-insights-analytics/025.png)

<span data-ttu-id="8ca36-122">De taal heeft veel voordelen bieden:</span><span class="sxs-lookup"><span data-stu-id="8ca36-122">The language has many attractive features:</span></span>


* <span data-ttu-id="8ca36-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) uw app onbewerkte telemetrie op alle velden, met inbegrip van uw aangepaste eigenschappen en metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8ca36-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="8ca36-124">[Deelnemen aan](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) meerdere tabellen – correleer aanvragen met paginaweergaven, afhankelijkheidsaanroepen, uitzonderingen en logboektraceringen.</span><span class="sxs-lookup"><span data-stu-id="8ca36-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="8ca36-125">Krachtige statistische [aggregaties](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="8ca36-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="8ca36-126">Net zo krachtig zijn als SQL, maar veel eenvoudiger voor complexe query's: in plaats van geneste instructies u de gegevens van de ene elementaire bewerking naar de volgende overbrengen.</span><span class="sxs-lookup"><span data-stu-id="8ca36-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="8ca36-127">Onmiddellijke en krachtige visualisaties.</span><span class="sxs-lookup"><span data-stu-id="8ca36-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="8ca36-128">[Grafieken naar Azure dashboards vastmaken](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="8ca36-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="8ca36-129">[Query's exporteren naar Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="8ca36-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="8ca36-130">Er is een [REST-API](https://dev.applicationinsights.io/) waarmee u kunt query's uitvoeren via een programma, bijvoorbeeld via Powershell.</span><span class="sxs-lookup"><span data-stu-id="8ca36-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="8ca36-131">Verbinding maken met uw Application Insights-gegevens</span><span class="sxs-lookup"><span data-stu-id="8ca36-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="8ca36-132">Analytics openen vanuit uw app [overzichtsblade](app-insights-dashboards.md) in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="8ca36-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="8ca36-134">Video</span><span class="sxs-lookup"><span data-stu-id="8ca36-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="8ca36-135">Query-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8ca36-135">Query examples</span></span>

<span data-ttu-id="8ca36-136">Probeer deze scenario's ter illustratie van de kracht van het gebruik van Analytics:</span><span class="sxs-lookup"><span data-stu-id="8ca36-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="8ca36-137">Automatische diagnoses van pieken en stap gaat in aanvragen duur</span><span class="sxs-lookup"><span data-stu-id="8ca36-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="8ca36-138">Analyse van prestaties degradations met time series-analyse</span><span class="sxs-lookup"><span data-stu-id="8ca36-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="8ca36-139">Problemen met toepassingen met autocluster en diffpatterns analyseren</span><span class="sxs-lookup"><span data-stu-id="8ca36-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="8ca36-140">Geavanceerde vorm detecties met time series-analyse</span><span class="sxs-lookup"><span data-stu-id="8ca36-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="8ca36-141">Met behulp van verschuivende venster bewerkingen voor het analyseren van toepassingsgebruik (rolling MAU/DAU enzovoort)</span><span class="sxs-lookup"><span data-stu-id="8ca36-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="8ca36-142">[Detectie van de serviceonderbrekingen op basis van de analyse van Logboeken voor foutopsporing](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) en een overeenkomende blogbericht [hier](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="8ca36-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="8ca36-143">[Profileren van de prestaties van toepassingen met behulp van Logboeken voor eenvoudige foutopsporing](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="8ca36-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="8ca36-144">[Meten van de duur voor elke stap in uw code-stroom met eenvoudige foutopsporingslogboeken](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="8ca36-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="8ca36-145">[Analyseren met behulp van Logboeken voor eenvoudige foutopsporing gelijktijdigheid](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) en een overeenkomende blogbericht [hier](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="8ca36-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="8ca36-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ca36-146">Next steps</span></span>
* <span data-ttu-id="8ca36-147">We raden u begint met de [taal rondleiding](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="8ca36-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="8ca36-148">Informatie over [met Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="8ca36-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="8ca36-149">[Taalreferentie](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8ca36-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
