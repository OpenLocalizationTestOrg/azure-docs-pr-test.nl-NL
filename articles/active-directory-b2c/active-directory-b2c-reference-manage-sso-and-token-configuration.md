---
title: 'Azure Active Directory B2C: Eenmalige aanmelding en token aanpassing met aangepast beleid beheren | Microsoft Docs'
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: Eenmalige aanmelding en token aanpassing met aangepast beleid beheren
Gebruik van aangepast beleid biedt dat u dezelfde controle over uw token, sessie en eenmalige aanmelding (SSO) configuraties Hallo via ingebouwde beleid.  toolearn welke elke instelling voor het geval is, Zie de documentatie van Hallo [hier](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configuratie van token levensduur en claims
toochange Hallo-instellingen van uw token levensduur, moet u tooadd een `<ClaimsProviders>` element in Hallo relying party-bestand van Hallo beleid gewenste tooimpact.  Hallo `<ClaimsProviders>` -element is een onderliggend element van Hallo `<TrustFrameworkPolicy>`.  U moet binnen tooput Hallo informatie die van invloed op uw token levensduur.  Hallo XML ziet er als volgt:

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**Toegang tot de levensduur van token** toegang levensduur van token kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo Hallo `<Item>` Hello Key = 'token_lifetime_secs' in seconden.  de standaardwaarde Hallo in ingebouwde is 3600 seconden (60 minuten).

**Levensduur van token ID** levensduur van token Hallo-ID kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo `<Item>` Hello Key = 'id_token_lifetime_secs' in seconden.  de standaardwaarde Hallo in ingebouwde is 3600 seconden (60 minuten).

**Vernieuwen van de levensduur van token** Hallo vernieuwen levensduur van token kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo `<Item>` Hello Key = 'refresh_token_lifetime_secs' in seconden.  de standaardwaarde Hallo in ingebouwde is 1209600 seconden (14 dagen).

**Vernieuwen van de levensduur van token verschuivende venster** indien een verschuivende venster levensduur tooyour vernieuwingstoken tooset gewenst, wijzigt u Hallo waarde binnen `<Item>` Hello Key = 'rolling_refresh_token_lifetime_secs' in seconden.  de standaardwaarde Hallo in ingebouwde is 7776000 (90 dagen).  Als u niet tooenfore wilt een Verschuivend venster levensduur, vervangt u deze regel:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Certificaatverlener (iss) claim** als u toochange Hallo verlener (iss) claim wilt, wijzigt u Hallo waarde binnen Hallo `<Item>` Hello Key = 'IssuanceClaimPattern'.  Hallo toepasselijke waarden zijn `AuthorityAndTenantGuid` en `AuthorityWithTfp`.

**Instelling claim die beleids-ID vertegenwoordigt** Hallo opties voor het instellen van deze waarde zijn TFP (vertrouwensbeleid framework) en ACR (authentication context verwijzing).  
We raden u aan deze tooTFP, toodo te stellen, controleert u Hallo `<Item>` Hello Key = "AuthenticationContextReferenceClaimPattern" bestaat en het Hallo-waarde is `None`.
In uw `<OutputClaims>` item, het toevoegen van dit element:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
ACR, verwijder Hallo `<Item>` Hello Key = 'AuthenticationContextReferenceClaimPattern'.

**Onderwerpnaam (sub) claim** deze optie is standaard tooObjectID, indien tooswitch gewenst dit te`Not Supported`, Hallo te volgen:

Deze regel vervangen 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
Met deze regel:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Sessie-gedrag en eenmalige aanmelding
toochange uw sessie gedrag en de SSO-configuraties, moet u tooadd een `<UserJourneyBehaviors>` -element in Hallo `<RelyingParty>` element.  Hallo `<UserJourneyBehaviors>` element moet direct volgen op Hallo `<DefaultUserJourney>`.  Hallo binnen uw `<UserJourneyBehavors>` element ziet er als volgt:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Eenmalige aanmelding (SSO) configuratie** toochange Hallo eenmalige aanmelding configuratie, moet u toomodify Hallo-waarde van `<SingleSignOn>`.  Hallo toepasselijke waarden zijn `Tenant`, `Application`, `Policy` en `Disabled`. 

**Sessie-levensduur (minuten) van de Web-app** toochange Hallo Hallo web-app sessie levensduur, moet u toomodify waarde Hallo `<SessionExpiryInSeconds>` element.  de standaardwaarde Hallo in ingebouwde beleid is 86400 seconden (1440 minuten).

**Web-app sessietime-out** toochange Hallo web app sessietime-out, moet u toomodify Hallo-waarde van `<SessionExpiryType>`.  Hallo toepasselijke waarden zijn `Absolute` en `Rolling`.
