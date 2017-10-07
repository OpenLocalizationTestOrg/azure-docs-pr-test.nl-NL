---
title: analyse van aaaUsage voor webtoepassingen met Azure Application Insights | Microsoft docs
description: Begrijp uw gebruikers- en wat ze doen met uw web-app.
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="0ac6f-103">Gebruiksanalyse voor webtoepassingen met Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ac6f-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="0ac6f-104">Welke functies van uw web-app zijn het meest populaire?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="0ac6f-105">Voer uw gebruikers hun doelstellingen met uw app controles?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="0ac6f-106">Ze niet verwijderen uit op bepaalde tijdstippen en ze kom later terug?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="0ac6f-107">[Azure Application Insights](app-insights-overview.md) kunt u krachtige inzicht in hoe mensen uw web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="0ac6f-108">Telkens wanneer u uw app bijwerkt, kunt u beoordelen hoe goed werkt voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="0ac6f-109">Met deze kennis, kunt u gegevensgestuurde nemen van beslissingen over de volgende ontwikkelingscycli.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="0ac6f-110">Verzend telemetrie vanuit uw app</span><span class="sxs-lookup"><span data-stu-id="0ac6f-110">Send telemetry from your app</span></span>

<span data-ttu-id="0ac6f-111">de beste ervaring Hello wordt verkregen door het installeren van Application Insights in uw servercode app, en in uw webpagina's.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="0ac6f-112">Hallo-client- en serveronderdelen van uw app verzenden telemetrie back toohello Azure-portal voor analyse.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="0ac6f-113">**Servercode:** installeren Hallo juiste-module voor uw [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), of [andere](app-insights-platforms.md) app.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="0ac6f-114">*Niet wilt dat servercode tooinstall? NET [een Azure Application Insights-resource maken](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="0ac6f-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="0ac6f-115">**Code webpagina:** Open Hallo [Azure-portal](https://portal.azure.com), Hallo Application Insights-resource voor uw app openen en open vervolgens **aan de slag > bewaken en onderzoeken van Client-Side**.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Hallo script naar Hallo hoofd van uw hoofdwebpagina kopiëren.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="0ac6f-117">**Telemetrie ophalen:** uw project in de foutopsporingsmodus uitvoeren voor een paar minuten en zoek naar resulteert in het Hallo-overzichtsblade in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="0ac6f-118">Publiceren van uw app toomonitor prestaties van uw app en weten wat uw gebruikers met uw app doen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="0ac6f-119">Gebruikers- en sessie-ID opnemen in uw telemetrie</span><span class="sxs-lookup"><span data-stu-id="0ac6f-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="0ac6f-120">tootrack gebruikers gedurende een bepaalde periode, Application Insights vereist een tooidentify manier ze.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="0ac6f-121">Hallo gebeurtenissen hulpprogramma is Hallo enige informatie over het gebruik hulpprogramma dat hoeft niet een gebruikers-ID of een sessie-ID.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="0ac6f-122">Beginnen met het verzenden van deze id's [hier](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="0ac6f-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="0ac6f-123">Gebruik demografische gegevens en statistieken verkennen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="0ac6f-124">Weten wanneer mensen uw app gebruikt, welke pagina's die ze zijn het meest geïnteresseerd, waar uw gebruikers zich bevinden, welke browsers en besturingssystemen die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="0ac6f-125">Hallo-gebruikers en sessies rapporten filter uw gegevens door's of aangepaste gebeurtenissen en ze segmenteren door eigenschappen zoals locatie-omgeving en pagina.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="0ac6f-126">U kunt ook uw eigen filters toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-126">You can also add your own filters.</span></span>

![Gebruikers](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="0ac6f-128">Inzichten op Hallo rechts wijst interessante patronen in Hallo reeks gegevens.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="0ac6f-129">Hallo **gebruikers** rapport telt het aantal unieke gebruikers die toegang hebben tot uw pagina's binnen uw gekozen perioden Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="0ac6f-130">(Gebruikers worden geteld met behulp van cookies.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="0ac6f-131">Als iemand toegang heeft tot uw site met verschillende browsers of clientcomputers, of hun cookies worden gewist en vervolgens wordt meer dan één keer worden geteld.)</span><span class="sxs-lookup"><span data-stu-id="0ac6f-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="0ac6f-132">Hallo **sessies** rapport telt Hallo aantal gebruikerssessies die toegang uw site tot.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="0ac6f-133">Een sessie is een periode van de activiteit van een gebruiker, gevolgd door een periode van inactiviteit van meer dan half uur.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="0ac6f-134">Meer informatie over gebruikers, sessies en gebeurtenissen Hallo-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="0ac6f-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="0ac6f-135">Paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="0ac6f-135">Page views</span></span>

<span data-ttu-id="0ac6f-136">Hallo gebruik blade doorklikken Hallo paginaweergaven tegel tooget een uitsplitsing van de meest populaire's:</span><span class="sxs-lookup"><span data-stu-id="0ac6f-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Overzichtsblade hello, klik op Hallo pagina weergaven grafiek](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="0ac6f-138">Hallo in bovenstaand voorbeeld is van een website games.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-138">hello example above is from a games web site.</span></span> <span data-ttu-id="0ac6f-139">Van Hallo grafieken ziet onmiddellijk:</span><span class="sxs-lookup"><span data-stu-id="0ac6f-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="0ac6f-140">Gebruik niet is verbeterd in Hallo afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="0ac6f-141">Mogelijk moet u bedenken Zoekmachineoptimalisatie?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="0ac6f-142">Tennis is de meest populaire game pagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="0ac6f-143">Laten we de nadruk gelegd op verdere verbeteringen toothis pagina.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="0ac6f-144">Gemiddeld bezoeken gebruikers Hallo Tennis drie keer per week.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="0ac6f-145">(Er zijn drie keer meer sessies dan gebruikers).</span><span class="sxs-lookup"><span data-stu-id="0ac6f-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="0ac6f-146">De meeste gebruikers bezoeken Hallo Hallo VS werkende week, en met werkuren.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="0ac6f-147">Misschien bieden we een knop 'snel verbergen' op Hallo-webpagina.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="0ac6f-148">Hallo [aantekeningen](app-insights-annotations.md) op Hallo grafiek weergeven wanneer nieuwe versies van het Hallo-website zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="0ac6f-149">Geen recente implementaties Hallo had een merkbare invloed op de informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="0ac6f-150">Wat gebeurt er als u wilt dat tooinvestigate Hallo verkeer tooyour site in meer detail, zoals de splitsing door een aangepaste eigenschap die in de telemetrie van paginaweergaven uw site stuurt?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="0ac6f-151">Open Hallo **gebeurtenissen** hulpprogramma in het menu Hallo Application Insights-bron.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="0ac6f-152">Dit hulpprogramma kunt u het aantal paginaweergaven en aangepaste gebeurtenissen is verzonden vanaf uw app, op basis van tal van opties voor filteren, cohorting en segmentering analyseren.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="0ac6f-153">Selecteer in de vervolgkeuzelijst "Wie gebruikt" Hallo, 'Any paginaweergave'.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="0ac6f-154">Selecteer in de vervolgkeuzelijst 'Gesplitste door' hello een eigenschap door welke toosplit uw pagina telemetrie weergeven.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="0ac6f-155">Bewaartermijn - hoeveel gebruikers terugkeren?</span><span class="sxs-lookup"><span data-stu-id="0ac6f-155">Retention - how many users come back?</span></span>

<span data-ttu-id="0ac6f-156">Bewaartermijn helpt u begrijpen hoe vaak uw gebruikers retourneren toouse hun app op basis van cohorten van gebruikers die een bepaalde actie business tijdens een bepaald tijdsinterval uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="0ac6f-157">Inzicht in welke specifieke functies ervoor zorgen dat gebruikers toocome back meer dan andere</span><span class="sxs-lookup"><span data-stu-id="0ac6f-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="0ac6f-158">Formulier hypothesen op basis van echte gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="0ac6f-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="0ac6f-159">Bepalen of bewaarperiode een probleem is met uw product is</span><span class="sxs-lookup"><span data-stu-id="0ac6f-159">Determine whether retention is a problem in your product</span></span> 

![Bewaartermijn](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="0ac6f-161">Hallo bewaren besturingselementen op de voorgrond kunt u toodefine specifieke gebeurtenissen en het tijdstip bereik toocalculate bewaren.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="0ac6f-162">Hallo grafiek in het midden Hallo biedt een visuele representatie van Hallo algehele bewaren percentage Hallo tijdbereik opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="0ac6f-163">Hallo-grafiek aan de onderkant Hallo vertegenwoordigt afzonderlijke bewaren in een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="0ac6f-164">Dit detailniveau kunt u toounderstand wat uw gebruikers doen en wat van invloed kunnen zijn op de bestaande gebruikers op een meer gedetailleerde granulatie.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="0ac6f-165">Meer informatie over het hulpprogramma voor het bewaren van Hallo</span><span class="sxs-lookup"><span data-stu-id="0ac6f-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="0ac6f-166">Aangepaste zakelijke gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-166">Custom business events</span></span>

<span data-ttu-id="0ac6f-167">tooget een duidelijk beeld krijgt van wat gebruikers doen met uw web-app, is het nuttig tooinsert regels code toolog aangepaste gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="0ac6f-168">Deze gebeurtenissen kunnen alles volgen op gedetailleerde gebruikersacties zoals specifieke knoppen toomore aanzienlijke zakelijke gebeurtenissen zoals tot aanschaf overgaat of een ronde winnen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="0ac6f-169">Hoewel in sommige gevallen paginaweergaven nuttige gebeurtenissen vertegenwoordigen kunnen, is het niet de waarde true in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="0ac6f-170">Een gebruiker kan een productpagina openen zonder Hallo product kopen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="0ac6f-171">Met specifieke zakelijke gebeurtenissen, kunt u uw gebruikers voortgang grafiekgebied via uw site.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="0ac6f-172">U kunt achterhalen van de voorkeuren voor de verschillende opties en wanneer ze drop out- of problemen hebt.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="0ac6f-173">Met deze kennis kunt u weloverwogen beslissingen over Hallo prioriteiten in uw achterstand ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="0ac6f-174">Gebeurtenissen kunnen worden vastgelegd in Hallo webpagina:</span><span class="sxs-lookup"><span data-stu-id="0ac6f-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="0ac6f-175">Of in Hallo servergedeelte van Hallo web-app:</span><span class="sxs-lookup"><span data-stu-id="0ac6f-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="0ac6f-176">U kunt eigenschap waarden toothese gebeurtenissen koppelen zodat u kunt filteren of Hallo gebeurtenissen wanneer u ze in de portal Hallo inspecteert splitsen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="0ac6f-177">Bovendien is een standaardset eigenschappen gekoppelde tooeach gebeurtenis, zoals anonieme gebruikers-ID, zodat u tootrace Hallo volgorde van activiteiten van een afzonderlijke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="0ac6f-178">Meer informatie over [aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md#trackevent) en [eigenschappen](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="0ac6f-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="0ac6f-179">Opdelen gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-179">Slice and dice events</span></span>

<span data-ttu-id="0ac6f-180">U kunt in Hallo gebruikers, sessies en gebeurtenissen's segmenteren en aangepaste gebeurtenissen door de gebruiker, de gebeurtenisnaam van de en eigenschappen te analyseren.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="0ac6f-181">![Gebruikers](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="0ac6f-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="0ac6f-182">Hallo telemetrie met Hallo app ontwerpen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="0ac6f-183">Tijdens het ontwerpen van elk onderdeel van uw app, overweeg dan hoe u gaat toomeasure de succes met uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="0ac6f-184">Bepaal wat zakelijke gebeurtenissen u toorecord nodig hebt en code aanroepen voor deze gebeurtenissen bijhouden in uw app uit Hallo Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="0ac6f-185">EEN | B-tests</span><span class="sxs-lookup"><span data-stu-id="0ac6f-185">A | B Testing</span></span>
<span data-ttu-id="0ac6f-186">Als u niet welke variant van een functie wel meer gemaakt weet, laat u beide parameters, waardoor elke gebruikers toegankelijk toodifferent.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="0ac6f-187">Hallo succes van elke meten en verplaats tooa uniforme versie.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="0ac6f-188">Voor deze methode, moet u afzonderlijke eigenschap waarden tooall Hallo telemetrie die is verzonden door elke versie van uw app koppelen.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="0ac6f-189">U kunt dit doen door de eigenschappen definiëren in Hallo active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="0ac6f-190">Deze standaardeigenschappen worden toegevoegd aan de tooevery telemetrie message die toepassing hello verzendt - niet alleen uw aangepaste berichten, maar ook in standaard telemetrie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="0ac6f-191">Filteren en uw gegevens op Hallo van eigenschapswaarden, dus als verschillende versies van toocompare Hallo splitsen in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="0ac6f-192">toodo, [instellen van een initialisatiefunctie telemetrie](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="0ac6f-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="0ac6f-193">In de web-app initialisatiefunctie Hallo zoals Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="0ac6f-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="0ac6f-194">Alle nieuwe TelemetryClients automatisch toegevoegd Hallo eigenschapswaarde die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="0ac6f-195">Afzonderlijke telemetrische gebeurtenissen kunnen Hallo standaardwaarden overschrijven.</span><span class="sxs-lookup"><span data-stu-id="0ac6f-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ac6f-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-196">Next steps</span></span>
   - [<span data-ttu-id="0ac6f-197">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="0ac6f-198">Trechters</span><span class="sxs-lookup"><span data-stu-id="0ac6f-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="0ac6f-199">Retentie</span><span class="sxs-lookup"><span data-stu-id="0ac6f-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="0ac6f-200">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="0ac6f-201">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="0ac6f-202">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="0ac6f-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
