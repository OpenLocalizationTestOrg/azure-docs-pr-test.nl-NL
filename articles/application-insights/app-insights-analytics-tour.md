---
title: aaaA rondleiding via Analytics in Azure Application Insights | Microsoft Docs
description: Korte voorbeelden van alle Hallo belangrijkste query's in Analytics, Hallo krachtige zoekfunctie van Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="6cdd8-103">Een rondleiding van Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6cdd8-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="6cdd8-104">[Analytics](app-insights-analytics.md) is Hallo krachtige zoekfunctie van [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6cdd8-105">Deze pagina's worden de Log Analytics query language beschreven.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="6cdd8-106">**[Hallo inleidende video bekijken](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="6cdd8-107">**[Uitprobeert Analytics op onze gesimuleerde gegevens](https://analytics.applicationinsights.io/demo)**  als uw app wordt niet nog gegevens tooApplication Insights verzendt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="6cdd8-108">**[SQL-gebruikers cheats blad](https://aka.ms/sql-analytics)**  Hallo meest voorkomende idioms vertaalt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="6cdd8-109">U gaat nu een stapsgewijze beschrijving van enkele eenvoudige query tooget die u gestart.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="6cdd8-110">Verbinding maken met gegevens van de Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="6cdd8-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="6cdd8-111">Analytics openen vanuit uw app [overzichtsblade](app-insights-dashboards.md) in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Open portal.azure.com open uw Application Insights-resource en klik op Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="6cdd8-113">[Nemen](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n rijen weergeven</span><span class="sxs-lookup"><span data-stu-id="6cdd8-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="6cdd8-114">Gegevenspunten die zich gebruiker operations (meestal HTTP-aanvragen ontvangen door uw web-app aanmelden) worden opgeslagen in een tabel met de naam `requests`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="6cdd8-115">Elke rij is een telemetrie gegevenspunt ontvangen van Hallo Application Insights-SDK in uw app.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="6cdd8-116">Laten we beginnen vindt u een paar voorbeeld rijen van de tabel Hallo van:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-116">Let's start by examining a few sample rows of hello table:</span></span>

![resultaten](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="6cdd8-118">Plaats Hallo cursor ergens in de instructie Hallo voordat u klikt op Start.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="6cdd8-119">U kunt een instructie verdelen over meer dan één regel, maar geen lege regels plaatsen in een instructie.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="6cdd8-120">Lege regels zijn een handige manier tookeep verschillende query's in het venster Hallo scheiden.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="6cdd8-121">Kolommen kiezen, sleept u deze groeperen op kolommen, en te filteren:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Klik op de kolom selecteren in de rechterbovenhoek van de resultaten](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="6cdd8-123">Vouw een item toosee Hallo detail:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-123">Expand any item toosee hello detail:</span></span>

![Kies tabel en kolommen configureren gebruiken](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="6cdd8-125">Klik op Hallo hoofd van een kolom toore volgorde Hallo resultaten-beschikbaar in de webbrowser Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="6cdd8-126">Maar houd er rekening mee dat voor een grote resultatenset Hallo aantal rijen gedownloade toohello browser is beperkt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="6cdd8-127">Sorteren op deze manier wordt niet altijd weergegeven u Hallo werkelijke hoogste of laagste items.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="6cdd8-128">toosort items betrouwbare manier gebruik Hallo `top` of `sort` operator.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="6cdd8-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) en [sorteren](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="6cdd8-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="6cdd8-130">`take`is handig tooget een snel voorbeeld van een resultaat, maar deze bevat rijen uit de tabel Hallo in willekeurige volgorde.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="6cdd8-131">gebruik van een geordende weergave tooget `top` (voor een voorbeeld) of `sort` (via de hele tabel Hallo).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="6cdd8-132">Hallo eerste n rijen, geordend op een bepaalde kolom weergeven:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="6cdd8-133">*Syntaxis:* hebben de meeste operators sleutelwoord parameters, zoals `by`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="6cdd8-134">`desc`aflopende volgorde = `asc` = oplopend.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="6cdd8-135">`top...`is een manier meer zodat de melding `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="6cdd8-136">We kunnen schrijven:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="6cdd8-137">Hallo resultaat zou zijn Hallo dezelfde, maar deze zou iets langzamer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="6cdd8-138">(U kunt ook schrijven `order`, dit is een alias van `sort`.)</span><span class="sxs-lookup"><span data-stu-id="6cdd8-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="6cdd8-139">Hallo kolomkoppen in tabelweergave Hallo kunnen ook worden gebruikt toosort Hallo resultaten op het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="6cdd8-140">Maar natuurlijk, als u hebt gebruikt `take` of `top` tooretrieve alleen maar een deel van een tabel, moet u alleen opnieuw rangschikken Hallo records die u hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="6cdd8-141">[Waar](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): voor het filteren van een voorwaarde</span><span class="sxs-lookup"><span data-stu-id="6cdd8-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="6cdd8-142">Laten we zien alleen aanvragen die een bepaalde resultaatcode geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="6cdd8-143">Hallo `where` operator werkt met een Boole-expressie.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="6cdd8-144">Hier volgen enkele belangrijke punten hierover:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-144">Here are some key points about them:</span></span>

* <span data-ttu-id="6cdd8-145">`and`, `or`: Booleaanse operators</span><span class="sxs-lookup"><span data-stu-id="6cdd8-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="6cdd8-146">`==`, `<>`, `!=` : gelijk en niet gelijk aan</span><span class="sxs-lookup"><span data-stu-id="6cdd8-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="6cdd8-147">`=~`, `!~` : niet-hoofdlettergevoelige tekenreeks gelijk en niet gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="6cdd8-148">Er zijn veel meer tekenreeks vergelijkingsoperators.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="6cdd8-149">Het juiste type Hallo</span><span class="sxs-lookup"><span data-stu-id="6cdd8-149">Getting hello right type</span></span>
<span data-ttu-id="6cdd8-150">Mislukte aanvragen zoeken:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="6cdd8-151">Time</span><span class="sxs-lookup"><span data-stu-id="6cdd8-151">Time</span></span>

<span data-ttu-id="6cdd8-152">Uw query's zijn standaard beperkte toohello afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="6cdd8-153">Maar u kunt dit bereik wijzigen:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="6cdd8-154">Hallo tijdsbereik overschrijven door een query noemt schrijven `timestamp` in een component where.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="6cdd8-155">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="6cdd8-156">Hallo tijd bereik functie is gelijkwaardig tooa 'where' component ingevoegd na elke vermelding van een van de brontabellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="6cdd8-157">`ago(3d)`betekent 'drie dagen geleden'.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="6cdd8-158">Andere tijdseenheden uren bevatten (`2h`, `2.5h`), minuten (`25m`), en seconden (`10s`).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="6cdd8-159">Andere voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="6cdd8-160">[Datums en tijden verwijzing](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="6cdd8-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selecteren en de namen van kolommen berekenen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="6cdd8-162">Gebruik [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick uit net Hallo kolommen die u wilt:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="6cdd8-163">U kunt ook wijzigen van kolommen en definiëren van nieuwe:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![Resultaat](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="6cdd8-165">Kolomnamen kunnen spaties bevatten of symbolen als ze zijn tussen zoals deze: `['...']` of`["..."]`</span><span class="sxs-lookup"><span data-stu-id="6cdd8-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="6cdd8-166">`%`Hallo is gebruikelijke modulo operator.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="6cdd8-167">`1d`(die wordt een cijfer, en vervolgens een had') is een letterlijke timespan wat betekent dat één dag.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="6cdd8-168">Hier volgen enkele meer timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="6cdd8-169">`floor`(alias `bin`) Rondt een waarde omlaag toohello dichtstbijzijnde meervoud van basiswaarde Hallo u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="6cdd8-170">Dus `floor(aTime, 1s)` Rondt tegelijk omlaag toohello dichtstbijzijnde seconde.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="6cdd8-171">Expressies kunnen bevatten alle Hallo gebruikelijke operators (`+`, `-`,...), en er is een aantal handige functies.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="6cdd8-172">Breid uit</span><span class="sxs-lookup"><span data-stu-id="6cdd8-172">Extend</span></span>
<span data-ttu-id="6cdd8-173">Als u alleen tooadd kolommen toohello bestaande toepassingsgroepen wilt, gebruikt u [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="6cdd8-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="6cdd8-174">Met behulp van [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is minder uitgebreid dan [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) als u wilt dat tookeep Hallo alle bestaande kolommen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="6cdd8-175">Toolocal tijd converteren</span><span class="sxs-lookup"><span data-stu-id="6cdd8-175">Convert toolocal time</span></span>

<span data-ttu-id="6cdd8-176">Tijdstempels worden altijd in UTC.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="6cdd8-177">Dus als u bijvoorbeeld op Hallo ons Pacific westkust winter is, kunt u als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="6cdd8-178">[Overzicht van](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): cumulatieve groepen rijen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="6cdd8-179">`Summarize`van toepassing is een opgegeven *aggregatiefunctie* via Rijgroepen koppelen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="6cdd8-180">Bijvoorbeeld, Hallo duurt voordat uw web-app toorespond tooa aanvraag wordt gerapporteerd in het veld Hallo `duration`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="6cdd8-181">Gemiddelde reactietijd van Hallo gaan we kijken tijd tooall aanvragen:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="6cdd8-182">Of we Hallo resultaat kan verdelen in aanvragen van verschillende namen:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="6cdd8-183">`Summarize`verzamelt gegevenspunten in de stroom Hallo Hallo in groepen voor welke Hallo `by` component evenveel evalueert.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="6cdd8-184">Elke waarde in Hallo `by` - elke bewerkingsnaam in Hallo boven de voorbeeld - expressie resulteert in een rij in de resultaattabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="6cdd8-185">Of we kan resultaten groeperen op tijd van de dag:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="6cdd8-186">U ziet hoe we maken gebruik van Hallo `bin` functie (aka `floor`).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="6cdd8-187">Als we zojuist gebruikt `by timestamp`, elke rij invoer in een eigen weinig groep zou eindigen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="6cdd8-188">Voor een continue scalaire like tijden of getallen, hebben we toobreak Hallo continue reeks in een beheersbare aantal discrete waarden.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="6cdd8-189">`bin`-Dit is slechts Hallo bekend afronden naar beneden `floor` werken - is de eenvoudigste manier toodo Hallo die.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="6cdd8-190">We kunnen gebruiken dezelfde techniek tooreduce bereiken met tekenreeksen Hallo:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="6cdd8-191">Merk op dat u kunt `name=` tooset Hallo-naam van een resultaatkolom in Hallo statistische expressies of Hallo door component.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="6cdd8-192">Voorbeeldgegevens tellen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-192">Counting sampled data</span></span>
<span data-ttu-id="6cdd8-193">`sum(itemCount)`is Hallo aanbevolen aggregatie toocount gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="6cdd8-194">In veel gevallen itemCount == 1, zodat het Hallo-functie gewoon een aantal rijen in de groep Hallo Hallo telt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="6cdd8-195">Maar wanneer [steekproeven](app-insights-sampling.md) is uitgevoerd, alleen een fractie van de oorspronkelijke gebeurtenissen Hallo blijven behouden als gegevenspunten in Application Insights, zodat er zijn voor elk gegevenspunt u ziet, `itemCount` gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="6cdd8-196">Bijvoorbeeld, als steekproeven 75% van de oorspronkelijke gebeurtenissen Hallo vervolgens itemCount negeert == 4 in Hallo bewaard records - dat wil zeggen, voor elke record behouden, zijn er vier oorspronkelijke records.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="6cdd8-197">Adaptieve steekproeven zorgt ervoor dat itemCount toobe hogere tijdens perioden wanneer uw toepassing veel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="6cdd8-198">Berekening van het itemCount daarom resulteert in een goede indicatie van de oorspronkelijke aantal Hallo van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="6cdd8-199">Er is ook een `count()` aggregatie (en een aantal bewerking) voor gevallen waarin u echt toocount Hallo aantal rijen in een groep wilt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="6cdd8-200">Er is een bereik van [aggregatiefuncties](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="6cdd8-201">Voor grafieken Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="6cdd8-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="6cdd8-202">Standaard worden de resultaten weergegeven als een tabel:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="6cdd8-203">We kunt beter dan Hallo tabelweergave doen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-203">We can do better than hello table view.</span></span> <span data-ttu-id="6cdd8-204">Bekijk Hallo resulteert in een diagramweergave Hallo in met de Hallo verticale balk optie:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Klik op grafiek, kiest u verticaal staafdiagram en toewijzen x en y assen](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="6cdd8-206">U ziet dat hoewel we niet sorteren Hallo resultaten tijd (zoals u ziet in Hallo tabel weergave), datum/tijd Hallo grafiekweergave altijd weergegeven in de juiste volgorde.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="6cdd8-207">Timecharts</span><span class="sxs-lookup"><span data-stu-id="6cdd8-207">Timecharts</span></span>
<span data-ttu-id="6cdd8-208">Weergeven hoeveel gebeurtenissen er elk uur zijn:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="6cdd8-209">Selecteer optie Hallo grafiek:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="6cdd8-211">Meerdere reeksen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-211">Multiple series</span></span>
<span data-ttu-id="6cdd8-212">Meerdere expressies in Hallo `summarize` component maakt meerdere kolommen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="6cdd8-213">Meerdere expressies in Hallo `by` component maakt meerdere rijen, één voor elke combinatie van waarden.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabel met aanvragen per uur en locatie](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="6cdd8-215">Een grafiek segmenteren door dimensies</span><span class="sxs-lookup"><span data-stu-id="6cdd8-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="6cdd8-216">Als u een tabel met een tekenreekskolom en een numerieke kolom Hallo tekenreeks grafiek gebruikte toosplit Hallo numerieke gegevens in afzonderlijke reeks punten zijn kan.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="6cdd8-217">Als er meer dan een kolom met tekenreeksen, kunt u welke toouse kolom als Hallo-discriminator.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Een grafiek met segmenteren](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="6cdd8-219">Stuiteren snelheid</span><span class="sxs-lookup"><span data-stu-id="6cdd8-219">Bounce rate</span></span>

<span data-ttu-id="6cdd8-220">Een boolean tooa tekenreeks toouse converteren als discriminator:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="6cdd8-221">Meerdere metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="6cdd8-221">Display multiple metrics</span></span>
<span data-ttu-id="6cdd8-222">Als u een tabel met meer dan een numerieke kolom, in aanvulling toohello tijdstempel grafiek, kunt u een combinatie van beide weergeven.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Een grafiek met segmenteren](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="6cdd8-224">U moet selecteren **niet splitsen** voordat u kunt meerdere numerieke kolommen selecteren.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="6cdd8-225">U kunt niet splitsen door een kolom met tekenreeksen op Hallo dezelfde tijd als meer dan een numerieke kolom om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="6cdd8-226">Dagelijkse gemiddelde cyclus</span><span class="sxs-lookup"><span data-stu-id="6cdd8-226">Daily average cycle</span></span>
<span data-ttu-id="6cdd8-227">Hoe informatie over het gebruik variëren op Hallo gemiddelde dag?</span><span class="sxs-lookup"><span data-stu-id="6cdd8-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="6cdd8-228">Aantal aanvragen door Hallo tijd modulo één dag voor binned in uren:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-228">Count requests by hello time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Lijndiagram van uren in een gemiddelde dag](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="6cdd8-230">U ziet dat momenteel we tooconvert tijdsduur toodatetimes in volgorde toodisplay in een lijndiagram hebben.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="6cdd8-231">Meerdere dagelijkse reeksen vergelijken</span><span class="sxs-lookup"><span data-stu-id="6cdd8-231">Compare multiple daily series</span></span>
<span data-ttu-id="6cdd8-232">Hoe informatie over het gebruik variëren na verloop van tijd van de dag Hallo in andere landen?</span><span class="sxs-lookup"><span data-stu-id="6cdd8-232">How does usage vary over hello time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Gesplitste door client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="6cdd8-234">Tekenen van een distributiepunt</span><span class="sxs-lookup"><span data-stu-id="6cdd8-234">Plot a distribution</span></span>
<span data-ttu-id="6cdd8-235">Hoeveel sessies zijn er van verschillende lengtes?</span><span class="sxs-lookup"><span data-stu-id="6cdd8-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="6cdd8-236">de laatste regel Hallo is vereist tooconvert toodatetime.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="6cdd8-237">Momenteel wordt Hallo x-as van een grafiek weergegeven als een scalaire alleen als het een datum/tijd.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="6cdd8-238">Hallo `where` component eindresultaat sessies worden uitgesloten (sessionDuration == 0) en stelt de lengte van de x-as Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="6cdd8-239">Percentielen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="6cdd8-240">Welke bereiken van duur hebben betrekking op verschillende percentages van sessies?</span><span class="sxs-lookup"><span data-stu-id="6cdd8-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="6cdd8-241">Hallo hierboven query gebruiken, maar vervang Hallo laatste regel:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-241">Use hello above query, but replace hello last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="6cdd8-242">We ook verwijderd Hallo bovengrens in Hallo waar component, in volgorde tooget cijfers inclusief alle sessies met meer dan één verzoek corrigeren:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![Resultaat](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="6cdd8-244">Waaruit zien we dat:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-244">From which we can see that:</span></span>

* <span data-ttu-id="6cdd8-245">5% van sessies hebben een duur van minder dan 3 minuten 34s;</span><span class="sxs-lookup"><span data-stu-id="6cdd8-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="6cdd8-246">50% van sessies laatste minder dan 36 minuten;</span><span class="sxs-lookup"><span data-stu-id="6cdd8-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="6cdd8-247">5% van sessies laatste meer dan 7 dagen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="6cdd8-248">tooget een afzonderlijke verdeling voor elk land, we hebben zojuist toobring hello client_CountryOrRegion kolom afzonderlijk via beide geven een overzicht van operators:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="6cdd8-249">Koppelen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-249">Join</span></span>
<span data-ttu-id="6cdd8-250">We hebben toegang tot tooseveral tabellen, inclusief aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="6cdd8-251">toofind hello uitzonderingen gerelateerde tooa aanvraag die foutantwoord geretourneerd, kunnen we Hallo tabellen samenvoegen op `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="6cdd8-252">Het is raadzaam om toouse `project` tooselect alleen Hallo kolommen we voordat u uitvoert moeten Hallo join.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="6cdd8-253">In Hallo dezelfde componenten we Hallo timestamp-kolom wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="6cdd8-254">[Laat](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): een resultaat tooa variabele toewijzen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="6cdd8-255">Gebruik `let` tooseparate Hallo delen van vorige Hallo-expressie.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="6cdd8-256">Hallo resultaten zijn niet gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="6cdd8-257">Plaats geen lege regels tussen de onderdelen van Hallo query Hallo Hallo Analytics-client.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="6cdd8-258">Zorg ervoor dat tooexecute hiervan.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="6cdd8-259">Gebruik `toscalar` tooconvert één tabel tooa celwaarde:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="6cdd8-260">Functies</span><span class="sxs-lookup"><span data-stu-id="6cdd8-260">Functions</span></span>

<span data-ttu-id="6cdd8-261">Gebruik *laten* toodefine een functie:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="6cdd8-262">Het openen van geneste objecten</span><span class="sxs-lookup"><span data-stu-id="6cdd8-262">Accessing nested objects</span></span>
<span data-ttu-id="6cdd8-263">Geneste objecten gemakkelijk toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="6cdd8-264">Bijvoorbeeld in Hallo uitzonderingen stroom ziet u gestructureerde objecten als volgt:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![Resultaat](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="6cdd8-266">U kunt deze afvlakken door te kiezen Hallo eigenschappen die u geïnteresseerd bent in:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="6cdd8-267">Houd er rekening mee dat u nodig hebt toocast hello toohello juiste resultaattype.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="6cdd8-268">Aangepaste eigenschappen en metingen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-268">Custom properties and measurements</span></span>
<span data-ttu-id="6cdd8-269">Als uw toepassing koppelt [aangepaste dimensies (eigenschappen) en aangepaste metingen](app-insights-api-custom-events-metrics.md#properties) tooevents en vervolgens worden deze weergegeven in Hallo `customDimensions` en `customMeasurements` objecten.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="6cdd8-270">Bijvoorbeeld, als uw app bevat:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="6cdd8-271">tooextract deze waarden in Analytics:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="6cdd8-272">tooverify of een aangepaste dimensie is van een bepaald type:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="6cdd8-273">Dashboards</span><span class="sxs-lookup"><span data-stu-id="6cdd8-273">Dashboards</span></span>
<span data-ttu-id="6cdd8-274">U kunt uw resultaten tooa dashboard in volgorde toobring samen vastmaken uw belangrijkste grafieken en tabellen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="6cdd8-275">[Azure gedeelde dashboard](app-insights-dashboards.md#share-dashboards): klik op het Punaisepictogram Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="6cdd8-276">Voordat u dit doet, moet u een gedeelde dashboard hebben.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="6cdd8-277">Open in hello Azure-portal, of een dashboard maken en klikt u op delen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="6cdd8-278">[Power BI-dashboard](app-insights-export-power-bi.md): klik op exporteren, Power BI Query.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="6cdd8-279">Een voordeel van dit alternatief is dat u uw query samen met andere resultaten van een breed scala van gegevensbronnen kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="6cdd8-280">Gecombineerd met de geïmporteerde gegevens</span><span class="sxs-lookup"><span data-stu-id="6cdd8-280">Combine with imported data</span></span>

<span data-ttu-id="6cdd8-281">Analytics-rapporten perfect op Hallo dashboard, maar soms wilt u tootranslate Hallo gegevens tooa meer digestible formulier.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="6cdd8-282">Stel bijvoorbeeld dat uw geverifieerde gebruikers worden geïdentificeerd in Hallo telemetrie door een alias.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="6cdd8-283">U wilt de namen van hun real tooshow in de resultaten.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="6cdd8-284">toodo, moet u een CSV-bestand dat kan worden toegewezen uit Hallo aliassen toohello echte namen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="6cdd8-285">U kunt een bestand importeren en gebruiken net als standaardtabellen hello (aanvragen, uitzonderingen, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="6cdd8-286">U kunt deze query uitvoeren op een eigen of deel hieraan met andere tabellen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="6cdd8-287">Bijvoorbeeld, als u een tabel met de naam usermap hebt en er kolommen `realName` en `userId`, kunt u deze tootranslate hello `user_AuthenticatedId` veld Hallo-aanvraagtelemetrie:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="6cdd8-288">een tabel, Hallo Schema blade tooimport onder **andere gegevensbronnen**, volg Hallo instructies tooadd een nieuwe gegevensbron door het uploaden van een steekproef van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="6cdd8-289">Vervolgens kunt u deze definitie tooupload tabellen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="6cdd8-290">Hallo import-functie is momenteel in preview zodat aanvankelijk ziet u een koppeling 'Contact met ons opnemen' onder "Andere gegevensbronnen."</span><span class="sxs-lookup"><span data-stu-id="6cdd8-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="6cdd8-291">Gebruik deze toosign toohello preview-programma en Hallo koppeling vervolgens worden vervangen door een knop 'Een nieuwe gegevensbron toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="6cdd8-292">Tabellen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-292">Tables</span></span>
<span data-ttu-id="6cdd8-293">Hallo-stroom ontvangen van uw app telemetrie is toegankelijk via verschillende tabellen.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="6cdd8-294">Hallo-schema van de eigenschappen die beschikbaar zijn voor elke tabel is Hallo links in Hallo-venster zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="6cdd8-295">Tabel aanvragen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-295">Requests table</span></span>
<span data-ttu-id="6cdd8-296">Aantal HTTP-aanvragen tooyour web-app en het segment met de paginanaam:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Aantal aanvragen gesegmenteerd op naam](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="6cdd8-298">Hallo-aanvragen die niet voldoen aan de meeste zoeken:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-298">Find hello requests that fail most:</span></span>

![Aantal aanvragen gesegmenteerd op naam](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="6cdd8-300">Aangepaste gebeurtenissentabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-300">Custom events table</span></span>
<span data-ttu-id="6cdd8-301">Als u [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend uw eigen gebeurtenissen, kunt u ze lezen uit deze tabel.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="6cdd8-302">We nemen een voorbeeld waarin uw app-code deze regels bevat:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="6cdd8-303">Hallo frequentie van deze gebeurtenissen worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-303">Display hello frequency of these events:</span></span>

![Aantal aangepaste gebeurtenissen weergeven](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="6cdd8-305">Pak metingen en dimensies van Hallo gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-305">Extract measurements and dimensions from hello events:</span></span>

![Aantal aangepaste gebeurtenissen weergeven](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="6cdd8-307">Tabel met aangepaste metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="6cdd8-307">Custom metrics table</span></span>
<span data-ttu-id="6cdd8-308">Als u [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend uw eigen metrische waarden vindt u de resultaten in Hallo **customMetrics** stroom.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="6cdd8-309">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-309">For example:</span></span>  

![Aangepaste metrische gegevens in Application Insights analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="6cdd8-311">In [Metrics Explorer](app-insights-metrics-explorer.md), alle aangepaste metingen gekoppelde tooany type telemetrie samen voorkomen in Hallo metrische gegevens blade samen met metrische gegevens die zijn verzonden met behulp van `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="6cdd8-312">Maar in Analytics, aangepaste metingen zijn nog steeds gekoppeld toowhichever type telemetrie ze werden uitgevoerd op - gebeurtenissen of aanvragen, enzovoort -terwijl metrische gegevens die zijn verzonden door TrackMetric worden weergegeven in hun eigen stroom.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="6cdd8-313">Prestaties tellers tabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-313">Performance counters table</span></span>
<span data-ttu-id="6cdd8-314">[Prestatiemeteritems](app-insights-performance-counters.md) u basissysteem metrische gegevens voor uw app, zoals CPU, geheugen, weergeven en netwerkgebruik.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="6cdd8-315">U kunt Hallo SDK toosend aanvullende prestatiemeteritems, met inbegrip van uw eigen aangepaste items configureren.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="6cdd8-316">Hallo **performanceCounters** schema beschrijft Hallo `category`, `counter` naam, en `instance` naam van elk prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="6cdd8-317">Namen van exemplaren zijn alleen van toepassing toosome prestatiemeteritems en geven doorgaans aan Hallo naam van het Hallo proces toowhich Hallo aantal is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="6cdd8-318">Hallo telemetrie voor elke toepassing ziet u alleen Hallo items voor die toepassing.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="6cdd8-319">Bijvoorbeeld: toosee welke items zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-319">For example, toosee what counters are available:</span></span>

![Prestatiemeters in Application Insights analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="6cdd8-321">een grafiek van het beschikbare geheugen over Hallo tooget periode geselecteerd:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-321">tooget a chart of available memory over hello selected period:</span></span>

![Geheugen timechart in Application Insights analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="6cdd8-323">Zoals u andere telemetrie **performanceCounters** heeft ook een kolom `cloud_RoleInstance` die aangeeft dat de identiteit Hallo van Hallo hostcomputer waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="6cdd8-324">Bijvoorbeeld: toocompare Hallo prestaties van uw app op verschillende computers Hallo:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Prestaties gesegmenteerd op rolinstantie in Application Insights analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="6cdd8-326">Uitzonderingentabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-326">Exceptions table</span></span>
<span data-ttu-id="6cdd8-327">[Uitzonderingen die zijn gerapporteerd door uw app](app-insights-asp-net-exceptions.md) zijn beschikbaar in deze tabel.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="6cdd8-328">toofind Hallo HTTP-aanvraag die uw app is verwerkt wanneer Hallo uitzondering is gegenereerd, operation_Id koppelen:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Uitzonderingen met aanvragen operation_Id koppelen](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="6cdd8-330">Browser tijdsinstellingen tabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-330">Browser timings table</span></span>
<span data-ttu-id="6cdd8-331">`browserTimings`toont de pagina laden gegevens verzameld in browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="6cdd8-332">[Instellen van uw app voor clientzijde telemetrie](app-insights-javascript.md) in volgorde toosee deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="6cdd8-333">Hallo-schema bevat [metrische gegevens die wijzen op Hallo lengten van verschillende fasen van Hallo pagina laadproces](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="6cdd8-334">(Ze niet duiden op Hallo tijdsduur die uw gebruikers een pagina lezen.)</span><span class="sxs-lookup"><span data-stu-id="6cdd8-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="6cdd8-335">Hallo popularities van verschillende pagina's weergeven en tijden voor elke pagina te laden:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Laadtijden voor pagina's in Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="6cdd8-337">Tabel met resultaten beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="6cdd8-337">Availability results table</span></span>
<span data-ttu-id="6cdd8-338">`availabilityResults`toont Hallo resultaten van uw [webtests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="6cdd8-339">Elke uitvoering van uw tests vanaf elke testlocatie wordt afzonderlijk gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-339">Each run of your tests from each test location is reported separately.</span></span>

![Laadtijden voor pagina's in Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="6cdd8-341">Afhankelijkheden tabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-341">Dependencies table</span></span>
<span data-ttu-id="6cdd8-342">Resultaten van aanroepen bevat dat uw app toodatabases en REST-API's en andere maakt tooTrackDependency() aanroept.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="6cdd8-343">Tevens AJAX-aanroepen vanuit de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="6cdd8-344">AJAX-aanroepen vanuit de browser Hallo:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="6cdd8-345">Afhankelijkheidsaanroepen van Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="6cdd8-346">Serverzijde afhankelijkheid resultaten altijd weergeven `success==False` als hello Application Insights-Agent niet is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="6cdd8-347">Echter zijn hello andere gegevens juist.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="6cdd8-348">Traceringen tabel</span><span class="sxs-lookup"><span data-stu-id="6cdd8-348">Traces table</span></span>
<span data-ttu-id="6cdd8-349">Hallo telemetrie verzonden door uw app met TrackTrace(), bevat of [andere frameworks voor logboekregistratie](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6cdd8-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="6cdd8-350">Video</span><span class="sxs-lookup"><span data-stu-id="6cdd8-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="6cdd8-351">Geavanceerde query's:</span><span class="sxs-lookup"><span data-stu-id="6cdd8-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="6cdd8-352">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cdd8-352">Next steps</span></span>
* [<span data-ttu-id="6cdd8-353">Naslaggids voor Analytics</span><span class="sxs-lookup"><span data-stu-id="6cdd8-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="6cdd8-354">[SQL-gebruikers cheats blad](https://aka.ms/sql-analytics) Hallo meest voorkomende idioms vertaalt.</span><span class="sxs-lookup"><span data-stu-id="6cdd8-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
