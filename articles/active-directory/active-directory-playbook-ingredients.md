---
title: "Azure Active Directory implementatiemodel Playbook ingrediënten | Microsoft Docs"
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
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="2ddc9-104">Azure Active Directory-bewijs van Concept Playbook ingrediënten</span><span class="sxs-lookup"><span data-stu-id="2ddc9-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="2ddc9-105">Thema</span><span class="sxs-lookup"><span data-stu-id="2ddc9-105">Theme</span></span>
<span data-ttu-id="2ddc9-106">Azure AD levert de oplossingen voor identiteits- en toegangsbeheer via meerdere gebieden in de onderneming.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="2ddc9-107">Classificeren van de scenario's in de volgende gebieden:</span><span class="sxs-lookup"><span data-stu-id="2ddc9-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="2ddc9-108">Veel apps, één identiteit</span><span class="sxs-lookup"><span data-stu-id="2ddc9-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="2ddc9-109">De beveiliging verbeteren</span><span class="sxs-lookup"><span data-stu-id="2ddc9-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="2ddc9-110">Schaal met selfservice</span><span class="sxs-lookup"><span data-stu-id="2ddc9-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="2ddc9-111">Voor het definiëren van een thema wilt toevoegen aan de POC-fase zorgt de concentreren dat binnen met zakelijke doelstellingen die vaak is het mogelijk zijn de triggers van de interesse in een POC in de eerste plaats.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="2ddc9-112">Omgeving</span><span class="sxs-lookup"><span data-stu-id="2ddc9-112">Environment</span></span>

<span data-ttu-id="2ddc9-113">Het is belangrijk om te bepalen van de details van de omgeving waarin u de POC-fase zullen leveren.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="2ddc9-114">U kunt in het ideale geval bouwen voort op het nadat de POC-fase is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="2ddc9-115">De doelomgeving is van cruciaal belang en vindt u de juiste balans tussen deze als echte mogelijk en de verwerkingstijd van de beperkingen of overwegingen zijn extra maken.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="2ddc9-116">De typische omgevingen voor POC's zijn:</span><span class="sxs-lookup"><span data-stu-id="2ddc9-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="2ddc9-117">**Productie:** de scenario's zullen worden uitgevoerd in uw productieomgeving en Microsoft Cloud-services (productie AD, Office 365, Azure AD-tenant/SSO oplossing) al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="2ddc9-118">**Gebruiker acceptatie testen (UAT) / Dev-omgeving:** u test-infrastructuur hebt (parallelle AD en mogelijk Azure AD-tenant/SSO oplossing) met testgegevens dat lijkt op productie.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="2ddc9-119">De testomgeving worden doorgaans verdeeld over meerdere projecten in de onderneming.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="2ddc9-120">De meeste scenario's in deze handleiding zijn additieve aard.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="2ddc9-121">Hierdoor kunnen kunnen ze worden geïmplementeerd in de productie-tenant zonder gebruikers buiten de POC-fase.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="2ddc9-122">In dit document bellen we uit welke scenario's tenant wide gevolgen zou hebben.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="2ddc9-123">In deze gevallen is het raadzaam rekening houden met een niet-productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="2ddc9-124">Doelgebruikers</span><span class="sxs-lookup"><span data-stu-id="2ddc9-124">Target Users</span></span>

<span data-ttu-id="2ddc9-125">Het is belangrijk om te bepalen welke doel van gebruikers die de scenario's, oefent vooral wanneer de omgeving testomgeving is.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="2ddc9-126">De categorieën van doelgebruikers voor implementatiemodel zijn:</span><span class="sxs-lookup"><span data-stu-id="2ddc9-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="2ddc9-127">**Testgebruikers:** echte gebruikers in de omgeving die de oplossing gaat gebruiken met het account dat ze voor hun dagelijkse taakfuncties gebruiken</span><span class="sxs-lookup"><span data-stu-id="2ddc9-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="2ddc9-128">**Testgebruikers:** accounts die zijn gemaakt in de omgeving testen</span><span class="sxs-lookup"><span data-stu-id="2ddc9-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="2ddc9-129">De meeste scenario's in deze handleiding kunnen worden uitgeoefend door testgebruikers.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="2ddc9-130">In dit document zullen we contact uit doel gebruiker overwegingen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2ddc9-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]