---
title: Azure Mobile Engagement-implementatie voor Gaming-App
description: Gaming-app-scenario voor het implementeren van Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="121d4-103">Mobile Engagement met Gaming-App implementeren</span><span class="sxs-lookup"><span data-stu-id="121d4-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="121d4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="121d4-104">Overview</span></span>
<span data-ttu-id="121d4-105">Een gaming-opstarten heeft een nieuwe visserij gebaseerd role play/strategie gameapps gestart.</span><span class="sxs-lookup"><span data-stu-id="121d4-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="121d4-106">Het spel is actief en werkend gedurende 6 maanden.</span><span class="sxs-lookup"><span data-stu-id="121d4-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="121d4-107">Dit spel is een grote voltooid en heeft miljoenen downloads en de bewaarperiode is zeer hoog in vergelijking met andere opstarten game apps.</span><span class="sxs-lookup"><span data-stu-id="121d4-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="121d4-108">Tijdens de vergadering elk kwartaal revisie akkoord belanghebbenden dat ze nodig hebben om te verhogen gemiddelde omzet per gebruiker (ARPU).</span><span class="sxs-lookup"><span data-stu-id="121d4-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="121d4-109">Premium in de game-pakketten zijn beschikbaar als speciale aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="121d4-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="121d4-110">Deze game packs kunnen gebruikers de vormgeving en prestaties van hun visserij regels en stelen of tackles in het spel bijwerken.</span><span class="sxs-lookup"><span data-stu-id="121d4-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="121d4-111">Er zijn echter pakket verkoop zeer lage.</span><span class="sxs-lookup"><span data-stu-id="121d4-111">However, package sales are very low.</span></span> <span data-ttu-id="121d4-112">Zodat zij eerst bepalen voor het analyseren van de gebruikerservaring met een hulpprogramma voor analyse en voor het ontwikkelen van een advies vervolgens geavanceerde programma om te verhogen met behulp van verkoop segmentering.</span><span class="sxs-lookup"><span data-stu-id="121d4-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="121d4-113">Op basis van de [Azure Mobile Engagement - instructiehandleiding met aanbevolen procedures](mobile-engagement-getting-started-best-practices.md) ze bouwen engagement-strategie.</span><span class="sxs-lookup"><span data-stu-id="121d4-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="121d4-114">Doelstellingen en KPI 's</span><span class="sxs-lookup"><span data-stu-id="121d4-114">Objectives and KPIs</span></span>
<span data-ttu-id="121d4-115">Voldoen aan de belangrijkste belanghebbenden voor het spel.</span><span class="sxs-lookup"><span data-stu-id="121d4-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="121d4-116">Alle overeenstemming worden bereikt over een hoofddoel - premium pakket verkoop verhogen met 15%.</span><span class="sxs-lookup"><span data-stu-id="121d4-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="121d4-117">Ze maken deze doelstelling Business Key Performance Indicators (KPI's) naar een meting en het station</span><span class="sxs-lookup"><span data-stu-id="121d4-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="121d4-118">Op welk niveau van het spel worden deze pakketten gekocht?</span><span class="sxs-lookup"><span data-stu-id="121d4-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="121d4-119">Wat is de omzet per gebruiker, per sessie, per week en per maand?</span><span class="sxs-lookup"><span data-stu-id="121d4-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="121d4-120">Wat zijn de typen favoriete aankoop?</span><span class="sxs-lookup"><span data-stu-id="121d4-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="121d4-121">Deel 1 van de [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wordt uitgelegd hoe de doelstellingen en KPI's definiëren.</span><span class="sxs-lookup"><span data-stu-id="121d4-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="121d4-122">De Mobile Product Manager maakt met de zakelijke KPI's nu gedefinieerd, Betrokkenheids-KPI's om te bepalen van de nieuwe gebruiker trends en te bewaren.</span><span class="sxs-lookup"><span data-stu-id="121d4-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="121d4-123">Controleren van de retentie en gebruiken in de volgende intervallen: dagelijks, 2 dagen, wekelijks, maandelijks en elke 3 maanden</span><span class="sxs-lookup"><span data-stu-id="121d4-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="121d4-124">Actieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="121d4-124">Active user counts</span></span>
* <span data-ttu-id="121d4-125">De classificatie van apps in het archief</span><span class="sxs-lookup"><span data-stu-id="121d4-125">The app rating in the store</span></span>

<span data-ttu-id="121d4-126">Op basis van de aanbevelingen van het IT-team, zijn de volgende technische KPI's toegevoegd aan de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="121d4-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="121d4-127">Wat is er een pad naar de gebruiker (welke bezochte hoeveel gebruikers besteden aan het)</span><span class="sxs-lookup"><span data-stu-id="121d4-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="121d4-128">Aantal crashes of fouten aangetroffen per sessie</span><span class="sxs-lookup"><span data-stu-id="121d4-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="121d4-129">Welke versies van het besturingssysteem worden uitgevoerd voor Mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="121d4-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="121d4-130">Wat is de gemiddelde grootte van het scherm voor Mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="121d4-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="121d4-131">Wat voor soort verbinding met internet hebt mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="121d4-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="121d4-132">De Mobile Product Manager geeft de gegevens die ze nodig heeft en waar deze zich bevindt in haar playbook voor elke KPI.</span><span class="sxs-lookup"><span data-stu-id="121d4-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="121d4-133">Betrokkenheidsprogramma en integratie</span><span class="sxs-lookup"><span data-stu-id="121d4-133">Engagement program and integration</span></span>
<span data-ttu-id="121d4-134">Voordat u een geavanceerde betrokkenheidsprogramma bouwt, moet de mobiele Project directeur die verantwoordelijk is voor het project een grondige kennis van hoe en wanneer u producten worden verbruikt door de gebruikers hebben.</span><span class="sxs-lookup"><span data-stu-id="121d4-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="121d4-135">Na drie maanden, de mobiele Project directeur voldoende gegevens om te verbeteren, zijn in-app-push notification-verkoop is verzameld.</span><span class="sxs-lookup"><span data-stu-id="121d4-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="121d4-136">Hij leert die:</span><span class="sxs-lookup"><span data-stu-id="121d4-136">He learns that:</span></span>

* <span data-ttu-id="121d4-137">De eerste aankoop gebeurt doorgaans op het niveau 14.</span><span class="sxs-lookup"><span data-stu-id="121d4-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="121d4-138">Gedurende 90% van de gevallen is de aankoop nieuwe legendarische wapens voor $3.</span><span class="sxs-lookup"><span data-stu-id="121d4-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="121d4-139">80% van de gevallen aankopen van gebruikers die u hebt aangebracht kopen, doorgaan met het product en meer.</span><span class="sxs-lookup"><span data-stu-id="121d4-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="121d4-140">Gebruikers die zijn geslaagd voor het niveau van 20, start te besteden aan meer dan $10/ week.</span><span class="sxs-lookup"><span data-stu-id="121d4-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="121d4-141">Gebruikers vaak pakketten op niveau 16, 24 en 32 premium aanschaffen.</span><span class="sxs-lookup"><span data-stu-id="121d4-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="121d4-142">Dankzij deze analyse besluit de Mobile Project directeur specifieke push notification-reeksen te verhogen in app verkoop maken.</span><span class="sxs-lookup"><span data-stu-id="121d4-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="121d4-143">Hij maakt drie push reeksen die hij aanroept: Welkom programma, verkoop-programma en niet-actieve programma.</span><span class="sxs-lookup"><span data-stu-id="121d4-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="121d4-144">Raadpleeg voor meer informatie de [hulpmiddelen marketing en verkoop](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="121d4-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
