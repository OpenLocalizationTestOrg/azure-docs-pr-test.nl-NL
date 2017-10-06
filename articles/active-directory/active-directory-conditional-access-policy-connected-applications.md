---
title: beleid voor voorwaardelijke toegang op basis van apparaten van aaaConfigure-Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe tooconfigure Azure Active Directory op basis van apparaten voorwaardelijke toegangsbeleid.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="1f652-103">Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren</span><span class="sxs-lookup"><span data-stu-id="1f652-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="1f652-104">Met [voorwaardelijke toegang van Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), kunt u aanpassen hoe geautoriseerde gebruikers toegang uw resources tot hebben.</span><span class="sxs-lookup"><span data-stu-id="1f652-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="1f652-105">Bijvoorbeeld, beperkt u het Hallo-toocertain resources tootrusted apparaten.</span><span class="sxs-lookup"><span data-stu-id="1f652-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="1f652-106">Beleid voor voorwaardelijke toegang waarvoor een vertrouwd apparaat wordt ook wel beleid voor voorwaardelijke toegang op basis van apparaten.</span><span class="sxs-lookup"><span data-stu-id="1f652-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="1f652-107">Dit onderwerp vindt u informatie over hoe tooconfigure op basis van apparaten voorwaardelijke toegangsbeleid voor Azure AD-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1f652-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="1f652-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="1f652-108">Before you begin</span></span>

<span data-ttu-id="1f652-109">Voorwaardelijke toegang op basis van apparaten ties **voorwaardelijke toegang van Azure AD** en **Azure AD-Apparaatbeheer samen**.</span><span class="sxs-lookup"><span data-stu-id="1f652-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="1f652-110">Als u niet bekend met een van deze gebieden bent, maar moet u de volgende onderwerpen, eerst Hallo lezen:</span><span class="sxs-lookup"><span data-stu-id="1f652-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="1f652-111">**[Voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -dit onderwerp vindt u een conceptueel overzicht van voorwaardelijke toegang en verwante terminologie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f652-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="1f652-112">**[Inleiding toodevice management in Azure Active Directory](device-management-introduction.md)**  -in dit onderwerp geeft een overzicht van Hallo verschillende opties er tooconnect apparaten met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f652-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="1f652-113">Vertrouwde apparaten</span><span class="sxs-lookup"><span data-stu-id="1f652-113">Trusted devices</span></span>

<span data-ttu-id="1f652-114">Azure Active Directory kunnen in een wereld mobiel eerste, cloud eerste toodevices voor eenmalige aanmelding, apps en services vanaf elke locatie.</span><span class="sxs-lookup"><span data-stu-id="1f652-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="1f652-115">Voor bepaalde bronnen in uw omgeving, het verlenen van toegang toohello juiste gebruikers mogelijk niet voldoende.</span><span class="sxs-lookup"><span data-stu-id="1f652-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="1f652-116">Naast de juiste gebruikers toohello, u ook mogelijk een vertrouwd apparaat toobe tooaccess een resource die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f652-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="1f652-117">In uw omgeving, kunt u definiëren wat een vertrouwd apparaat is gebaseerd op Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="1f652-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="1f652-118">Hallo [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) op een apparaat</span><span class="sxs-lookup"><span data-stu-id="1f652-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="1f652-119">Hiermee wordt aangegeven of een apparaat is compatibel met</span><span class="sxs-lookup"><span data-stu-id="1f652-119">Whether a device is compliant</span></span>
- <span data-ttu-id="1f652-120">Hiermee wordt aangegeven of een apparaat is lid van een domein</span><span class="sxs-lookup"><span data-stu-id="1f652-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="1f652-121">Hallo [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) wordt gekenmerkt door Hallo-besturingssysteem dat wordt uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="1f652-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="1f652-122">In uw beleid voor voorwaardelijke toegang op basis van apparaten, kunt u access toocertain resources toospecific-apparaatplatforms beperken.</span><span class="sxs-lookup"><span data-stu-id="1f652-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="1f652-123">In een beleid voor voorwaardelijke toegang op basis van apparaten, kunt u de vertrouwde apparaten toobe gemarkeerd als compatibel vereisen.</span><span class="sxs-lookup"><span data-stu-id="1f652-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="1f652-125">Apparaten kunnen worden gemarkeerd als compatibel zijn in de directory Hallo door:</span><span class="sxs-lookup"><span data-stu-id="1f652-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="1f652-126">Intune</span><span class="sxs-lookup"><span data-stu-id="1f652-126">Intune</span></span> 
- <span data-ttu-id="1f652-127">Een beheersysteem voor mobiele apparaten van derden dat kan worden geïntegreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f652-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="1f652-128">Alleen apparaten die verbonden tooAzure AD zijn kunnen worden gemarkeerd als compatibel.</span><span class="sxs-lookup"><span data-stu-id="1f652-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="1f652-129">tooconnect een apparaat tooAzure Active Directory, hebt u Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="1f652-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="1f652-130">Azure AD geregistreerd</span><span class="sxs-lookup"><span data-stu-id="1f652-130">Azure AD registered</span></span>
- <span data-ttu-id="1f652-131">Azure AD die lid zijn van</span><span class="sxs-lookup"><span data-stu-id="1f652-131">Azure AD joined</span></span>
- <span data-ttu-id="1f652-132">Hybride die lid zijn van Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f652-132">Hybrid Azure AD joined</span></span>

    ![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="1f652-134">Als u de voetafdruk van een lokale Active Directory (AD) hebt, kunt u apparaten die niet verbonden tooAzure AD maar lid tooyour AD toobe vertrouwd.</span><span class="sxs-lookup"><span data-stu-id="1f652-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="1f652-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f652-136">Next steps</span></span>

<span data-ttu-id="1f652-137">Voordat u configureert een beleid voor voorwaardelijke toegang op basis van apparaten in uw omgeving, moet u rekening houden bekijkt hello [best practices voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="1f652-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

