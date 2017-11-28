---
title: Azure Active Directory B2B-samenwerking API en de aanpassing | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners selectief toegang te verlenen tot uw zakelijke toepassingen
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="8d75b-103">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="8d75b-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="8d75b-104">We hebben veel klanten laat ons weten dat ze willen aanpassen van het proces uitnodiging op een manier die het meest geschikt is voor hun organisatie gehad.</span><span class="sxs-lookup"><span data-stu-id="8d75b-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="8d75b-105">Met onze API kunt u dat doen.</span><span class="sxs-lookup"><span data-stu-id="8d75b-105">With our API, you can do just that.</span></span> [<span data-ttu-id="8d75b-106">https://Developer.Microsoft.com/Graph/Docs/API-Reference/V1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="8d75b-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="8d75b-107">Mogelijkheden van de uitnodiging API</span><span class="sxs-lookup"><span data-stu-id="8d75b-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="8d75b-108">De API biedt de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="8d75b-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="8d75b-109">Een externe gebruiker met uitnodigen *eventuele* e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="8d75b-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="8d75b-110">Aanpassen waar u uw gebruikers land wanneer ze hun uitnodiging hebt geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="8d75b-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="8d75b-111">Kies de uitnodiging voor een standaard e-mail via ons</span><span class="sxs-lookup"><span data-stu-id="8d75b-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="8d75b-112">met een bericht naar de ontvanger die u kunt aanpassen</span><span class="sxs-lookup"><span data-stu-id="8d75b-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="8d75b-113">En kies met cc: mensen die u wilt behouden in de lus uw uitnodigen deze medewerker.</span><span class="sxs-lookup"><span data-stu-id="8d75b-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="8d75b-114">Of volledig aanpassen aan uw uitnodiging en werkstroom voorbereiden door te kiezen geen om meldingen te verzenden via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d75b-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="8d75b-115">In dit geval terughalen u een inwisseling-URL van de API die u in een e-mailsjabloon, IM of andere distributiemethode van uw keuze insluiten kunt.</span><span class="sxs-lookup"><span data-stu-id="8d75b-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="8d75b-116">Ten slotte, als u een beheerder bent, kunt u om uit te nodigen van de gebruiker die lid is.</span><span class="sxs-lookup"><span data-stu-id="8d75b-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="8d75b-117">Autorisatie-model</span><span class="sxs-lookup"><span data-stu-id="8d75b-117">Authorization model</span></span>
<span data-ttu-id="8d75b-118">De API kan worden uitgevoerd in de volgende autorisatie-modi:</span><span class="sxs-lookup"><span data-stu-id="8d75b-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="8d75b-119">App + gebruikersmodus</span><span class="sxs-lookup"><span data-stu-id="8d75b-119">App + User mode</span></span>
<span data-ttu-id="8d75b-120">In deze modus is degene die de machtigingen om te worden uitnodigingen voor B2B met behulp van de behoeften van de API.</span><span class="sxs-lookup"><span data-stu-id="8d75b-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="8d75b-121">App alleen de modus</span><span class="sxs-lookup"><span data-stu-id="8d75b-121">App only mode</span></span>
<span data-ttu-id="8d75b-122">In de app alleen context moet de app de User.ReadWrite.All of Directory.ReadWrite.All bereiken voor de uitnodiging te kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d75b-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="8d75b-123">Raadpleeg voor meer informatie: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="8d75b-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="8d75b-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d75b-124">PowerShell</span></span>
<span data-ttu-id="8d75b-125">Het is nu mogelijk om te gebruiken van PowerShell toe te voegen en externe gebruikers uitnodigen voor een organisatie eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="8d75b-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="8d75b-126">Maak een uitnodiging met de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8d75b-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="8d75b-127">U kunt de volgende opties gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d75b-127">You can use the following options:</span></span>

* <span data-ttu-id="8d75b-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="8d75b-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="8d75b-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="8d75b-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="8d75b-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="8d75b-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="8d75b-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="8d75b-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="8d75b-132">U kunt ook de uitnodiging voor een API-verwijzing in uitchecken [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="8d75b-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d75b-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d75b-133">Next steps</span></span>

<span data-ttu-id="8d75b-134">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="8d75b-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8d75b-135">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="8d75b-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8d75b-136">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="8d75b-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="8d75b-137">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d75b-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="8d75b-138">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="8d75b-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="8d75b-139">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="8d75b-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="8d75b-140">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="8d75b-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="8d75b-141">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="8d75b-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="8d75b-142">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="8d75b-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="8d75b-143">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="8d75b-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="8d75b-144">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d75b-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="8d75b-145">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="8d75b-145">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
