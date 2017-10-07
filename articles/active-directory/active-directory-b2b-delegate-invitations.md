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
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Gemachtigde uitnodigingen voor Azure Active Directory B2B-samenwerking

Met business-to-business (B2B)-samenwerking van Azure Active Directory (Azure AD), hoeft u geen toobe een globale beheerder toosend uitnodigingen. U kunt in plaats daarvan gebruik van beleid en uitnodigingen toousers waarvan rollen toosend uitnodigingen kunnen delegeren. Er is een belangrijke nieuwe manier toodelegate Gast gebruiker uitnodigingen via Hallo Gast uitnodiging antwoorden functie.

## <a name="guest-inviter-role"></a>Rol van Gast uitnodiging antwoorden
We kunnen Hallo gebruiker tooGuest uitnodiging antwoorden rol toosend uitnodigingen toewijzen. U hebt geen toobe lid van de rol toosend uitnodigingen voor Hallo globale beheerder. Standaard aanroepen gewone gebruikers ook Hallo uitnodiging API als een globale beheerder uitgeschakeld uitnodigingen voor reguliere gebruikers. Een gebruiker kan ook met hello Azure-portal of PowerShell Hallo-API aanroepen.

Hier volgt een voorbeeld ziet u hoe toouse PowerShell tooadd een gebruikersrol voor toohello Gast uitnodiging antwoorden:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Beheren wie kunt uitnodigen

![Besturingselement hoe tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Een tenantbeheerder kan Hallo volgende uitnodiging beleidsregels instellen met Azure AD B2B-samenwerking:

- Uitnodigingen uitschakelen
- Alleen beheerders en gebruikers in Hallo Gast uitnodiging antwoorden rol kunnen uitnodigen
- Beheerders, Hallo Gast uitnodiging antwoorden rol en leden kunnen uitnodigen
- Alle gebruikers bevat, inclusief gasten, kunnen uitnodigen

Standaard tenants te worden ingesteld #4. (U kunnen B2B gebruikers uitnodigen voor alle gebruikers, met inbegrip van gastgebruikers.)

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [SaaS-apps voor B2B-samenwerking configureren](active-directory-b2b-configure-saas-apps.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)
