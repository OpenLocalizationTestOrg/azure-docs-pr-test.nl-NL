---
title: uitnodigingen voor Azure Active Directory B2B-samenwerking aaaDelegate | Microsoft Docs
description: Azure Active Directory B2B-samenwerking gebruikerseigenschappen kunnen worden geconfigureerd
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="cc847-103">Gemachtigde uitnodigingen voor Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="cc847-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="cc847-104">Met business-to-business (B2B)-samenwerking van Azure Active Directory (Azure AD), hoeft u geen toobe een globale beheerder toosend uitnodigingen.</span><span class="sxs-lookup"><span data-stu-id="cc847-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="cc847-105">U kunt in plaats daarvan gebruik van beleid en uitnodigingen toousers waarvan rollen toosend uitnodigingen kunnen delegeren.</span><span class="sxs-lookup"><span data-stu-id="cc847-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="cc847-106">Er is een belangrijke nieuwe manier toodelegate Gast gebruiker uitnodigingen via Hallo Gast uitnodiging antwoorden functie.</span><span class="sxs-lookup"><span data-stu-id="cc847-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="cc847-107">Rol van Gast uitnodiging antwoorden</span><span class="sxs-lookup"><span data-stu-id="cc847-107">Guest Inviter role</span></span>
<span data-ttu-id="cc847-108">We kunnen Hallo gebruiker tooGuest uitnodiging antwoorden rol toosend uitnodigingen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="cc847-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="cc847-109">U hebt geen toobe lid van de rol toosend uitnodigingen voor Hallo globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="cc847-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="cc847-110">Standaard aanroepen gewone gebruikers ook Hallo uitnodiging API als een globale beheerder uitgeschakeld uitnodigingen voor reguliere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cc847-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="cc847-111">Een gebruiker kan ook met hello Azure-portal of PowerShell Hallo-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cc847-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="cc847-112">Hier volgt een voorbeeld ziet u hoe toouse PowerShell tooadd een gebruikersrol voor toohello Gast uitnodiging antwoorden:</span><span class="sxs-lookup"><span data-stu-id="cc847-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="cc847-113">Beheren wie kunt uitnodigen</span><span class="sxs-lookup"><span data-stu-id="cc847-113">Control who can invite</span></span>

![Besturingselement hoe tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="cc847-115">Een tenantbeheerder kan Hallo volgende uitnodiging beleidsregels instellen met Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="cc847-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="cc847-116">Uitnodigingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="cc847-116">Turn off invitations</span></span>
- <span data-ttu-id="cc847-117">Alleen beheerders en gebruikers in Hallo Gast uitnodiging antwoorden rol kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="cc847-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="cc847-118">Beheerders, Hallo Gast uitnodiging antwoorden rol en leden kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="cc847-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="cc847-119">Alle gebruikers bevat, inclusief gasten, kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="cc847-119">All users, including guests, can invite</span></span>

<span data-ttu-id="cc847-120">Standaard tenants te worden ingesteld #4.</span><span class="sxs-lookup"><span data-stu-id="cc847-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="cc847-121">(U kunnen B2B gebruikers uitnodigen voor alle gebruikers, met inbegrip van gastgebruikers.)</span><span class="sxs-lookup"><span data-stu-id="cc847-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc847-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc847-122">Next steps</span></span>

<span data-ttu-id="cc847-123">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="cc847-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="cc847-124">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="cc847-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="cc847-125">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="cc847-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="cc847-126">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="cc847-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="cc847-127">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="cc847-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="cc847-128">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="cc847-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="cc847-129">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="cc847-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="cc847-130">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="cc847-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="cc847-131">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="cc847-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="cc847-132">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="cc847-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="cc847-133">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="cc847-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
