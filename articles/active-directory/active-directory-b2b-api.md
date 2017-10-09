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
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Azure Active Directory B2B-samenwerking API en de aanpassing

We hebben veel klanten laat ons weten dat ze willen toocustomize Hallo uitnodiging voor een proces op een manier die het meest geschikt is voor hun organisatie gehad. Met onze API kunt u dat doen. [https://Developer.Microsoft.com/Graph/Docs/API-Reference/V1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Mogelijkheden van Hallo uitnodiging API
Hallo API biedt Hallo volgende mogelijkheden:

1. Een externe gebruiker met uitnodigen *eventuele* e-mailadres.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Aanpassen waar u uw gebruikers tooland nadat ze hun uitnodiging accepteren.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Kies toosend Hallo standaard uitnodiging e-mail via ons

    ```
    "sendInvitationMessage": true
    ```

  met een bericht toohello-ontvanger die u kunt aanpassen

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. En kies toocc: gewenste tookeep in Hallo personen in een lus uw uitnodigen deze medewerker.

5. Of volledig aanpassen aan uw uitnodiging en werkstroom voorbereiden door te kiezen geen toosend meldingen via Azure AD.

    ```
    "sendInvitationMessage": false
    ```

  In dit geval u weer een inwisseling-URL ophalen van Hallo-API die u in een e-mailsjabloon, IM of andere distributiemethode van uw keuze insluiten kunt.

6. Ten slotte, als u een beheerder bent, kunt u tooinvite Hallo gebruiker als lid.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Autorisatie-model
Hallo API kan worden uitgevoerd in Hallo autorisatie modi te volgen:

### <a name="app--user-mode"></a>App + gebruikersmodus
In deze modus gebruikt degene die behoeften Hallo API toohave Hallo machtigingen toobe B2B uitnodigingen maken.

### <a name="app-only-mode"></a>App alleen de modus
Hallo-app moet in de app alleen context, Hallo User.ReadWrite.All of Directory.ReadWrite.All scopes voor Hallo uitnodiging toosucceed.

Raadpleeg voor meer informatie: https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
Het is nu mogelijk toouse PowerShell tooadd en uitnodiging externe gebruikers tooan organisatie eenvoudig. Maak een uitnodiging met Hallo cmdlet:

```
New-AzureADMSInvitation
```

U kunt Hallo volgende opties gebruiken:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

U kunt ook Hallo uitnodiging voor een API-verwijzing in uitchecken [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking](active-directory-b2b-invitation-email.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B-samenwerking licentieverlening](active-directory-b2b-licensing.md)
* [Het oplossen van Azure Active Directory B2B-samenwerking](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)](active-directory-b2b-faq.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
