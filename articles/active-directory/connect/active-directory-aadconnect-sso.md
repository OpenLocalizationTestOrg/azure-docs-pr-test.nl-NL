---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding | Microsoft Docs'
description: Dit onderwerp beschrijft de Azure Active Directory (Azure AD) naadloze eenmalige aanmelding en hoe kunt u tooprovide true eenmalige aanmelding voor desktop-zakelijke gebruikers binnen uw bedrijfsnetwerk.
services: active-directory
keywords: Wat is Azure AD Connect, installeer Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory naadloze eenmalige aanmelding

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Wat is Azure Active Directory naadloze eenmalige aanmelding?

Azure Active Directory naadloze eenmalige aanmelding (Azure AD naadloze SSO) wordt automatisch aangemeld gebruikers wanneer ze zijn op hun apparaten het bedrijf verbonden tooyour bedrijfsnetwerk bevinden. Wanneer ingeschakeld, niet gebruikers moet tootype in hun wachtwoorden toosign in tooAzure AD en meestal, zelfs in hun gebruikersnamen typen. Deze functie biedt uw gebruikers eenvoudig toegang tooyour cloud-gebaseerde toepassingen zonder extra on-premises onderdelen.

Naadloze eenmalige aanmelding kan worden gecombineerd met de Hallo [synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md) of [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md) aanmeldingsmethoden.

![Naadloze eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>Naadloze eenmalige aanmelding is momenteel in preview. Deze functie is _niet_ toepasselijke tooActive Directory Federation Services (ADFS).

## <a name="key-benefits"></a>Belangrijkste voordelen

- *Gebruikerservaring*
  - Gebruikers worden automatisch aangemeld bij zowel on-premises en cloudtoepassingen.
  - Gebruikers hebben geen tooenter hun wachtwoorden herhaaldelijk.
- *Eenvoudig toodeploy & beheren*
  - Er zijn geen extra onderdelen nodig lokale toomake dit werk.
  - Werkt met een cloud-verificatie --methode [synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md) of [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md).
  - Kan worden teruggedraaid toosome of alle gebruikers met behulp van Groepsbeleid.
  - Windows 10-apparaten registreren met Azure AD zonder Hallo nodig is voor een AD FS-infrastructuur. Deze mogelijkheid moet u toouse versie 2.1 of hoger Hallo [client voor werkplek koppelen](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Highlights van functie

- Aanmeldnaam mag ofwel Hallo lokale standaardgebruikersnaam (`userPrincipalName`) of een ander kenmerk geconfigureerd in Azure AD Connect (`Alternate ID`). Beide gevallen werken niet gebruiken omdat naadloze eenmalige aanmelding Hallo gebruikt `securityIdentifier` claim in Hallo Kerberos-ticket toolook upobject Hallo overeenkomende gebruiker in Azure AD.
- Naadloze eenmalige aanmelding is een opportunistisch functie. Als het om een bepaalde reden mislukt, Hallo aanmelden gebruikerservaring terug tooits reguliere gedrag - eenledige, Hallo gebruiker moet tooenter hun wachtwoord op de aanmeldingspagina Hallo.
- Als een toepassing stuurt een `domain_hint` (OpenID Connect) of `whr` (SAML) parameter - identificeren van uw tenant of `login_hint` parameter - Hallo-gebruiker te identificeren in de Azure AD-in aanvraag gebruikers worden automatisch aangemeld zonder ze gebruikersnamen of wachtwoorden invoeren.
- Het kan worden ingeschakeld via Azure AD Connect.
- Dit is een gratis functie en hoeft u niet alle betaald edities van Azure AD-toouse deze.
- Het wordt ondersteund op het web browser gebaseerde en Office-clients die ondersteuning bieden voor [moderne verificatie](https://aka.ms/modernauthga) op platforms en browsers die geschikt is voor Kerberos-verificatie:

| OS\Browser |Internet Explorer|Rand|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Ja|Nee|Ja|Ja\*|N.v.t.
|Windows 8.1|Ja|N.v.t.|Ja|Ja\*|N.v.t.
|Windows 8|Ja|N.v.t.|Ja|Ja\*|N.v.t.
|Windows 7|Ja|N.v.t.|Ja|Ja\*|N.v.t.
|Mac OS X|N.v.t.|N.v.t.|Ja\*|Ja\*|Ja\*

\*Vereist [aanvullende configuratie](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>We onlangs teruggedraaid ondersteuning voor rand tooinvestigate klanten gemelde problemen.

>[!NOTE]
>Voor Windows 10 is Hallo aanbeveling toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) voor Hallo optimale eenmalige aanmelding ervaring met Azure AD.

## <a name="next-steps"></a>Volgende stappen

- [**Snel starten** ](active-directory-aadconnect-sso-quick-start.md) - laten en Azure AD naadloze eenmalige aanmelding wordt uitgevoerd.
- [**Technische diepgaand** ](active-directory-aadconnect-sso-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
