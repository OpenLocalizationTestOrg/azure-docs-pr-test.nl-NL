---
title: aaaPublish Azure Media Services-inhoud met behulp van REST
description: Meer informatie over hoe toocreate een locator die gebruikte toobuild een streaming-URL. Hallo code maakt gebruik van REST-API.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="69189-104">Azure Media Services-inhoud met behulp van REST publiceren</span><span class="sxs-lookup"><span data-stu-id="69189-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69189-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69189-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="69189-106">REST</span><span class="sxs-lookup"><span data-stu-id="69189-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="69189-107">Portal</span><span class="sxs-lookup"><span data-stu-id="69189-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="69189-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="69189-108">Overview</span></span>
<span data-ttu-id="69189-109">Een adaptive bitrate MP4-set door een OnDemand-locator voor streaming maken en het bouwen van een streaming-URL kan worden gestreamd.</span><span class="sxs-lookup"><span data-stu-id="69189-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="69189-110">Hallo [een asset coderen](media-services-rest-encode-asset.md) onderwerp ziet u hoe tooencode in een adaptive bitrate MP4 instellen.</span><span class="sxs-lookup"><span data-stu-id="69189-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="69189-111">Als uw inhoud is versleuteld, leveringsbeleid voor Assets configureren (zoals beschreven in [dit](media-services-rest-configure-asset-delivery-policy.md) onderwerp) voordat u een locator maakt.</span><span class="sxs-lookup"><span data-stu-id="69189-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="69189-112">U kunt ook een OnDemand streaming-locator toobuild URL's die punt tooMP4-bestanden die geleidelijk kunnen worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="69189-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="69189-113">Dit onderwerp wordt beschreven hoe toocreate een OnDemand-locator voor streaming in volgorde toopublish uw asset en bouwen van een Smooth, MPEG DASH en streaming-URL voor HLS.</span><span class="sxs-lookup"><span data-stu-id="69189-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="69189-114">U ziet ook hot toobuild progressieve download-URL's.</span><span class="sxs-lookup"><span data-stu-id="69189-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="69189-115">Hallo [volgende](#types) sectie toont Hallo enum-typen waarvan de waarden worden gebruikt in Hallo REST-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="69189-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="69189-116">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="69189-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="69189-117">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="69189-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="69189-118">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="69189-118">Connect tooMedia Services</span></span>

<span data-ttu-id="69189-119">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="69189-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="69189-120">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="69189-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="69189-121">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="69189-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="69189-122">Een OnDemand-streaminglocator maken</span><span class="sxs-lookup"><span data-stu-id="69189-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="69189-123">toocreate Hallo OnDemand-streaminglocator en URL's moet u toodo Hallo na ophalen:</span><span class="sxs-lookup"><span data-stu-id="69189-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="69189-124">Als het Hallo-inhoud is versleuteld, een toegangsbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="69189-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="69189-125">Een OnDemand-streaminglocator maken.</span><span class="sxs-lookup"><span data-stu-id="69189-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="69189-126">Als u van plan toostream bent, krijgt u Hallo manifestbestand (ISM) in Hallo asset streamen.</span><span class="sxs-lookup"><span data-stu-id="69189-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="69189-127">Als u van plan tooprogressively downloaden bent, moet u de namen van de Hallo MP4-bestanden in Hallo-activum ophalen.</span><span class="sxs-lookup"><span data-stu-id="69189-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="69189-128">URL's toohello manifestbestand of MP4-bestanden maken.</span><span class="sxs-lookup"><span data-stu-id="69189-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="69189-129">Merk op dat u een streaming-locator met behulp van een AccessPolicy die bevat geen maken schrijven of verwijderen van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="69189-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="69189-130">Een toegangsbeleid maken</span><span class="sxs-lookup"><span data-stu-id="69189-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="69189-131">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="69189-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="69189-132">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="69189-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="69189-133">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="69189-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="69189-134">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="69189-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="69189-135">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="69189-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="69189-136">Een OnDemand-streaminglocator maken</span><span class="sxs-lookup"><span data-stu-id="69189-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="69189-137">Hallo-locator voor Hallo opgegeven asset en activa-beleid maken.</span><span class="sxs-lookup"><span data-stu-id="69189-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="69189-138">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="69189-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="69189-139">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="69189-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="69189-140">Streaming-URL's samenstellen</span><span class="sxs-lookup"><span data-stu-id="69189-140">Build streaming URLs</span></span>
<span data-ttu-id="69189-141">Gebruik Hallo **pad** waarde geretourneerd na het maken van Hallo locator toobuild Hallo Hallo Smooth, HLS en MPEG DASH-URL's.</span><span class="sxs-lookup"><span data-stu-id="69189-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="69189-142">Smooth Streaming: **pad** + manifestbestand naam + "/ manifest"</span><span class="sxs-lookup"><span data-stu-id="69189-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="69189-143">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69189-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="69189-144">HLS: **pad** + manifestbestand naam + "/ manifest(format=m3u8-aapl) '</span><span class="sxs-lookup"><span data-stu-id="69189-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="69189-145">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69189-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="69189-146">DASH: **pad** + manifestbestand naam + "/ manifest(format=mpd-time-csf) '</span><span class="sxs-lookup"><span data-stu-id="69189-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="69189-147">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69189-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="69189-148">Progressieve download-URL's samenstellen</span><span class="sxs-lookup"><span data-stu-id="69189-148">Build progressive download URLs</span></span>
<span data-ttu-id="69189-149">Gebruik Hallo **pad** waarde geretourneerd nadat het maken van Hallo van Hallo locator toobuild Hallo progressieve download-URL.</span><span class="sxs-lookup"><span data-stu-id="69189-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="69189-150">URL: **pad** + asset mp4 bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="69189-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="69189-151">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69189-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="69189-152"><a id="types"></a>Enum-typen</span><span class="sxs-lookup"><span data-stu-id="69189-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="69189-153">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="69189-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="69189-154">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="69189-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="69189-155">Zie ook</span><span class="sxs-lookup"><span data-stu-id="69189-155">See also</span></span>
[<span data-ttu-id="69189-156">Media Services operations REST-API-overzicht</span><span class="sxs-lookup"><span data-stu-id="69189-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="69189-157">Leveringsbeleid voor Assets configureren</span><span class="sxs-lookup"><span data-stu-id="69189-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

