---
title: leveringsbeleid voor aaaConfiguring asset met Media Services REST-API | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooconfigure leveringsbeleid voor verschillende asset met Media Services REST-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="e5383-103">Beleid voor de levering asset configureren</span><span class="sxs-lookup"><span data-stu-id="e5383-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="e5383-104">Als u van plan activa toodeliver dynamisch worden versleuteld bent, stappen een Hallo Hallo Media Services content delivery werkstroom is leveringsbeleid voor assets configureren.</span><span class="sxs-lookup"><span data-stu-id="e5383-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="e5383-105">Hallo-leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset toobe geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), al dan niet de gewenste toodynamically uw asset coderen en hoe (envelop of common encryption).</span><span class="sxs-lookup"><span data-stu-id="e5383-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="e5383-106">Dit onderwerp wordt beschreven waarom en hoe toocreate en beleid voor de levering asset configureren.</span><span class="sxs-lookup"><span data-stu-id="e5383-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="e5383-107">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="e5383-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="e5383-108">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="e5383-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="e5383-109">Bovendien toobe kunnen toouse dynamische pakketten en dynamische versleuteling uw asset moet bevatten een set adaptive bitrate MP4s of adaptive bitrate Smooth Streaming-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e5383-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="e5383-110">U kunt ook verschillende beleidsregels toohello toepassen dezelfde asset.</span><span class="sxs-lookup"><span data-stu-id="e5383-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="e5383-111">U kunt bijvoorbeeld PlayReady-versleuteling tooSmooth Streaming en AES Envelope versleuteling tooMPEG toepassen DASH- en HLS.</span><span class="sxs-lookup"><span data-stu-id="e5383-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="e5383-112">Alle protocollen die niet zijn gedefinieerd in een leveringsbeleid (bijvoorbeeld, u toevoegen één beleid waarmee alleen HLS als protocol Hallo) van streaming wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e5383-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="e5383-113">Hallo uitzondering toothis is als u geen leveringsbeleid voor Assets helemaal gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e5383-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="e5383-114">Vervolgens zijn alle protocollen toegestaan in Hallo wissen.</span><span class="sxs-lookup"><span data-stu-id="e5383-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="e5383-115">Als u toodeliver een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief configureren.</span><span class="sxs-lookup"><span data-stu-id="e5383-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="e5383-116">Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor.</span><span class="sxs-lookup"><span data-stu-id="e5383-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="e5383-117">Bijvoorbeeld toodeliver uw asset versleuteld met Advanced Encryption Standard (AES) envelop versleutelingssleutel, stelt u het beleidstype hello te**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="e5383-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="e5383-118">versleuteling van opslag tooremove en stroom Hallo asset in Hallo wissen, stelt u Hallo beleidstype te**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="e5383-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="e5383-119">Voorbeelden van hoe tooconfigure deze beleidstypen volgen.</span><span class="sxs-lookup"><span data-stu-id="e5383-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="e5383-120">Afhankelijk van hoe u Hallo-leveringsbeleid voor Assets configureren die u zou kunnen toodynamically pakket worden dynamisch versleutelen en stream Hallo streaming protocollen te volgen: Smooth Streaming, HLS, MPEG DASH-streams.</span><span class="sxs-lookup"><span data-stu-id="e5383-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="e5383-121">Hallo volgende lijst bevat Hallo opgemaakt toostream Smooth, HLS, DASH te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e5383-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="e5383-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="e5383-122">Smooth Streaming:</span></span>

<span data-ttu-id="e5383-123">{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="e5383-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="e5383-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="e5383-124">HLS:</span></span>

<span data-ttu-id="e5383-125">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="e5383-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="e5383-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="e5383-126">MPEG DASH</span></span>

<span data-ttu-id="e5383-127">{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="e5383-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="e5383-128">Voor instructies over hoe toopublish een asset en bouwen van een streaming-URL, Zie [bouwen van een streaming-URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="e5383-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="e5383-129">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="e5383-129">Considerations</span></span>
* <span data-ttu-id="e5383-130">U kunt een AssetDeliveryPolicy die zijn gekoppeld aan een asset, terwijl een (streaming) OnDemand-locator voor de activa bestaat niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e5383-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="e5383-131">Hallo-aanbeveling is tooremove Hallo beleid uit Hallo actief voordat Hallo beleid wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e5383-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="e5383-132">Een streaming-locator kan niet worden gemaakt op een versleutelde actief opslag wanneer geen leveringsbeleid voor Assets is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e5383-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="e5383-133">Als Hallo Asset niet opslag versleuteld, kunt Hallo-systeem u een locator en stream Hallo-asset maken in Hallo wissen zonder een leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="e5383-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="e5383-134">U kunt meerdere asset levering beleidsregels die zijn gekoppeld aan één element hebben maar u kunt alleen eenrichtingssessie toohandle een bepaalde AssetDeliveryProtocol opgeven.</span><span class="sxs-lookup"><span data-stu-id="e5383-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="e5383-135">Dit betekent dat als u toolink twee leveringsbeleid die Hallo AssetDeliveryProtocol.SmoothStreaming protocol die resulteren in een fout opgetreden probeert opgeeft omdat Hallo systeem welke niet weet u dat wilt tooapply wanneer een client een Smooth Streaming-aanvraag indient.</span><span class="sxs-lookup"><span data-stu-id="e5383-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="e5383-136">Hebt u een asset met een bestaande streaming-locator, kan u een nieuw beleid toohello activum koppelen, ontkoppelen van een bestaand beleid uit Hallo actief of bijwerken van een leveringsbeleid Hallo asset gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e5383-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="e5383-137">U eerst tooremove Hallo streaming-locator hebben, Hallo beleid aanpassen en streaming-locator Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="e5383-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="e5383-138">U kunt Hallo dezelfde locatorId wanneer u opnieuw Hallo streaming maakt-locator, maar u moet ervoor zorgen dat niet toe leiden problemen voor clients dat omdat inhoud kan worden in het cachegeheugen van de oorsprong hello of een downstream CDN gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e5383-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="e5383-139">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="e5383-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="e5383-140">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e5383-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="e5383-141">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="e5383-141">Connect tooMedia Services</span></span>

<span data-ttu-id="e5383-142">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e5383-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="e5383-143">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="e5383-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="e5383-144">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="e5383-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="e5383-145">Leveringsbeleid voor Assets wissen</span><span class="sxs-lookup"><span data-stu-id="e5383-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="e5383-146"><a id="create_asset_delivery_policy"></a>Leveringsbeleid voor Assets maken</span><span class="sxs-lookup"><span data-stu-id="e5383-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="e5383-147">Hallo volgende HTTP-aanvraag maakt een leveringsbeleid asset waarmee toonot toepassen dynamische versleuteling en toodeliver Hallo stream in een van volgende Hallo protocollen: MPEG DASH, HLS en Smooth Streaming-protocollen.</span><span class="sxs-lookup"><span data-stu-id="e5383-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="e5383-148">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e5383-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="e5383-149">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="e5383-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="e5383-150">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="e5383-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="e5383-151"><a id="link_asset_with_asset_delivery_policy"></a>Koppeling asset met leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e5383-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="e5383-152">Hallo volgende HTTP-aanvraag koppelingen Hallo opgegeven toohello asset leveringsbeleid voor Assets op.</span><span class="sxs-lookup"><span data-stu-id="e5383-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="e5383-153">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="e5383-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="e5383-154">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="e5383-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="e5383-155">DynamicEnvelopeEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e5383-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="e5383-156">Inhoudssleutel van Hallo EnvelopeEncryption type maken en koppelen toohello asset</span><span class="sxs-lookup"><span data-stu-id="e5383-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="e5383-157">Wanneer u het leveringsbeleid DynamicEnvelopeEncryption opgeeft, moet u ervoor dat toolink toomake uw asset tooa-inhoudssleutel Hallo EnvelopeEncryption type.</span><span class="sxs-lookup"><span data-stu-id="e5383-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="e5383-158">Zie voor meer informatie: [maken van een inhoudssleutel](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="e5383-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="e5383-159"><a id="get_delivery_url"></a>Levering-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="e5383-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="e5383-160">Get Hallo levering URL voor Hallo opgegeven leveringsmethode van inhoud Hallo-sleutel in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e5383-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="e5383-161">Een client gebruikt Hallo geretourneerd URL toorequest AES-sleutel of een PlayReady-licenties in volgorde tooplayback Hallo beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="e5383-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="e5383-162">Hallo type Hallo URL tooget opgeven in de hoofdtekst Hallo van Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e5383-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="e5383-163">Als u uw inhoud met PlayReady beveiligt aanvragen van een Media Services PlayReady licentie overname URL, met behulp van 1 voor Hallo keyDeliveryType: {'keyDeliveryType': 1}.</span><span class="sxs-lookup"><span data-stu-id="e5383-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="e5383-164">Als u uw inhoud met Hallo envelop versleuteling beveiligt, een URL voor het belangrijkste aanvragen door op te geven van 2 voor keyDeliveryType: {'keyDeliveryType': 2}.</span><span class="sxs-lookup"><span data-stu-id="e5383-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="e5383-165">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="e5383-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="e5383-166">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="e5383-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="e5383-167">Leveringsbeleid voor Assets maken</span><span class="sxs-lookup"><span data-stu-id="e5383-167">Create asset delivery policy</span></span>
<span data-ttu-id="e5383-168">Hallo volgende HTTP-aanvraag maakt Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische versleuteling (**DynamicEnvelopeEncryption**) toohello **HLS**protocol (in dit voorbeeld andere protocollen worden geblokkeerd van streaming).</span><span class="sxs-lookup"><span data-stu-id="e5383-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="e5383-169">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e5383-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="e5383-170">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="e5383-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="e5383-171">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="e5383-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="e5383-172">Koppeling asset met leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e5383-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="e5383-173">Zie [koppeling asset met leveringsbeleid voor Assets](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="e5383-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="e5383-174">DynamicCommonEncryption-leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e5383-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="e5383-175">Inhoudssleutel van Hallo CommonEncryption type maken en koppelen toohello asset</span><span class="sxs-lookup"><span data-stu-id="e5383-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="e5383-176">Wanneer u het leveringsbeleid DynamicCommonEncryption opgeeft, moet u ervoor dat toolink toomake uw asset tooa-inhoudssleutel Hallo CommonEncryption type.</span><span class="sxs-lookup"><span data-stu-id="e5383-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="e5383-177">Zie voor meer informatie: [maken van een inhoudssleutel](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="e5383-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="e5383-178">Levering-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="e5383-178">Get Delivery URL</span></span>
<span data-ttu-id="e5383-179">Hallo levering URL voor Hallo PlayReady leveringsmethode van gemaakt in de vorige stap Hallo Hallo-inhoudssleutel niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="e5383-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="e5383-180">Een client gebruikt Hallo URL toorequest een PlayReady-licenties in volgorde tooplayback Hallo beveiligde inhoud geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e5383-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="e5383-181">Zie voor meer informatie [levering-URL ophalen](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="e5383-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="e5383-182">Leveringsbeleid voor Assets maken</span><span class="sxs-lookup"><span data-stu-id="e5383-182">Create asset delivery policy</span></span>
<span data-ttu-id="e5383-183">Hallo volgende HTTP-aanvraag maakt Hallo **AssetDeliveryPolicy** die geconfigureerde tooapply dynamische common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocol (in dit voorbeeld andere protocollen worden geblokkeerd van streaming).</span><span class="sxs-lookup"><span data-stu-id="e5383-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="e5383-184">Zie voor meer informatie over wat u waarden opgeven kunt bij het maken van een AssetDeliveryPolicy, Hallo [typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy](#types) sectie.</span><span class="sxs-lookup"><span data-stu-id="e5383-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="e5383-185">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="e5383-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="e5383-186">Als u uw inhoud met Widevine DRM tooprotect wilt, bijwerken Hallo AssetDeliveryConfiguration waarden toouse WidevineLicenseAcquisitionUrl (die Hallo waarde heeft van 7) en geef Hallo-URL van een service voor het leveren van licenties.</span><span class="sxs-lookup"><span data-stu-id="e5383-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="e5383-187">U kunt Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="e5383-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="e5383-188">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e5383-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="e5383-189">Bij het versleutelen met Widevine, zou u alleen kunnen toodeliver met STREEPJES zijn.</span><span class="sxs-lookup"><span data-stu-id="e5383-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="e5383-190">Zorg ervoor dat toospecify streepje (2) in Hallo asset leveringsprotocol.</span><span class="sxs-lookup"><span data-stu-id="e5383-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="e5383-191">Koppeling asset met leveringsbeleid voor Assets</span><span class="sxs-lookup"><span data-stu-id="e5383-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="e5383-192">Zie [koppeling asset met leveringsbeleid voor Assets](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="e5383-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="e5383-193"><a id="types"></a>Typen die worden gebruikt bij het definiëren van AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="e5383-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="e5383-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="e5383-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="e5383-195">Hallo beschrijft volgende enum waarden die u voor Hallo asset leveringsprotocol instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="e5383-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="e5383-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="e5383-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="e5383-197">Hallo beschrijft volgende enum waarden die u voor Hallo asset bezorgingstype beleid instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="e5383-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="e5383-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="e5383-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="e5383-199">Hallo beschrijft volgende enum waarden kunt u tooconfigure Hallo leveringsmethode van Hallo inhoud sleutel toohello client.</span><span class="sxs-lookup"><span data-stu-id="e5383-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="e5383-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="e5383-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="e5383-201">Hallo na enum beschrijft waarden kunt u tooget specifieke configuratie van tooconfigure sleutels die worden gebruikt voor een leveringsbeleid voor Assets instellen.</span><span class="sxs-lookup"><span data-stu-id="e5383-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="e5383-202">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="e5383-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5383-203">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="e5383-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

