---
title: B2B-samenwerking gebruikers toevoegen aan Azure Active Directory zonder een uitnodiging | Microsoft Docs
description: U kunt een andere gastgebruikers toevoegen aan uw Azure AD zonder een uitnodiging in Azure Active Directory B2B-samenwerking wisselt gastgebruiker.
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="a2704-103">B2B-samenwerking gastgebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="a2704-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="a2704-104">U kunt een gebruiker, zoals een vertegenwoordiger partner gebruikers van de partner toevoegen aan uw organisatie zonder uitnodigingen worden ingewisseld toestaan.</span><span class="sxs-lookup"><span data-stu-id="a2704-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="a2704-105">U moet doen, is verlenen die gebruiker opsomming bevoegdheden in de map die u voor bijzonder partner gebruikt</span><span class="sxs-lookup"><span data-stu-id="a2704-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="a2704-106">Verleen deze bevoegdheden beschikt wanneer:</span><span class="sxs-lookup"><span data-stu-id="a2704-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="a2704-107">Een gebruiker in de organisatie van de host (bijvoorbeeld WoodGrove) nodigt één gebruiker van de andere organisatie (bijvoorbeeld Sam@litware.com) als gast.</span><span class="sxs-lookup"><span data-stu-id="a2704-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="a2704-108">De beheerder in de organisatie van de host stelt u de beleidsregels waarmee Sam om te bepalen en andere gebruikers van de partnerorganisatie (Litware) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a2704-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="a2704-109">Nu kunt Sam toevoegen andere gebruikers van Litware aan de directory WoodGrove, groepen of toepassingen zonder uitnodigingen die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a2704-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="a2704-110">Als de juiste opsomming Sam in Litware bevoegdheden, wordt deze automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2704-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="a2704-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2704-111">Next steps</span></span>

<span data-ttu-id="a2704-112">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="a2704-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a2704-113">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="a2704-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a2704-114">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="a2704-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="a2704-115">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="a2704-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="a2704-116">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a2704-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="a2704-117">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="a2704-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="a2704-118">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="a2704-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="a2704-119">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a2704-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="a2704-120">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="a2704-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="a2704-121">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="a2704-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="a2704-122">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="a2704-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* <span data-ttu-id="a2704-123">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="a2704-123">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>