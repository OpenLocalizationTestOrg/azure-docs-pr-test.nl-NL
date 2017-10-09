---
title: aaaAzure Media Services Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen (FAQ's)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="451c1-103">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="451c1-103">Frequently asked questions</span></span>

<span data-ttu-id="451c1-104">In dit artikel komen Veelgestelde vragen die worden gegenereerd door de gebruikersgemeenschap van hello Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="451c1-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="451c1-105">Algemene AMS Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="451c1-105">General AMS FAQs</span></span>
<span data-ttu-id="451c1-106">V: hoe u de schaal van indexeren?</span><span class="sxs-lookup"><span data-stu-id="451c1-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="451c1-107">A: Hallo gereserveerde eenheden zijn hello dezelfde voor codering en taken te indexeren.</span><span class="sxs-lookup"><span data-stu-id="451c1-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="451c1-108">Volg de instructies op [hoe tooScale met gereserveerde Coderingseenheden](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="451c1-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="451c1-109">**Opmerking** prestaties van de indexeerfunctie wordt niet beïnvloed door gereserveerde eenheidstype.</span><span class="sxs-lookup"><span data-stu-id="451c1-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="451c1-110">V: ik geüpload, gecodeerd en u een video gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="451c1-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="451c1-111">Wat Hallo reden Hallo video zou zijn niet afgespeeld wanneer ik probeer toostream deze?</span><span class="sxs-lookup"><span data-stu-id="451c1-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="451c1-112">A: een van de meest voorkomende redenen is er geen streaming-eindpunt van waaruit u tooplayback in Hallo probeert Hallo Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="451c1-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="451c1-113">V: kan ik samenstellen op een live stream doen?</span><span class="sxs-lookup"><span data-stu-id="451c1-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="451c1-114">A: samenstellen op live gegevensstromen is momenteel niet beschikbaar in Azure Media Services, dus u toopre moet-opstellen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="451c1-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="451c1-115">V: kan ik Azure CDN gebruiken met Live Streaming</span><span class="sxs-lookup"><span data-stu-id="451c1-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="451c1-116">A: Media Services ondersteunt de integratie met Azure CDN (Zie voor meer informatie [hoe tooManage Streaming-eindpunten in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="451c1-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="451c1-117">U kunt Live streamen met CDN.</span><span class="sxs-lookup"><span data-stu-id="451c1-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="451c1-118">Azure Media Services biedt Smooth Streaming, HLS en MPEG-DASH-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="451c1-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="451c1-119">Alle deze indelingen HTTP gebruiken voor het overbrengen van gegevens en voordelen van het HTTP-caching krijgen.</span><span class="sxs-lookup"><span data-stu-id="451c1-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="451c1-120">In live streaming werkelijke video en audio-gegevens is onderverdeeld toofragments en deze afzonderlijke fragmenten ophalen in de cache opgeslagen in CDN.</span><span class="sxs-lookup"><span data-stu-id="451c1-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="451c1-121">Alleen gegevens behoeften toobe vernieuwd is Hallo manifest gegevens.</span><span class="sxs-lookup"><span data-stu-id="451c1-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="451c1-122">CDN worden regelmatig vernieuwd manifest gegevens.</span><span class="sxs-lookup"><span data-stu-id="451c1-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="451c1-123">V: biedt Azure Media services ondersteuning voor installatiekopieën van opslaan?</span><span class="sxs-lookup"><span data-stu-id="451c1-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="451c1-124">A: als u alleen toostore JPEG of PNG-afbeeldingen zoekt, moet u die in Azure Blob Storage behouden.</span><span class="sxs-lookup"><span data-stu-id="451c1-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="451c1-125">Er is geen voordeel tooputting die ze op in uw Media Services-account, tenzij u ze die zijn gekoppeld aan uw Video of Audio activa tookeep wilt.</span><span class="sxs-lookup"><span data-stu-id="451c1-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="451c1-126">Of als u nodig toouse Hallo afbeeldingen als overlays in Hallo video encoder wellicht. Media Encoder Standard ondersteunt hierbij afbeeldingen boven op video's en dat deze lijsten JPEG- en PNG-ondersteunde indelingen invoer.</span><span class="sxs-lookup"><span data-stu-id="451c1-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="451c1-127">Zie voor meer informatie [Overlays maken](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="451c1-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="451c1-128">V: hoe kan ik de activa van een Media Services-account tooanother kopiëren.</span><span class="sxs-lookup"><span data-stu-id="451c1-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="451c1-129">A: toocopy activa van een Media Services-account tooanother met .NET, gebruik [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) uitbreidingsmethode beschikbaar in Hallo [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="451c1-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="451c1-130">Zie voor meer informatie [dit](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span><span class="sxs-lookup"><span data-stu-id="451c1-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="451c1-131">V: wat zijn Hallo-ondersteunde tekens voor het benoemen van bestanden wanneer u werkt met AMS?</span><span class="sxs-lookup"><span data-stu-id="451c1-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="451c1-132">A: Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="451c1-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="451c1-133">waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '.</span><span class="sxs-lookup"><span data-stu-id="451c1-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="451c1-134">Bovendien kunnen alleen er een '.'</span><span class="sxs-lookup"><span data-stu-id="451c1-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="451c1-135">Hallo bestandsnaamextensie.</span><span class="sxs-lookup"><span data-stu-id="451c1-135">for hello file name extension.</span></span>

<span data-ttu-id="451c1-136">V: hoe tooconnect met behulp van REST?</span><span class="sxs-lookup"><span data-stu-id="451c1-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="451c1-137">A: voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="451c1-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="451c1-138">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="451c1-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="451c1-139">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="451c1-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="451c1-140">V: hoe kan ik een video draaien tijdens Hallo proces codering.</span><span class="sxs-lookup"><span data-stu-id="451c1-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="451c1-141">A: Hallo [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) draaihoek door hoeken van 180-90/270 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="451c1-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="451c1-142">Hallo standaardgedrag is 'Auto', waarbij toodetect Hallo rotatie metagegevens in Hallo binnenkomende MP4/MOV-bestand probeert en compenseren voor het.</span><span class="sxs-lookup"><span data-stu-id="451c1-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="451c1-143">Neem de volgende Hallo **bronnen** element tooone van Hallo json standaardinstellingen gedefinieerd [hier](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="451c1-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="451c1-144">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="451c1-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="451c1-145">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="451c1-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
