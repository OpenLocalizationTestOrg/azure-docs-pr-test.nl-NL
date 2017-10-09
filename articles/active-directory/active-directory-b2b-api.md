---
title: aaaAzure Active Directory B2B-samenwerking API en de aanpassing | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners tooselectively toegang tot uw zakelijke toepassingen inschakelen
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="dcf4d-103">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="dcf4d-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="dcf4d-104">We hebben veel klanten laat ons weten dat ze willen toocustomize Hallo uitnodiging voor een proces op een manier die het meest geschikt is voor hun organisatie gehad.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="dcf4d-105">Met onze API kunt u dat doen.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-105">With our API, you can do just that.</span></span> [<span data-ttu-id="dcf4d-106">https://Developer.Microsoft.com/Graph/Docs/API-Reference/V1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="dcf4d-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="dcf4d-107">Mogelijkheden van Hallo uitnodiging API</span><span class="sxs-lookup"><span data-stu-id="dcf4d-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="dcf4d-108">Hallo API biedt Hallo volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="dcf4d-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="dcf4d-109">Een externe gebruiker met uitnodigen *eventuele* e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="dcf4d-110">Aanpassen waar u uw gebruikers tooland nadat ze hun uitnodiging accepteren.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="dcf4d-111">Kies toosend Hallo standaard uitnodiging e-mail via ons</span><span class="sxs-lookup"><span data-stu-id="dcf4d-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="dcf4d-112">met een bericht toohello-ontvanger die u kunt aanpassen</span><span class="sxs-lookup"><span data-stu-id="dcf4d-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="dcf4d-113">En kies toocc: gewenste tookeep in Hallo personen in een lus uw uitnodigen deze medewerker.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="dcf4d-114">Of volledig aanpassen aan uw uitnodiging en werkstroom voorbereiden door te kiezen geen toosend meldingen via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="dcf4d-115">In dit geval u weer een inwisseling-URL ophalen van Hallo-API die u in een e-mailsjabloon, IM of andere distributiemethode van uw keuze insluiten kunt.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="dcf4d-116">Ten slotte, als u een beheerder bent, kunt u tooinvite Hallo gebruiker als lid.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="dcf4d-117">Autorisatie-model</span><span class="sxs-lookup"><span data-stu-id="dcf4d-117">Authorization model</span></span>
<span data-ttu-id="dcf4d-118">Hallo API kan worden uitgevoerd in Hallo autorisatie modi te volgen:</span><span class="sxs-lookup"><span data-stu-id="dcf4d-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="dcf4d-119">App + gebruikersmodus</span><span class="sxs-lookup"><span data-stu-id="dcf4d-119">App + User mode</span></span>
<span data-ttu-id="dcf4d-120">In deze modus gebruikt degene die behoeften Hallo API toohave Hallo machtigingen toobe B2B uitnodigingen maken.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="dcf4d-121">App alleen de modus</span><span class="sxs-lookup"><span data-stu-id="dcf4d-121">App only mode</span></span>
<span data-ttu-id="dcf4d-122">Hallo-app moet in de app alleen context, Hallo User.ReadWrite.All of Directory.ReadWrite.All scopes voor Hallo uitnodiging toosucceed.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="dcf4d-123">Raadpleeg voor meer informatie: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="dcf4d-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="dcf4d-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcf4d-124">PowerShell</span></span>
<span data-ttu-id="dcf4d-125">Het is nu mogelijk toouse PowerShell tooadd en uitnodiging externe gebruikers tooan organisatie eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="dcf4d-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="dcf4d-126">Maak een uitnodiging met Hallo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dcf4d-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="dcf4d-127">U kunt Hallo volgende opties gebruiken:</span><span class="sxs-lookup"><span data-stu-id="dcf4d-127">You can use hello following options:</span></span>

* <span data-ttu-id="dcf4d-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="dcf4d-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="dcf4d-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="dcf4d-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="dcf4d-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="dcf4d-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="dcf4d-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="dcf4d-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="dcf4d-132">U kunt ook Hallo uitnodiging voor een API-verwijzing in uitchecken [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="dcf4d-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcf4d-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dcf4d-133">Next steps</span></span>

<span data-ttu-id="dcf4d-134">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="dcf4d-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dcf4d-135">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="dcf4d-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dcf4d-136">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="dcf4d-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="dcf4d-137">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="dcf4d-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="dcf4d-138">Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="dcf4d-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="dcf4d-139">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="dcf4d-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="dcf4d-140">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="dcf4d-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="dcf4d-141">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="dcf4d-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="dcf4d-142">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="dcf4d-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="dcf4d-143">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="dcf4d-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="dcf4d-144">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="dcf4d-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="dcf4d-145">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="dcf4d-145">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
