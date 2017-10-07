---
title: Eenmalige aanmelding op SAML Protocol aaaAzure | Microsoft Docs
description: Dit artikel wordt beschreven Hallo eenmalige aanmelding op SAML-protocol in Azure Active Directory
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Single Sign-On SAML-protocol
In dit artikel bevat informatie over Hallo SAML 2.0-verificatieaanvragen en -antwoorden die ondersteuning biedt voor eenmalige aanmelding voor Azure Active Directory (Azure AD).

Hallo protocol diagram hieronder wordt beschreven één Hallo aanmelding reeks. Hallo-cloudservice (Hallo serviceprovider) maakt gebruik van een HTTP-omleiding binding toopass een `AuthnRequest` (verificatieaanvraag) element tooAzure AD (Hallo id-provider). Vervolgens Azure AD maakt gebruik van een HTTP post-binding toopost een `Response` element toohello-cloudservice.

![Eenmalige aanmelding werkstroom](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
verzenden van een gebruikersverificatie toorequest, cloudservices een `AuthnRequest` element tooAzure AD. Een voorbeeld van SAML 2.0 `AuthnRequest` kan moeten uitzien:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parameter |  | Beschrijving |
| --- | --- | --- |
| Id |Vereist |Azure AD maakt gebruik van dit kenmerk toopopulate hello `InResponseTo` kenmerk Hallo antwoord geretourneerd. ID moet niet beginnen met een getal, zodat een strategie voor een algemene tooprepend een tekenreeks, zoals 'id' toohello tekenreeksweergave van een GUID. Bijvoorbeeld: `id6c1c178c166d486687be4aaf5e482730` is een geldige ID. |
| Versie |Vereist |Dit moet **2.0**. |
| IssueInstant |Vereist |Dit is een datum/tijd-tekenreeks met een UTC-waarde en [round trip-indeling ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD een DateTime-waarde van dit type verwacht maar niet evalueren of gebruik Hallo-waarde. |
| AssertionConsumerServiceUrl |Optioneel |Indien opgegeven, deze moet overeenkomen met Hallo `RedirectUri` van de cloudservice Hallo in Azure AD. |
| ForceAuthn |Optioneel | Dit is een Booleaanse waarde. Als waar, betekent dit dat die gebruiker Hallo worden gedwongen toore-verifiëren, zelfs als ze een geldige sessie met Azure AD hebben. |
| IsPassive |Optioneel |Dit is een Booleaanse waarde die aangeeft of Azure AD Hallo gebruiker achtergrond, zonder tussenkomst van de gebruiker met behulp van sessiecookie Hallo verifiëren moet als er een bestaat. Als dit waar is, probeert Azure AD tooauthenticate Hallo gebruiker met behulp van sessiecookie Hallo. |

Alle andere `AuthnRequest` kenmerken, zoals toestemming, bestemming, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex en ProviderName zich **genegeerd**.

Azure AD negeert ook Hallo `Conditions` -element in `AuthnRequest`.

### certificaatverlener
Hallo `Issuer` -element in een `AuthnRequest` moet exact overeenkomen met een Hallo **ServicePrincipalNames** in de cloudservice Hallo in Azure AD. Dit is normaal gesproken toohello ingesteld **App ID URI** die is opgegeven tijdens de toepassingsregistratie.

Een voorbeeld SAML-fragment met Hallo `Issuer` element uitziet:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Dit element vraagt de indeling van een bepaalde naam-ID in het Hallo-antwoord en is optioneel in `AuthnRequest` elementen verzonden tooAzure AD.

Een voorbeeld van een `NameIdPolicy` element uitziet:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Als `NameIDPolicy` is opgegeven, kunt u de optionele opnemen `Format` kenmerk. Hallo `Format` kenmerk kan slechts één van de volgende waarden Hallo; een andere waarde resulteert in een fout hebben.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Hallo NameID claim problemen azure Active Directory als een pairwise id.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Hallo NameID claim in de e-mailadres wordt uitgegeven door azure Active Directory.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Met deze waarde is toegestaan voor Azure Active Directory tooselect Hallo claim indeling. Azure Active Directory problemen Hallo NameID als een pairwise id.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Hallo NameID claim problemen azure Active Directory als een willekeurig gegenereerde waarde die de unieke toohello huidige SSO-bewerking. Dit betekent dat Hallo-waarde tijdelijk is en kan niet worden gebruikt tooidentify Hallo verificatie van gebruiker.

Azure AD negeert Hallo `AllowCreate` kenmerk.

### RequestAuthnContext
Hallo `RequestedAuthnContext` element geeft Hallo gewenst verificatiemethoden. Dit is optioneel in `AuthnRequest` elementen verzonden tooAzure AD. Azure AD ondersteunt slechts één `AuthnContextClassRef` waarde: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Bereik
Hallo `Scoping` -element een lijst met identiteitsproviders bevat, is optioneel in `AuthnRequest` elementen verzonden tooAzure AD.

Indien opgegeven, bevatten geen Hallo `ProxyCount` kenmerk `IDPListOption` of `RequesterID` element als ze worden niet ondersteund.

### Handtekening
Neem geen een `Signature` -element in `AuthnRequest` elementen, zoals Azure AD biedt geen ondersteuning voor ondertekend verificatieaanvragen.

### Onderwerp
Azure AD negeert Hallo `Subject` element van `AuthnRequest` elementen.

## Antwoord
Wanneer een aangevraagde eenmalige aanmelding voltooid is, boekt Azure AD een antwoord toohello-cloudservice. Een voorbeeld antwoord tooa geslaagde aanmelding poging ziet er als volgt:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Antwoord
Hallo `Response` element Hallo resultaat van Hallo autorisatieaanvraag bevat. Azure AD ingesteld Hallo `ID`, `Version` en `IssueInstant` waarden in Hallo `Response` element. Dit stelt ook Hallo volgende kenmerken:

* `Destination`: Wanneer de aanmelding is voltooid, is dit ingesteld toohello `RedirectUri` van Hallo-provider (cloudservice).
* `InResponseTo`: Dit is ingesteld toohello `ID` kenmerk Hallo `AuthnRequest` element dat antwoord Hallo gestart.

### certificaatverlener
Azure AD ingesteld Hallo `Issuer` element te`https://login.microsoftonline.com/<TenantIDGUID>/` waar <TenantIDGUID> hello tenant-ID van hello Azure AD-tenant is.

Voor, een voorbeeldreactie met verlener element kan als volgt uitzien:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Status
Hallo `Status` element Hallo slagen of mislukken van de aanmelding worden weergegeven. Het omvat Hallo `StatusCode` -element bevat een code of een set geneste codes die Hallo status van aanvraag Hallo vertegenwoordigen. Dit omvat ook Hallo `StatusMessage` -element bevat aangepaste foutberichten die zijn gegenereerd tijdens het Hallo eenmalige aanmelding.

<!-- TODO: Add a authentication protocol error reference -->

Hallo Hieronder volgt een SAML-antwoord tooan mislukte aanmelding poging.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Verklaring
In aanvulling toohello `ID`, `IssueInstant` en `Version`, Azure AD wordt ingesteld na elementen in Hallo Hallo `Assertion` element van het antwoord Hallo.

#### certificaatverlener
Dit is te ingesteld`https://sts.windows.net/<TenantIDGUID>/`waar <TenantIDGUID> hello Tenant-ID van hello Azure AD-tenant is.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Handtekening
Azure AD ondertekent Hallo verklaring in antwoord tooa geslaagde aanmelding. Hallo `Signature` element bevat een digitale handtekening die Hallo cloudservice tooauthenticate Hallo bron tooverify Hallo integriteit van Hallo verklaring kunt gebruiken.

maakt gebruik van de digitale handtekening, Azure AD toogenerate Hallo ondertekeningssleutel in Hallo `IDPSSODescriptor` element van het document met metagegevens.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Onderwerp
Hiermee geeft u Hallo principal die Hallo onderwerp is van het Hallo-instructies in het Hallo-verklaring. Het bevat een `NameID` -element Hallo geverifieerde gebruiker vertegenwoordigt. Hallo `NameID` waarde is een gerichte id die is gerichte alleen toohello-provider die is Hallo doelgroep voor Hallo-token. Het is permanent - kunnen worden ingetrokken, maar nooit opnieuw wordt toegewezen. Het is ook ondoorzichtig, omdat het over Hallo gebruiker niet vrijgegeven en kan niet worden gebruikt als een id voor kenmerk query's.

Hallo `Method` kenmerk Hallo `SubjectConfirmation` element is altijd ingesteld te`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Voorwaarden
Dit element bevat voorwaarden waarmee Hallo aanvaardbaar gebruik van asserties SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Hallo `NotBefore` en `NotOnOrAfter` kenmerken opgeven tijdens welke Hallo verklaring geldig is hello-interval.

* waarde van Hallo Hallo `NotBefore` kenmerk is gelijk tooor enigszins (minder dan een seconde) hoger is dan de waarde van Hallo `IssueInstant` kenmerk Hallo `Assertion` element. Azure AD wordt geen rekening gehouden met eventuele tijdsverschil tussen zichzelf en Hallo cloudservice (serviceprovider) en voegt geen tijde toothis buffer.
* waarde van Hallo Hallo `NotOnOrAfter` kenmerk is later dan de waarde van Hallo Hallo 70 minuten `NotBefore` kenmerk.

#### Doelgroep
Dit document bevat een URI die een doelgroep identificeert. Azure AD stelt Hallo-waarde van de waarde van dit element toohello van `Issuer` element Hallo `AuthnRequest` die gestart Hallo eenmalige aanmelding. Hallo tooevaluate `Audience` waarde: gebruik Hallo-waarde van Hallo `App ID URI` dat is opgegeven tijdens de toepassingsregistratie.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Zoals Hallo `Issuer` waarde hello `Audience` waarde moet exact overeenkomen met een Hallo SPN-namen die Hallo cloudservice vertegenwoordigt in Azure AD. Echter, als Hallo-waarde van Hallo `Issuer` element is niet een URI-waarde hello `Audience` waarde in het antwoord Hallo is Hallo `Issuer` waarde voorafgegaan door `spn:`.

#### AttributeStatement
Hierin worden claims over Hallo onderwerp of de gebruiker. Hallo volgende fragment bevat een voorbeeld van een `AttributeStatement` element. Hallo weglatingsteken geeft aan dat Hallo-element kan bestaan uit meerdere kenmerken en kenmerkwaarden.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Naam van Claim** : waarde van Hallo Hallo `Name` kenmerk (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) is Hallo user principal name van Hallo geverifieerde gebruiker, zoals `testuser@managedtenant.com`.
* **ObjectIdentifier Claim** : waarde van Hallo Hallo `ObjectIdentifier` kenmerk (`http://schemas.microsoft.com/identity/claims/objectidentifier`) is Hallo `ObjectId` van Hallo directory-object waarmee Hallo gebruiker heeft geverifieerd in Azure AD. `ObjectId`is een niet-wijzigbaar, globaal unieke en veilige id hergebruik van Hallo geverifieerde gebruiker.

#### AuthnStatement
Dit element asserts dat Hallo verklaring onderwerp op een bepaalde manier op een bepaald tijdstip is geverifieerd.

* Hallo `AuthnInstant` kenmerk geeft Hallo tijdstip welke Hallo door gebruiker geverifieerd met Azure AD.
* Hallo `AuthnContext` element geeft Hallo authentication context tooauthenticate Hallo gebruiker gebruikt.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```