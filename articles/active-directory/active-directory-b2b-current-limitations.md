---
title: aaaLimitations van Azure Active Directory B2B-samenwerking | Microsoft Docs
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="de16a-103">Beperkingen van Azure AD B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="de16a-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="de16a-104">Azure Active Directory (Azure AD) B2B-samenwerking is momenteel onderwerp toohello beperkingen die in dit artikel worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="de16a-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="de16a-105">Mogelijke dubbele multi-factor authentication-server</span><span class="sxs-lookup"><span data-stu-id="de16a-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="de16a-106">Met Azure AD B2B, kunt u multi-factor authentication op Hallo bronorganisatie (hello organisatie uitnodigen) afdwingen.</span><span class="sxs-lookup"><span data-stu-id="de16a-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="de16a-107">Hallo redenen voor deze benadering zijn aangegeven in [voorwaardelijke toegang voor gebruikers voor B2B-samenwerking](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="de16a-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="de16a-108">Als een partner heeft al een multi-factorauthenticatie ingesteld en afgedwongen, hun gebruikers wellicht tooperform Hallo verificatie eenmaal binnen hun organisatie thuis en vervolgens opnieuw in jouw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="de16a-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="de16a-109">Instant op</span><span class="sxs-lookup"><span data-stu-id="de16a-109">Instant-on</span></span>
<span data-ttu-id="de16a-110">In Hallo B2B-samenwerking flows we gebruikers toohello map toevoegen en ze dynamisch bijwerken tijdens uitnodiging inwisseling en app-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="de16a-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="de16a-111">Hallo-updates- en schrijfbewerkingen normaal gebeuren in een directory-exemplaar en in alle exemplaren moeten worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="de16a-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="de16a-112">Replicatie is voltooid zodra alle exemplaren worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="de16a-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="de16a-113">Soms wanneer Hallo-object wordt geschreven of bijgewerkt in één exemplaar en Hallo aanroepen tooretrieve dit object is tooanother exemplaar, replicatielatentie kunnen zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="de16a-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="de16a-114">Als dat gebeurt, vernieuw of probeer toohelp.</span><span class="sxs-lookup"><span data-stu-id="de16a-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="de16a-115">Als u een app met onze API en klik vervolgens op nieuwe pogingen met enkele schrijft back-off is een goede, defensive practice tooalleviate dit probleem.</span><span class="sxs-lookup"><span data-stu-id="de16a-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de16a-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de16a-116">Next steps</span></span>

<span data-ttu-id="de16a-117">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="de16a-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="de16a-118">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="de16a-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="de16a-119">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="de16a-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="de16a-120">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="de16a-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="de16a-121">B2bB samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="de16a-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="de16a-122">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="de16a-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="de16a-123">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="de16a-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="de16a-124">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="de16a-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="de16a-125">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="de16a-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="de16a-126">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="de16a-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="de16a-127">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="de16a-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
