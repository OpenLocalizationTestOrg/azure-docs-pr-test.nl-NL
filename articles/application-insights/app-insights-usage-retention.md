---
title: analyse van de aaaUser bewaren voor webtoepassingen met Azure Application Insights | Microsoft docs
description: Hoeveel gebruikers retourneren tooyour app?
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="d946e-103">Analyse van de gebruiker bewaren voor webtoepassingen met Application Insights</span><span class="sxs-lookup"><span data-stu-id="d946e-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="d946e-104">Hallo bewaren functie in [Azure Application Insights](app-insights-overview.md) helpt u hoeveel gebruikers analyseren retourneren tooyour app, en hoe vaak ze bepaalde taken uitvoeren of deze doelstellingen te bereiken.</span><span class="sxs-lookup"><span data-stu-id="d946e-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="d946e-105">Als u een game site uitvoert, kan u bijvoorbeeld Hallo aantallen gebruikers die toohello site na het verlies van een game met Hallo getal retourneren en nadat winnen retourneren vergelijken.</span><span class="sxs-lookup"><span data-stu-id="d946e-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="d946e-106">Deze informatie kunt u zowel uw gebruikerservaring en de bedrijfsstrategie verbeteren.</span><span class="sxs-lookup"><span data-stu-id="d946e-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="d946e-107">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="d946e-107">Get started</span></span>

<span data-ttu-id="d946e-108">Als er geen gegevens in Hallo bewaren hulpprogramma in de Application Insights-portal Hallo nog [meer informatie over hoe tooget gestart met gebruik van hulpprogramma's voor Hallo](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d946e-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="d946e-109">Hallo bewaren hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="d946e-109">hello Retention tool</span></span>

![Retentie-informatie](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="d946e-111">Hallo werkbalk kan gebruikers de nieuwe bewaarperiode rapporten toocreate, bestaande bewaren rapporten openen, huidige bewaren rapport opslaan of opslaan als, wijzigingen toosaved rapporten herstellen, gegevens op Hallo rapport, delen via e-mail of directe koppeling en toegang Hallo vernieuwen pagina met documentatie.</span><span class="sxs-lookup"><span data-stu-id="d946e-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="d946e-112">Standaard bevat bewaren alle gebruikers die u hebt vervolgens terug documentatie en iets anders heeft gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="d946e-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="d946e-113">U kunt andere combinatie van gebeurtenissen toonarrow Hallo concentreren op specifieke gebruikersactiviteiten selecteren.</span><span class="sxs-lookup"><span data-stu-id="d946e-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="d946e-114">Een of meer filters toevoegen op Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d946e-114">Add one or more filters on properties.</span></span> <span data-ttu-id="d946e-115">Bijvoorbeeld, kunt u zich richten op gebruikers in een bepaald land of regio.</span><span class="sxs-lookup"><span data-stu-id="d946e-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="d946e-116">Klik op **Update** na het Hallo-filters instellen.</span><span class="sxs-lookup"><span data-stu-id="d946e-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="d946e-117">Hallo algehele bewaren diagram toont een overzicht van de gebruiker bewaren op Hallo geselecteerde periode.</span><span class="sxs-lookup"><span data-stu-id="d946e-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="d946e-118">Hallo raster toont Hallo aantal gebruikers volgens toohello opbouwfunctie voor query's in #2 bewaard.</span><span class="sxs-lookup"><span data-stu-id="d946e-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="d946e-119">Vertegenwoordigt een cohort van gebruikers die een gebeurtenis uitgevoerd in de Hallo tijd weergegeven van elke rij.</span><span class="sxs-lookup"><span data-stu-id="d946e-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="d946e-120">Elke cel in rij Hallo bevat ten minste eenmaal in een latere periode hoeveel die cohort geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d946e-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="d946e-121">Sommige gebruikers mogelijk geretourneerd uit meer dan één periode.</span><span class="sxs-lookup"><span data-stu-id="d946e-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="d946e-122">Hallo insights kaarten weergeven bovenste vijf gang worden gezet gebeurtenissen en bovenste vijf geretourneerd gebeurtenissen toogive gebruikers een beter begrip van de retentie-rapport.</span><span class="sxs-lookup"><span data-stu-id="d946e-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Bewaartermijn muis aanwijzen](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="d946e-124">Gebruikers kunnen de muisaanwijzer cellen op Hallo bewaren hulpprogramma tooaccess Hallo analytics-knop en knopinfo waarin wordt uitgelegd welke cel Hallo betekent.</span><span class="sxs-lookup"><span data-stu-id="d946e-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="d946e-125">Hallo Analytics-knop gaat gebruikers toohello Analytics hulpprogramma met een vooraf ingestelde query toogenerate gebruikers uit Hallo cel.</span><span class="sxs-lookup"><span data-stu-id="d946e-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="d946e-126">Gebruik van zakelijke gebeurtenissen tootrack bewaren</span><span class="sxs-lookup"><span data-stu-id="d946e-126">Use business events tootrack retention</span></span>

<span data-ttu-id="d946e-127">tooget hello nuttigst bewaren analyse, meting gebeurtenissen waarbij aanzienlijke zakelijke activiteiten.</span><span class="sxs-lookup"><span data-stu-id="d946e-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="d946e-128">Bijvoorbeeld: veel gebruikers mogelijk open een pagina in uw app zonder Hallo spel die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d946e-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="d946e-129">NET Hallo paginaweergaven bijhouden, zou een onnauwkeurige schatting maken van hoeveel mensen tooplay Hallo game retourneren na eerder genieten daarom bieden.</span><span class="sxs-lookup"><span data-stu-id="d946e-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="d946e-130">tooget duidelijk beeld van de spelers, moet uw app een aangepaste gebeurtenis wanneer een gebruiker daadwerkelijk speelt verzenden.</span><span class="sxs-lookup"><span data-stu-id="d946e-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="d946e-131">Het is raadzaam om aangepaste gebeurtenissen toocode die dit beleid gebruiken voor het bewaren van analyse en acties van de belangrijkste zakelijke vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="d946e-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="d946e-132">toocapture hello game resultaat, moet u een line-of code toosend een aangepaste gebeurtenis tooApplication Insights toowrite.</span><span class="sxs-lookup"><span data-stu-id="d946e-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="d946e-133">Als u deze in Hallo webpagina code of in Node.JS schrijft, als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="d946e-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="d946e-134">Of in de servercode ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d946e-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="d946e-135">[Meer informatie over het schrijven van aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="d946e-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d946e-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d946e-136">Next steps</span></span>
- <span data-ttu-id="d946e-137">Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="d946e-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="d946e-138">Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d946e-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="d946e-139">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="d946e-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="d946e-140">Trechters</span><span class="sxs-lookup"><span data-stu-id="d946e-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="d946e-141">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="d946e-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="d946e-142">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="d946e-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="d946e-143">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="d946e-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


