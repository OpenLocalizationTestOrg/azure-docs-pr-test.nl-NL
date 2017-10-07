---
title: implementatie van Mobile Engagement aaaAzure voor Gaming-App
description: Gaming-app scenario tooimplement Azure Mobile Engagement
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="49468-103">Mobile Engagement met Gaming-App implementeren</span><span class="sxs-lookup"><span data-stu-id="49468-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="49468-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="49468-104">Overview</span></span>
<span data-ttu-id="49468-105">Een gaming-opstarten heeft een nieuwe visserij gebaseerd role play/strategie gameapps gestart.</span><span class="sxs-lookup"><span data-stu-id="49468-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="49468-106">Hallo game is actief en werkend gedurende 6 maanden.</span><span class="sxs-lookup"><span data-stu-id="49468-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="49468-107">Dit spel is een grote voltooid en heeft miljoenen downloads en Hallo bewaartermijn is zeer hoog in vergelijking tooother opstarten game apps.</span><span class="sxs-lookup"><span data-stu-id="49468-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="49468-108">Op Hallo elk kwartaal revisie vergadering akkoord belanghebbenden moeten tooincrease gemiddelde omzet per gebruiker (ARPU).</span><span class="sxs-lookup"><span data-stu-id="49468-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="49468-109">Premium in de game-pakketten zijn beschikbaar als speciale aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="49468-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="49468-110">Deze game packs toestaan gebruikers tooupgrade Hallo vormgeving en prestaties van hun visserij regels en stelen of tackles in Hallo spel.</span><span class="sxs-lookup"><span data-stu-id="49468-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="49468-111">Er zijn echter pakket verkoop zeer lage.</span><span class="sxs-lookup"><span data-stu-id="49468-111">However, package sales are very low.</span></span> <span data-ttu-id="49468-112">Zodat zij beslissen eerste tooanalyze Hallo klant ervaring met een hulpprogramma voor analyse en vervolgens toodevelop een engagement program tooincrease verkoop met behulp van advanced segmentering.</span><span class="sxs-lookup"><span data-stu-id="49468-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="49468-113">Op basis van Hallo [Azure Mobile Engagement - instructiehandleiding met aanbevolen procedures](mobile-engagement-getting-started-best-practices.md) ze bouwen engagement-strategie.</span><span class="sxs-lookup"><span data-stu-id="49468-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="49468-114">Doelstellingen en KPI 's</span><span class="sxs-lookup"><span data-stu-id="49468-114">Objectives and KPIs</span></span>
<span data-ttu-id="49468-115">Voldoen aan de belangrijkste belanghebbenden voor Hallo spel.</span><span class="sxs-lookup"><span data-stu-id="49468-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="49468-116">Alle overeenstemming worden bereikt over een hoofddoel - tooincrease premium pakket omzet per 15%.</span><span class="sxs-lookup"><span data-stu-id="49468-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="49468-117">Ze maken toomeasure Business Key Performance Indicators (KPI's) en het station deze doelstelling</span><span class="sxs-lookup"><span data-stu-id="49468-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="49468-118">Op welk niveau van Hallo spel worden deze pakketten gekocht?</span><span class="sxs-lookup"><span data-stu-id="49468-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="49468-119">Wat is Hallo omzet per gebruiker, per sessie, per week en per maand?</span><span class="sxs-lookup"><span data-stu-id="49468-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="49468-120">Wat zijn Hallo favoriete aankoop typen?</span><span class="sxs-lookup"><span data-stu-id="49468-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="49468-121">Deel 1 van Hallo [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wordt uitgelegd hoe toodefine Hallo doelstellingen en KPI's.</span><span class="sxs-lookup"><span data-stu-id="49468-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="49468-122">Hallo Mobile Product Manager maakt met de Hallo die zakelijke KPI's nu gedefinieerd, Betrokkenheids-KPI's toodetermine nieuwe gebruiker trends en te bewaren.</span><span class="sxs-lookup"><span data-stu-id="49468-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="49468-123">Bewaken van de retentie en het gebruik in Hallo intervallen volgen: dagelijks, 2 dagen, wekelijks, maandelijks en elke 3 maanden</span><span class="sxs-lookup"><span data-stu-id="49468-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="49468-124">Actieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="49468-124">Active user counts</span></span>
* <span data-ttu-id="49468-125">app-classificatie in Hallo Hallo opslaan</span><span class="sxs-lookup"><span data-stu-id="49468-125">hello app rating in hello store</span></span>

<span data-ttu-id="49468-126">Op basis van de aanbevelingen van Hallo IT-team, zijn Hallo technische KPI's te volgen tooanswer Hallo vragen volgende toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="49468-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="49468-127">Wat is er een pad naar de gebruiker (welke bezochte hoeveel gebruikers besteden aan het)</span><span class="sxs-lookup"><span data-stu-id="49468-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="49468-128">Aantal crashes of fouten aangetroffen per sessie</span><span class="sxs-lookup"><span data-stu-id="49468-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="49468-129">Welke versies van het besturingssysteem worden uitgevoerd voor Mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="49468-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="49468-130">Wat is de gemiddelde grootte Hallo van het scherm voor Mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="49468-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="49468-131">Wat voor soort verbinding met internet hebt mijn gebruikers?</span><span class="sxs-lookup"><span data-stu-id="49468-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="49468-132">Voor elke KPI geeft Hallo Mobile Product Manager Hallo gegevens die ze nodig heeft en waar deze zich bevindt in haar playbook.</span><span class="sxs-lookup"><span data-stu-id="49468-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="49468-133">Betrokkenheidsprogramma en integratie</span><span class="sxs-lookup"><span data-stu-id="49468-133">Engagement program and integration</span></span>
<span data-ttu-id="49468-134">Vóór het bouwen van een geavanceerde betrokkenheidsprogramma moet Hallo Mobile Project directeur verantwoordelijk Hallo project een grondige kennis van hoe en wanneer producten worden verbruikt door Hallo gebruikers hebben.</span><span class="sxs-lookup"><span data-stu-id="49468-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="49468-135">Na drie maanden heeft Hallo Mobile Project directeur verzameld voldoende tooenhance gegevens zijn in-app-push notification-verkoop.</span><span class="sxs-lookup"><span data-stu-id="49468-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="49468-136">Hij leert die:</span><span class="sxs-lookup"><span data-stu-id="49468-136">He learns that:</span></span>

* <span data-ttu-id="49468-137">de eerste aankoop Hallo gebeurt doorgaans op Hallo-niveau 14.</span><span class="sxs-lookup"><span data-stu-id="49468-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="49468-138">Hallo aankoop is voor 90% van de gevallen, nieuwe legendarische wapens voor $3.</span><span class="sxs-lookup"><span data-stu-id="49468-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="49468-139">80% van de gevallen aankopen van gebruikers die u hebt aangebracht kopen, doorgaan met Hallo product en meer.</span><span class="sxs-lookup"><span data-stu-id="49468-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="49468-140">Gebruikers die zijn geslaagd Hallo niveau 20, starten toospend meer dan $10/ week.</span><span class="sxs-lookup"><span data-stu-id="49468-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="49468-141">Gebruikers vaak toobuy premium pakketten op niveau 16, 24 en 32.</span><span class="sxs-lookup"><span data-stu-id="49468-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="49468-142">Bedankt toothis analysis Hallo Mobile Project directeur besluit toocreate specifieke push notification-reeksen tooincrease in app verkoop.</span><span class="sxs-lookup"><span data-stu-id="49468-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="49468-143">Hij maakt drie push reeksen die hij aanroept: Welkom programma, verkoop-programma en niet-actieve programma.</span><span class="sxs-lookup"><span data-stu-id="49468-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="49468-144">Raadpleeg voor meer informatie toohello [hulpmiddelen marketing en verkoop](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="49468-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
