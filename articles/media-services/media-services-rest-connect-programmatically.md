---
title: aaaConnecting tooMedia Services-Account met REST-API | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooconnect tooMedia Services met behulp REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="09b6e-103">Verbinding maken met tooMedia Services-Account met Media Services REST-API</span><span class="sxs-lookup"><span data-stu-id="09b6e-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09b6e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="09b6e-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="09b6e-105">REST</span><span class="sxs-lookup"><span data-stu-id="09b6e-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="09b6e-106">Dit onderwerp beschrijft hoe een programmatische verbinding tooMicrosoft Azure Media Services tijdens het programmeren met tooobtain Hallo REST API voor Media Services.</span><span class="sxs-lookup"><span data-stu-id="09b6e-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="09b6e-107">Twee dingen zijn vereist bij het openen van Microsoft Azure Media Services: een toegangstoken die is verstrekt door Azure Access Control-Services (ACS) en het Hallo-URI van Media Services zelf.</span><span class="sxs-lookup"><span data-stu-id="09b6e-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="09b6e-108">U kunt een wijze die u wilt dat bij het maken van deze aanvragen, zolang u Geef de juiste headerwaarden hello en in Hallo toegangstoken correct bij het aanroepen van in Media Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="09b6e-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="09b6e-109">Hallo stappen te volgen beschrijven de meest voorkomende werkstroom Hallo wanneer met behulp van Hallo REST API voor Media Services tooconnect tooMedia Services:</span><span class="sxs-lookup"><span data-stu-id="09b6e-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="09b6e-110">Ophalen van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="09b6e-110">Getting an access token</span></span> 
2. <span data-ttu-id="09b6e-111">Verbinding maken met toohello Media Services-URI</span><span class="sxs-lookup"><span data-stu-id="09b6e-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="09b6e-112">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="09b6e-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="09b6e-113">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="09b6e-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="09b6e-114">U kunt ook een HTTP/1.1 200-antwoord dat Hallo beschrijving van de ODATA-API-metagegevens bevat ontvangen.</span><span class="sxs-lookup"><span data-stu-id="09b6e-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="09b6e-115">De volgende API-aanroepen na toohello nieuwe URL.</span><span class="sxs-lookup"><span data-stu-id="09b6e-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="09b6e-116">Bijvoorbeeld, als nadat u hebt geprobeerd tooconnect, u hebt verkregen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="09b6e-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="09b6e-117">U moet de volgende API-aanroepen toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ boeken.</span><span class="sxs-lookup"><span data-stu-id="09b6e-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="09b6e-118">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="09b6e-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="09b6e-119">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="09b6e-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="09b6e-120">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="09b6e-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="09b6e-121">Adres Access control</span><span class="sxs-lookup"><span data-stu-id="09b6e-121">Access control address</span></span>
<span data-ttu-id="09b6e-122">Media Services-adres is https://wamsprodglobal001acs.accesscontrol.windows.net, met uitzondering van China Noord regio, waar deze https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn is.</span><span class="sxs-lookup"><span data-stu-id="09b6e-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="09b6e-123">Ophalen van een toegangstoken</span><span class="sxs-lookup"><span data-stu-id="09b6e-123">Getting an access token</span></span>
<span data-ttu-id="09b6e-124">tooaccess Media Services rechtstreeks via Hallo REST-API, een toegangstoken ophalen uit ACS en deze gebruiken tijdens elke HTTP-aanvraag die u in Hallo-service aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="09b6e-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="09b6e-125">Dit token is vergelijkbaar tooother tokens die worden geleverd door ACS op basis van de toegang tot claims die zijn opgegeven in Hallo-header van een HTTP-aanvraag en met Hallo OAuth-v2-protocol.</span><span class="sxs-lookup"><span data-stu-id="09b6e-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="09b6e-126">U hoeft niet alle andere vereiste onderdelen voor tooMedia Services rechtstreeks verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="09b6e-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="09b6e-127">Hallo volgende voorbeeld ziet Hallo HTTP-aanvraag-header en tooretrieve instantie gebruikt een token.</span><span class="sxs-lookup"><span data-stu-id="09b6e-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="09b6e-128">**Koptekst**:</span><span class="sxs-lookup"><span data-stu-id="09b6e-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="09b6e-129">**Hoofdtekst**:</span><span class="sxs-lookup"><span data-stu-id="09b6e-129">**Body**:</span></span>

<span data-ttu-id="09b6e-130">U moet tooprove hello client_id en client_secret waarden in de hoofdtekst Hallo van deze aanvraag; client_id en client_secret komen overeen respectievelijk toohello AccountName en AccountKey waarden.</span><span class="sxs-lookup"><span data-stu-id="09b6e-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="09b6e-131">Deze waarden worden tooyou geleverd door Media Services bij het instellen van uw account.</span><span class="sxs-lookup"><span data-stu-id="09b6e-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="09b6e-132">Houd er rekening mee dat Hallo AccountKey voor uw Media Services-account URL-codering moet (Zie [procent codering](http://tools.ietf.org/html/rfc3986#section-2.1) wanneer deze worden gebruikt als Hallo client_secret waarde in het token verzoek om toegang.</span><span class="sxs-lookup"><span data-stu-id="09b6e-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="09b6e-133">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="09b6e-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="09b6e-134">Hallo volgende voorbeeld ziet Hallo HTTP-antwoord met Hallo access token in Hallo antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="09b6e-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="09b6e-135">Het verdient aanbeveling toocache Hallo 'access_token' en 'expires_in' waarden tooan externe opslag.</span><span class="sxs-lookup"><span data-stu-id="09b6e-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="09b6e-136">Hallo token gegevens kan later worden opgehaald uit het Hallo-opslag en opnieuw worden gebruikt voor uw Media Services REST API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="09b6e-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="09b6e-137">Dit is vooral nuttig voor scenario's waarbij Hallo token kan veilig worden gedeeld tussen meerdere processen en computers.</span><span class="sxs-lookup"><span data-stu-id="09b6e-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="09b6e-138">Zorg ervoor dat toomonitor Hallo 'expires_in'-waarde van Hallo toegang token en de REST-API-aanroepen bijwerken met nieuwe tokens, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="09b6e-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="09b6e-139">Verbinding maken met toohello Media Services-URI</span><span class="sxs-lookup"><span data-stu-id="09b6e-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="09b6e-140">Hallo basis-URI voor Media Services is https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="09b6e-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="09b6e-141">U moet eerst verbinding maakt met toothis URI en als u een 301 omleiding terug in het antwoord krijgt, moet u volgende aanroepen toohello nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="09b6e-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="09b6e-142">Gebruik bovendien niet alle logica automatisch omleiden, volgen in uw aanvragen.</span><span class="sxs-lookup"><span data-stu-id="09b6e-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="09b6e-143">HTTP-termen en instanties van de aanvraag niet doorgestuurd toohello nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="09b6e-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="09b6e-144">Houd er rekening mee dat Hallo hoofdmap URI voor het uploaden en downloaden van bestanden van de Asset is https://yourstorageaccount.blob.core.windows.net/ waarbij opslagaccountnaam Hallo Hallo hetzelfde abonnement dat u tijdens de installatie van uw Media Services-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="09b6e-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="09b6e-145">Hallo volgende voorbeeld ziet u HTTP-aanvraag toohello Media Services hoofdmap URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="09b6e-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="09b6e-146">Hallo aanvraag haalt een 301 omleiding terug in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="09b6e-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="09b6e-147">Hallo volgend verzoek maakt gebruik van Hallo nieuwe URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="09b6e-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="09b6e-148">**HTTP-aanvraag**:</span><span class="sxs-lookup"><span data-stu-id="09b6e-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="09b6e-149">**HTTP-antwoord**:</span><span class="sxs-lookup"><span data-stu-id="09b6e-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="09b6e-150">**HTTP-aanvraag** (met behulp van nieuwe URI Hallo):</span><span class="sxs-lookup"><span data-stu-id="09b6e-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="09b6e-151">**HTTP-antwoord**:</span><span class="sxs-lookup"><span data-stu-id="09b6e-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="09b6e-152">Als u eenmaal Hallo nieuwe Hallo URI die de URI die moet worden gebruikt toocommunicate met Media Services.</span><span class="sxs-lookup"><span data-stu-id="09b6e-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="09b6e-153">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="09b6e-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09b6e-154">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="09b6e-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

