---
title: Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren | Microsoft Docs
description: Informatie over het configureren van Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten.
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
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="215f7-103">Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren</span><span class="sxs-lookup"><span data-stu-id="215f7-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="215f7-104">Met [voorwaardelijke toegang van Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), kunt u aanpassen hoe geautoriseerde gebruikers toegang uw resources tot hebben.</span><span class="sxs-lookup"><span data-stu-id="215f7-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="215f7-105">Bijvoorbeeld, beperkt u de toegang tot bepaalde bronnen op vertrouwde apparaten.</span><span class="sxs-lookup"><span data-stu-id="215f7-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="215f7-106">Beleid voor voorwaardelijke toegang waarvoor een vertrouwd apparaat wordt ook wel beleid voor voorwaardelijke toegang op basis van apparaten.</span><span class="sxs-lookup"><span data-stu-id="215f7-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="215f7-107">In dit onderwerp vindt u informatie over het configureren van beleidsregels voor voorwaardelijke toegang op basis van apparaten voor Azure AD-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="215f7-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="215f7-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="215f7-108">Before you begin</span></span>

<span data-ttu-id="215f7-109">Voorwaardelijke toegang op basis van apparaten ties **voorwaardelijke toegang van Azure AD** en **Azure AD-Apparaatbeheer samen**.</span><span class="sxs-lookup"><span data-stu-id="215f7-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="215f7-110">Als u nog niet bekend bent met een van deze gebieden, moet u eerst de volgende onderwerpen lezen:</span><span class="sxs-lookup"><span data-stu-id="215f7-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="215f7-111">**[Voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -dit onderwerp vindt u een conceptueel overzicht van voorwaardelijke toegang en de verwante terminologie.</span><span class="sxs-lookup"><span data-stu-id="215f7-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="215f7-112">**[Inleiding tot beheer van apparaten in Azure Active Directory](device-management-introduction.md)**  -in dit onderwerp geeft een overzicht van de verschillende opties die u hebt om apparaten te verbinden met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="215f7-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="215f7-113">Vertrouwde apparaten</span><span class="sxs-lookup"><span data-stu-id="215f7-113">Trusted devices</span></span>

<span data-ttu-id="215f7-114">In een wereld mobiel eerste, cloud eerste kunnen Azure Active Directory eenmalige aanmelding aan apparaten, apps en services vanaf elke locatie.</span><span class="sxs-lookup"><span data-stu-id="215f7-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="215f7-115">Voor bepaalde bronnen in uw omgeving, het verlenen van toegang aan de juiste gebruikers mogelijk niet voldoende.</span><span class="sxs-lookup"><span data-stu-id="215f7-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="215f7-116">Naast de juiste gebruikers, kunt u ook een vertrouwd apparaat moet worden gebruikt voor toegang tot een bron vereisen.</span><span class="sxs-lookup"><span data-stu-id="215f7-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="215f7-117">In uw omgeving, kunt u definiëren wat een vertrouwd apparaat is gebaseerd op de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="215f7-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="215f7-118">De [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) op een apparaat</span><span class="sxs-lookup"><span data-stu-id="215f7-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="215f7-119">Hiermee wordt aangegeven of een apparaat is compatibel met</span><span class="sxs-lookup"><span data-stu-id="215f7-119">Whether a device is compliant</span></span>
- <span data-ttu-id="215f7-120">Hiermee wordt aangegeven of een apparaat is lid van een domein</span><span class="sxs-lookup"><span data-stu-id="215f7-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="215f7-121">De [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) wordt gekenmerkt door het besturingssysteem dat wordt uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="215f7-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="215f7-122">In uw beleid voor voorwaardelijke toegang op basis van apparaten, kunt u toegang tot bepaalde bronnen voor specifieke apparaatplatforms beperken.</span><span class="sxs-lookup"><span data-stu-id="215f7-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="215f7-123">In een beleid voor voorwaardelijke toegang op basis van apparaten, kunt u de vertrouwde apparaten zijn gemarkeerd als compatibel vereisen.</span><span class="sxs-lookup"><span data-stu-id="215f7-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="215f7-125">Apparaten kunnen worden gemarkeerd als compatibel zijn in de map aan:</span><span class="sxs-lookup"><span data-stu-id="215f7-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="215f7-126">Intune</span><span class="sxs-lookup"><span data-stu-id="215f7-126">Intune</span></span> 
- <span data-ttu-id="215f7-127">Een beheersysteem voor mobiele apparaten van derden dat kan worden geïntegreerd met Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f7-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="215f7-128">Alleen apparaten die zijn verbonden met Azure AD kunnen worden gemarkeerd als compatibel.</span><span class="sxs-lookup"><span data-stu-id="215f7-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="215f7-129">Voor een apparaat verbinding met Azure Active Directory, hebt u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="215f7-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="215f7-130">Azure AD geregistreerd</span><span class="sxs-lookup"><span data-stu-id="215f7-130">Azure AD registered</span></span>
- <span data-ttu-id="215f7-131">Azure AD die lid zijn van</span><span class="sxs-lookup"><span data-stu-id="215f7-131">Azure AD joined</span></span>
- <span data-ttu-id="215f7-132">Hybride die lid zijn van Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f7-132">Hybrid Azure AD joined</span></span>

    ![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="215f7-134">Als u de voetafdruk van een lokale Active Directory (AD) hebt, kunt u apparaten die niet zijn verbonden met Azure AD maar lid is van uw AD te worden vertrouwd.</span><span class="sxs-lookup"><span data-stu-id="215f7-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="215f7-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="215f7-136">Next steps</span></span>

<span data-ttu-id="215f7-137">Voordat u configureert een beleid voor voorwaardelijke toegang op basis van apparaten in uw omgeving, dient u te kijken hoe de [best practices voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="215f7-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

