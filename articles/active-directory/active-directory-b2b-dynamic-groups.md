---
title: Dynamische groepen en Azure Active Directory B2B-samenwerking | Microsoft Docs
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="18b9a-103">Dynamische groepen en Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="18b9a-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="18b9a-104">Wat zijn dynamische groepen?</span><span class="sxs-lookup"><span data-stu-id="18b9a-104">What are dynamic groups?</span></span>
<span data-ttu-id="18b9a-105">Dynamische configuratie van de beveiligingsgroep voor Azure Active Directory (Azure AD) is beschikbaar in [de Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="18b9a-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="18b9a-106">Beheerders kunnen de regels voor het vullen van groepen die zijn gemaakt in Azure Active Directory op basis van gebruikerskenmerken (zoals userType, afdeling of land) instellen.</span><span class="sxs-lookup"><span data-stu-id="18b9a-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="18b9a-107">Leden kunnen automatisch worden toegevoegd aan of verwijderd uit een beveiligingsgroep op basis van hun kenmerken.</span><span class="sxs-lookup"><span data-stu-id="18b9a-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="18b9a-108">Deze groepen krijgt u toegang tot toepassingen of cloudbronnen (SharePoint-sites, documenten) en licenties toewijzen aan leden.</span><span class="sxs-lookup"><span data-stu-id="18b9a-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="18b9a-109">Meer informatie over dynamische groepen in [groepen in Azure Active Directory-specifieke](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="18b9a-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="18b9a-110">De juiste [Azure AD Premium-P1 of P2 licentieverlening](https://azure.microsoft.com/pricing/details/active-directory/) is vereist voor dynamische groepen maken en gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18b9a-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="18b9a-111">Meer informatie in het artikel [op kenmerken gebaseerde regels maken voor dynamisch lidmaatschap in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18b9a-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="18b9a-112">Wat zijn de ingebouwde dynamische groepen?</span><span class="sxs-lookup"><span data-stu-id="18b9a-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="18b9a-113">De **alle gebruikers** kunnen dynamische groep tenantbeheerders voor het maken van een groep met alle gebruikers in de tenant met een enkele klik.</span><span class="sxs-lookup"><span data-stu-id="18b9a-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="18b9a-114">Standaard de **alle gebruikers** groep bevat alle gebruikers in de directory, inclusief leden en gastbesturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="18b9a-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="18b9a-115">Binnen het nieuwe Azure Active Directory-beheerportal kunt u kiezen om in te schakelen de **alle gebruikers** groep in de weergave instellingen.</span><span class="sxs-lookup"><span data-stu-id="18b9a-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![ingebouwde groepen](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="18b9a-117">De dynamische groep met alle gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="18b9a-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="18b9a-118">Standaard de **alle gebruikers** groep bevat uw B2B-samenwerking (Gast) gebruikers ook.</span><span class="sxs-lookup"><span data-stu-id="18b9a-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="18b9a-119">U kunt verder te beveiligen, uw **alle gebruikers** groeperen met behulp van een regel te verwijderen van gastgebruikers.</span><span class="sxs-lookup"><span data-stu-id="18b9a-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="18b9a-120">De volgende afbeelding ziet u de **alle gebruikers** groep Gasten uitsluiten is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="18b9a-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![groep alle gebruikers inschakelen](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="18b9a-122">Ook het wellicht handig voor het maken van een nieuwe dynamische groep met alleen gastgebruikers zodat u kunt beleidsregels (zoals Azure AD voorwaardelijk toegangsbeleid) toe.</span><span class="sxs-lookup"><span data-stu-id="18b9a-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="18b9a-123">Wat zo'n groep als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="18b9a-123">What such a group might look like:</span></span>

![gastgebruikers uitsluiten](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="18b9a-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18b9a-125">Next steps</span></span>

<span data-ttu-id="18b9a-126">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="18b9a-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="18b9a-127">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="18b9a-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="18b9a-128">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="18b9a-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="18b9a-129">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="18b9a-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="18b9a-130">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="18b9a-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="18b9a-131">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="18b9a-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="18b9a-132">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="18b9a-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="18b9a-133">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="18b9a-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="18b9a-134">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="18b9a-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="18b9a-135">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="18b9a-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="18b9a-136">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="18b9a-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
