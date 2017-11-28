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
# <a name="federation-metadata"></a><span data-ttu-id="03031-103">Federatieve metagegevens</span><span class="sxs-lookup"><span data-stu-id="03031-103">Federation metadata</span></span>
<span data-ttu-id="03031-104">Azure Active Directory (Azure AD) een document met federatieve metagegevens publiceert voor services die is geconfigureerd tooaccept Hallo beveiligingstokens die Azure AD geeft.</span><span class="sxs-lookup"><span data-stu-id="03031-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="03031-105">Hallo wordt federatieve metagegevens documentindeling beschreven in Hallo [Web Services Federation Language (WS-Federation) versie 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), die breidt [metagegevens voor Hallo OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="03031-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="03031-106">Tenant-specifieke en Tenant-onafhankelijke metagegevens-eindpunten</span><span class="sxs-lookup"><span data-stu-id="03031-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="03031-107">Azure AD publiceert-tenant-specifieke en tenant-onafhankelijke eindpunten.</span><span class="sxs-lookup"><span data-stu-id="03031-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="03031-108">Tenant-specifieke eindpunten zijn ontworpen voor een bepaalde tenant.</span><span class="sxs-lookup"><span data-stu-id="03031-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="03031-109">Hallo tenantspecifieke federatiemetagegevens bevat informatie over het Hallo-tenant, met inbegrip van tenantspecifieke verlener en informatie over endpoint.</span><span class="sxs-lookup"><span data-stu-id="03031-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="03031-110">Toepassingen die toegang tooa één tenant beperken gebruiken tenantspecifieke eindpunten.</span><span class="sxs-lookup"><span data-stu-id="03031-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="03031-111">Tenant-onafhankelijke eindpunten bevatten informatie die algemene tooall Azure AD-tenants.</span><span class="sxs-lookup"><span data-stu-id="03031-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="03031-112">Deze informatie is van toepassing tootenants gehost op *login.microsoftonline.com* en wordt gedeeld door tenants.</span><span class="sxs-lookup"><span data-stu-id="03031-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="03031-113">Tenant-onafhankelijke eindpunten worden aanbevolen voor multitenant-toepassingen, omdat ze niet gekoppeld aan een bepaalde tenant zijn.</span><span class="sxs-lookup"><span data-stu-id="03031-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="03031-114">Federatieve metagegevens-eindpunten</span><span class="sxs-lookup"><span data-stu-id="03031-114">Federation metadata endpoints</span></span>
<span data-ttu-id="03031-115">Azure AD publiceert federatiemetagegevens op `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="03031-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="03031-116">Voor **tenantspecifieke eindpunten**, Hallo `TenantDomainName` een Hallo volgende typen:</span><span class="sxs-lookup"><span data-stu-id="03031-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="03031-117">Een geregistreerde domeinnaam van een Azure AD-tenant, zoals: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="03031-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="03031-118">niet-wijzigbaar Hallo tenant-ID van Hallo-domein, zoals `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="03031-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="03031-119">Voor **tenant-onafhankelijke eindpunten**, Hallo `TenantDomainName` is `common`.</span><span class="sxs-lookup"><span data-stu-id="03031-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="03031-120">Dit document bevat alleen Hallo Federatiemetagegevens elementen die zijn algemene tooall Azure AD-tenants die worden gehost op login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="03031-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="03031-121">Bijvoorbeeld, een eindpunt tenantspecifieke mogelijk `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="03031-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="03031-122">Hallo onafhankelijk van de tenant-eindpunt is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="03031-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="03031-123">U kunt een document met federatieve metagegevens Hallo weergeven door deze URL te typen in een browser.</span><span class="sxs-lookup"><span data-stu-id="03031-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="03031-124">Inhoud van de federatieve metagegevens</span><span class="sxs-lookup"><span data-stu-id="03031-124">Contents of federation Metadata</span></span>
<span data-ttu-id="03031-125">Hallo bevat volgende sectie informatie die door services die Hallo-tokens die zijn uitgegeven door Azure AD gebruiken die nodig is.</span><span class="sxs-lookup"><span data-stu-id="03031-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="03031-126">Entiteit-ID</span><span class="sxs-lookup"><span data-stu-id="03031-126">Entity ID</span></span>
<span data-ttu-id="03031-127">Hallo `EntityDescriptor` element bevat een `EntityID` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="03031-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="03031-128">waarde van Hallo Hallo `EntityID` kenmerk Hallo verlener vertegenwoordigt, dat wil zeggen hello security token service (STS) dat uitgegeven Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="03031-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="03031-129">Het is belangrijk toovalidate Hallo verlener wanneer u een token ontvangt.</span><span class="sxs-lookup"><span data-stu-id="03031-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="03031-130">Hallo volgende metagegevens toont een voorbeeld van een tenantspecifieke `EntityDescriptor` element met een `EntityID` element.</span><span class="sxs-lookup"><span data-stu-id="03031-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="03031-131">U kunt vervangen Hallo tenant-ID in Hallo tenant-onafhankelijke eindpunt uw tenant-ID toocreate een tenantspecifieke `EntityID` waarde.</span><span class="sxs-lookup"><span data-stu-id="03031-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="03031-132">de resulterende waarde Hello wordt hetzelfde als uitgever beveiligingstoken Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="03031-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="03031-133">Hallo manier kan een toepassing met meerdere tenants toovalidate Hallo certificaatverlener voor een bepaalde tenant.</span><span class="sxs-lookup"><span data-stu-id="03031-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="03031-134">Hallo volgende metagegevens toont een voorbeeld van een tenant-onafhankelijke `EntityID` element.</span><span class="sxs-lookup"><span data-stu-id="03031-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="03031-135">Houd er rekening mee dat Hallo `{tenant}` is een letterlijke tekenreeks, niet een tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="03031-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="03031-136">Certificaten voor tokenondertekening</span><span class="sxs-lookup"><span data-stu-id="03031-136">Token signing certificates</span></span>
<span data-ttu-id="03031-137">Wanneer een service een token dat is uitgegeven door een Azure AD-tenant ontvangt, moet hello handtekening van Hallo token worden gevalideerd met een ondertekeningssleutel die is gepubliceerd in het document met federatieve metagegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="03031-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="03031-138">Hallo federatiemetagegevens bevat Hallo openbare deel van Hallo-certificaten die tenants hello voor token-ondertekening gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03031-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="03031-139">Hallo certificaat onbewerkte bytes worden weergegeven in Hallo `KeyDescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="03031-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="03031-140">Hallo voor token-ondertekening certificaat is geldig voor de waarde van Hallo wanneer alleen ondertekening Hallo `use` kenmerk `signing`.</span><span class="sxs-lookup"><span data-stu-id="03031-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="03031-141">Een document met federatieve metagegevens gepubliceerd door Azure AD kan meerdere handtekeningsleutels, zoals wanneer tooupdate Hallo handtekeningcertificaat wordt voorbereid om Azure AD hebben.</span><span class="sxs-lookup"><span data-stu-id="03031-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="03031-142">Wanneer een document met federatieve metagegevens meer dan één certificaat bevat, moet een service die wordt gevalideerd Hallo tokens ondersteuning voor alle certificaten in het Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="03031-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="03031-143">Hallo volgende metagegevens toont een voorbeeld van een `KeyDescriptor` element met een ondertekeningssleutel.</span><span class="sxs-lookup"><span data-stu-id="03031-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="03031-144">Hallo `KeyDescriptor` element wordt weergegeven op twee plaatsen in een document met federatieve metagegevens Hallo; in Hallo WS-Federation-specifieke en Hallo SAML-specifieke sectie.</span><span class="sxs-lookup"><span data-stu-id="03031-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="03031-145">Hallo-certificaten die zijn gepubliceerd in beide secties wordt dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="03031-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="03031-146">In de sectie Hallo WS-Federation-specifieke, leest een lezer WS-Federation-metagegevens Hallo certificaten van een `RoleDescriptor` element Hello `SecurityTokenServiceType` type.</span><span class="sxs-lookup"><span data-stu-id="03031-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="03031-147">Hallo volgende metagegevens toont een voorbeeld van een `RoleDescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="03031-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="03031-148">In de sectie Hallo SAML-specifieke, leest een lezer WS-Federation-metagegevens Hallo certificaten van een `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="03031-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="03031-149">Hallo volgende metagegevens toont een voorbeeld van een `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="03031-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="03031-150">Er zijn geen verschillen in de indeling van certificaten met tenantspecifieke en tenant-onafhankelijke Hallo.</span><span class="sxs-lookup"><span data-stu-id="03031-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="03031-151">WS-Federation-eindpunt-URL</span><span class="sxs-lookup"><span data-stu-id="03031-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="03031-152">Hallo federatiemetagegevens bevat Hallo URL die Azure AD is gebruikt voor één aanmelding toe en één afmelden in het protocol WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="03031-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="03031-153">Dit eindpunt wordt weergegeven in Hallo `PassiveRequestorEndpoint` element.</span><span class="sxs-lookup"><span data-stu-id="03031-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="03031-154">Hallo volgende metagegevens toont een voorbeeld van een `PassiveRequestorEndpoint` element voor een tenantspecifieke-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="03031-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="03031-155">Voor het eindpunt van de tenant-onafhankelijke hello, Hallo WS-Federation-URL wordt weergegeven in Hallo WS-Federation-eindpunt, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="03031-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="03031-156">De eindpunt-URL voor SAML-protocol</span><span class="sxs-lookup"><span data-stu-id="03031-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="03031-157">Hallo federatiemetagegevens bevat Hallo-URL die gebruikmaakt van Azure AD voor één aanmelding toe en één afmelden in SAML 2.0-protocol.</span><span class="sxs-lookup"><span data-stu-id="03031-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="03031-158">Deze eindpunten worden weergegeven in Hallo `IDPSSODescriptor` element.</span><span class="sxs-lookup"><span data-stu-id="03031-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="03031-159">Hallo aanmelden en afmelden URL's worden weergegeven in Hallo `SingleSignOnService` en `SingleLogoutService` elementen.</span><span class="sxs-lookup"><span data-stu-id="03031-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="03031-160">Hallo volgende metagegevens toont een voorbeeld van een `PassiveResistorEndpoint` voor een tenantspecifieke-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="03031-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="03031-161">Hallo-eindpunten voor Hallo algemene SAML 2.0-protocoleindpunten worden op dezelfde manier gepubliceerd in Hallo tenant-onafhankelijke federatiemetagegevens, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="03031-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
