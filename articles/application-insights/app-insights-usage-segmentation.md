---
title: Analyse van de gebruiker, sessie en gebeurtenissen in Azure Application Insights | Microsoft docs
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="ab80c-103">Analyse van de gebruikers, sessies en gebeurtenissen in Application Insights</span><span class="sxs-lookup"><span data-stu-id="ab80c-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="ab80c-104">Weten wanneer mensen uw web-app gebruikt, welke pagina's die ze zijn het meest geïnteresseerd, waar uw gebruikers zich bevinden, welke browsers en besturingssystemen die ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab80c-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="ab80c-105">Bedrijfs- en gebruiksgegevens telemetrie analyseren met behulp van [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab80c-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="ab80c-106">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="ab80c-106">Get started</span></span>

<span data-ttu-id="ab80c-107">Als er geen gegevens in de gebruikers, sessies of blades gebeurtenissen in de Application Insights-portal nog [informatie over het aan de slag met het gebruik van hulpprogramma's voor](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab80c-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="ab80c-108">Het hulpprogramma van de segmentering van gebruikers, sessies en gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="ab80c-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="ab80c-109">Drie van de blades gebruik hetzelfde hulpprogramma gebruiken om te opdelen telemetrie van uw web-app uit drie perspectieven.</span><span class="sxs-lookup"><span data-stu-id="ab80c-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="ab80c-110">Door het filteren en de gegevens worden gesplitst, kunt u inzicht in het relatieve gebruik van verschillende pagina's en onderdelen onthullen.</span><span class="sxs-lookup"><span data-stu-id="ab80c-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="ab80c-111">**Gebruikers hulpprogramma**: hoeveel mensen uw app en de bijbehorende functies gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ab80c-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="ab80c-112">Gebruikers worden met behulp van anonieme id's die zijn opgeslagen in de browsercookies geteld.</span><span class="sxs-lookup"><span data-stu-id="ab80c-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="ab80c-113">Verschillende browsers of machines met één persoon wordt geteld als meer dan één gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ab80c-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="ab80c-114">**Sessies hulpprogramma**: het aantal sessies van gebruikersactiviteit bepaalde pagina's en functies van uw app hebt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="ab80c-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="ab80c-115">Een sessie worden geteld nadat half uur gebruiker inactief of nadat continue 24 uur van gebruik.</span><span class="sxs-lookup"><span data-stu-id="ab80c-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="ab80c-116">**Gebeurtenissen hulpprogramma**: hoe vaak bepaalde pagina's en functies van uw app worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ab80c-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="ab80c-117">Een paginaweergave geteld als een pagina in een browser wordt geladen vanuit uw app, mits u [geïnstrumenteerd deze](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ab80c-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="ab80c-118">Een aangepaste gebeurtenis vertegenwoordigt een exemplaar van dat er iets gebeurt in uw app, vaak een gebruikersinteractie, zoals een knop klikt u op of de voltooiing van een taak.</span><span class="sxs-lookup"><span data-stu-id="ab80c-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="ab80c-119">Voeg in uw app code [aangepaste gebeurtenissen genereren](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="ab80c-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Gebruik hulpprogramma](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="ab80c-121">Uitvoeren van query's voor bepaalde gebruikers</span><span class="sxs-lookup"><span data-stu-id="ab80c-121">Querying for Certain Users</span></span> 

<span data-ttu-id="ab80c-122">Leer de verschillende groepen gebruikers door de query-opties aan de bovenkant van het hulpprogramma gebruikers aan te passen:</span><span class="sxs-lookup"><span data-stu-id="ab80c-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="ab80c-123">Wie gebruikt: Kies aangepaste gebeurtenissen en paginaweergaven.</span><span class="sxs-lookup"><span data-stu-id="ab80c-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="ab80c-124">Tijdens: Kies een tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="ab80c-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="ab80c-125">Door: Kiezen hoe de gegevens laden door een bepaalde periode of door een andere eigenschap zoals browser of een plaats.</span><span class="sxs-lookup"><span data-stu-id="ab80c-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="ab80c-126">Splitsen: Kies een eigenschap waarmee te splitsen of segment de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ab80c-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="ab80c-127">Filters toevoegen: De query beperken tot bepaalde gebruikers, sessies of gebeurtenissen op basis van hun eigenschappen, zoals de browser of een plaats.</span><span class="sxs-lookup"><span data-stu-id="ab80c-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="ab80c-128">Opslaan en delen van rapporten</span><span class="sxs-lookup"><span data-stu-id="ab80c-128">Saving and sharing reports</span></span> 
<span data-ttu-id="ab80c-129">U kunt gebruikers rapporten, persoonlijke aan u in de sectie Mijn rapporten of gedeeld met iedereen met toegang tot deze Application Insights-resource in de sectie gedeelde rapporten anders opslaan.</span><span class="sxs-lookup"><span data-stu-id="ab80c-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="ab80c-130">Tijdens het opslaan van een rapport of de eigenschappen bewerken, kiest u 'Actueel relatief tijdsbereik' voor het opslaan van een rapport wordt voortdurend vernieuwd gegevens, een vaste hoeveelheid tijd als u terugkeert.</span><span class="sxs-lookup"><span data-stu-id="ab80c-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="ab80c-131">Kies 'Huidig absoluut tijdsbereik' een rapport opslaan met een vaste set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ab80c-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="ab80c-132">Houd er rekening mee dat de gegevens in Application Insights alleen worden opgeslagen voor 90 dagen, dus als er meer dan 90 dagen zijn verstreken sinds een rapport met een absoluut tijdsbereik is opgeslagen, wordt het rapport leeg, weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab80c-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="ab80c-133">Voorbeeld-exemplaren</span><span class="sxs-lookup"><span data-stu-id="ab80c-133">Example instances</span></span>

<span data-ttu-id="ab80c-134">De voorbeeld-exemplaren in deze sectie bevat informatie over een aantal afzonderlijke gebruikers, sessies of gebeurtenissen die door de huidige query worden vergeleken.</span><span class="sxs-lookup"><span data-stu-id="ab80c-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="ab80c-135">Overweegt en verkennen van het gedrag van personen naast statistische functies, krijgt u inzicht in hoe mensen uw app daadwerkelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab80c-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="ab80c-136">Inzichten</span><span class="sxs-lookup"><span data-stu-id="ab80c-136">Insights</span></span> 

<span data-ttu-id="ab80c-137">De zijbalk Insights bevat grote clusters van gebruikers die algemene eigenschappen voor delen.</span><span class="sxs-lookup"><span data-stu-id="ab80c-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="ab80c-138">Deze clusters kunnen onthullen verrassend trends in hoe mensen uw app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab80c-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="ab80c-139">Als bijvoorbeeld 40% van alle over het gebruik van uw app afkomstig is van mensen met een enkele functie.</span><span class="sxs-lookup"><span data-stu-id="ab80c-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="ab80c-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ab80c-140">Next steps</span></span>
- <span data-ttu-id="ab80c-141">Om in te schakelen ervaringen gebruik, beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="ab80c-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="ab80c-142">Als u al aangepaste gebeurtenissen of paginaweergaven verzendt, gebruik de informatie over het gebruik hulpprogramma's voor meer informatie over hoe gebruikers gebruiken voor uw service.</span><span class="sxs-lookup"><span data-stu-id="ab80c-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="ab80c-143">Trechters</span><span class="sxs-lookup"><span data-stu-id="ab80c-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="ab80c-144">Retentie</span><span class="sxs-lookup"><span data-stu-id="ab80c-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="ab80c-145">Gebruikersstromen</span><span class="sxs-lookup"><span data-stu-id="ab80c-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="ab80c-146">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="ab80c-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="ab80c-147">Gebruikerscontext toevoegen</span><span class="sxs-lookup"><span data-stu-id="ab80c-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

