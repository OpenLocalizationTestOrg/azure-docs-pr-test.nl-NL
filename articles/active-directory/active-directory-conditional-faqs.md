---
title: aaaAzure voorwaardelijke toegang tot Active Directory Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over voorwaardelijke toegang in Azure Active Directory worden opgehaald.
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
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="15a0f-103">Voorwaardelijke toegang van Azure Active Directory Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="15a0f-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="15a0f-104">Welke toepassingen werken met beleid voor voorwaardelijke toegang?</span><span class="sxs-lookup"><span data-stu-id="15a0f-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="15a0f-105">Zie voor meer informatie over toepassingen die met beleid voor voorwaardelijke toegang werken [toepassingen en browsers die gebruikmaken van regels voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="15a0f-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="15a0f-106">Afgedwongen beleid voor voorwaardelijke toegang voor B2B-samenwerking en gastgebruikers?</span><span class="sxs-lookup"><span data-stu-id="15a0f-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="15a0f-107">Beleid wordt afgedwongen voor business-to-business (B2B) samenwerking gebruikers.</span><span class="sxs-lookup"><span data-stu-id="15a0f-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="15a0f-108">Echter, in sommige gevallen kan een gebruiker mogelijk niet kunnen toosatisfy Hallo beleidsvereisten.</span><span class="sxs-lookup"><span data-stu-id="15a0f-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="15a0f-109">De organisatie van de gastgebruiker van een mogelijk bijvoorbeeld geen ondersteuning voor multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="15a0f-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="15a0f-110">Is een SharePoint Online-beleid ook van toepassing tooOneDrive voor bedrijven?</span><span class="sxs-lookup"><span data-stu-id="15a0f-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="15a0f-111">Ja.</span><span class="sxs-lookup"><span data-stu-id="15a0f-111">Yes.</span></span> <span data-ttu-id="15a0f-112">Een SharePoint Online-beleid geldt ook tooOneDrive voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="15a0f-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="15a0f-113">Waarom niet kan ik een beleid op ClientApps, zoals Word of Outlook instellen?</span><span class="sxs-lookup"><span data-stu-id="15a0f-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="15a0f-114">Beleid voor voorwaardelijke toegang stelt vereisten voor het openen van een service.</span><span class="sxs-lookup"><span data-stu-id="15a0f-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="15a0f-115">Het wordt afgedwongen wanneer toothat verificatieservice optreedt.</span><span class="sxs-lookup"><span data-stu-id="15a0f-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="15a0f-116">Hallo-beleid is niet rechtstreeks op een clienttoepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="15a0f-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="15a0f-117">In plaats daarvan wordt toegepast wanneer een client een service aanroept.</span><span class="sxs-lookup"><span data-stu-id="15a0f-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="15a0f-118">Een beleid dat is ingesteld op SharePoint geldt bijvoorbeeld tooclients aanroepen van SharePoint.</span><span class="sxs-lookup"><span data-stu-id="15a0f-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="15a0f-119">Een beleid dat is ingesteld op Exchange geldt tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="15a0f-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="15a0f-120">Is een beleid voor voorwaardelijke toegang van toepassing tooservice accounts?</span><span class="sxs-lookup"><span data-stu-id="15a0f-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="15a0f-121">Beleid voor voorwaardelijke toegang toepassen tooall gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="15a0f-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="15a0f-122">Dit omvat de gebruikersaccounts die worden gebruikt als serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="15a0f-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="15a0f-123">Vaak Hallo vereisten van een beleid voor voorwaardelijke toegang kan niet voldoen aan een serviceaccount dat wordt uitgevoerd zonder toezicht.</span><span class="sxs-lookup"><span data-stu-id="15a0f-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="15a0f-124">Multi-factor authentication-server zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="15a0f-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="15a0f-125">Service-accounts kunnen worden uitgesloten van een beleid met behulp van de instellingen voor beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="15a0f-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="15a0f-126">Graph API's beschikbaar zijn voor beleid voor voorwaardelijke toegang configureren?</span><span class="sxs-lookup"><span data-stu-id="15a0f-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="15a0f-127">Op dit moment niet.</span><span class="sxs-lookup"><span data-stu-id="15a0f-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="15a0f-128">Wat is een standaardbeleid met uitsluiting van Hallo voor niet-ondersteunde platforms?</span><span class="sxs-lookup"><span data-stu-id="15a0f-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="15a0f-129">Beleid voor voorwaardelijke toegang worden op dit moment selectief afgedwongen voor gebruikers van iOS- en Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="15a0f-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="15a0f-130">Toepassingen op andere apparaatplatforms, standaard niet worden beïnvloed door Hallo-beleid voor voorwaardelijke toegang voor iOS en Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="15a0f-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="15a0f-131">Een tenantbeheerder kunt toooverride Hallo globaal beleid toodisallow toegang toousers op platforms die niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15a0f-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="15a0f-132">Hoe werken beleidsregels voor voorwaardelijke toegang voor Microsoft-Teams?</span><span class="sxs-lookup"><span data-stu-id="15a0f-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="15a0f-133">Microsoft-Teams is sterk afhankelijk van Exchange Online en SharePoint Online voor core productiviteit scenario's, zoals vergaderingen, agenda's en bestanden delen.</span><span class="sxs-lookup"><span data-stu-id="15a0f-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="15a0f-134">Beleid voor voorwaardelijke toegang die zijn ingesteld voor deze cloud-apps van toepassing tooMicrosoft Teams wanneer een gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="15a0f-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="15a0f-135">Microsoft-Teams wordt ook ondersteund afzonderlijk als een cloud-app in Azure Active Directory-beleid voor voorwaardelijke toegang.</span><span class="sxs-lookup"><span data-stu-id="15a0f-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="15a0f-136">Certificaat autoriteit beleidsregels die zijn ingesteld voor een cloud-app toepassing tooMicrosoft Teams wanneer een gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="15a0f-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="15a0f-137">Microsoft-Teams bureaublad-clients voor Windows en Mac ondersteuning voor moderne verificatie.</span><span class="sxs-lookup"><span data-stu-id="15a0f-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="15a0f-138">Moderne verificatie brengt op aanmelden op basis van hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office-clienttoepassingen in verschillende platforms.</span><span class="sxs-lookup"><span data-stu-id="15a0f-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
