---
title: Uitnodigingen voor Azure Active Directory B2B-samenwerking delegeren | Microsoft Docs
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="9f130-103">Gemachtigde uitnodigingen voor Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9f130-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="9f130-104">Samenwerking van Azure Active Directory (Azure AD)-business-to-business (B2B), moet u beschikt niet over een globale beheerder uitnodigingen verzenden.</span><span class="sxs-lookup"><span data-stu-id="9f130-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="9f130-105">In plaats daarvan kunt u beleidsregels gebruiken en uitnodigingen voor gebruikers waarvan rollen kunnen worden uitnodiging delegeren.</span><span class="sxs-lookup"><span data-stu-id="9f130-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="9f130-106">Er is een belangrijke nieuwe manier om te delegeren Gast gebruiker uitnodigingen via de functie Gast uitnodiging antwoorden.</span><span class="sxs-lookup"><span data-stu-id="9f130-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="9f130-107">Rol van Gast uitnodiging antwoorden</span><span class="sxs-lookup"><span data-stu-id="9f130-107">Guest Inviter role</span></span>
<span data-ttu-id="9f130-108">We kan de gebruiker toewijzen aan de rol van Gast uitnodiging antwoorden uitnodigingen verzenden.</span><span class="sxs-lookup"><span data-stu-id="9f130-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="9f130-109">U hoeft niet te worden lid van de rol globale beheerder uitnodigingen verzenden.</span><span class="sxs-lookup"><span data-stu-id="9f130-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="9f130-110">Standaard aanroepen gewone gebruikers ook de uitnodiging-API als een globale beheerder uitgeschakeld uitnodigingen voor reguliere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9f130-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="9f130-111">Een gebruiker kan ook de met de Azure-portal of PowerShell API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9f130-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="9f130-112">Hier volgt een voorbeeld ziet u hoe u een gebruiker toevoegen aan de rol van Gast uitnodiging antwoorden met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9f130-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="9f130-113">Beheren wie kunt uitnodigen</span><span class="sxs-lookup"><span data-stu-id="9f130-113">Control who can invite</span></span>

![Beheren hoe om uit te nodigen](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="9f130-115">Een tenantbeheerder kan de volgende beleidsregels voor uitnodiging ingesteld met Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="9f130-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="9f130-116">Uitnodigingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="9f130-116">Turn off invitations</span></span>
- <span data-ttu-id="9f130-117">Alleen beheerders en gebruikers in de rol van Gast uitnodiging antwoorden kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="9f130-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="9f130-118">Beheerders, de rol van Gast uitnodiging antwoorden en leden kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="9f130-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="9f130-119">Alle gebruikers bevat, inclusief gasten, kunnen uitnodigen</span><span class="sxs-lookup"><span data-stu-id="9f130-119">All users, including guests, can invite</span></span>

<span data-ttu-id="9f130-120">Tenants zijn standaard ingesteld op #4.</span><span class="sxs-lookup"><span data-stu-id="9f130-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="9f130-121">(U kunnen B2B gebruikers uitnodigen voor alle gebruikers, met inbegrip van gastgebruikers.)</span><span class="sxs-lookup"><span data-stu-id="9f130-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f130-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f130-122">Next steps</span></span>

<span data-ttu-id="9f130-123">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="9f130-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9f130-124">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="9f130-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9f130-125">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9f130-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="9f130-126">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="9f130-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="9f130-127">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9f130-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="9f130-128">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f130-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="9f130-129">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="9f130-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="9f130-130">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="9f130-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="9f130-131">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="9f130-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="9f130-132">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="9f130-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="9f130-133">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="9f130-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
