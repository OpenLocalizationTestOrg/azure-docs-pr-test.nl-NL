---
title: Voorwaardelijke toegang van Azure Active Directory Veelgestelde vragen | Microsoft Docs
description: Vind antwoorden op veelgestelde vragen over voorwaardelijke toegang in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="a9b73-103">Voorwaardelijke toegang van Azure Active Directory Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a9b73-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="a9b73-104">Welke toepassingen werken met beleid voor voorwaardelijke toegang?</span><span class="sxs-lookup"><span data-stu-id="a9b73-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="a9b73-105">Zie voor meer informatie over toepassingen die met beleid voor voorwaardelijke toegang werken [toepassingen en browsers die gebruikmaken van regels voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a9b73-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="a9b73-106">Afgedwongen beleid voor voorwaardelijke toegang voor B2B-samenwerking en gastgebruikers?</span><span class="sxs-lookup"><span data-stu-id="a9b73-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="a9b73-107">Beleid wordt afgedwongen voor business-to-business (B2B) samenwerking gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a9b73-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="a9b73-108">Echter, in sommige gevallen kan een gebruiker niet mogelijk om te voldoen aan de beleidsvereisten.</span><span class="sxs-lookup"><span data-stu-id="a9b73-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="a9b73-109">De organisatie van de gastgebruiker van een mogelijk bijvoorbeeld geen ondersteuning voor multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="a9b73-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="a9b73-110">Een SharePoint Online-beleid ook van toepassing op OneDrive voor bedrijven?</span><span class="sxs-lookup"><span data-stu-id="a9b73-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="a9b73-111">Ja.</span><span class="sxs-lookup"><span data-stu-id="a9b73-111">Yes.</span></span> <span data-ttu-id="a9b73-112">Een SharePoint Online-beleid geldt ook voor OneDrive voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="a9b73-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="a9b73-113">Waarom niet kan ik een beleid op ClientApps, zoals Word of Outlook instellen?</span><span class="sxs-lookup"><span data-stu-id="a9b73-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="a9b73-114">Beleid voor voorwaardelijke toegang stelt vereisten voor het openen van een service.</span><span class="sxs-lookup"><span data-stu-id="a9b73-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="a9b73-115">Het wordt afgedwongen wanneer verificatie die service optreedt.</span><span class="sxs-lookup"><span data-stu-id="a9b73-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="a9b73-116">Het beleid is niet rechtstreeks op een clienttoepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a9b73-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="a9b73-117">In plaats daarvan wordt toegepast wanneer een client een service aanroept.</span><span class="sxs-lookup"><span data-stu-id="a9b73-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="a9b73-118">Een beleid dat is ingesteld op SharePoint geldt bijvoorbeeld voor clients voor het aanroepen van SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9b73-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="a9b73-119">Een beleid dat is ingesteld op Exchange geldt voor Outlook.</span><span class="sxs-lookup"><span data-stu-id="a9b73-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="a9b73-120">Is een beleid voor voorwaardelijke toegang van toepassing op service-accounts?</span><span class="sxs-lookup"><span data-stu-id="a9b73-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="a9b73-121">Beleid voor voorwaardelijke toegang van toepassing op alle gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a9b73-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="a9b73-122">Dit omvat de gebruikersaccounts die worden gebruikt als serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="a9b73-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="a9b73-123">Vaak een serviceaccount dat wordt uitgevoerd zonder toezicht kan niet voldoen aan de vereisten van een beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="a9b73-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="a9b73-124">Multi-factor authentication-server zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="a9b73-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="a9b73-125">Service-accounts kunnen worden uitgesloten van een beleid met behulp van de instellingen voor beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="a9b73-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="a9b73-126">Graph API's beschikbaar zijn voor beleid voor voorwaardelijke toegang configureren?</span><span class="sxs-lookup"><span data-stu-id="a9b73-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="a9b73-127">Op dit moment niet.</span><span class="sxs-lookup"><span data-stu-id="a9b73-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="a9b73-128">Wat is het standaardbeleid voor uitsluiting voor niet-ondersteunde platforms?</span><span class="sxs-lookup"><span data-stu-id="a9b73-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="a9b73-129">Beleid voor voorwaardelijke toegang worden op dit moment selectief afgedwongen voor gebruikers van iOS- en Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a9b73-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="a9b73-130">Toepassingen op andere apparaatplatforms, standaard niet worden beïnvloed door het beleid voor voorwaardelijke toegang voor iOS en Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a9b73-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="a9b73-131">Een tenantbeheerder kunt kiezen voor het onderdrukken van het globaal beleid niet toestaan van toegang tot gebruikers op platforms die niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a9b73-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="a9b73-132">Hoe werken beleidsregels voor voorwaardelijke toegang voor Microsoft-Teams?</span><span class="sxs-lookup"><span data-stu-id="a9b73-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="a9b73-133">Microsoft-Teams is sterk afhankelijk van Exchange Online en SharePoint Online voor core productiviteit scenario's, zoals vergaderingen, agenda's en bestanden delen.</span><span class="sxs-lookup"><span data-stu-id="a9b73-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="a9b73-134">Beleid voor voorwaardelijke toegang die zijn ingesteld voor deze cloud-apps van toepassing op Microsoft-Teams wanneer een gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="a9b73-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="a9b73-135">Microsoft-Teams wordt ook ondersteund afzonderlijk als een cloud-app in Azure Active Directory-beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="a9b73-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="a9b73-136">Certificaat-instantie beleidsregels die zijn ingesteld voor een cloud-app van toepassing op Microsoft-Teams wanneer een gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="a9b73-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="a9b73-137">Microsoft-Teams bureaublad-clients voor Windows en Mac ondersteuning voor moderne verificatie.</span><span class="sxs-lookup"><span data-stu-id="a9b73-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="a9b73-138">Moderne verificatie brengt op aanmelden op basis van de Azure Active Directory Authentication Library (ADAL) voor Microsoft Office-clienttoepassingen in verschillende platforms.</span><span class="sxs-lookup"><span data-stu-id="a9b73-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 