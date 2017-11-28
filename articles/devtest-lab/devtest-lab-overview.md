---
title: Over Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe DevTest Labs kunt u gemakkelijk kunt maken, beheren en bewaken van virtuele machines in Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="aaee1-103">Over Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aaee1-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="aaee1-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="aaee1-104">Overview</span></span>
<span data-ttu-id="aaee1-105">Ontwikkelaars en testers zoekt om op te lossen de vertragingen in het maken en beheren van hun omgeving door te gaan naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="aaee1-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="aaee1-106">Azure lost het probleem van vertragingen omgeving en kunt u selfservice binnen een nieuwe kosten efficiënte structuur.</span><span class="sxs-lookup"><span data-stu-id="aaee1-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="aaee1-107">Ontwikkelaars en testers moeten echter nog steeds te besteden veel tijd in hun omgeving zelf aangeboden configureren.</span><span class="sxs-lookup"><span data-stu-id="aaee1-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="aaee1-108">Er zijn ook besluitvormers twijfels hebt over het gebruik van de cloud om hun kostenbesparingen maximaliseren zonder de overhead van te veel proces toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="aaee1-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="aaee1-109">Azure DevTest Labs is een service waarmee ontwikkelaars en testers snel maken omgevingen in Azure tijdens het minimaliseren van verspilling en kosten beheren.</span><span class="sxs-lookup"><span data-stu-id="aaee1-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="aaee1-110">U kunt de nieuwste versie van uw toepassing testen door Windows- en Linux-omgevingen snel in te richten met herbruikbare sjablonen en artefacten.</span><span class="sxs-lookup"><span data-stu-id="aaee1-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="aaee1-111">Uw implementatie pijplijn eenvoudig worden geïntegreerd met DevTest Labs om in te richten op aanvraag omgevingen.</span><span class="sxs-lookup"><span data-stu-id="aaee1-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="aaee1-112">Uw load testen door meerdere agents van de test provisioning opschalen en vooraf is ingericht omgevingen voor training en demo's maken.</span><span class="sxs-lookup"><span data-stu-id="aaee1-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="aaee1-113">DevTest Labs biedt de volgende voordelen bij het maken, configureren en beheren van ontwikkelaars en testomgevingen in de cloud</span><span class="sxs-lookup"><span data-stu-id="aaee1-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="aaee1-114">Self-service probleemloos</span><span class="sxs-lookup"><span data-stu-id="aaee1-114">Worry-free self-service</span></span>
<span data-ttu-id="aaee1-115">DevTest Labs vergemakkelijkt het beheer van kosten doordat u beleidsregels instellen op uw lab - zoals het aantal virtuele machines (VM) per gebruiker en het aantal virtuele machines per lab.</span><span class="sxs-lookup"><span data-stu-id="aaee1-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="aaee1-116">DevTest Labs kunt u beleid maken om automatisch afgesloten en virtuele machines te starten.</span><span class="sxs-lookup"><span data-stu-id="aaee1-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="aaee1-117">Snelle toegang tot gereed om te testen</span><span class="sxs-lookup"><span data-stu-id="aaee1-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="aaee1-118">DevTest Labs kunt u vooraf is ingericht om omgevingen te maken met alles wat die uw team nodig heeft om te beginnen met het ontwikkelen en testen van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="aaee1-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="aaee1-119">Gewoon de claim de omgevingen waarop de laatste goede build van uw toepassing is geïnstalleerd en u meteen werkt.</span><span class="sxs-lookup"><span data-stu-id="aaee1-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="aaee1-120">Of containers te gebruiken voor het maken van de omgeving zelfs sneller en minder complex.</span><span class="sxs-lookup"><span data-stu-id="aaee1-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="aaee1-121">Eenmaal maken, overal gebruiken</span><span class="sxs-lookup"><span data-stu-id="aaee1-121">Create once, use everywhere</span></span>
<span data-ttu-id="aaee1-122">Vastleggen en omgeving sjablonen en artefacten binnen uw team of organisatie - allemaal in Bronbeheer - ontwikkelaars maken en testen omgevingen eenvoudig delen.</span><span class="sxs-lookup"><span data-stu-id="aaee1-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="aaee1-123">Integratie met uw bestaande hulpprogrammaketen</span><span class="sxs-lookup"><span data-stu-id="aaee1-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="aaee1-124">Gebruikmaken van vooraf gemaakte invoegtoepassingen of onze API om in te richten ontwikkelen en testen omgevingen rechtstreeks vanuit uw voorkeur continue integratie (CI)-hulpprogramma integrated development environment (IDE), of geautomatiseerde release pijplijn.</span><span class="sxs-lookup"><span data-stu-id="aaee1-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="aaee1-125">U kunt ook ons uitgebreide opdrachtregelprogramma gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aaee1-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="aaee1-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aaee1-126">Next steps</span></span>
[<span data-ttu-id="aaee1-127">DevTest Labs-concepten</span><span class="sxs-lookup"><span data-stu-id="aaee1-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

