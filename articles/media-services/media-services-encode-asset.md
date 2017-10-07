---
title: aaaOverview en vergelijking van Azure op vraag media coderingsprogramma's | Microsoft Docs
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="ed606-103">Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma 's</span><span class="sxs-lookup"><span data-stu-id="ed606-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="ed606-104">Overzicht van de codering</span><span class="sxs-lookup"><span data-stu-id="ed606-104">Encoding overview</span></span>
<span data-ttu-id="ed606-105">Azure Media Services biedt meerdere opties voor het Hallo-codering van media in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="ed606-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="ed606-106">Wanneer u begint met Media Services, is het belangrijk toounderstand Hallo verschil tussen codecs en bestandsindelingen.</span><span class="sxs-lookup"><span data-stu-id="ed606-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="ed606-107">Codecs zijn Hallo-software die Hallo compressie/decompressie algoritmen implementeert dat bestandsindelingen zijn containers waarin Hallo gecomprimeerd video.</span><span class="sxs-lookup"><span data-stu-id="ed606-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="ed606-108">Media Services biedt dynamische pakketten zodat u uw adaptive bitrate MP4- of Smooth Streaming inhoud gecodeerde in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) toodeliver zonder dat u hoeft toore-pakket in een van deze streaming-indelingen.</span><span class="sxs-lookup"><span data-stu-id="ed606-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="ed606-109">Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="ed606-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ed606-110">uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status.</span><span class="sxs-lookup"><span data-stu-id="ed606-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="ed606-111">tootake profiteren van [dynamische pakketten](media-services-dynamic-packaging-overview.md), hebt u toodo Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ed606-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="ed606-112">Bovendien moet u uw bronbestand coderen in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden (Hallo coderingsstappen worden verderop in deze zelfstudie uitgelegd).</span><span class="sxs-lookup"><span data-stu-id="ed606-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="ed606-113">Media Services ondersteunt de volgende Hallo op aanvraag coderingsprogramma's die worden beschreven in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="ed606-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="ed606-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="ed606-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="ed606-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="ed606-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="ed606-116">Dit artikel bevat een kort overzicht van op verzoek media coderingsprogramma's en koppelingen tooarticles waarmee u meer gedetailleerde informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="ed606-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="ed606-117">Hallo-onderwerp bevat ook een vergelijking van Hallo coderingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="ed606-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="ed606-118">Standaard hebben elke Media Services-account een actieve codering taak tegelijk.</span><span class="sxs-lookup"><span data-stu-id="ed606-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="ed606-119">Meerdere codering taken gelijktijdig uitgevoerd, één voor elke codering gereserveerde eenheid die u hebt gekocht, kunt u codering eenheden waarmee u toohave reserveren.</span><span class="sxs-lookup"><span data-stu-id="ed606-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="ed606-120">Zie voor informatie [codering eenheden schalen](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed606-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="ed606-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="ed606-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="ed606-122">Hoe toouse</span><span class="sxs-lookup"><span data-stu-id="ed606-122">How toouse</span></span>
[<span data-ttu-id="ed606-123">Hoe tooencode met Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="ed606-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="ed606-124">Indelingen</span><span class="sxs-lookup"><span data-stu-id="ed606-124">Formats</span></span>
[<span data-ttu-id="ed606-125">Indelingen en codecs</span><span class="sxs-lookup"><span data-stu-id="ed606-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="ed606-126">Standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="ed606-126">Presets</span></span>
<span data-ttu-id="ed606-127">Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ed606-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="ed606-128">Invoer en uitvoer van metagegevens</span><span class="sxs-lookup"><span data-stu-id="ed606-128">Input and output metadata</span></span>
<span data-ttu-id="ed606-129">Hallo encoders invoer metagegevens wordt beschreven [hier](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ed606-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="ed606-130">Hallo encoders uitvoer metagegevens wordt beschreven [hier](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ed606-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="ed606-131">Genereren van miniaturen</span><span class="sxs-lookup"><span data-stu-id="ed606-131">Generate thumbnails</span></span>
<span data-ttu-id="ed606-132">Zie voor informatie [hoe toogenerate miniaturen met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="ed606-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="ed606-133">Trim video's (paginaknipsel)</span><span class="sxs-lookup"><span data-stu-id="ed606-133">Trim videos (clipping)</span></span>
<span data-ttu-id="ed606-134">Zie voor informatie [hoe tootrim video's met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="ed606-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="ed606-135">Overlays maken</span><span class="sxs-lookup"><span data-stu-id="ed606-135">Create overlays</span></span>
<span data-ttu-id="ed606-136">Zie voor informatie [hoe toocreate overlays met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="ed606-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="ed606-137">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ed606-137">See also</span></span>
[<span data-ttu-id="ed606-138">Hallo Media Services-blog</span><span class="sxs-lookup"><span data-stu-id="ed606-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="ed606-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="ed606-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="ed606-140">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ed606-140">Overview</span></span>
[<span data-ttu-id="ed606-141">Inleiding tot Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="ed606-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="ed606-142">Hoe toouse</span><span class="sxs-lookup"><span data-stu-id="ed606-142">How toouse</span></span>
<span data-ttu-id="ed606-143">Werkstroom voor Media Encoder Premium is geconfigureerd met behulp van complexe werkstromen.</span><span class="sxs-lookup"><span data-stu-id="ed606-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="ed606-144">Werkstroombestanden kan worden gemaakt en bijgewerkt met Hallo [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ed606-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="ed606-145">Hoe tooUse Premium codering in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="ed606-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="ed606-146">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ed606-146">Known issues</span></span>
<span data-ttu-id="ed606-147">Als uw invoervideo bevat geen ondertiteling, uitvoer Hallo dat Asset bevatten nog steeds een leeg TTML-bestand.</span><span class="sxs-lookup"><span data-stu-id="ed606-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ed606-148">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ed606-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ed606-149">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ed606-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="ed606-150">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="ed606-150">Related articles</span></span>
* [<span data-ttu-id="ed606-151">Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen</span><span class="sxs-lookup"><span data-stu-id="ed606-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="ed606-152">Quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="ed606-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
