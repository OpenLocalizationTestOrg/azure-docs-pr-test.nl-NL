---
title: Azure Active Directory implementatiemodel Playbook Inleiding | Microsoft Docs
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
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="71b31-104">Azure Active Directory-bewijs van Concept Playbook: Inleiding</span><span class="sxs-lookup"><span data-stu-id="71b31-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="71b31-105">Dit artikel bevat richtlijnen voor het verkennen van andere Azure AD-mogelijkheden in een bewijs van Concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="71b31-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="71b31-106">De doelgroep van dit document is identiteit architecten, IT-Professionals en systeemintegrators</span><span class="sxs-lookup"><span data-stu-id="71b31-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="71b31-107">Het gebruik van deze Playbook</span><span class="sxs-lookup"><span data-stu-id="71b31-107">How to use this Playbook</span></span>

1. <span data-ttu-id="71b31-108">Gebruik de [thema](active-directory-playbook-ingredients.md#theme) sectie en selecteer de module (s) van belang op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="71b31-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="71b31-109">Het bereik van de POC-fase door het kiezen van de scenario's die zijn afgestemd op uw zakelijke doelstellingen.</span><span class="sxs-lookup"><span data-stu-id="71b31-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="71b31-110">Hoe korter hoe beter.</span><span class="sxs-lookup"><span data-stu-id="71b31-110">The shorter the better.</span></span> <span data-ttu-id="71b31-111">Het is raadzaam om dit te doen als kort en bondig mogelijk bij de waarde voor de belanghebbenden terwijl het minimaliseert de complexiteit voor het overbrengen.</span><span class="sxs-lookup"><span data-stu-id="71b31-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="71b31-112">Gebruik de [implementatie](active-directory-playbook-implementation.md) sectie over de scenario's en wat ze betekent voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="71b31-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="71b31-113">In elk scenario beschreven hoe u instelt (zogeheten [bouwstenen](active-directory-playbook-building-blocks.md)), en de scenario's te navigeren.</span><span class="sxs-lookup"><span data-stu-id="71b31-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="71b31-114">Elke bouwsteen verklaart de vereisten die nodig zijn, evenals een bij benadering de tijd om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="71b31-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="71b31-115">Dit kan u helpen bij het planningsproces.</span><span class="sxs-lookup"><span data-stu-id="71b31-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="71b31-116">Definiëren op basis van 1-3 hierboven, de [omgeving](active-directory-playbook-ingredients.md#environment) waarin uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="71b31-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="71b31-117">We raden streven voor een productieomgeving om op te halen van een goede werking van de ervaring voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="71b31-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="71b31-118">Bij een conflicterende vereisten, gebruiken deze matrix handig afweging</span><span class="sxs-lookup"><span data-stu-id="71b31-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="71b31-119">Thema gericht weergeeft van waarde</span><span class="sxs-lookup"><span data-stu-id="71b31-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="71b31-120">Vloeiend om voor te bereiden, kunt u instellen en uitvoeren van de scenario 's</span><span class="sxs-lookup"><span data-stu-id="71b31-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="71b31-121">Minimale tijd voor het uitvoeren van de doel-scenario 's</span><span class="sxs-lookup"><span data-stu-id="71b31-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="71b31-122">Als in de buurt productie als haalbaar binnen uw beperkingen</span><span class="sxs-lookup"><span data-stu-id="71b31-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="71b31-123">In dit artikel ziet u enkele toepassingen van derden specifieke en de producten vermeld als voorbeelden voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="71b31-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="71b31-124">Azure AD ondersteunt duizenden toepassingen in onze [toepassingsgalerie](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) waarmee u kunt op basis van uw behoeften en omgeving.</span><span class="sxs-lookup"><span data-stu-id="71b31-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]