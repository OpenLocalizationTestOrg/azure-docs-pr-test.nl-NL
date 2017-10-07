---
title: aaaAzure AD Federatiemetagegevens | Microsoft Docs
description: Dit artikel wordt beschreven Hallo document met federatieve metagegevens die Azure Active Directory publiceert voor services die Azure Active Directory-tokens accepteert.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Federatieve metagegevens
Azure Active Directory (Azure AD) een document met federatieve metagegevens publiceert voor services die is geconfigureerd tooaccept Hallo beveiligingstokens die Azure AD geeft. Hallo wordt federatieve metagegevens documentindeling beschreven in Hallo [Web Services Federation Language (WS-Federation) versie 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), die breidt [metagegevens voor Hallo OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Tenant-specifieke en Tenant-onafhankelijke metagegevens-eindpunten
Azure AD publiceert-tenant-specifieke en tenant-onafhankelijke eindpunten.

Tenant-specifieke eindpunten zijn ontworpen voor een bepaalde tenant. Hallo tenantspecifieke federatiemetagegevens bevat informatie over het Hallo-tenant, met inbegrip van tenantspecifieke verlener en informatie over endpoint. Toepassingen die toegang tooa één tenant beperken gebruiken tenantspecifieke eindpunten.

Tenant-onafhankelijke eindpunten bevatten informatie die algemene tooall Azure AD-tenants. Deze informatie is van toepassing tootenants gehost op *login.microsoftonline.com* en wordt gedeeld door tenants. Tenant-onafhankelijke eindpunten worden aanbevolen voor multitenant-toepassingen, omdat ze niet gekoppeld aan een bepaalde tenant zijn.

## <a name="federation-metadata-endpoints"></a>Federatieve metagegevens-eindpunten
Azure AD publiceert federatiemetagegevens op `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Voor **tenantspecifieke eindpunten**, Hallo `TenantDomainName` een Hallo volgende typen:

* Een geregistreerde domeinnaam van een Azure AD-tenant, zoals: `contoso.onmicrosoft.com`.
* niet-wijzigbaar Hallo tenant-ID van Hallo-domein, zoals `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Voor **tenant-onafhankelijke eindpunten**, Hallo `TenantDomainName` is `common`. Dit document bevat alleen Hallo Federatiemetagegevens elementen die zijn algemene tooall Azure AD-tenants die worden gehost op login.microsoftonline.com.

Bijvoorbeeld, een eindpunt tenantspecifieke mogelijk `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. Hallo onafhankelijk van de tenant-eindpunt is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). U kunt een document met federatieve metagegevens Hallo weergeven door deze URL te typen in een browser.

## <a name="contents-of-federation-metadata"></a>Inhoud van de federatieve metagegevens
Hallo bevat volgende sectie informatie die door services die Hallo-tokens die zijn uitgegeven door Azure AD gebruiken die nodig is.

### <a name="entity-id"></a>Entiteit-ID
Hallo `EntityDescriptor` element bevat een `EntityID` kenmerk. waarde van Hallo Hallo `EntityID` kenmerk Hallo verlener vertegenwoordigt, dat wil zeggen hello security token service (STS) dat uitgegeven Hallo-token. Het is belangrijk toovalidate Hallo verlener wanneer u een token ontvangt.

Hallo volgende metagegevens toont een voorbeeld van een tenantspecifieke `EntityDescriptor` element met een `EntityID` element.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
U kunt vervangen Hallo tenant-ID in Hallo tenant-onafhankelijke eindpunt uw tenant-ID toocreate een tenantspecifieke `EntityID` waarde. de resulterende waarde Hello wordt hetzelfde als uitgever beveiligingstoken Hallo Hallo. Hallo manier kan een toepassing met meerdere tenants toovalidate Hallo certificaatverlener voor een bepaalde tenant.

Hallo volgende metagegevens toont een voorbeeld van een tenant-onafhankelijke `EntityID` element. Houd er rekening mee dat Hallo `{tenant}` is een letterlijke tekenreeks, niet een tijdelijke aanduiding.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificaten voor tokenondertekening
Wanneer een service een token dat is uitgegeven door een Azure AD-tenant ontvangt, moet hello handtekening van Hallo token worden gevalideerd met een ondertekeningssleutel die is gepubliceerd in het document met federatieve metagegevens Hallo. Hallo federatiemetagegevens bevat Hallo openbare deel van Hallo-certificaten die tenants hello voor token-ondertekening gebruiken. Hallo certificaat onbewerkte bytes worden weergegeven in Hallo `KeyDescriptor` element. Hallo voor token-ondertekening certificaat is geldig voor de waarde van Hallo wanneer alleen ondertekening Hallo `use` kenmerk `signing`.

Een document met federatieve metagegevens gepubliceerd door Azure AD kan meerdere handtekeningsleutels, zoals wanneer tooupdate Hallo handtekeningcertificaat wordt voorbereid om Azure AD hebben. Wanneer een document met federatieve metagegevens meer dan één certificaat bevat, moet een service die wordt gevalideerd Hallo tokens ondersteuning voor alle certificaten in het Hallo-document.

Hallo volgende metagegevens toont een voorbeeld van een `KeyDescriptor` element met een ondertekeningssleutel.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Hallo `KeyDescriptor` element wordt weergegeven op twee plaatsen in een document met federatieve metagegevens Hallo; in Hallo WS-Federation-specifieke en Hallo SAML-specifieke sectie. Hallo-certificaten die zijn gepubliceerd in beide secties wordt dezelfde Hallo.

In de sectie Hallo WS-Federation-specifieke, leest een lezer WS-Federation-metagegevens Hallo certificaten van een `RoleDescriptor` element Hello `SecurityTokenServiceType` type.

Hallo volgende metagegevens toont een voorbeeld van een `RoleDescriptor` element.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

In de sectie Hallo SAML-specifieke, leest een lezer WS-Federation-metagegevens Hallo certificaten van een `IDPSSODescriptor` element.

Hallo volgende metagegevens toont een voorbeeld van een `IDPSSODescriptor` element.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Er zijn geen verschillen in de indeling van certificaten met tenantspecifieke en tenant-onafhankelijke Hallo.

### <a name="ws-federation-endpoint-url"></a>WS-Federation-eindpunt-URL
Hallo federatiemetagegevens bevat Hallo URL die Azure AD is gebruikt voor één aanmelding toe en één afmelden in het protocol WS-Federation. Dit eindpunt wordt weergegeven in Hallo `PassiveRequestorEndpoint` element.

Hallo volgende metagegevens toont een voorbeeld van een `PassiveRequestorEndpoint` element voor een tenantspecifieke-eindpunt.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Voor het eindpunt van de tenant-onafhankelijke hello, Hallo WS-Federation-URL wordt weergegeven in Hallo WS-Federation-eindpunt, zoals wordt weergegeven in Hallo voorbeeld te volgen.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>De eindpunt-URL voor SAML-protocol
Hallo federatiemetagegevens bevat Hallo-URL die gebruikmaakt van Azure AD voor één aanmelding toe en één afmelden in SAML 2.0-protocol. Deze eindpunten worden weergegeven in Hallo `IDPSSODescriptor` element.

Hallo aanmelden en afmelden URL's worden weergegeven in Hallo `SingleSignOnService` en `SingleLogoutService` elementen.

Hallo volgende metagegevens toont een voorbeeld van een `PassiveResistorEndpoint` voor een tenantspecifieke-eindpunt.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Hallo-eindpunten voor Hallo algemene SAML 2.0-protocoleindpunten worden op dezelfde manier gepubliceerd in Hallo tenant-onafhankelijke federatiemetagegevens, zoals wordt weergegeven in Hallo voorbeeld te volgen.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
