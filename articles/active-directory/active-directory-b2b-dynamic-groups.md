---
title: aaaDynamic groepen en Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking kan met Azure AD-dynamische groepen worden gebruikt
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="46e23-103">Dynamische groepen en Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="46e23-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="46e23-104">Wat zijn dynamische groepen?</span><span class="sxs-lookup"><span data-stu-id="46e23-104">What are dynamic groups?</span></span>
<span data-ttu-id="46e23-105">Dynamische configuratie van de beveiligingsgroep voor Azure Active Directory (Azure AD) is beschikbaar in [hello Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46e23-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="46e23-106">Beheerders kunnen regels toopopulate groepen die zijn gemaakt in Azure Active Directory op basis van gebruikerskenmerken (zoals userType, afdeling of land) instellen.</span><span class="sxs-lookup"><span data-stu-id="46e23-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="46e23-107">Leden kunnen automatisch worden toegevoegd tooor verwijderd uit een beveiligingsgroep op basis van hun kenmerken.</span><span class="sxs-lookup"><span data-stu-id="46e23-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="46e23-108">Deze groepen kunnen toegang bieden tooapplications of -cloud-bronnen (SharePoint-sites, documenten) en tooassign toomembers licenties.</span><span class="sxs-lookup"><span data-stu-id="46e23-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="46e23-109">Meer informatie over dynamische groepen in [groepen in Azure Active Directory-specifieke](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="46e23-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="46e23-110">Hallo juiste [Azure AD Premium-P1 of P2 licentieverlening](https://azure.microsoft.com/pricing/details/active-directory/) is vereist toocreate en gebruik dynamische groepen.</span><span class="sxs-lookup"><span data-stu-id="46e23-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="46e23-111">Meer informatie artikel Hallo [op kenmerken gebaseerde regels maken voor dynamisch lidmaatschap in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="46e23-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="46e23-112">Wat zijn de ingebouwde dynamische groepen Hallo?</span><span class="sxs-lookup"><span data-stu-id="46e23-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="46e23-113">Hallo **alle gebruikers** kunnen dynamische groep tenant admins toocreate een groep met alle gebruikers in het Hallo-tenant met één klik.</span><span class="sxs-lookup"><span data-stu-id="46e23-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="46e23-114">Standaard Hallo **alle gebruikers** groep bevat alle gebruikers in Hallo directory, inclusief leden en gastbesturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="46e23-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="46e23-115">Binnen Hallo nieuwe Azure Active Directory-beheerportal, kunt u tooenable hello **alle gebruikers** groep in Hallo groepsinstellingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="46e23-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![ingebouwde groepen](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="46e23-117">Hardening Hallo dynamische groep voor alle gebruikers</span><span class="sxs-lookup"><span data-stu-id="46e23-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="46e23-118">Standaard Hallo **alle gebruikers** groep bevat uw B2B-samenwerking (Gast) gebruikers ook.</span><span class="sxs-lookup"><span data-stu-id="46e23-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="46e23-119">U kunt verder te beveiligen, uw **alle gebruikers** groeperen met behulp van een regel tooremove-gastgebruikers.</span><span class="sxs-lookup"><span data-stu-id="46e23-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="46e23-120">Hallo volgende afbeelding ziet u Hallo **alle gebruikers** groep Gasten tooexclude is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="46e23-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![groep alle gebruikers inschakelen](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="46e23-122">Ook het wellicht handig toocreate een nieuwe dynamische groep waarin alleen gastgebruikers, zodat u beleid (zoals Azure AD voorwaardelijk toegangsbeleid) toothem kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="46e23-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="46e23-123">Wat zo'n groep als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="46e23-123">What such a group might look like:</span></span>

![gastgebruikers uitsluiten](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="46e23-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46e23-125">Next steps</span></span>

<span data-ttu-id="46e23-126">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="46e23-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="46e23-127">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="46e23-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="46e23-128">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="46e23-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="46e23-129">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="46e23-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="46e23-130">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="46e23-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="46e23-131">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="46e23-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="46e23-132">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="46e23-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="46e23-133">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="46e23-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="46e23-134">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="46e23-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="46e23-135">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="46e23-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="46e23-136">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="46e23-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
