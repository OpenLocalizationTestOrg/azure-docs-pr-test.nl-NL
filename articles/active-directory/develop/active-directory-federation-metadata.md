---
title: Azure AD-Federatiemetagegevens | Microsoft Docs
description: Dit artikel wordt het document met federatieve metagegevens die Azure Active Directory publiceert voor services die Azure Active Directory-tokens accepteert.
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="13c97-103">Federatieve metagegevens</span><span class="sxs-lookup"><span data-stu-id="13c97-103">Federation metadata</span></span>
<span data-ttu-id="13c97-104">Azure Active Directory (Azure AD) publiceert een document met federatieve metagegevens voor services die is geconfigureerd voor het accepteren van de beveiligingstokens die Azure AD geeft.</span><span class="sxs-lookup"><span data-stu-id="13c97-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="13c97-105">De indeling van federatieve metagegevens document wordt beschreven in de [Web Services Federation Language (WS-Federation) versie 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), die breidt [metagegevens voor de OASIS Security Assertion Markup Language (SAML) 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="13c97-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="13c97-106">Tenant-specifieke en Tenant-onafhankelijke metagegevens-eindpunten</span><span class="sxs-lookup"><span data-stu-id="13c97-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="13c97-107">Azure AD publiceert-tenant-specifieke en tenant-onafhankelijke eindpunten.</span><span class="sxs-lookup"><span data-stu-id="13c97-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="13c97-108">Tenant-specifieke eindpunten zijn ontworpen voor een bepaalde tenant.</span><span class="sxs-lookup"><span data-stu-id="13c97-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="13c97-109">De tenant-specifieke federatiemetagegevens bevat informatie over de tenant, met inbegrip van de verlener en eindpunt informatie tenantspecifieke.</span><span class="sxs-lookup"><span data-stu-id="13c97-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="13c97-110">Toepassingen die toegang tot een enkel tenant beperken gebruiken tenantspecifieke eindpunten.</span><span class="sxs-lookup"><span data-stu-id="13c97-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="13c97-111">Tenant-onafhankelijke eindpunten bevatten informatie die geldt voor alle Azure AD-tenants.</span><span class="sxs-lookup"><span data-stu-id="13c97-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="13c97-112">Deze informatie is van toepassing op tenants die worden gehost op *login.microsoftonline.com* en wordt gedeeld door tenants.</span><span class="sxs-lookup"><span data-stu-id="13c97-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="13c97-113">Tenant-onafhankelijke eindpunten worden aanbevolen voor multitenant-toepassingen, omdat ze niet gekoppeld aan een bepaalde tenant zijn.</span><span class="sxs-lookup"><span data-stu-id="13c97-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="13c97-114">Federatieve metagegevens-eindpunten</span><span class="sxs-lookup"><span data-stu-id="13c97-114">Federation metadata endpoints</span></span>
<span data-ttu-id="13c97-115">Azure AD publiceert federatiemetagegevens op `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="13c97-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="13c97-116">Voor **tenantspecifieke eindpunten**, wordt de `TenantDomainName` een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="13c97-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="13c97-117">Een geregistreerde domeinnaam van een Azure AD-tenant, zoals: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="13c97-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="13c97-118">De niet-wijzigbaar tenant-ID van het domein, zoals `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="13c97-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="13c97-119">Voor **tenant-onafhankelijke eindpunten**, wordt de `TenantDomainName` is `common`.</span><span class="sxs-lookup"><span data-stu-id="13c97-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="13c97-120">Dit document worden de Federatiemetagegevens-elementen die gemeenschappelijk zijn voor alle Azure AD-tenants die worden gehost op login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="13c97-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="13c97-121">Bijvoorbeeld, een eindpunt tenantspecifieke mogelijk `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="13c97-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="13c97-122">Het eindpunt van de tenant-onafhankelijke [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="13c97-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="13c97-123">U kunt het document met federatieve metagegevens weergeven door deze URL te typen in een browser.</span><span class="sxs-lookup"><span data-stu-id="13c97-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="13c97-124">Inhoud van de federatieve metagegevens</span><span class="sxs-lookup"><span data-stu-id="13c97-124">Contents of federation Metadata</span></span>
<span data-ttu-id="13c97-125">De volgende sectie bevat informatie die door services die de tokens die zijn uitgegeven door Azure AD gebruiken die nodig is.</span><span class="sxs-lookup"><span data-stu-id="13c97-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="13c97-126">Entiteit-ID</span><span class="sxs-lookup"><span data-stu-id="13c97-126">Entity ID</span></span>
<span data-ttu-id="13c97-127">De `EntityDescriptor` element bevat een `EntityID` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="13c97-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="13c97-128">De waarde van de `EntityID` kenmerk vertegenwoordigt de verlener, dat wil zeggen, de beveiligingstokenservice (STS) die het token heeft uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="13c97-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="13c97-129">Het is belangrijk om te valideren van de verlener wanneer u een token ontvangt.</span><span class="sxs-lookup"><span data-stu-id="13c97-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="13c97-130">De volgende metagegevens toont een voorbeeld van een tenantspecifieke `EntityDescriptor` element met een `EntityID` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="13c97-131">U kunt de tenant-ID uit het eindpunt van de tenant-onafhankelijke vervangen door uw tenant-ID voor het maken van een tenantspecifieke `EntityID` waarde.</span><span class="sxs-lookup"><span data-stu-id="13c97-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="13c97-132">De resulterende waarde is hetzelfde als de uitgever van het beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="13c97-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="13c97-133">De strategie kan een multitenant-toepassing voor het valideren van de verlener voor een bepaalde tenant.</span><span class="sxs-lookup"><span data-stu-id="13c97-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="13c97-134">De volgende metagegevens toont een voorbeeld van een tenant-onafhankelijke `EntityID` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="13c97-135">Houd er rekening mee dat de `{tenant}` is een letterlijke tekenreeks, niet een tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="13c97-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="13c97-136">Certificaten voor tokenondertekening</span><span class="sxs-lookup"><span data-stu-id="13c97-136">Token signing certificates</span></span>
<span data-ttu-id="13c97-137">Wanneer een service een token dat is uitgegeven door een Azure AD-tenant ontvangt, kan de handtekening van het token moet worden gevalideerd met een ondertekeningssleutel die is gepubliceerd in het document met federatieve metagegevens.</span><span class="sxs-lookup"><span data-stu-id="13c97-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="13c97-138">De federatiemetagegevens bevat voor het openbare deel van de certificaten die gebruikmaken van de tenants voor token-ondertekening.</span><span class="sxs-lookup"><span data-stu-id="13c97-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="13c97-139">De onbewerkte bytes certificaat worden weergegeven in de `KeyDescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="13c97-140">Het token-ondertekening certificaat is geldig voor de ondertekening alleen wanneer de waarde van de `use` kenmerk `signing`.</span><span class="sxs-lookup"><span data-stu-id="13c97-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="13c97-141">Een document met federatieve metagegevens gepubliceerd door Azure AD kan meerdere handtekeningsleutels, zoals wanneer Azure AD wordt voorbereid om bij te werken van het handtekeningcertificaat hebben.</span><span class="sxs-lookup"><span data-stu-id="13c97-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="13c97-142">Wanneer een document met federatieve metagegevens meer dan één certificaat bevat, moet een service die het valideren van de tokens ondersteuning voor alle certificaten in het document.</span><span class="sxs-lookup"><span data-stu-id="13c97-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="13c97-143">De volgende metagegevens toont een voorbeeld van een `KeyDescriptor` element met een ondertekeningssleutel.</span><span class="sxs-lookup"><span data-stu-id="13c97-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="13c97-144">De `KeyDescriptor` element wordt weergegeven op twee plaatsen in het document met federatieve metagegevens; in de WS-Federation-specifieke en de SAML-specifieke-sectie.</span><span class="sxs-lookup"><span data-stu-id="13c97-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="13c97-145">De certificaten die zijn gepubliceerd in beide secties wordt hetzelfde zijn.</span><span class="sxs-lookup"><span data-stu-id="13c97-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="13c97-146">In de sectie WS-Federation-specifieke leest een lezer WS-Federation-metagegevens van de certificaten van een `RoleDescriptor` element met de `SecurityTokenServiceType` type.</span><span class="sxs-lookup"><span data-stu-id="13c97-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="13c97-147">De volgende metagegevens toont een voorbeeld van een `RoleDescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="13c97-148">In de sectie SAML-specifieke leest een lezer WS-Federation-metagegevens van de certificaten van een `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="13c97-149">De volgende metagegevens toont een voorbeeld van een `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="13c97-150">Er zijn geen verschillen in de indeling van certificaten met tenantspecifieke en onafhankelijk van de tenant.</span><span class="sxs-lookup"><span data-stu-id="13c97-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="13c97-151">WS-Federation-eindpunt-URL</span><span class="sxs-lookup"><span data-stu-id="13c97-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="13c97-152">De federatiemetagegevens bevat de URL die wordt gebruikt voor één aanmelding toe en één afmelden in het protocol WS-Federation Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13c97-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="13c97-153">Dit eindpunt wordt weergegeven in de `PassiveRequestorEndpoint` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="13c97-154">De volgende metagegevens toont een voorbeeld van een `PassiveRequestorEndpoint` element voor een tenantspecifieke-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="13c97-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="13c97-155">Voor het eindpunt van de tenant-onafhankelijke, de WS-Federation-URL wordt weergegeven in de WS-Federation-eindpunt, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="13c97-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="13c97-156">De eindpunt-URL voor SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="13c97-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="13c97-157">De federatiemetagegevens bevat de URL die gebruikmaakt van Azure AD voor één aanmelding toe en één afmelden in SAML 2.0-protocol.</span><span class="sxs-lookup"><span data-stu-id="13c97-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="13c97-158">Deze eindpunten worden weergegeven in de `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="13c97-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="13c97-159">De URL's voor aanmelden en afmelden worden weergegeven in de `SingleSignOnService` en `SingleLogoutService` elementen.</span><span class="sxs-lookup"><span data-stu-id="13c97-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="13c97-160">De volgende metagegevens toont een voorbeeld van een `PassiveResistorEndpoint` voor een tenantspecifieke-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="13c97-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="13c97-161">Op dezelfde manier worden de eindpunten voor de algemene SAML 2.0-protocoleindpunten worden gepubliceerd in de tenant-onafhankelijke federatiemetagegevens, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="13c97-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
