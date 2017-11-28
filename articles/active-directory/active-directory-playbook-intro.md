---
title: aaaAzure Active Directory implementatiemodel Playbook Inleiding | Microsoft Docs
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="f8e1e-104">Azure Active Directory-bewijs van Concept Playbook: Inleiding</span><span class="sxs-lookup"><span data-stu-id="f8e1e-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="f8e1e-105">In dit artikel bevat richtlijnen tooexplore andere Azure AD-mogelijkheden in een bewijs van Concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="f8e1e-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="f8e1e-106">Hallo bedoeld doelgroep van dit document is identiteit architecten, IT-Professionals en systeemintegrators</span><span class="sxs-lookup"><span data-stu-id="f8e1e-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="f8e1e-107">Hoe toouse deze Playbook</span><span class="sxs-lookup"><span data-stu-id="f8e1e-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="f8e1e-108">Gebruik Hallo [thema](active-directory-playbook-ingredients.md#theme) sectie en kies (s) voor Hallo van belang op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="f8e1e-109">Het bereik van Hallo implementatiemodel door het Hallo-scenario's die zijn afgestemd op uw zakelijke doelstellingen kiezen.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="f8e1e-110">Hallo korter Hallo beter.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-110">hello shorter hello better.</span></span> <span data-ttu-id="f8e1e-111">Aangeraden om dit te doen als de korte en mogelijke tooconvey Hallo waarde beknopt toohello belanghebbenden terwijl het minimaliseert Hallo complexiteit toorealize deze.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="f8e1e-112">Gebruik Hallo [implementatie](active-directory-playbook-implementation.md) sectie toounderstand Hallo scenario's, en wordt hun betekenis voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="f8e1e-113">In elk scenario wordt beschreven hoe tooset het (zogeheten [bouwstenen](active-directory-playbook-building-blocks.md)), en hoe toonavigate Hallo scenario's.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="f8e1e-114">Elke bouwsteen wordt uitgelegd Hallo vereisten nodig, evenals een toocomplete bij benadering de tijd.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="f8e1e-115">Hiermee kunt u tijdens het Hallo planningsproces.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="f8e1e-116">Op basis van 1-3 hierboven, Hallo definiëren [omgeving](active-directory-playbook-ingredients.md#environment) in welke tooexecute.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="f8e1e-117">We raden toostrive voor een productie-omgeving tooget een goede werking van Hallo ervaring voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="f8e1e-118">Bij een conflicterende vereisten, gebruiken deze matrix handig afweging</span><span class="sxs-lookup"><span data-stu-id="f8e1e-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="f8e1e-119">Thema gericht weergeeft van waarde</span><span class="sxs-lookup"><span data-stu-id="f8e1e-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="f8e1e-120">Vloeiend tooprepare en tooset up tooexecute Hallo scenario 's</span><span class="sxs-lookup"><span data-stu-id="f8e1e-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="f8e1e-121">Minimale tijd tooexecute Hallo doelscenario 's</span><span class="sxs-lookup"><span data-stu-id="f8e1e-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="f8e1e-122">Als sluiten tooproduction als haalbaar binnen uw beperkingen</span><span class="sxs-lookup"><span data-stu-id="f8e1e-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="f8e1e-123">In dit artikel ziet u enkele toepassingen van derden specifieke en de producten vermeld als voorbeelden voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="f8e1e-124">Azure AD ondersteunt duizenden toepassingen in onze [toepassingsgalerie](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) waarmee u kunt op basis van uw behoeften en omgeving.</span><span class="sxs-lookup"><span data-stu-id="f8e1e-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]