---
title: aaaB2B samenwerking gebruikersclaims toewijzen in Azure Active Directory | Microsoft Docs
description: claims toewijzing verwijzing voor Azure Active Directory B2B-samenwerking
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
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="74318-103">B2B-samenwerking gebruikersclaims toewijzen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74318-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="74318-104">Azure Active Directory (Azure AD) ondersteunt Hallo uitgegeven claims in Hallo SAML-token voor B2B-samenwerking gebruikers aanpassen.</span><span class="sxs-lookup"><span data-stu-id="74318-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="74318-105">Als een gebruiker zich toohello toepassing verifieert, geeft Azure AD een SAML-token toohello-app met informatie (of claims) over Hallo-gebruiker die uniek wordt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="74318-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="74318-106">Dit omvat standaard gebruikersnaam, e-mailadres, voornaam en achternaam op Hallo van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74318-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="74318-107">U kunt weergeven of bewerken Hallo claims in Hallo SAML-token toohello toepassing hello kenmerken tabblad verzonden.</span><span class="sxs-lookup"><span data-stu-id="74318-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="74318-108">Er zijn twee mogelijke redenen waarom u tooedit Hallo uitgegeven claims in Hallo SAML-token wellicht.</span><span class="sxs-lookup"><span data-stu-id="74318-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="74318-109">Hallo-toepassing is geschreven toorequire een andere set claim URI's of claimwaarden</span><span class="sxs-lookup"><span data-stu-id="74318-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="74318-110">Uw toepassing vereist Hallo NameIdentifier claim toobe iets anders dan Hallo UPN opgeslagen in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="74318-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![weergave claims in SAML-token](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="74318-112">Raadpleeg voor informatie over hoe claims van tooadd en bewerken, in dit artikel op claims aanpassing, [uitgegeven claims in Hallo SAML-token voor vooraf geïntegreerde apps in Azure Active Directory aanpassen](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="74318-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="74318-113">Voor B2B-samenwerking, gebruikers, toewijzing NameID en UPN cross-tenant worden uit veiligheidsoverwegingen voorkomen.</span><span class="sxs-lookup"><span data-stu-id="74318-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="74318-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74318-114">Next steps</span></span>

<span data-ttu-id="74318-115">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="74318-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="74318-116">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="74318-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="74318-117">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="74318-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="74318-118">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="74318-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="74318-119">B2bB samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="74318-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="74318-120">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="74318-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="74318-121">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="74318-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="74318-122">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="74318-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="74318-123">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="74318-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="74318-124">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="74318-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="74318-125">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="74318-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
