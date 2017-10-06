---
title: aaaConditional-toegang voor gebruikers van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Azure Active Directory B2B-samenwerking ondersteunt multi-factor authentication (MFA) voor selectieve toegang tooyour zakelijke toepassingen
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Voorwaardelijke toegang voor gebruikers voor B2B-samenwerking

## <a name="multi-factor-authentication-for-b2b-users"></a>Multi-factor authentication voor B2B-gebruikers
Met de Azure AD B2B-samenwerking organisaties kunnen multi-factor authentication (MFA) beleid afdwingen voor B2B-gebruikers. Dit beleid kunnen worden afgedwongen op het Hallo-tenant, app of afzonderlijke gebruikersniveau, hello dezelfde manier als ze zijn ingeschakeld voor fulltime werknemers en leden van het Hallo-organisatie. MFA-beleid wordt afgedwongen op Hallo bronorganisatie.

Voorbeeld:
1. Beheerder of de werknemer in bedrijf A nodigt gebruiker uit bedrijf B tooan toepassing *Foo* in bedrijf A.
2. Toepassing *Foo* in bedrijf is een geconfigureerde toorequire MFA op toegang.
3. Wanneer de gebruiker Hallo van bedrijf B tooaccess app probeert *Foo* in Hallo bedrijf een tenant, zijn ze toocomplete gevraagd een challenge MFA.
4. Hallo gebruiker hun MFA met bedrijf A kunt instellen en de MFA-optie kiest.
5. Dit scenario is geschikt voor een identiteit (Azure AD of MSA, bijvoorbeeld, als gebruikers van bedrijf B zich verifiëren met behulp van sociale ID)
6. Bedrijf A moet voldoende Azure AD Premium-licenties die ondersteuning bieden voor MFA hebt. Hallo gebruiker uit bedrijf B verbruikt deze licentie van bedrijf A.

Hallo nodigen tenancymodus is altijd verantwoordelijk zijn voor MFA voor gebruikers van de partnerorganisatie Hallo, zelfs als Hallo partnerorganisatie MFA mogelijkheden heeft.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>MFA in te stellen voor gebruikers voor B2B-samenwerking
toodiscover hoe eenvoudig het is tooset van MFA voor B2B-samenwerking gebruikers, Zie hoe in Hallo volgende video:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>B2B-gebruikers MFA voor ervaren bieden inwisseling
Bekijk Hallo animatie toosee Hallo inwisseling ervaring te volgen:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>MFA voor B2B-samenwerking gebruikers opnieuw instellen
Op dit moment Hallo beheerder kan vereisen B2B-samenwerking gebruikers tooproof up opnieuw alleen met behulp van PowerShell-cmdlets volgen Hallo:

1. Verbinding maken met tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Alle gebruikers krijgen met bewijs van methoden

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Hier volgt een voorbeeld:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Hallo MFA-methode voor een specifieke gebruiker toorequire Hallo B2B-samenwerking gebruiker tooset bewijs van methoden opnieuw instellen. Voorbeeld:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Waarom we MFA op Hallo resource tenancymodus uitvoeren?

In de huidige release Hallo is MFA altijd in Hallo resource tenancymodus omwille van de hoge voorspelbaarheid is vereist. Stel dat bijvoorbeeld een gebruiker Contoso (Sandra) uitgenodigde tooFabrikam en Fabrikam MFA voor B2B-gebruikers heeft ingeschakeld.

Als Contoso ingeschakeld voor App1, maar niet App2 MFA-beleid heeft, klikt u vervolgens als we hello Contoso MFA claim in Hallo-token bekijkt, mogelijk zien we Hallo na:

* Dag 1: Een gebruiker heeft MFA in Contoso en toegang heeft tot App1 en er zijn geen extra MFA prompt wordt weergegeven in Fabrikam.

* Dag 2: Hallo gebruiker toegang heeft gehad tot 2 van de App in Contoso, dus bij het openen van Fabrikam, moeten ze zich registreren voor MFA er.

Dit proces kan verwarrend zijn en leiden toodrop in aanmelden voltooiingen.

Bovendien, zelfs als Contoso MFA-mogelijkheid heeft, is het niet altijd Hallo case Hallo Fabrikam zou vertrouwen Hallo Contoso MFA-beleid.

Tot slot werkt resource tenant MFA ook voor MSA's en sociale-id's en voor de partner-organisaties waarvoor geen MFA instellen.

Hallo aanbeveling voor MFA voor B2B-gebruikers is daarom tooalways MFA in Hallo uitnodigen tenant vereisen. Deze vereiste toodouble MFA in sommige gevallen kan leiden, maar wanneer toegang tot Hallo nodigen tenant, Hallo-ervaring voor eindgebruikers is voorspelbaar: Sandra moet registreren voor MFA bij Hallo nodigen tenant.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Op basis van apparaten, op basis van locatie en risico gebaseerde voorwaardelijke toegang voor B2B-gebruikers

Wanneer Contoso beleidsregels voor voorwaardelijke toegang op basis van apparaten voor hun zakelijke gegevens kunt, wordt toegang niet van apparaten die niet worden beheerd door Contoso en niet compatibel zijn met beleidsregels Hallo Contoso-apparaten.

Als Hallo B2B gebruikersapparaat wordt niet beheerd door Contoso, toegang van gebruikers van Hallo partnerorganisaties B2B geblokkeerd en in welke context deze beleidsregels worden afgedwongen. Contoso kan echter uitsluiting lijsten met specifieke partner gebruikers tooexclude Hallo van beleid voor voorwaardelijke toegang op basis van apparaten te maken.

#### <a name="location-based-conditional-access-for-b2b"></a>Voorwaardelijke toegang voor B2B op basis van locatie

Beleid voor voorwaardelijke toegang op basis van locatie kunnen worden afgedwongen voor B2B-gebruikers als Hallo nodigen organisatie kunnen toocreate een vertrouwde IP-adresbereik dat hun partnerorganisaties definieert.

#### <a name="risk-based-conditional-access-for-b2b"></a>Voorwaardelijke toegang op basis van een risico voor B2B

Op dit moment aanmelden beleid op basis van risico's die toegepaste tooB2B gebruikers kunnen niet worden, omdat Hallo risico-evaluatie wordt uitgevoerd op thuisorganisatie Hallo B2B van de gebruiker.

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
* [Azure Active Directory B2B-samenwerking API en de aanpassing](active-directory-b2b-api.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
