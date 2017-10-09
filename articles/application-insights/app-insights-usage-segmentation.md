---
title: aaaUser, sessie en gebeurtenis analyse in Azure Application Insights | Microsoft docs
description: Demografische analyse van gebruikers van uw web-app.
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="3cee3-103">Analyse van de gebruikers, sessies en gebeurtenissen in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3cee3-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="3cee3-104">Weten wanneer mensen uw web-app gebruikt, welke pagina's die ze zijn het meest geïnteresseerd, waar uw gebruikers zich bevinden, welke browsers en besturingssystemen die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cee3-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="3cee3-105">Bedrijfs- en gebruiksgegevens telemetrie analyseren met behulp van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3cee3-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="3cee3-106">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="3cee3-106">Get started</span></span>

<span data-ttu-id="3cee3-107">Als er geen gegevens in het Hallo-gebruikers, sessies of blades gebeurtenissen in Application Insights-portal Hallo nog [meer informatie over hoe tooget gestart met gebruik van hulpprogramma's voor Hallo](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3cee3-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="3cee3-108">Hallo gebruikers, sessies en gebeurtenissen segmentering hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="3cee3-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="3cee3-109">Drie Hallo gebruik blades gebruiken dezelfde hulpprogramma tooslice en opdelen telemetrie van uw web-app uit drie perspectieven Hallo.</span><span class="sxs-lookup"><span data-stu-id="3cee3-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="3cee3-110">Door het filteren en Hallo gegevens gesplitst, kunt u inzicht in Hallo relatieve gebruik van verschillende pagina's en onderdelen onthullen.</span><span class="sxs-lookup"><span data-stu-id="3cee3-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="3cee3-111">**Gebruikers hulpprogramma**: hoeveel mensen uw app en de bijbehorende functies gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3cee3-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="3cee3-112">Gebruikers worden met behulp van anonieme id's die zijn opgeslagen in de browsercookies geteld.</span><span class="sxs-lookup"><span data-stu-id="3cee3-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="3cee3-113">Verschillende browsers of machines met één persoon wordt geteld als meer dan één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3cee3-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="3cee3-114">**Sessies hulpprogramma**: het aantal sessies van gebruikersactiviteit bepaalde pagina's en functies van uw app hebt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="3cee3-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="3cee3-115">Een sessie worden geteld nadat half uur gebruiker inactief of nadat continue 24 uur van gebruik.</span><span class="sxs-lookup"><span data-stu-id="3cee3-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="3cee3-116">**Gebeurtenissen hulpprogramma**: hoe vaak bepaalde pagina's en functies van uw app worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3cee3-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="3cee3-117">Een paginaweergave geteld als een pagina in een browser wordt geladen vanuit uw app, mits u [geïnstrumenteerd deze](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3cee3-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="3cee3-118">Een aangepaste gebeurtenis vertegenwoordigt een exemplaar van dat er iets gebeurt in uw app, vaak een gebruikersinteractie zoals een knop klikt u op of Hallo van een taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3cee3-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="3cee3-119">U code invoegen in uw app te[aangepaste gebeurtenissen genereren](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="3cee3-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Gebruik hulpprogramma](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="3cee3-121">Uitvoeren van query's voor bepaalde gebruikers</span><span class="sxs-lookup"><span data-stu-id="3cee3-121">Querying for Certain Users</span></span> 

<span data-ttu-id="3cee3-122">Bekijk verschillende groepen gebruikers aan de queryopties Hallo HALLO hallo gebruikers hulpprogramma bovenaan in het aanpassen:</span><span class="sxs-lookup"><span data-stu-id="3cee3-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="3cee3-123">Wie gebruikt: Kies aangepaste gebeurtenissen en paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="3cee3-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="3cee3-124">Tijdens: Kies een tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="3cee3-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="3cee3-125">Door: Kies toobucket Hallo hoe gegevens door een bepaalde periode of door een andere eigenschap zoals browser of een plaats.</span><span class="sxs-lookup"><span data-stu-id="3cee3-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="3cee3-126">Splitsen: Kies een eigenschap door welke toosplit of segment Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="3cee3-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="3cee3-127">Filters toevoegen: Beperk Hallo query toocertain gebruikers, sessies of gebeurtenissen op basis van hun eigenschappen, zoals de browser of een plaats.</span><span class="sxs-lookup"><span data-stu-id="3cee3-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="3cee3-128">Opslaan en delen van rapporten</span><span class="sxs-lookup"><span data-stu-id="3cee3-128">Saving and sharing reports</span></span> 
<span data-ttu-id="3cee3-129">U kunt gebruikers rapporten, ofwel private alleen tooyou in sectie Hallo mijn rapporten opslaan of gedeeld met iedereen met toegang toothis Application Insights-resource anders in Hallo sectie gedeelde rapporten.</span><span class="sxs-lookup"><span data-stu-id="3cee3-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="3cee3-130">Tijdens het opslaan van een rapport of de eigenschappen bewerken, kiest u 'Huidige relatief tijdsbereik' toosave die een rapport voortdurend wordt vernieuwd gegevens, een vaste hoeveelheid tijd als u terugkeert.</span><span class="sxs-lookup"><span data-stu-id="3cee3-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="3cee3-131">Kies 'Huidige absoluut tijdsbereik' toosave een rapport met een vaste set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="3cee3-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="3cee3-132">Houd er rekening mee dat de gegevens in Application Insights alleen worden opgeslagen voor 90 dagen, dus als er meer dan 90 dagen zijn verstreken sinds een rapport met een absoluut tijdsbereik is opgeslagen, Hallo rapport leeg, weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3cee3-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="3cee3-133">Voorbeeld-exemplaren</span><span class="sxs-lookup"><span data-stu-id="3cee3-133">Example instances</span></span>

<span data-ttu-id="3cee3-134">Hallo voorbeeld exemplaren in deze sectie bevat informatie over een aantal afzonderlijke gebruikers, sessies of gebeurtenissen die door de huidige query Hallo worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="3cee3-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="3cee3-135">Overweegt en verkennen Hallo gedrag van personen in toevoeging tooaggregates, krijgt u inzicht in hoe mensen uw app daadwerkelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cee3-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="3cee3-136">Inzichten</span><span class="sxs-lookup"><span data-stu-id="3cee3-136">Insights</span></span> 

<span data-ttu-id="3cee3-137">Hallo Insights zijbalk bevat grote clusters van gebruikers die algemene eigenschappen voor delen.</span><span class="sxs-lookup"><span data-stu-id="3cee3-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="3cee3-138">Deze clusters kunnen onthullen verrassend trends in hoe mensen uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cee3-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="3cee3-139">Als bijvoorbeeld 40% van alle Hallo informatie over het gebruik van uw app afkomstig is van mensen met een enkele functie.</span><span class="sxs-lookup"><span data-stu-id="3cee3-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="3cee3-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cee3-140">Next steps</span></span>
- <span data-ttu-id="3cee3-141">Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="3cee3-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="3cee3-142">Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cee3-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="3cee3-143">Trechters</span><span class="sxs-lookup"><span data-stu-id="3cee3-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="3cee3-144">Retentie</span><span class="sxs-lookup"><span data-stu-id="3cee3-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="3cee3-145">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="3cee3-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="3cee3-146">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="3cee3-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="3cee3-147">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="3cee3-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

