---
title: Autorisatiebeleid voor inhoudssleutels configureren met REST - Azure | Microsoft Docs
description: Informatie over het configureren van een verificatiebeleid voor een inhoudssleutel met Media Services REST-API.
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
ms.openlocfilehash: ed20fca35070c190bb63925d0a57cf919bcdd96c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="f4e9b-103">Dynamische versleuteling: autorisatiebeleid voor Inhoudssleutels configureren</span><span class="sxs-lookup"><span data-stu-id="f4e9b-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="f4e9b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f4e9b-104">Overview</span></span>
<span data-ttu-id="f4e9b-105">Microsoft Azure Media Services kunt u uw inhoud (dynamisch) worden versleuteld met Advanced Encryption Standard (AES) (met behulp van 128-bits coderingssleutels) en PlayReady of Widevine DRM leveren.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-105">Microsoft Azure Media Services enables you to deliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="f4e9b-106">Media Services biedt ook een service voor het leveren van sleutels en PlayReady/Widevine-licenties naar geautoriseerde clients.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span></span>

<span data-ttu-id="f4e9b-107">Als u voor Media Services wilt voor het versleutelen van een asset, moet u een versleutelingssleutel koppelen (**CommonEncryption** of **EnvelopeEncryption**) aan de asset (zoals beschreven [hier](media-services-rest-create-contentkey.md)) en het autorisatiebeleid voor de sleutel ook configureren (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-107">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="f4e9b-108">Wanneer een stream is aangevraagd door een speler, gebruikt Media Services de opgegeven sleutel voor het dynamisch versleutelen van uw inhoud met behulp van AES of PlayReady-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-108">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="f4e9b-109">Voor het ontsleutelen van de stroom, Windows media player vraagt om de sleutel van de service sleutellevering.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-109">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="f4e9b-110">De service beoordeelt om te bepalen of de gebruiker is gemachtigd om op te halen van de sleutel, de autorisatie-beleidsregels die u hebt opgegeven voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-110">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="f4e9b-111">Media Services ondersteunt meerdere manieren om gebruikers te verifiëren die sleutels aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="f4e9b-112">Het autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-112">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="f4e9b-113">Het beleid met de tokenbeperking moet vergezeld gaan van een token dat is uitgegeven door Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-113">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="f4e9b-114">Media Services ondersteunt tokens in de **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) indeling en ** JSON Web Token **(JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-114">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="f4e9b-115">Media Services biedt geen Token Services beveiligen.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="f4e9b-116">U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS voor het probleem van tokens.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-116">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="f4e9b-117">De STS moeten worden geconfigureerd voor het maken van een token dat is ondertekend met de opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van de tokenbeperking (zoals beschreven in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-117">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="f4e9b-118">De sleutellevering van Media Services wordt de versleutelingssleutel geretourneerd naar de client als het token geldig is en de claims in het token overeenkomen met die zijn geconfigureerd voor de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-118">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="f4e9b-119">Zie voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="f4e9b-119">For more information, see</span></span>

[<span data-ttu-id="f4e9b-120">JWT-token verificatie</span><span class="sxs-lookup"><span data-stu-id="f4e9b-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="f4e9b-121">[Azure Media Services OWIN MVC op basis van app integreren met Azure Active Directory en beperken van de belangrijkste inhouddistributie op basis van claims JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="f4e9b-122">[Azure ACS gebruiken voor het probleem van tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-122">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="f4e9b-123">Hierbij geldt het volgende:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-123">Some considerations apply:</span></span>
* <span data-ttu-id="f4e9b-124">Als u dynamische pakketten en dynamische versleuteling gebruiken, zorg ervoor dat het streaming-eindpunt van waaruit u wilt de inhoud streamen is in de **met** status.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-124">To be able to use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>
* <span data-ttu-id="f4e9b-125">Uw asset moet een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="f4e9b-126">Zie voor meer informatie [een asset coderen](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="f4e9b-127">Uploaden en uw met behulp van assets coderen **AssetCreationOptions.StorageEncrypted** optie.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="f4e9b-128">Als u van plan bent om meerdere inhoudssleutels waarvoor de dezelfde configuratie van beleid, moet het is raadzaam een enkel verificatiebeleid maken en deze opnieuw te gebruiken met meerdere inhoudssleutels.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-128">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="f4e9b-129">De service voor het leveren van de sleutel in de cache opgeslagen ContentKeyAuthorizationPolicy en de verwante objecten (beleidsopties en beperkingen) gedurende 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-129">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="f4e9b-130">Als u een ContentKeyAuthorizationPolicy maken en geef voor het gebruik van een '' tokenbeperking, test deze, en werk vervolgens het beleid op 'Open' beperking, duurt het ongeveer 15 minuten voordat het beleid wordt overgeschakeld naar de 'Geopende' versie van het beleid.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-130">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="f4e9b-131">Als u het leveringsbeleid voor uw asset toevoegt of bijwerkt, moet u een bestaande locator (indien aanwezig) verwijderen en een nieuwe locator maken.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="f4e9b-132">U kunt progressief downloaden op dit moment niet coderen.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="f4e9b-133">Dynamische AES-128-versleuteling</span><span class="sxs-lookup"><span data-stu-id="f4e9b-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="f4e9b-134">Als u werkt met de REST-API van Media Services, past u de volgende overwegingen:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-134">When working with the Media Services REST API, the following considerations apply:</span></span>
> 
> <span data-ttu-id="f4e9b-135">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f4e9b-136">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="f4e9b-137">Na het correct verbinding maakt met https://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-137">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f4e9b-138">U moet de volgende aanroepen naar de nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-138">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="f4e9b-139">Zie voor meer informatie over de verbinding maken met de AMS API [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="f4e9b-140">Open beperking</span><span class="sxs-lookup"><span data-stu-id="f4e9b-140">Open Restriction</span></span>
<span data-ttu-id="f4e9b-141">Open beperking betekent dat het systeem levert de sleutel voor iedereen die een sleutel aanvraag indient.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-141">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="f4e9b-142">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f4e9b-143">Het volgende voorbeeld maakt een open autorisatiebeleid en voegt het toe aan de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-143">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="f4e9b-144"><a id="ContentKeyAuthorizationPolicies"></a>ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="f4e9b-145">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-145">Request:</span></span>

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

<span data-ttu-id="f4e9b-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-146">Response:</span></span>

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

#### <span data-ttu-id="f4e9b-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="f4e9b-148">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-148">Request:</span></span>

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

<span data-ttu-id="f4e9b-149">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-149">Response:</span></span>    

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

#### <span data-ttu-id="f4e9b-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="f4e9b-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="f4e9b-151">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-151">Request:</span></span>

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

<span data-ttu-id="f4e9b-152">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="f4e9b-153"><a id="AddAuthorizationPolicyToKey"></a>Autorisatiebeleid toevoegen aan de inhoudssleutel</span><span class="sxs-lookup"><span data-stu-id="f4e9b-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy to the content key</span></span>
<span data-ttu-id="f4e9b-154">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-154">Request:</span></span>

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

<span data-ttu-id="f4e9b-155">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="f4e9b-156">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="f4e9b-156">Token Restriction</span></span>
<span data-ttu-id="f4e9b-157">Deze sectie wordt beschreven hoe een autorisatiebeleid voor inhoudssleutels maken en deze koppelen aan de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-157">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="f4e9b-158">Het verificatiebeleid wordt beschreven welke autorisatievereisten moeten worden voldaan om te bepalen of de gebruiker is gemachtigd voor het ontvangen van de sleutel (heeft bijvoorbeeld de lijst 'verificatie sleutel' bevatten de sleutel die het token is ondertekend met).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-158">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="f4e9b-159">Voor het configureren van de tokenbeperking-optie, moet u een XML-tekenreeks gebruiken om te beschrijven van autorisatievereisten van het token.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-159">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="f4e9b-160">De configuratie-XML van de tokenbeperking moet voldoen aan de volgende XML-schema.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-160">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="f4e9b-161"><a id="schema"></a>Tokenbeperking schema</span><span class="sxs-lookup"><span data-stu-id="f4e9b-161"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="f4e9b-162">Bij het configureren van de **token** beperkt beleid, moet u de primaire ** verificatie sleutel **, **verlener** en **doelgroep** parameters.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-162">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="f4e9b-163">De ** verificatie van de primaire sleutel ** bevat de sleutel die het token is ondertekend, **verlener** is de secure token service die de token uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-163">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="f4e9b-164">De **doelgroep** (ook wel genoemd **bereik**) beschrijft de intentie van het token of de resource die is gemachtigd voor toegang tot het token.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-164">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="f4e9b-165">De Media Services-service sleutellevering valideert dat deze waarden in het token overeenkomen met de waarden in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-165">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="f4e9b-166">Het volgende voorbeeld wordt een verificatiebeleid met een beperking van de token.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-166">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="f4e9b-167">In dit voorbeeld wordt de client zou moeten een token dat bevat aanwezig: ondertekening sleutel (VerificationKey), de uitgever van een token en vereiste claims.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-167">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="f4e9b-168">ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="f4e9b-169">'Token restrictiebeleid' maken, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-169">Create the "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="f4e9b-170">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="f4e9b-171">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-171">Request:</span></span>

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

<span data-ttu-id="f4e9b-172">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-172">Response:</span></span>    

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="f4e9b-173">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="f4e9b-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="f4e9b-174">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="f4e9b-175">Autorisatiebeleid toevoegen aan de inhoudssleutel</span><span class="sxs-lookup"><span data-stu-id="f4e9b-175">Add authorization policy to the content key</span></span>
<span data-ttu-id="f4e9b-176">Voeg AuthorizationPolicy toe aan de ContentKey zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-176">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="f4e9b-177">Dynamische PlayReady-versleuteling</span><span class="sxs-lookup"><span data-stu-id="f4e9b-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="f4e9b-178">Media Services kunt u voor het configureren van de rechten en beperkingen die u voor de runtime PlayReady DRM afdwingen wilt wanneer een gebruiker probeert te beveiligde inhoud af te spelen.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-178">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="f4e9b-179">Bij het beveiligen van uw inhoud met PlayReady een van de dingen die u wilt opgeven in het autorisatiebeleid is een XML-tekenreeks die definieert de [PlayReady-licentiesjabloon](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-179">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="f4e9b-180">Open beperking</span><span class="sxs-lookup"><span data-stu-id="f4e9b-180">Open Restriction</span></span>
<span data-ttu-id="f4e9b-181">Open beperking betekent dat het systeem levert de sleutel voor iedereen die een sleutel aanvraag indient.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-181">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="f4e9b-182">Deze beperking kan handig zijn voor testdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f4e9b-183">Het volgende voorbeeld maakt een open autorisatiebeleid en voegt het toe aan de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-183">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="f4e9b-184"><a id="ContentKeyAuthorizationPolicies2"></a>ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="f4e9b-185">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-185">Request:</span></span>

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

<span data-ttu-id="f4e9b-186">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-186">Response:</span></span>

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


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="f4e9b-187">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="f4e9b-188">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-188">Request:</span></span>

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

<span data-ttu-id="f4e9b-189">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-189">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="f4e9b-190">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="f4e9b-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="f4e9b-191">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="f4e9b-192">Autorisatiebeleid toevoegen aan de inhoudssleutel</span><span class="sxs-lookup"><span data-stu-id="f4e9b-192">Add authorization policy to the content key</span></span>
<span data-ttu-id="f4e9b-193">Voeg AuthorizationPolicy toe aan de ContentKey zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-193">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="f4e9b-194">Tokenbeperking</span><span class="sxs-lookup"><span data-stu-id="f4e9b-194">Token Restriction</span></span>
<span data-ttu-id="f4e9b-195">Voor het configureren van de tokenbeperking-optie, moet u een XML-tekenreeks gebruiken om te beschrijven van autorisatievereisten van het token.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-195">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="f4e9b-196">De XML aan het XML-schema wordt weergegeven voldoen moet in configuratie van de tokenbeperking [dit](#schema) sectie.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-196">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="f4e9b-197">ContentKeyAuthorizationPolicies maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="f4e9b-198">ContentKeyAuthorizationPolicies maken zoals [hier](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="f4e9b-199">ContentKeyAuthorizationPolicyOptions maken</span><span class="sxs-lookup"><span data-stu-id="f4e9b-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="f4e9b-200">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-200">Request:</span></span>

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

<span data-ttu-id="f4e9b-201">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="f4e9b-201">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="f4e9b-202">Koppeling ContentKeyAuthorizationPolicies met opties</span><span class="sxs-lookup"><span data-stu-id="f4e9b-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="f4e9b-203">Koppeling ContentKeyAuthorizationPolicies met opties, zoals [hier](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="f4e9b-204">Autorisatiebeleid toevoegen aan de inhoudssleutel</span><span class="sxs-lookup"><span data-stu-id="f4e9b-204">Add authorization policy to the content key</span></span>
<span data-ttu-id="f4e9b-205">Voeg AuthorizationPolicy toe aan de ContentKey zoals [hier](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="f4e9b-205">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="f4e9b-206"><a id="types"></a>Typen die worden gebruikt bij het definiëren van ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="f4e9b-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="f4e9b-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="f4e9b-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="f4e9b-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="f4e9b-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="f4e9b-209">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f4e9b-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4e9b-210">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f4e9b-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f4e9b-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4e9b-211">Next Steps</span></span>
<span data-ttu-id="f4e9b-212">Nu dat u de inhoudssleutel autorisatiebeleid hebt geconfigureerd, gaat u naar de [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f4e9b-212">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

