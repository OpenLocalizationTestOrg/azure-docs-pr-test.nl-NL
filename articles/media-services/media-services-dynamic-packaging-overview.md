---
title: aaaAzure Media Services dynamische pakketten overzicht | Microsoft Docs
description: Hallo onderwerp biedt en overzicht van dynamische pakketten.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="a1038-103">Dynamische verpakking</span><span class="sxs-lookup"><span data-stu-id="a1038-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="a1038-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a1038-104">Overview</span></span>
<span data-ttu-id="a1038-105">Microsoft Azure Media Services kunnen worden gebruikt toodeliver veel media bron bestandsindelingen, media streaming-indelingen en beveiliging van inhoud indelingen tooa verschillende technologieën van de client (bijvoorbeeld iOS-, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="a1038-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="a1038-106">Deze clients begrijpen verschillende protocollen, bijvoorbeeld iOS een HTTP Live Streaming (HLS)-V4-indeling heeft en Silverlight en Xbox vereisen Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a1038-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="a1038-107">Als u een set adaptive bitrate (multi-bitrate) hebt MP4-bestanden (ISO Base Media 14496-12) of een set adaptive bitrate Smooth Streaming-bestanden die u wilt dat tooserve tooclients die MPEG DASH, HLS of Smooth Streaming begrijpen, moet u ook te profiteren van Media Services dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="a1038-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="a1038-108">Met dynamische verpakking alles wat die u nodig is toocreate een asset die een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="a1038-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="a1038-109">Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo of fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="a1038-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="a1038-110">Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="a1038-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="a1038-111">Hallo volgende diagram toont Hallo traditionele codering en werkstroom voor statische pakketten.</span><span class="sxs-lookup"><span data-stu-id="a1038-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Statische codering](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="a1038-113">Hallo toont volgende diagram Hallo dynamische pakketten werkstroom.</span><span class="sxs-lookup"><span data-stu-id="a1038-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Dynamische codering](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="a1038-115">Gangbare scenario</span><span class="sxs-lookup"><span data-stu-id="a1038-115">Common scenario</span></span>
1. <span data-ttu-id="a1038-116">Upload een invoerbestand (een tussentijds bestand genoemd).</span><span class="sxs-lookup"><span data-stu-id="a1038-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="a1038-117">Bijvoorbeeld, H.264 MP4 of WMV (Zie voor een lijst met ondersteunde indelingen Hallo [indelingen ondersteund door de Media Encoder Standard Hallo](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="a1038-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="a1038-118">Codeer uw tussentijds bestand tooH.264 MP4 adaptive bitrate sets.</span><span class="sxs-lookup"><span data-stu-id="a1038-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="a1038-119">Publiceer Hallo asset met Hallo adaptive bitrate MP4-set Hallo On Demand Locator maken.</span><span class="sxs-lookup"><span data-stu-id="a1038-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="a1038-120">Hallo streaming-URL's tooaccess bouwen en de inhoud streamen.</span><span class="sxs-lookup"><span data-stu-id="a1038-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="a1038-121">Activa voorbereiden voor dynamische streaming</span><span class="sxs-lookup"><span data-stu-id="a1038-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="a1038-122">tooprepare uw asset voor dynamische streaming-u hebt twee opties:</span><span class="sxs-lookup"><span data-stu-id="a1038-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="a1038-123">[Een master-bestand uploaden](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="a1038-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="a1038-124">[Hallo Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets gebruiken](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="a1038-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="a1038-125">[De inhoud streamen](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1038-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="a1038-126"><a id="unsupported_formats"></a>De opmaak die niet worden ondersteund door dynamische pakketten</span><span class="sxs-lookup"><span data-stu-id="a1038-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="a1038-127">Hallo worden volgende bron indelingen niet ondersteund voor dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="a1038-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="a1038-128">Dolby digitale mp4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="a1038-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="a1038-129">Dolby digitale smooth bestanden.</span><span class="sxs-lookup"><span data-stu-id="a1038-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a1038-130">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="a1038-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1038-131">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="a1038-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

