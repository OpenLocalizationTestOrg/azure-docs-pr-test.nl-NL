---
title: aaaConfigure autorisatiebeleid voor inhoudssleutels met Media Services .NET SDK | Microsoft Docs
description: Meer informatie over hoe tooconfigure een verificatiebeleid voor een inhoudssleutel met Media Services .NET SDK.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="c2f4f-103">Dynamische versleuteling: autorisatiebeleid voor inhoudssleutels configureren</span><span class="sxs-lookup"><span data-stu-id="c2f4f-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="c2f4f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c2f4f-104">Overview</span></span>
<span data-ttu-id="c2f4f-105">Microsoft Azure Media Services kunt u toodeliver MPEG-DASH-, Smooth Streaming- en HTTP-Live-Streaming (HLS)-streams beveiligd met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits) of [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="c2f4f-106">AMS ook kunt u toodeliver DASH-streams versleuteld met Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="c2f4f-107">Zowel PlayReady als Widevine zijn versleuteld volgens de specificatie Common Encryption (ISO/IEC 23001-7 CENC) Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="c2f4f-108">Media Services biedt ook een **Service voor het leveren van sleutel/licentie** waarvan clients kunt AES-sleutels ophalen of PlayReady/Widevine-licenties tooplay Hallo versleutelde inhoud.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="c2f4f-109">Als u voor Media Services tooencrypt een asset wilt, moet u een versleutelingssleutel tooassociate (**CommonEncryption** of **EnvelopeEncryption**) aan Hallo asset (zoals beschreven [hier](media-services-dotnet-create-contentkey.md)) en ook configureren autorisatiebeleid voor Hallo-sleutel (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="c2f4f-110">Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van versleuteling AES of DRM.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="c2f4f-111">toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="c2f4f-112">toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="c2f4f-113">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c2f4f-114">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="c2f4f-115">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="c2f4f-116">Media Services ondersteunt tokens in Hallo **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) indeling en **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) indeling.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="c2f4f-117">Media Services biedt geen Token Services beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="c2f4f-118">U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="c2f4f-119">Hallo STS moet geconfigureerde toocreate token van een ondertekend met de opgegeven sleutel Hallo en claims uitgeven dat u hebt opgegeven in configuratie van de tokenbeperking hello (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="c2f4f-120">Hallo retourneert Media Services sleutellevering-service Hallo encryption key toohello client als Hallo token geldig is en hello claims in Hallo token overeenkomen met die zijn geconfigureerd voor de inhoudssleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="c2f4f-121">Zie voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="c2f4f-121">For more information, see</span></span>

[<span data-ttu-id="c2f4f-122">JWT-token verificatie</span><span class="sxs-lookup"><span data-stu-id="c2f4f-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="c2f4f-123">[Azure Media Services OWIN MVC op basis van app integreren met Azure Active Directory en beperken van de belangrijkste inhouddistributie op basis van claims JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="c2f4f-124">[Gebruik Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="c2f4f-125">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="c2f4f-125">Some considerations apply:</span></span>
* <span data-ttu-id="c2f4f-126">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="c2f4f-127">toostart streaming van uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling, uw streaming-eindpunt heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="c2f4f-128">Uw asset moet een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="c2f4f-129">Zie voor meer informatie [een asset coderen](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="c2f4f-130">Uploaden en uw met behulp van assets coderen **AssetCreationOptions.StorageEncrypted** optie.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="c2f4f-131">Als u van plan toohave bent meerdere inhoudssleutels waarvoor dezelfde Hallo-beleidsconfiguratie, het wordt ten zeerste aanbevolen toocreate een enkel verificatiebeleid en het opnieuw te gebruiken met meerdere inhoudssleutels.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="c2f4f-132">Hallo service voor het leveren van de sleutel in de cache opgeslagen ContentKeyAuthorizationPolicy en de verwante objecten (beleidsopties en beperkingen) gedurende 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="c2f4f-133">Als u een ContentKeyAuthorizationPolicy maakt en toouse '' tokenbeperking opgeven en vervolgens testen en werk vervolgens Hallo beleid te 'Open' beperking, duurt het ongeveer 15 minuten voordat Hallo beleid switches toohello 'Open' versie van Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="c2f4f-134">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="c2f4f-135">U kunt progressief downloaden op dit moment niet coderen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="c2f4f-136">Dynamische AES-128-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c2f4f-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="c2f4f-137">Open beperking</span><span class="sxs-lookup"><span data-stu-id="c2f4f-137">Open Restriction</span></span>
<span data-ttu-id="c2f4f-138">Open beperking betekent Hallo system levert sleutel tooanyone Hallo die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c2f4f-139">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c2f4f-140">Hallo volgende voorbeeld maakt u een open autorisatiebeleid en toohello inhoudssleutel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="c2f4f-141">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="c2f4f-141">Token Restriction</span></span>
<span data-ttu-id="c2f4f-142">Deze sectie beschrijft hoe een inhoud toocreate autorisatiebeleid voor de sleutel en deze koppelen aan Hallo inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="c2f4f-143">Hallo-autorisatiebeleid wordt beschreven welke autorisatievereisten moet voldaan toodetermine als Hallo gebruiker geautoriseerde tooreceive Hallo sleutel (bijvoorbeeld Hallo 'verificatie sleutel' lijst bevat Hallo sleutel dat Hallo-token is ondertekend met).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="c2f4f-144">tooconfigure hello tokenbeperking optie, moet u een XML-toouse autorisatievereisten toodescribe Hallo token.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c2f4f-145">Hallo tokenbeperking configuratie-XML moet voldoen toohello XML-schema te volgen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="c2f4f-146"><a id="schema"></a>Tokenbeperking schema</span><span class="sxs-lookup"><span data-stu-id="c2f4f-146"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="c2f4f-147">Bij het configureren van Hallo **token** beperkt beleid, moet u Hallo primaire ** verificatie sleutel **, **verlener** en **doelgroep** parameters.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="c2f4f-148">Hallo ** verificatie van de primaire sleutel ** bevat Hallo-sleutel die Hallo token is ondertekend, **verlener** Hallo secure token-service is dat problemen Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="c2f4f-149">Hallo **doelgroep** (wel **bereik**) beschrijft Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="c2f4f-150">Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="c2f4f-151">Wanneer u **Media Services SDK voor .NET**, kunt u Hallo **TokenRestrictionTemplate** klassentoken toogenerate Hallo beperking.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="c2f4f-152">een autorisatiebeleid maakt Hallo volgende voorbeeld met een beperking van de token.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="c2f4f-153">In dit voorbeeld Hallo client zou hebben toopresent een token dat bevat: ondertekening sleutel (VerificationKey), de uitgever van een token en vereiste claims.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="c2f4f-154"><a id="test"></a>Test-token</span><span class="sxs-lookup"><span data-stu-id="c2f4f-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="c2f4f-155">tooget een test-token op basis van de tokenbeperking Hallo die werd gebruikt voor het sleutelautorisatiebeleid Hallo, Hallo te volgen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="c2f4f-156">Dynamische PlayReady-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c2f4f-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="c2f4f-157">U kunt Media Services tooconfigure Hallo rechten en beperkingen dat u voor Hallo PlayReady DRM runtime tooenforce wilt wanneer een gebruiker probeert tooplay terug beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="c2f4f-158">Bij het beveiligen van uw inhoud met PlayReady Hallo-bewerkingen moet u toospecify in uw verificatiebeleid is een XML-tekenreeks die Hallo definieert [PlayReady-licentiesjabloon](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2f4f-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="c2f4f-159">In Media Services SDK voor .NET, Hallo **PlayReadyLicenseResponseTemplate** en **PlayReadyLicenseTemplate** klassen helpt u Hallo PlayReady-Licentiesjabloon definiëren.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="c2f4f-160">[In dit onderwerp](media-services-protect-with-drm.md) ziet u hoe tooencrypt uw inhoud met **PlayReady** en **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="c2f4f-161">Open beperking</span><span class="sxs-lookup"><span data-stu-id="c2f4f-161">Open Restriction</span></span>
<span data-ttu-id="c2f4f-162">Open beperking betekent Hallo system levert sleutel tooanyone Hallo die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="c2f4f-163">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c2f4f-164">Hallo volgende voorbeeld maakt u een open autorisatiebeleid en toohello inhoudssleutel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="c2f4f-165">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="c2f4f-165">Token Restriction</span></span>
<span data-ttu-id="c2f4f-166">tooconfigure hello tokenbeperking optie, moet u een XML-toouse autorisatievereisten toodescribe Hallo token.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="c2f4f-167">Hallo tokenbeperking configuratie-XML toohello XML-schema wordt weergegeven in moet voldoen [dit](#schema) sectie.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="c2f4f-168">een test-token op basis van de tokenbeperking Hallo die werd gebruikt voor Hallo autorisatiebeleid beleid Zie tooget [dit](#test) sectie.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="c2f4f-169"><a id="types"></a>Typen die worden gebruikt bij het definiëren van ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="c2f4f-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="c2f4f-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="c2f4f-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="c2f4f-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c2f4f-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="c2f4f-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="c2f4f-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="c2f4f-173">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c2f4f-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c2f4f-174">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c2f4f-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="c2f4f-175">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="c2f4f-175">Next step</span></span>
<span data-ttu-id="c2f4f-176">Nu dat u de inhoudssleutel autorisatiebeleid hebt geconfigureerd, gaat u toohello [hoe tooconfigure-leveringsbeleid voor Assets](media-services-dotnet-configure-asset-delivery-policy.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c2f4f-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

