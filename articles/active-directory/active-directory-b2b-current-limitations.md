---
title: Beperkingen van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Huidige beperkingen voor Azure Active Directory B2B-samenwerking
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="315ef-103">Beperkingen van Azure AD B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="315ef-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="315ef-104">Azure Active Directory (Azure AD) B2B-samenwerking is momenteel onderworpen aan de beperkingen die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="315ef-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="315ef-105">Mogelijke dubbele multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="315ef-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="315ef-106">Met Azure AD B2B, kunt u multi-factor authentication op de bronorganisatie (de organisatie uitnodigen) afdwingen.</span><span class="sxs-lookup"><span data-stu-id="315ef-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="315ef-107">De redenen voor deze benadering zijn aangegeven in [voorwaardelijke toegang voor gebruikers voor B2B-samenwerking](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="315ef-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="315ef-108">Als een partner al meervoudige verificatie instellen en het systeem is, wordt hun gebruikers wellicht één keer de verificatie uitvoeren binnen hun organisatie thuis en vervolgens opnieuw in jouw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="315ef-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="315ef-109">Instant op</span><span class="sxs-lookup"><span data-stu-id="315ef-109">Instant-on</span></span>
<span data-ttu-id="315ef-110">In het stroomt B2B-samenwerking we gebruikers toevoegen aan de map en ze dynamisch bijwerken tijdens uitnodiging inwisseling en app-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="315ef-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="315ef-111">De updates- en schrijfbewerkingen normaal gebeuren in een directory-exemplaar en in alle exemplaren moeten worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="315ef-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="315ef-112">Replicatie is voltooid zodra alle exemplaren worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="315ef-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="315ef-113">Soms wanneer het object wordt geschreven of bijgewerkt in één exemplaar en de aanroep voor het ophalen van dit object naar een ander exemplaar is, kunnen de replicatielatentie optreden.</span><span class="sxs-lookup"><span data-stu-id="315ef-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="315ef-114">Als dat gebeurt, vernieuwen of probeer om te helpen.</span><span class="sxs-lookup"><span data-stu-id="315ef-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="315ef-115">Als u een app met behulp van onze API schrijft, is opnieuw wordt geprobeerd met sommige terug uit een goede, defensive procedure voor het verlichten van dit probleem.</span><span class="sxs-lookup"><span data-stu-id="315ef-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="315ef-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="315ef-116">Next steps</span></span>

<span data-ttu-id="315ef-117">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="315ef-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="315ef-118">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="315ef-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="315ef-119">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="315ef-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="315ef-120">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="315ef-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="315ef-121">B2bB samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="315ef-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="315ef-122">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="315ef-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="315ef-123">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="315ef-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="315ef-124">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="315ef-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="315ef-125">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="315ef-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="315ef-126">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="315ef-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="315ef-127">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="315ef-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
