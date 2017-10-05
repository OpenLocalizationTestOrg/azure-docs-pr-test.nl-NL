---
title: Overzicht en een vergelijking van Azure op aanvraag media encoders | Microsoft Docs
description: In dit onderwerp biedt een overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma's.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="f3e55-103">Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma 's</span><span class="sxs-lookup"><span data-stu-id="f3e55-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="f3e55-104">Overzicht van de codering</span><span class="sxs-lookup"><span data-stu-id="f3e55-104">Encoding overview</span></span>
<span data-ttu-id="f3e55-105">Azure Media Services biedt meerdere opties voor de codering van media in de cloud.</span><span class="sxs-lookup"><span data-stu-id="f3e55-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="f3e55-106">Wanneer u begint met Media Services, is het belangrijk om het verschil tussen codecs en bestandsindelingen.</span><span class="sxs-lookup"><span data-stu-id="f3e55-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="f3e55-107">Codecs zijn de software die u de algoritmen compressie/decompressie implementeert dat bestandsindelingen zijn containers waarin de gecomprimeerde video.</span><span class="sxs-lookup"><span data-stu-id="f3e55-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="f3e55-108">Media Services biedt dynamische pakketten zodat u uw adaptive bitrate MP4- of Smooth Streaming gecodeerde inhoud kunt in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) leveren zonder dat u opnieuw verpakken in een van deze streaming-indelingen hoeft.</span><span class="sxs-lookup"><span data-stu-id="f3e55-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="f3e55-109">Wanneer uw AMS-account is gemaakt, wordt er een **standaardstreaming-eindpunt** met de status **Gestopt** toegevoegd aan uw account.</span><span class="sxs-lookup"><span data-stu-id="f3e55-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="f3e55-110">Als u inhoud wilt streamen en gebruik wilt maken van dynamische pakketten en dynamische versleuteling, moet het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** hebben.</span><span class="sxs-lookup"><span data-stu-id="f3e55-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="f3e55-111">Om te profiteren van [dynamische pakketten](media-services-dynamic-packaging-overview.md), moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f3e55-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="f3e55-112">Bovendien moet u uw bronbestand coderen in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden (de coderingsstappen worden verderop in deze zelfstudie uitgelegd).</span><span class="sxs-lookup"><span data-stu-id="f3e55-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="f3e55-113">Media Services ondersteunt de volgende op aanvraag coderingsprogramma's die worden beschreven in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="f3e55-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="f3e55-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="f3e55-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="f3e55-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="f3e55-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="f3e55-116">Dit artikel bevat een kort overzicht van op verzoek media coderingsprogramma's en koppelingen naar artikelen waarmee u meer gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="f3e55-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="f3e55-117">Het onderwerp bevat ook een vergelijking van het coderingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="f3e55-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="f3e55-118">Standaard hebben elke Media Services-account een actieve codering taak tegelijk.</span><span class="sxs-lookup"><span data-stu-id="f3e55-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="f3e55-119">U kunt codering eenheden waarmee u kunt meerdere codering taken gelijktijdig uitgevoerd, één voor elke codering gereserveerde eenheid aankoop reserveren.</span><span class="sxs-lookup"><span data-stu-id="f3e55-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="f3e55-120">Zie voor informatie [codering eenheden schalen](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3e55-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="f3e55-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="f3e55-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="f3e55-122">Gebruiksinstructies</span><span class="sxs-lookup"><span data-stu-id="f3e55-122">How to use</span></span>
[<span data-ttu-id="f3e55-123">Het coderen met Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="f3e55-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="f3e55-124">Indelingen</span><span class="sxs-lookup"><span data-stu-id="f3e55-124">Formats</span></span>
[<span data-ttu-id="f3e55-125">Indelingen en codecs</span><span class="sxs-lookup"><span data-stu-id="f3e55-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="f3e55-126">Standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="f3e55-126">Presets</span></span>
<span data-ttu-id="f3e55-127">Media Encoder Standard is geconfigureerd met een van de encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f3e55-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="f3e55-128">Invoer en uitvoer van metagegevens</span><span class="sxs-lookup"><span data-stu-id="f3e55-128">Input and output metadata</span></span>
<span data-ttu-id="f3e55-129">De invoer metagegevens coderingsprogramma's wordt beschreven [hier](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f3e55-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="f3e55-130">De metagegevens van de uitvoer coderingsprogramma's wordt beschreven [hier](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f3e55-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="f3e55-131">Genereren van miniaturen</span><span class="sxs-lookup"><span data-stu-id="f3e55-131">Generate thumbnails</span></span>
<span data-ttu-id="f3e55-132">Zie voor informatie [het genereren van miniaturen met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="f3e55-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="f3e55-133">Trim video's (paginaknipsel)</span><span class="sxs-lookup"><span data-stu-id="f3e55-133">Trim videos (clipping)</span></span>
<span data-ttu-id="f3e55-134">Zie voor informatie [hoe video's met Media Encoder Standard trim](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="f3e55-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="f3e55-135">Overlays maken</span><span class="sxs-lookup"><span data-stu-id="f3e55-135">Create overlays</span></span>
<span data-ttu-id="f3e55-136">Zie voor informatie [maken met behulp van Media Encoder Standard overlays](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="f3e55-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="f3e55-137">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f3e55-137">See also</span></span>
[<span data-ttu-id="f3e55-138">De Media Services-blog</span><span class="sxs-lookup"><span data-stu-id="f3e55-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="f3e55-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="f3e55-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="f3e55-140">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f3e55-140">Overview</span></span>
[<span data-ttu-id="f3e55-141">Inleiding tot Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f3e55-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="f3e55-142">Gebruiksinstructies</span><span class="sxs-lookup"><span data-stu-id="f3e55-142">How to use</span></span>
<span data-ttu-id="f3e55-143">Werkstroom voor Media Encoder Premium is geconfigureerd met behulp van complexe werkstromen.</span><span class="sxs-lookup"><span data-stu-id="f3e55-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="f3e55-144">Werkstroombestanden kan worden gemaakt en bijgewerkt met de [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="f3e55-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="f3e55-145">Het gebruik van Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f3e55-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="f3e55-146">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="f3e55-146">Known issues</span></span>
<span data-ttu-id="f3e55-147">Als uw invoervideo geen bevat nog ondertiteling, de uitvoer van de Asset bevatten steeds een leeg TTML-bestand.</span><span class="sxs-lookup"><span data-stu-id="f3e55-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="f3e55-148">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f3e55-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f3e55-149">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f3e55-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="f3e55-150">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="f3e55-150">Related articles</span></span>
* [<span data-ttu-id="f3e55-151">Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen</span><span class="sxs-lookup"><span data-stu-id="f3e55-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="f3e55-152">Quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="f3e55-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
