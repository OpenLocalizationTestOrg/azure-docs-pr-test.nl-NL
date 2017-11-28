---
title: aaaAdd een Azure Active Directory B2B-samenwerking gebruikersrol tooa | Microsoft Docs
description: Toevoegen van een gast tooa gebruikersrol in Azure Active Directory
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="3565b-103">Het verlenen van machtigingen toousers van partnerorganisaties in uw Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="3565b-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="3565b-104">Azure Active Directory (Azure AD) B2B-samenwerking gebruikers worden toegevoegd als gast gebruikers toohello directory en gastmachtigingen in Hallo directory standaard worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="3565b-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="3565b-105">Uw bedrijf wellicht sommige Gast gebruikers toofill hogere bevoegdheid rollen in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3565b-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="3565b-106">hogere bevoegdheid-rollen definiëren toosupport gastgebruikers kunnen worden toegevoegd tooany functies die u wenst, op basis van de behoeften van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3565b-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="3565b-107">standaardrol</span><span class="sxs-lookup"><span data-stu-id="3565b-107">Default role</span></span>

![standaardrol](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="3565b-109">Rol van algemeen beheerder</span><span class="sxs-lookup"><span data-stu-id="3565b-109">Global Administrator Role</span></span>

![de rol globale beheerder](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="3565b-111">Beperkte Administrator-rol</span><span class="sxs-lookup"><span data-stu-id="3565b-111">Limited Administrator Role</span></span>

![beperkte Administrator-rol](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="3565b-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3565b-113">Next steps</span></span>

<span data-ttu-id="3565b-114">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="3565b-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3565b-115">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="3565b-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3565b-116">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="3565b-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="3565b-117">B2bB samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="3565b-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="3565b-118">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="3565b-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="3565b-119">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3565b-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="3565b-120">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="3565b-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="3565b-121">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="3565b-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="3565b-122">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="3565b-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="3565b-123">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="3565b-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="3565b-124">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="3565b-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
