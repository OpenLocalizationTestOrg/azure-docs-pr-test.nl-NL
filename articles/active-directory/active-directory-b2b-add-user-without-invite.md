---
title: aaaAdd B2B-samenwerking gebruikers tooAzure Active Directory zonder een uitnodiging | Microsoft Docs
description: U kunt een andere gast gebruikers tooyour Azure AD toevoegen zonder een uitnodiging in Azure Active Directory B2B-samenwerking wisselt gastgebruiker.
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="a7bd5-103">B2B-samenwerking gastgebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="a7bd5-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="a7bd5-104">U kunt een gebruiker, zoals een partner representatief, tooadd gebruikers van Hallo partnerorganisatie tooyour zonder uitnodigingen toobe ingewisseld toestaan.</span><span class="sxs-lookup"><span data-stu-id="a7bd5-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="a7bd5-105">U moet hoeft alleen die gebruiker opsomming bevoegdheden in Hallo-directory die u voor Hallo partner org. gebruikt verlenen</span><span class="sxs-lookup"><span data-stu-id="a7bd5-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="a7bd5-106">Verleen deze bevoegdheden beschikt wanneer:</span><span class="sxs-lookup"><span data-stu-id="a7bd5-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="a7bd5-107">Een gebruiker in Hallo host organisatie (bijvoorbeeld WoodGrove) nodigt één gebruiker van de partnerorganisatie hello (bijvoorbeeld Sam@litware.com) als gast.</span><span class="sxs-lookup"><span data-stu-id="a7bd5-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="a7bd5-108">Hallo beheerder in Hallo host organisatie stelt u de beleidsregels die van andere gebruikers van de partnerorganisatie hello (Litware) toevoegen en Sam tooidentify toestaan.</span><span class="sxs-lookup"><span data-stu-id="a7bd5-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="a7bd5-109">Sam kan andere gebruikers nu toevoegen via Litware toohello WoodGrove directory, groepen of toepassingen zonder uitnodigingen toobe ingewisseld.</span><span class="sxs-lookup"><span data-stu-id="a7bd5-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="a7bd5-110">Als bij Sam Hallo de opsomming van de juiste bevoegdheden Litware, wordt deze automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a7bd5-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="a7bd5-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7bd5-111">Next steps</span></span>

<span data-ttu-id="a7bd5-112">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="a7bd5-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a7bd5-113">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="a7bd5-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a7bd5-114">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="a7bd5-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="a7bd5-115">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="a7bd5-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="a7bd5-116">Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a7bd5-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="a7bd5-117">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="a7bd5-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="a7bd5-118">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="a7bd5-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="a7bd5-119">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a7bd5-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="a7bd5-120">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="a7bd5-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="a7bd5-121">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="a7bd5-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="a7bd5-122">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a7bd5-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* <span data-ttu-id="a7bd5-123">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="a7bd5-123">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>