---
title: Overzicht van Azure Media Services dynamische pakketten | Microsoft Docs
description: Het onderwerp biedt en overzicht van dynamische pakketten.
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
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="d3bbf-103">Dynamische verpakking</span><span class="sxs-lookup"><span data-stu-id="d3bbf-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="d3bbf-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d3bbf-104">Overview</span></span>
<span data-ttu-id="d3bbf-105">Microsoft Azure Media Services kunnen worden gebruikt voor het leveren van veel bron bestandsindelingen mediastreaming indelingen, en beveiliging van inhoud bestandsindelingen naar verschillende technologieën van de client (bijvoorbeeld iOS-, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="d3bbf-106">Deze clients begrijpen verschillende protocollen, bijvoorbeeld iOS een HTTP Live Streaming (HLS)-V4-indeling heeft en Silverlight en Xbox vereisen Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="d3bbf-107">Als u een set adaptive bitrate (multi-bitrate) hebt MP4-bestanden (ISO Base Media 14496-12) of een set adaptive bitrate Smooth Streaming-bestanden die u wilt leveren aan clients die MPEG DASH, HLS of Smooth Streaming begrijpen, moet u ook te profiteren van Media Services dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="d3bbf-108">Dynamische pakketten hoeft u een asset die bestaat uit een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden te maken.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="d3bbf-109">Klik, op basis van de opgegeven indeling de manifest- of fragmentdeel aanvraag, de On-Demand Streaming server zorgt ervoor dat u de stream ontvangt in het protocol dat u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="d3bbf-110">Hierdoor hoeft u voor slechts één opslagindeling de bestanden op te slaan en hiervoor te betalen. De Media Services-service bouwt en levert de juiste reactie op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d3bbf-111">Het volgende diagram ziet u de traditionele codering en de werkstroom voor statische pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Statische codering](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="d3bbf-113">Het volgende diagram toont de werkstroom dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Dynamische codering](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="d3bbf-115">Gangbare scenario</span><span class="sxs-lookup"><span data-stu-id="d3bbf-115">Common scenario</span></span>
1. <span data-ttu-id="d3bbf-116">Upload een invoerbestand (een tussentijds bestand genoemd).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="d3bbf-117">Bijvoorbeeld, H.264 MP4 of WMV (voor een lijst met ondersteunde indelingen raadpleegt [indelingen ondersteund door de Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="d3bbf-118">Codeer uw tussentijds bestand op H.264 MP4 adaptive bitrate sets.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="d3bbf-119">Publiceer de asset met de adaptive bitrate MP4-set door de On-Demand-Locator te maken.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="d3bbf-120">Bouw de streaming-URL's voor toegang tot en de inhoud streamen.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="d3bbf-121">Activa voorbereiden voor dynamische streaming</span><span class="sxs-lookup"><span data-stu-id="d3bbf-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="d3bbf-122">Als u wilt uw asset voorbereiden voor het streamen van dynamische hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="d3bbf-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="d3bbf-123">[Een master-bestand uploaden](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="d3bbf-124">[De Media Encoder Standard encoder gebruiken voor het produceren MP4 H.264 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="d3bbf-125">[De inhoud streamen](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3bbf-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="d3bbf-126"><a id="unsupported_formats"></a>De opmaak die niet worden ondersteund door dynamische pakketten</span><span class="sxs-lookup"><span data-stu-id="d3bbf-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="d3bbf-127">De volgende indelingen voor bron worden niet ondersteund voor dynamische pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="d3bbf-128">Dolby digitale mp4-bestanden.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="d3bbf-129">Dolby digitale smooth bestanden.</span><span class="sxs-lookup"><span data-stu-id="d3bbf-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d3bbf-130">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="d3bbf-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3bbf-131">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d3bbf-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

