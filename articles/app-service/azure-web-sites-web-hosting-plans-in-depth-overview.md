---
title: gedetailleerd overzicht van aaaAzure App Service-plannen | Microsoft Docs
description: Lees hoe App Service-plannen voor Azure App Service werk, en hoe ze uw beheerervaring profiteren.
keywords: App Service, Azure App Service, schaal, schaalbaar, App Service-abonnement, kosten App Service
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="02258-104">Gedetailleerd overzicht van de abonnementen voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="02258-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="02258-105">App Service-abonnementen vertegenwoordigen Hallo-verzameling van fysieke resources gebruikt toohost uw apps.</span><span class="sxs-lookup"><span data-stu-id="02258-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="02258-106">In App Service-plannen wordt het volgende gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="02258-106">App Service plans define:</span></span>

- <span data-ttu-id="02258-107">Regio (VS-West, VS-Oost, enz.)</span><span class="sxs-lookup"><span data-stu-id="02258-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="02258-108">Schaalaanpassingsaantal (een, twee, drie exemplaren, enz.)</span><span class="sxs-lookup"><span data-stu-id="02258-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="02258-109">De exemplaargrootte van het (klein, normaal, groot)</span><span class="sxs-lookup"><span data-stu-id="02258-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="02258-110">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="02258-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="02258-111">Web-Apps, Mobile Apps, API-Apps, Apps van de functie (of functies), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) alle uitvoeren in een App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="02258-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="02258-112">Apps in Hallo hetzelfde abonnement en regio een App Service-abonnement kunt delen.</span><span class="sxs-lookup"><span data-stu-id="02258-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="02258-113">Alle toepassingen toegewezen tooan **App Service-abonnement** gedefinieerd door het Hallo-resources delen.</span><span class="sxs-lookup"><span data-stu-id="02258-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="02258-114">Deze delen, bespaart geld bij het hosten van meerdere apps in een enkele App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="02258-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="02258-115">Uw **App Service-abonnement** kunt opschalen van **vrije** en **gedeelde** SKU's te**Basic**, **standaard**, en **Premium** SKU's zodat u toegang tot resources toomore en functies langs Hallo manier.</span><span class="sxs-lookup"><span data-stu-id="02258-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="02258-116">Als uw App Service-abonnement te is ingesteld**Basic** SKU of hoger, en vervolgens u Hallo bepalen kunt **grootte** en aantal Hallo virtuele machines worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="02258-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="02258-117">Bijvoorbeeld: als het abonnement heeft een geconfigureerde toouse twee 'kleine' exemplaren in de standaard servicelaag hello, uitvoeren alle apps die gekoppeld aan een plan zijn voor beide exemplaren.</span><span class="sxs-lookup"><span data-stu-id="02258-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="02258-118">Apps hebben ook toegangsfuncties toohello standaardservice laag.</span><span class="sxs-lookup"><span data-stu-id="02258-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="02258-119">Plan exemplaren apps waarop zijn volledig beheerde en maximaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="02258-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02258-120">Hallo **SKU** en **Scale** Hallo App Service plan bepaalt Hallo kosten en niet Hallo aantal apps die erin worden gehost.</span><span class="sxs-lookup"><span data-stu-id="02258-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="02258-121">Dit artikel behandelt Hallo belangrijke kenmerken, zoals laag en schaal van een App Service-plan en hoe ze rol spelen bij het beheren van uw apps.</span><span class="sxs-lookup"><span data-stu-id="02258-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="02258-122">Apps en App Service-abonnementen</span><span class="sxs-lookup"><span data-stu-id="02258-122">Apps and App Service plans</span></span>

<span data-ttu-id="02258-123">Een app in App Service kan worden gekoppeld aan slechts één App Service-abonnement op elk moment.</span><span class="sxs-lookup"><span data-stu-id="02258-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="02258-124">Zowel apps als abonnementen zijn opgenomen in een **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="02258-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="02258-125">Een resourcegroep fungeert als Hallo lifecycle grens voor elke bron die binnen het.</span><span class="sxs-lookup"><span data-stu-id="02258-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="02258-126">U kunt resource groepen toomanage alle Hallo gedeelten van een toepassing samen.</span><span class="sxs-lookup"><span data-stu-id="02258-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="02258-127">Omdat één resourcegroep meerdere App Service-abonnementen hebt kan, kunt u verschillende apps toodifferent fysieke bronnen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="02258-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="02258-128">U kunt bijvoorbeeld resources tussen de ontwikkeling, testen en productie-omgevingen scheiden.</span><span class="sxs-lookup"><span data-stu-id="02258-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="02258-129">Met afzonderlijke omgevingen voor productie en ontwikkelen en testen, kunt u resources isoleren.</span><span class="sxs-lookup"><span data-stu-id="02258-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="02258-130">Op deze manier load getest op een nieuwe versie van uw apps niet zou concurreren voor Hallo dezelfde bronnen als uw productie-apps, die echte klanten fungeren.</span><span class="sxs-lookup"><span data-stu-id="02258-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="02258-131">Wanneer u meerdere abonnementen in één resourcegroep hebt, kunt u ook een toepassing die geografische regio's omvat definiëren.</span><span class="sxs-lookup"><span data-stu-id="02258-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="02258-132">Bijvoorbeeld: een maximaal beschikbare app uitgevoerd in twee gebieden bevat ten minste twee plannen, één voor elke regio en een app die is gekoppeld aan elk plan.</span><span class="sxs-lookup"><span data-stu-id="02258-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="02258-133">In een dergelijke situatie zijn vervolgens alle Hallo kopieën van Hallo app opgenomen in één resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="02258-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="02258-134">Met een resourcegroep met meerdere abonnementen en meerdere apps maakt het eenvoudig toomanage, controle en status van de weergave Hallo van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="02258-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="02258-135">Maken van een App Service-abonnement of bestaande gebruiken</span><span class="sxs-lookup"><span data-stu-id="02258-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="02258-136">Wanneer u een app maakt, kunt u overwegen een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="02258-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="02258-137">Op Hallo anderzijds, als deze app is een onderdeel voor een grotere toepassing, maakt u dit binnen de resourcegroep Hallo die voor die grotere toepassing toegewezen.</span><span class="sxs-lookup"><span data-stu-id="02258-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="02258-138">Of Hallo-app een geheel nieuwe toepassing of een deel van een groter voorbeeld is, kunt u kiezen toouse een bestaand plan toohost deze of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="02258-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="02258-139">Deze beslissing is meer een vraag van capaciteit en de verwachte belasting.</span><span class="sxs-lookup"><span data-stu-id="02258-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="02258-140">Het is raadzaam het isoleren van uw app in een nieuwe App Service plannen wanneer:</span><span class="sxs-lookup"><span data-stu-id="02258-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="02258-141">App is een bronintensieve.</span><span class="sxs-lookup"><span data-stu-id="02258-141">App is resource-intensive.</span></span>
- <span data-ttu-id="02258-142">App heeft verschillende schalen factoren van Hallo andere apps die wordt gehost in een bestaand abonnement.</span><span class="sxs-lookup"><span data-stu-id="02258-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="02258-143">App moet resource in een andere geografische regio.</span><span class="sxs-lookup"><span data-stu-id="02258-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="02258-144">Op deze manier kunt u een nieuwe set bronnen toewijzen voor uw app en meer controle over uw apps te krijgen.</span><span class="sxs-lookup"><span data-stu-id="02258-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="02258-145">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="02258-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="02258-146">Als u een App Service-omgeving hebt, kunt u Hallo documentatie specifieke tooApp Service-omgevingen hier bekijken: [maken van een App Service-abonnement in een App-serviceomgeving](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="02258-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="02258-147">U kunt een lege App Service-abonnement maken van App Service plan Bladerervaring Hallo of als onderdeel van app maken.</span><span class="sxs-lookup"><span data-stu-id="02258-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="02258-148">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel**, en selecteer vervolgens **Web-App** of een ander type App Service-app.</span><span class="sxs-lookup"><span data-stu-id="02258-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Een app maken in hello Azure-portal.][createWebApp]

<span data-ttu-id="02258-150">Vervolgens kunt u selecteren of maken van App Service-plan voor de nieuwe app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="02258-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Maak een App Service-abonnement.][createASP]

<span data-ttu-id="02258-152">toocreate een App Service-abonnement, klik op **[+] maken nieuwe**, type Hallo **App Service-abonnement** een naam en selecteer vervolgens een geschikte **locatie**.</span><span class="sxs-lookup"><span data-stu-id="02258-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="02258-153">Klik op **prijscategorie**, en selecteer vervolgens een juiste prijscategorie voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="02258-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="02258-154">Selecteer **weergeven van alle** tooview meer opties, zoals prijzen **vrije** en **gedeelde**.</span><span class="sxs-lookup"><span data-stu-id="02258-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="02258-155">Nadat u Hallo prijscategorie hebt geselecteerd, klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="02258-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="02258-156">Verplaatsen van een app tooa verschillende App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="02258-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="02258-157">U kunt een app tooa verschillende App Service-abonnement in Hallo verplaatsen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02258-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="02258-158">U kunt apps verplaatsen tussen plannen zolang Hallo plannen in Hallo zijn dezelfde resourcegroep en de geografische regio.</span><span class="sxs-lookup"><span data-stu-id="02258-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="02258-159">een app tooanother plan toomove:</span><span class="sxs-lookup"><span data-stu-id="02258-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="02258-160">Navigeer toohello app die u toomove wilt.</span><span class="sxs-lookup"><span data-stu-id="02258-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="02258-161">In Hallo **Menu**, zoekt u naar Hallo **App Service-Plan** sectie.</span><span class="sxs-lookup"><span data-stu-id="02258-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="02258-162">Selecteer **wijziging App Service-abonnement** toostart Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="02258-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="02258-163">**App Service-abonnement wijzigen** wordt geopend Hallo **App Service-abonnement** selector.</span><span class="sxs-lookup"><span data-stu-id="02258-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="02258-164">Op dit moment kunt u kiezen een bestaand plan toomove deze app in.</span><span class="sxs-lookup"><span data-stu-id="02258-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02258-165">Hallo Selecteer App Service-abonnement UI wordt gefilterd op Hallo volgende criteria:</span><span class="sxs-lookup"><span data-stu-id="02258-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="02258-166">Binnen bestaat Hallo dezelfde resourcegroep</span><span class="sxs-lookup"><span data-stu-id="02258-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="02258-167">Bestaat in Hallo dezelfde geografische regio</span><span class="sxs-lookup"><span data-stu-id="02258-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="02258-168">Binnen bestaat Hallo dezelfde webruimte</span><span class="sxs-lookup"><span data-stu-id="02258-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="02258-169">Een webruimte is een logische constructie in App Service waarmee een groepering van serverbronnen zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="02258-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="02258-170">Een geografische regio (zoals VS-West) bevat veel Webspaces in volgorde tooallocate klanten die gebruikmaken van App Service.</span><span class="sxs-lookup"><span data-stu-id="02258-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="02258-171">App Service-resources zijn op dit moment kunnen toobe verplaatst tussen Webspaces niet.</span><span class="sxs-lookup"><span data-stu-id="02258-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Selector van App Service-plan.][change]

<span data-ttu-id="02258-173">Elk plan heeft zijn eigen prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="02258-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="02258-174">Voor informatie over het verplaatsen van een site van een gratis laag tooa Standard-laag kan bijvoorbeeld alle apps die zijn toegewezen tooit toouse Hallo functies en bronnen van Hallo Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="02258-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="02258-175">Klonen van een app tooa verschillende App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="02258-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="02258-176">Als u toomove Hallo app tooa andere regio wilt, een alternatief is app klonen.</span><span class="sxs-lookup"><span data-stu-id="02258-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="02258-177">Klonen wordt een kopie van uw app in een nieuw of bestaand App Service-abonnement in elke regio.</span><span class="sxs-lookup"><span data-stu-id="02258-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="02258-178">U vindt **kloon App** in Hallo **ontwikkelingsprogramma's** gedeelte van Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="02258-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02258-179">Klonen, is enkele beperkingen die u op over kunt lezen [klonen van de Azure App Service-App met Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="02258-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="02258-180">Schalen van een App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="02258-180">Scale an App Service plan</span></span>

<span data-ttu-id="02258-181">Er zijn drie manieren tooscale een plan:</span><span class="sxs-lookup"><span data-stu-id="02258-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="02258-182">**Wijziging Hallo abonnement de prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="02258-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="02258-183">Een plan in de basisstaffel Hallo kunt geconverteerde tooStandard, en alle apps toegewezen tooit toouse Hallo functies van Hallo Standard-laag.</span><span class="sxs-lookup"><span data-stu-id="02258-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="02258-184">**Wijzig de exemplaargrootte van het plan Hallo**.</span><span class="sxs-lookup"><span data-stu-id="02258-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="02258-185">Als u bijvoorbeeld mag een plan in de basisstaffel Hallo die gebruikmaakt van kleine exemplaren zijn gewijzigde toouse grote exemplaren.</span><span class="sxs-lookup"><span data-stu-id="02258-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="02258-186">Alle apps die gekoppeld aan een plan nu zijn kunnen Hallo extra geheugen en CPU-bronnen die grotere exemplaar grootte aanbiedingen Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02258-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="02258-187">**Aantal exemplaren op Hallo-abonnement wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="02258-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="02258-188">Een standaard-plan toothree exemplaren wordt uitgebreid kan bijvoorbeeld geschaalde too10 exemplaren.</span><span class="sxs-lookup"><span data-stu-id="02258-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="02258-189">Premium-abonnement kan worden uitgebreid tot too20 exemplaren (onderwerp tooavailability).</span><span class="sxs-lookup"><span data-stu-id="02258-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="02258-190">Alle apps die gekoppeld aan een plan nu zijn kunnen Hallo extra geheugen en CPU-bronnen die grotere exemplaar aantal aanbiedingen Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02258-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="02258-191">Kunt u Hallo prijscategorie laag en de exemplaar-grootte door te klikken op Hallo **omhoog schalen** item onder instellingen voor Hallo app of Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="02258-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="02258-192">Wijzigingen toepassen toohello App Service-abonnement en van invloed zijn op alle apps die deze als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="02258-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Stel tooscale waarden van een app.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="02258-194">App Service plan opschonen</span><span class="sxs-lookup"><span data-stu-id="02258-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02258-195">**App Service-plannen** die geen apps die zijn gekoppeld toothem nog steeds kosten omdat ze nog steeds tooreserve Hallo rekencapaciteit hebben.</span><span class="sxs-lookup"><span data-stu-id="02258-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="02258-196">tooavoid onverwachte kosten, wanneer de laatste app Hallo gehost in een App Service-abonnement wordt verwijderd, Hallo resulterende lege App Service-abonnement wordt ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="02258-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="02258-197">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="02258-197">Summary</span></span>

<span data-ttu-id="02258-198">App Service-abonnementen vertegenwoordigen een reeks functies en mogelijkheden die u in uw apps delen kunt.</span><span class="sxs-lookup"><span data-stu-id="02258-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="02258-199">App Service-plannen kunt u Hallo flexibiliteit tooallocate specifieke apps tooa set resources en het gebruik van uw Azure-resource verder te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="02258-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="02258-200">Op deze manier als u wilt dat toosave money op de testomgeving kunt u een plan voor meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="02258-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="02258-201">U kunt ook doorvoer voor uw productieomgeving maximaliseren door schalen in meerdere regio's en plannen.</span><span class="sxs-lookup"><span data-stu-id="02258-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="02258-202">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="02258-202">What's changed</span></span>

- <span data-ttu-id="02258-203">Zie voor een wijziging van de toohello handleiding van Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="02258-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
