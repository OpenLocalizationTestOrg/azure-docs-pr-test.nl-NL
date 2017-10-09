---
title: aaaConfigure autorisatiebeleid voor inhoudssleutels met REST - Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure een verificatiebeleid voor een inhoudssleutel met Media Services REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="3ae74-103">Dynamische versleuteling: autorisatiebeleid voor Inhoudssleutels configureren</span><span class="sxs-lookup"><span data-stu-id="3ae74-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="3ae74-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3ae74-104">Overview</span></span>
<span data-ttu-id="3ae74-105">Microsoft Azure Media Services kunt u toodeliver uw inhoud (dynamisch) worden versleuteld met Advanced Encryption Standard (AES) (met behulp van 128-bits coderingssleutels) en PlayReady of Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="3ae74-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="3ae74-106">Media Services biedt ook een service voor het leveren van sleutels en PlayReady/Widevine-licenties tooauthorized clients.</span><span class="sxs-lookup"><span data-stu-id="3ae74-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="3ae74-107">Als u voor Media Services tooencrypt een asset wilt, moet u een versleutelingssleutel tooassociate (**CommonEncryption** of **EnvelopeEncryption**) aan Hallo asset (zoals beschreven [hier](media-services-rest-create-contentkey.md)) en ook configureren autorisatiebeleid voor Hallo-sleutel (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="3ae74-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="3ae74-108">Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van AES of PlayReady-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="3ae74-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="3ae74-109">toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service.</span><span class="sxs-lookup"><span data-stu-id="3ae74-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="3ae74-110">toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="3ae74-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="3ae74-111">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="3ae74-112">Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.</span><span class="sxs-lookup"><span data-stu-id="3ae74-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="3ae74-113">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="3ae74-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="3ae74-114">Media Services ondersteunt tokens in Hallo **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) indeling en ** JSON Web Token **(JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="3ae74-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="3ae74-115">Media Services biedt geen Token Services beveiligen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="3ae74-116">U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens.</span><span class="sxs-lookup"><span data-stu-id="3ae74-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="3ae74-117">Hallo STS moet geconfigureerde toocreate token van een ondertekend met de opgegeven sleutel Hallo en claims uitgeven dat u hebt opgegeven in configuratie van de tokenbeperking hello (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="3ae74-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="3ae74-118">Hallo retourneert Media Services sleutellevering-service Hallo encryption key toohello client als Hallo token geldig is en hello claims in Hallo token overeenkomen met die zijn geconfigureerd voor de inhoudssleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3ae74-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="3ae74-119">Zie voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="3ae74-119">For more information, see</span></span>

[<span data-ttu-id="3ae74-120">JWT-token verificatie</span><span class="sxs-lookup"><span data-stu-id="3ae74-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="3ae74-121">[Azure Media Services OWIN MVC op basis van app integreren met Azure Active Directory en beperken van de belangrijkste inhouddistributie op basis van claims JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="3ae74-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="3ae74-122">[Gebruik Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="3ae74-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="3ae74-123">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="3ae74-123">Some considerations apply:</span></span>
* <span data-ttu-id="3ae74-124">toobe kunnen toouse dynamische pakketten en dynamische versleuteling, zorg ervoor dat Hallo streaming-eindpunt van waaruit u wilt dat toostream uw inhoud wordt Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="3ae74-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="3ae74-125">Uw asset moet een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="3ae74-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="3ae74-126">Zie voor meer informatie [een asset coderen](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="3ae74-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="3ae74-127">Uploaden en uw met behulp van assets coderen **AssetCreationOptions.StorageEncrypted** optie.</span><span class="sxs-lookup"><span data-stu-id="3ae74-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="3ae74-128">Als u van plan toohave bent meerdere inhoudssleutels waarvoor dezelfde Hallo-beleidsconfiguratie, het wordt ten zeerste aanbevolen toocreate een enkel verificatiebeleid en het opnieuw te gebruiken met meerdere inhoudssleutels.</span><span class="sxs-lookup"><span data-stu-id="3ae74-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="3ae74-129">Hallo service voor het leveren van de sleutel in de cache opgeslagen ContentKeyAuthorizationPolicy en de verwante objecten (beleidsopties en beperkingen) gedurende 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="3ae74-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="3ae74-130">Als u een ContentKeyAuthorizationPolicy maakt en toouse '' tokenbeperking opgeven en vervolgens testen en werk vervolgens Hallo beleid te 'Open' beperking, duurt het ongeveer 15 minuten voordat Hallo beleid switches toohello 'Open' versie van Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="3ae74-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="3ae74-131">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="3ae74-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="3ae74-132">U kunt progressief downloaden op dit moment niet coderen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="3ae74-133">Dynamische AES-128-versleuteling</span><span class="sxs-lookup"><span data-stu-id="3ae74-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="3ae74-134">Bij het werken met Media Services REST API, Hallo Hallo letten volgende:</span><span class="sxs-lookup"><span data-stu-id="3ae74-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="3ae74-135">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="3ae74-136">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3ae74-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="3ae74-137">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="3ae74-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="3ae74-138">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="3ae74-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="3ae74-139">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3ae74-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="3ae74-140">Open beperking</span><span class="sxs-lookup"><span data-stu-id="3ae74-140">Open Restriction</span></span>
<span data-ttu-id="3ae74-141">Open beperking betekent Hallo system levert sleutel tooanyone Hallo die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="3ae74-142">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3ae74-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="3ae74-143">Hallo volgende voorbeeld maakt u een open autorisatiebeleid en toohello inhoudssleutel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3ae74-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="3ae74-144"><a id="ContentKeyAuthorizationPolicies"></a>ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="3ae74-145">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="3ae74-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="3ae74-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="3ae74-148">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="3ae74-149">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="3ae74-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="3ae74-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="3ae74-151">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="3ae74-152">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="3ae74-153"><a id="AddAuthorizationPolicyToKey"></a>Autorisatie beleid toohello inhoudssleutel toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ae74-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="3ae74-154">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="3ae74-155">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="3ae74-156">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="3ae74-156">Token Restriction</span></span>
<span data-ttu-id="3ae74-157">Deze sectie beschrijft hoe een inhoud toocreate autorisatiebeleid voor de sleutel en deze koppelen aan Hallo inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="3ae74-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="3ae74-158">Hallo-autorisatiebeleid wordt beschreven welke autorisatievereisten moet voldaan toodetermine als Hallo gebruiker geautoriseerde tooreceive Hallo sleutel (bijvoorbeeld Hallo 'verificatie sleutel' lijst bevat Hallo sleutel dat Hallo-token is ondertekend met).</span><span class="sxs-lookup"><span data-stu-id="3ae74-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="3ae74-159">tooconfigure hello tokenbeperking optie, moet u een XML-toouse autorisatievereisten toodescribe Hallo token.</span><span class="sxs-lookup"><span data-stu-id="3ae74-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="3ae74-160">Hallo tokenbeperking configuratie-XML moet voldoen toohello XML-schema te volgen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="3ae74-161"><a id="schema"></a>Tokenbeperking schema</span><span class="sxs-lookup"><span data-stu-id="3ae74-161"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="3ae74-162">Bij het configureren van Hallo **token** beperkt beleid, moet u Hallo primaire ** verificatie sleutel **, **verlener** en **doelgroep** parameters.</span><span class="sxs-lookup"><span data-stu-id="3ae74-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="3ae74-163">Hallo ** verificatie van de primaire sleutel ** bevat Hallo-sleutel die Hallo token is ondertekend, **verlener** Hallo secure token-service is dat problemen Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="3ae74-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="3ae74-164">Hallo **doelgroep** (wel **bereik**) beschrijft Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot.</span><span class="sxs-lookup"><span data-stu-id="3ae74-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="3ae74-165">Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="3ae74-166">een autorisatiebeleid maakt Hallo volgende voorbeeld met een beperking van de token.</span><span class="sxs-lookup"><span data-stu-id="3ae74-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="3ae74-167">In dit voorbeeld Hallo client zou hebben toopresent een token dat bevat: ondertekening sleutel (VerificationKey), de uitgever van een token en vereiste claims.</span><span class="sxs-lookup"><span data-stu-id="3ae74-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="3ae74-168">ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="3ae74-169">Hallo 'Token restrictiebeleid' maken, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="3ae74-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="3ae74-170">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="3ae74-171">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="3ae74-172">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="3ae74-173">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="3ae74-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="3ae74-174">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="3ae74-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="3ae74-175">Autorisatie beleid toohello inhoudssleutel toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ae74-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="3ae74-176">AuthorizationPolicy toohello ContentKey toevoegen zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="3ae74-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="3ae74-177">Dynamische PlayReady-versleuteling</span><span class="sxs-lookup"><span data-stu-id="3ae74-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="3ae74-178">U kunt Media Services tooconfigure Hallo rechten en beperkingen dat u voor Hallo PlayReady DRM runtime tooenforce wilt wanneer een gebruiker probeert tooplay terug beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="3ae74-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="3ae74-179">Bij het beveiligen van uw inhoud met PlayReady Hallo-bewerkingen moet u toospecify in uw verificatiebeleid is een XML-tekenreeks die Hallo definieert [PlayReady-licentiesjabloon](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ae74-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="3ae74-180">Open beperking</span><span class="sxs-lookup"><span data-stu-id="3ae74-180">Open Restriction</span></span>
<span data-ttu-id="3ae74-181">Open beperking betekent Hallo system levert sleutel tooanyone Hallo die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3ae74-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="3ae74-182">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="3ae74-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="3ae74-183">Hallo volgende voorbeeld maakt u een open autorisatiebeleid en toohello inhoudssleutel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3ae74-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="3ae74-184"><a id="ContentKeyAuthorizationPolicies2"></a>ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="3ae74-185">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="3ae74-186">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="3ae74-187">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="3ae74-188">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="3ae74-189">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="3ae74-190">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="3ae74-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="3ae74-191">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="3ae74-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="3ae74-192">Autorisatie beleid toohello inhoudssleutel toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ae74-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="3ae74-193">AuthorizationPolicy toohello ContentKey toevoegen zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="3ae74-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="3ae74-194">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="3ae74-194">Token Restriction</span></span>
<span data-ttu-id="3ae74-195">tooconfigure hello tokenbeperking optie, moet u een XML-toouse autorisatievereisten toodescribe Hallo token.</span><span class="sxs-lookup"><span data-stu-id="3ae74-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="3ae74-196">Hallo tokenbeperking configuratie-XML toohello XML-schema wordt weergegeven in moet voldoen [dit](#schema) sectie.</span><span class="sxs-lookup"><span data-stu-id="3ae74-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="3ae74-197">ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="3ae74-198">ContentKeyAuthorizationPolicies maken zoals [hier](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="3ae74-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="3ae74-199">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="3ae74-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="3ae74-200">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="3ae74-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="3ae74-201">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="3ae74-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="3ae74-202">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="3ae74-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="3ae74-203">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="3ae74-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="3ae74-204">Autorisatie beleid toohello inhoudssleutel toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ae74-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="3ae74-205">AuthorizationPolicy toohello ContentKey toevoegen zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="3ae74-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="3ae74-206"><a id="types"></a>Typen die worden gebruikt bij het definiëren van ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="3ae74-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="3ae74-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="3ae74-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="3ae74-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="3ae74-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="3ae74-209">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="3ae74-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3ae74-210">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="3ae74-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3ae74-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3ae74-211">Next Steps</span></span>
<span data-ttu-id="3ae74-212">Nu dat u de inhoudssleutel autorisatiebeleid hebt geconfigureerd, gaat u toohello [hoe tooconfigure-leveringsbeleid voor Assets](media-services-rest-configure-asset-delivery-policy.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3ae74-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

