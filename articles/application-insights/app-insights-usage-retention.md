---
title: Analyse van de gebruiker bewaren voor webtoepassingen met Azure Application Insights | Microsoft docs
description: Hoeveel gebruikers terug naar uw app?
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="250ce-103">Analyse van de gebruiker bewaren voor webtoepassingen met Application Insights</span><span class="sxs-lookup"><span data-stu-id="250ce-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="250ce-104">De functie bewaren in [Azure Application Insights](app-insights-overview.md) helpt u hoeveel gebruikers terug naar uw app en hoe vaak ze bepaalde taken uitvoeren of bereiken van doelen analyseren.</span><span class="sxs-lookup"><span data-stu-id="250ce-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="250ce-105">Als u een game site uitvoert, kan u bijvoorbeeld de aantallen gebruikers die terug naar de site na het verlies van een game met het nummer en nadat winnen retourneren vergelijken.</span><span class="sxs-lookup"><span data-stu-id="250ce-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="250ce-106">Deze informatie kunt u zowel uw gebruikerservaring en de bedrijfsstrategie verbeteren.</span><span class="sxs-lookup"><span data-stu-id="250ce-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="250ce-107">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="250ce-107">Get started</span></span>

<span data-ttu-id="250ce-108">Als er geen gegevens in het hulpprogramma bewaren in de Application Insights-portal nog [informatie over het aan de slag met het gebruik van hulpprogramma's voor](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="250ce-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="250ce-109">Het hulpprogramma bewaren</span><span class="sxs-lookup"><span data-stu-id="250ce-109">The Retention tool</span></span>

![Retentie-informatie](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="250ce-111">De werkbalk kan gebruikers maken van nieuwe bewaren, bestaande bewaren rapporten openen, huidige bewaren rapport opslaan of niet opslaan omdat wijzigingen aangebracht in de opgeslagen rapporten terug te draaien, gegevens in het rapport te vernieuwen, rapport via e-mail of directe koppeling te delen en toegang de documentatie tot pagina.</span><span class="sxs-lookup"><span data-stu-id="250ce-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="250ce-112">Standaard bevat bewaren alle gebruikers die u hebt vervolgens terug documentatie en iets anders heeft gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="250ce-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="250ce-113">U kunt andere combinatie van gebeurtenissen naar toespitsen op specifieke gebruikersactiviteiten selecteren.</span><span class="sxs-lookup"><span data-stu-id="250ce-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="250ce-114">Een of meer filters toevoegen op Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="250ce-114">Add one or more filters on properties.</span></span> <span data-ttu-id="250ce-115">Bijvoorbeeld, kunt u zich richten op gebruikers in een bepaald land of regio.</span><span class="sxs-lookup"><span data-stu-id="250ce-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="250ce-116">Klik op **Update** na het instellen van de filters.</span><span class="sxs-lookup"><span data-stu-id="250ce-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="250ce-117">De algehele bewaren grafiek bevat een overzicht van de gebruiker bewaren in de geselecteerde periode.</span><span class="sxs-lookup"><span data-stu-id="250ce-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="250ce-118">Het raster toont het aantal gebruikers dat volgens de opbouwfunctie voor query's in #2 wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="250ce-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="250ce-119">Elke rij vertegenwoordigt een cohort van gebruikers die een gebeurtenis in de weergegeven tijd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="250ce-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="250ce-120">Elke cel in de rij bevat ten minste eenmaal in een latere periode hoeveel die cohort geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="250ce-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="250ce-121">Sommige gebruikers mogelijk geretourneerd uit meer dan één periode.</span><span class="sxs-lookup"><span data-stu-id="250ce-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="250ce-122">De kaarten insights weergeven bovenste vijf gang worden gezet en bovenste vijf geretourneerde gebeurtenissen om gebruikers een beter begrip van de retentie-rapport</span><span class="sxs-lookup"><span data-stu-id="250ce-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Bewaartermijn muis aanwijzen](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="250ce-124">Gebruikers kunnen de muisaanwijzer cellen in het hulpprogramma bewaren voor toegang tot het analytics-knop en knopinfo zijn waarin wordt uitgelegd wat de cel betekent.</span><span class="sxs-lookup"><span data-stu-id="250ce-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="250ce-125">De knop Analytics, kunnen gebruikers voor het Analytics-hulpprogramma met een vooraf ingestelde query voor het genereren van gebruikers van de cel.</span><span class="sxs-lookup"><span data-stu-id="250ce-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="250ce-126">Gebruik zakelijke gebeurtenissen bijhouden bewaren</span><span class="sxs-lookup"><span data-stu-id="250ce-126">Use business events to track retention</span></span>

<span data-ttu-id="250ce-127">Als u de nuttigste retentie-analyse, meten gebeurtenissen waarbij aanzienlijke zakelijke activiteiten.</span><span class="sxs-lookup"><span data-stu-id="250ce-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="250ce-128">Bijvoorbeeld: veel gebruikers mogelijk open een pagina in uw app zonder het spel dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="250ce-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="250ce-129">Alleen de paginaweergaven bijhouden, zou een onnauwkeurige schatting maken van hoeveel mensen terugkeren om in te spelen na eerder genieten daarom bieden.</span><span class="sxs-lookup"><span data-stu-id="250ce-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="250ce-130">Als u een duidelijk beeld van spelers retourneren, moet uw app een aangepaste gebeurtenis wanneer een gebruiker daadwerkelijk speelt verzenden.</span><span class="sxs-lookup"><span data-stu-id="250ce-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="250ce-131">Het is raadzaam om aangepaste gebeurtenissen die belangrijke zakelijke acties vertegenwoordigt code en dit beleid gebruiken voor uw analyse bewaren.</span><span class="sxs-lookup"><span data-stu-id="250ce-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="250ce-132">Voor het vastleggen van de game uitkomst, moet u een regel van een aangepaste gebeurtenis verzenden naar Application Insights-code schrijven.</span><span class="sxs-lookup"><span data-stu-id="250ce-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="250ce-133">Als u deze in de code van de webpagina's of in Node.JS schrijft, als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="250ce-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="250ce-134">Of in de servercode ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="250ce-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="250ce-135">[Meer informatie over het schrijven van aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="250ce-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="250ce-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="250ce-136">Next steps</span></span>
- <span data-ttu-id="250ce-137">Om in te schakelen ervaringen gebruik, beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="250ce-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="250ce-138">Als u al aangepaste gebeurtenissen of paginaweergaven verzendt, gebruik de informatie over het gebruik hulpprogramma's voor meer informatie over hoe gebruikers gebruiken voor uw service.</span><span class="sxs-lookup"><span data-stu-id="250ce-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="250ce-139">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="250ce-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="250ce-140">Trechters</span><span class="sxs-lookup"><span data-stu-id="250ce-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="250ce-141">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="250ce-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="250ce-142">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="250ce-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="250ce-143">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="250ce-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


