---
title: B2B-samenwerking gebruikersclaims toewijzen in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="9dee0-103">B2B-samenwerking gebruikersclaims toewijzen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9dee0-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="9dee0-104">Azure Active Directory (Azure AD) ondersteunt het aanpassen van de uitgegeven claims in het SAML-token voor B2B-samenwerking gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9dee0-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="9dee0-105">Wanneer een gebruiker zich bij de toepassing verifieert, verstrekt Azure AD een SAML-token aan de app die informatie (of claims) bevat over de gebruiker die uniek wordt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="9dee0-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="9dee0-106">Dit omvat standaard gebruikersnaam, e-mailadres, de voornaam en achternaam van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9dee0-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="9dee0-107">U kunt weergeven of bewerken van de claims in het SAML-token naar de toepassing op het tabblad kenmerken verzonden.</span><span class="sxs-lookup"><span data-stu-id="9dee0-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="9dee0-108">Er zijn twee mogelijke redenen waarom moet u mogelijk de uitgegeven claims in het SAML-token bewerken.</span><span class="sxs-lookup"><span data-stu-id="9dee0-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="9dee0-109">De toepassing is geschreven naar een andere set claimregels URI's is vereist of claimwaarden</span><span class="sxs-lookup"><span data-stu-id="9dee0-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="9dee0-110">Uw toepassing vereist dat de NameIdentifier claim iets anders dan de user principal name opgeslagen in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9dee0-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![weergave claims in SAML-token](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="9dee0-112">Bekijk voor meer informatie over het toevoegen en bewerken van claims, in dit artikel op claims aanpassing, [uitgegeven claims in het SAML-token voor vooraf geïntegreerde apps in Azure Active Directory aanpassen](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="9dee0-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="9dee0-113">Voor B2B-samenwerking, gebruikers, toewijzing NameID en UPN cross-tenant worden uit veiligheidsoverwegingen voorkomen.</span><span class="sxs-lookup"><span data-stu-id="9dee0-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9dee0-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9dee0-114">Next steps</span></span>

<span data-ttu-id="9dee0-115">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="9dee0-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9dee0-116">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="9dee0-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9dee0-117">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9dee0-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="9dee0-118">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="9dee0-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="9dee0-119">B2bB samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="9dee0-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="9dee0-120">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9dee0-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="9dee0-121">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9dee0-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="9dee0-122">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="9dee0-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="9dee0-123">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="9dee0-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="9dee0-124">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="9dee0-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="9dee0-125">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9dee0-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
