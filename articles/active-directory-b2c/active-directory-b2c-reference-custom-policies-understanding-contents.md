---
title: 'Azure Active Directory B2C: Informatie over aangepaste beleidsregels van Hallo starter pack | Microsoft Docs'
description: Een onderwerp op Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Aangepaste beleidsregels van hello Azure AD B2C aangepast beleid starter pack Hallo begrijpen

Deze sectie vindt u alle Hallo core elementen van Hallo B2C_1A_base beleid dat wordt geleverd met Hallo **Starter Pack** en die wordt gebruikt voor het ontwerpen van uw eigen beleid via overname Hallo Hallo *B2C_1A_base_ beleid voor uitbreidingen*.

Als zodanig deze meer met name is gericht op het Hallo al gedefinieerd claim typen, claimtransformaties, definities van inhoud, claimproviders met hun technische profielen en core gebruiker trajecten Hallo.

> [!IMPORTANT]
> Microsoft biedt geen enkele expliciete of impliciete, met ten opzichte van toohello informatie hierna opgegeven. Wijzigingen kunnen worden ingevoerd op elk moment vóór GA tijdstip, GA tijdens of na.

Uw eigen beleid en de Hallo B2C_1A_base_extensions beleid kunnen deze definities overschrijven en uitbreiden van het beleid van dit bovenliggende verstrekken die aanvullende bepalingen nodig.

hoofdonderdelen van Hallo Hallo *B2C_1A_base beleid* zijn claimtypen, claimtransformaties en inhoud definities. Deze elementen kunnen vatbaar toobe waarnaar wordt verwezen in uw eigen beleid ook als in Hallo *B2C_1A_base_extensions beleid*.

## <a name="claims-schemas"></a>Claims schema 's

Dit claims schema's is onderverdeeld in drie secties:

1.  Een eerste sectie worden de minimale Hallo-claims die vereist voor Hallo gebruiker trajecten toowork goed zijn.
2.  Een tweede sectie dat een lijst met claims die zijn vereist voor queryreeksparameters Hallo en andere toobe speciale parameters tooother claimproviders doorgegeven, met name login.microsoftonline.com voor verificatie. **Wijzig geen deze claims**.
3.  En uiteindelijk een derde sectie met een lijst met aanvullende, optionele claims die kunnen worden verzameld van de gebruiker hello, opgeslagen in de directory hello en in tokens verzonden tijdens het aanmelden. Nieuwe claims type toobe verzameld van Hallo gebruiker en/of verzonden in Hallo token kunnen in deze sectie worden toegevoegd.

> [!IMPORTANT]
> Hallo claims schema bevat beperkingen op bepaalde claims zoals wachtwoorden en gebruikersnamen. Hallo vertrouwen Framework (TF) beleid behandelt Azure AD als andere claimprovider en alle bijbehorende beperkingen zijn gemodelleerd in Hallo premium beleid. Een beleid kan worden gewijzigd tooadd meer beperkingen of een andere claimprovider gebruiken voor de opslag van referenties waarvoor een eigen beperkingen.

Hallo beschikbaar claimtypen worden hieronder vermeld.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Claims die vereist voor Hallo gebruiker trajecten zijn

Hallo na claims zijn vereist voor gebruiker trajecten toowork correct:

| Claims type | Beschrijving |
|-------------|-------------|
| *Gebruikers-id* | Gebruikersnaam |
| *signInName* | Meld u aan de naam |
| *tenantId* | Tenant-id (ID) van het gebruikersobject Hallo in Azure AD B2C Premium |
| *object-id* | Object-id (ID) van het gebruikersobject Hallo in Azure AD B2C Premium |
| *wachtwoord* | Wachtwoord |
| *NieuwWachtwoord* | |
| *reenterPassword* | |
| *passwordPolicies* | Wachtwoordbeleid gebruikt door Azure AD B2C Premium toodetermine Wachtwoordsterkte, verlopen, enzovoort. |
| *Sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *Weergavenaam* | |
| *strongAuthenticationPhoneNumber* | Het telefoonnummer van de gebruiker |
| *Verified.strongAuthenticationPhoneNumber* | |
| *E-mail* | E-mailadres dat gebruikt toocontact Hallo gebruiker worden kan |
| *signInNamesInfo.emailAddress* | E-mailadres dat Hallo gebruiker kunt toosign in gebruiken |
| *otherMails* | E-mailadressen die gebruikt toocontact Hallo gebruiker worden kunnen |
| *userPrincipalName* | De gebruikersnaam die is opgeslagen in Azure AD B2C Premium Hallo |
| *upnUserName* | Gebruikersnaam voor het maken van de UPN-naam |
| *mailNickName* | De naam van gebruiker e-mail nick die is opgeslagen in Azure AD B2C Premium Hallo |
| *nieuwegebruiker* | |
| *uitgevoerd SelfAsserted invoer* | Claim die aangeeft of de kenmerken van de gebruiker Hallo zijn verzameld |
| *uitgevoerd PhoneFactor invoer* | Claim waarmee wordt aangegeven of een nieuw telefoonnummer Hallo gebruiker is verzameld |
| *authenticationSource* | Hiermee geeft u op of Hallo gebruiker is geverifieerd op sociale id-Provider, login.microsoftonline.com of lokale account |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Claims die vereist zijn voor queryreeksparameters en andere speciale parameters

Hallo zijn volgende claims vereiste toopass op speciale parameters (inclusief een aantal queryreeksparameters) tooother claimproviders:

| Claims type | Beschrijving |
|-------------|-------------|
| *Nux* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *NCA* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *prompt* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *Mkt* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *kredietbrief* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *grant_type* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *bereik* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *client_id* | Speciale parameter doorgegeven voor lokaal account verificatie toologin.microsoftonline.com |
| *objectIdFromSession* | Opgegeven door Hallo standaard sessie management provider tooindicate die Hallo object-id-parameter is opgehaald van een sessie voor eenmalige aanmelding |
| *isActiveMFASession* | De parameter opgegeven door Hallo MFA sessie management tooindicate dat die Hallo de gebruiker heeft een actieve sessie voor MFA |

### <a name="additional-optional-claims-that-can-be-collected"></a>Aanvullende (optioneel) claims die kunnen worden verzameld

Hallo volgende claims zijn extra claims die kunnen worden verzameld van Hallo gebruikers, opgeslagen in de directory hello en in Hallo token verzonden. Zoals beschreven voordat, kunnen aanvullende claims toothis lijst worden toegevoegd.

| Claims type | Beschrijving |
|-------------|-------------|
| *Voornaam* | Van de gebruiker opgegeven naam (ook wel bekend als voornaam) |
| *Achternaam* | De achternaam van de gebruiker (ook wel bekend als familienaam of achternaam) |
| *Extension_picture* | Afbeelding van de gebruiker op sociale |

## <a name="claim-transformations"></a>Claimtransformaties

Hallo beschikbaar claimtransformaties worden hieronder vermeld.

| Claim-transformatie | Beschrijving |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Definities van inhoud

Deze sectie beschrijft Hallo inhoud definities al gedeclareerd in Hallo *B2C_1A_base* beleid. Deze inhoud definities zijn vatbaar toobe waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.

| Claimprovider | Beschrijving |
|-----------------|-------------|
| *Facebook* | |
| *Aanmelding voor lokaal Account* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Self die wordt beweerd* | |
| *Lokaal Account* | |
| *Sessiebeheer* | |
| *Beleidsengine Trustframework* | |
| *TechnicalProfiles* | |
| *Uitgever van beveiligingstoken* | |

## <a name="technical-profiles"></a>Technische profielen

Deze sectie beschrijft Hallo technische profielen al gedeclareerd voor de claimprovider in Hallo *B2C_1A_base* beleid. Deze technische profielen zijn vatbaar toobe verdere waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.

### <a name="technical-profiles-for-facebook"></a>Technische profielen voor Facebook

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *Facebook OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Technische profielen voor lokale aanmelding met Account

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *Aanmelding niet-interactieve* | |

### <a name="technical-profiles-for-phone-factor"></a>Technische profielen voor Phone Factor

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *PhoneFactor-invoer* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor controleren* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Technische profielen voor Azure Active Directory

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *AAD-algemeen* | Technische profiel die zijn opgenomen in de Hallo andere technische AAD-xxx-profielen |
| *AAD-UserWriteUsingAlternativeSecurityId* | Technische profiel voor het sociaal-aanmeldingen |
| *AAD-UserReadUsingAlternativeSecurityId* | Technische profiel voor het sociaal-aanmeldingen |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Technische profiel voor het sociaal-aanmeldingen |
| *AAD-UserWritePasswordUsingLogonEmail* | Technische profiel voor lokale accounts |
| *AAD-UserReadUsingEmailAddress* | Technische profiel voor lokale accounts |
| *AAD-UserWriteProfileUsingObjectId* | Technische profiel voor het bijwerken van de gebruikersrecord met object-id |
| *AAD-UserWritePhoneNumberUsingObjectId* | Technische profiel voor het bijwerken van de gebruikersrecord met object-id |
| *AAD-UserWritePasswordUsingObjectId* | Technische profiel voor het bijwerken van de gebruikersrecord met object-id |
| *AAD-UserReadUsingObjectId* | Technische profiel is gebruikte tooread gegevens nadat de gebruiker wordt geverifieerd |

### <a name="technical-profiles-for-self-asserted"></a>Technische profielen voor Self die wordt beweerd

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *SelfAsserted sociale* | |
| *SelfAsserted ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Technische profielen voor lokaal Account

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Technische profielen voor sessiebeheer

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *SM-NoOperation* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Profielnaam wordt gebruikte toodisambiguate AAD sessie tussen sign up en aanmelden |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Technische profielen voor Trustframework beleid Engine TechnicalProfiles

Momenteel geen technische profielen zijn gedefinieerd voor Hallo **Trustframework beleid Engine TechnicalProfiles** claimprovider.

### <a name="technical-profiles-for-token-issuer"></a>Technische profielen voor uitgever van beveiligingstoken

| Technische profiel | Beschrijving |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Gebruiker trajecten

Deze sectie beschrijft Hallo gebruiker trajecten is al gedeclareerd in Hallo *B2C_1A_base* beleid. Deze gebruiker trajecten zijn vatbaar toobe verdere waarnaar wordt verwezen, genegeerd en/of uitgebreid desgewenst ook uw eigen beleid zoals in Hallo *B2C_1A_base_extensions* beleid.

| Gebruiker reis | Beschrijving |
|--------------|-------------|
| *Aanmelden* | |
| *Aanmelding* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
