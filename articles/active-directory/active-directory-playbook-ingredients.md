---
title: "Active Directory implementatiemodel Playbook ingrediënten aaaAzure | Microsoft Docs"
description: Verkennen en snel implementeren scenario's voor Identity and Access Management
services: active-directory
keywords: Azure active directory, playbook, Proof-of-Concept, implementatiemodel
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="f774e-104">Azure Active Directory-bewijs van Concept Playbook ingrediënten</span><span class="sxs-lookup"><span data-stu-id="f774e-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="f774e-105">Thema</span><span class="sxs-lookup"><span data-stu-id="f774e-105">Theme</span></span>
<span data-ttu-id="f774e-106">Azure AD levert de oplossingen voor identiteits- en toegangsbeheer via meerdere gebieden in de onderneming Hallo.</span><span class="sxs-lookup"><span data-stu-id="f774e-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="f774e-107">We classificeren Hallo scenario's in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="f774e-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="f774e-108">Veel apps, één identiteit</span><span class="sxs-lookup"><span data-stu-id="f774e-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="f774e-109">De beveiliging verbeteren</span><span class="sxs-lookup"><span data-stu-id="f774e-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="f774e-110">Schaal met selfservice</span><span class="sxs-lookup"><span data-stu-id="f774e-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="f774e-111">Voor het definiëren van een thema tooframe Hallo implementatiemodel helpt toofocus Hallo inspanningen die binnen met zakelijke doelstellingen die vaak ook Hallo triggers van Hallo interesse in een POC in de eerste plaats Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="f774e-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="f774e-112">Omgeving</span><span class="sxs-lookup"><span data-stu-id="f774e-112">Environment</span></span>

<span data-ttu-id="f774e-113">Het is belangrijk toodetermine Hallo details van Hallo-omgeving waarin u Hallo implementatiemodel levert.</span><span class="sxs-lookup"><span data-stu-id="f774e-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="f774e-114">U kunt in het ideale geval bouwen voort op deze na Hallo die POC-fase is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f774e-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="f774e-115">Hallo doelomgeving is van cruciaal belang en vindt u de juiste balans Hallo tussen deze als echte mogelijk en Hallo overhead van beperkingen of extra overwegingen.</span><span class="sxs-lookup"><span data-stu-id="f774e-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="f774e-116">Hallo typische omgevingen voor POC's zijn:</span><span class="sxs-lookup"><span data-stu-id="f774e-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="f774e-117">**Productie:** Hallo scenario's zullen worden uitgevoerd in uw productieomgeving en Microsoft Cloud-services (productie AD, Office 365, Azure AD-tenant/SSO oplossing) al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f774e-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="f774e-118">**Gebruiker acceptatie testen (UAT) / Dev-omgeving:** u test-infrastructuur hebt (parallelle AD en mogelijk Azure AD-tenant/SSO oplossing) met testgegevens dat lijkt op productie.</span><span class="sxs-lookup"><span data-stu-id="f774e-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="f774e-119">Normaal gesproken worden Hallo testomgeving verdeeld over meerdere projecten in Hallo onderneming.</span><span class="sxs-lookup"><span data-stu-id="f774e-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="f774e-120">De meeste scenario's in deze handleiding zijn additieve aard.</span><span class="sxs-lookup"><span data-stu-id="f774e-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="f774e-121">Als gevolg hiervan kunnen ze worden geïmplementeerd in productie-tenant Hallo zonder gebruikers buiten Hallo implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f774e-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="f774e-122">In dit document bellen we uit welke scenario's tenant wide gevolgen zou hebben.</span><span class="sxs-lookup"><span data-stu-id="f774e-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="f774e-123">U kunt in deze gevallen tooconsider een niet-productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f774e-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="f774e-124">Doelgebruikers</span><span class="sxs-lookup"><span data-stu-id="f774e-124">Target Users</span></span>

<span data-ttu-id="f774e-125">Het is belangrijk toodetermine Hallo doel reeks gebruikers die Hallo scenario's, oefent vooral wanneer Hallo-omgeving testomgeving is.</span><span class="sxs-lookup"><span data-stu-id="f774e-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="f774e-126">Hallo categorieën van doelgebruikers voor implementatiemodel zijn:</span><span class="sxs-lookup"><span data-stu-id="f774e-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="f774e-127">**Testgebruikers:** taakfuncties echte gebruikers in Hallo-omgeving die Hallo-oplossing gaat gebruiken met Hallo account ze voor hun tooday dag gebruiken</span><span class="sxs-lookup"><span data-stu-id="f774e-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="f774e-128">**Testgebruikers:** accounts die zijn gemaakt in Hallo omgeving testen</span><span class="sxs-lookup"><span data-stu-id="f774e-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="f774e-129">De meeste scenario's in deze handleiding kunnen worden uitgeoefend door testgebruikers.</span><span class="sxs-lookup"><span data-stu-id="f774e-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="f774e-130">In dit document zullen we contact uit doel gebruiker overwegingen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="f774e-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]