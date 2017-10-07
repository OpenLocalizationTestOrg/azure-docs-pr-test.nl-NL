---
title: een asset met Media Encoder Standard met hello Azure-portal aaaEncode | Microsoft Docs
description: Deze zelfstudie leert u Hallo van een activum met Media Encoder Standard met hello Azure-portal-codering.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="67165-103">Een asset met Media Encoder Standard met hello Azure-portal coderen</span><span class="sxs-lookup"><span data-stu-id="67165-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="67165-104">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="67165-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="67165-105">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67165-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="67165-106">Als u werkt met Azure Media Services is een van de meest voorkomende scenario's Hallo adaptive bitrate streaming tooyour clients leveren.</span><span class="sxs-lookup"><span data-stu-id="67165-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="67165-107">Media Services ondersteunt de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="67165-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="67165-108">tooprepare uw video's voor adaptive bitrate streaming, moet u tooencode de bron-video in multi-bitrate-bestanden.</span><span class="sxs-lookup"><span data-stu-id="67165-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="67165-109">Moet u Hallo **Media Encoder Standard** encoder tooencode uw video's.</span><span class="sxs-lookup"><span data-stu-id="67165-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="67165-110">Media Services biedt ook dynamische pakketten zodat u toodeliver uw multi-bitrate MP4s in de volgende streaming-indelingen Hallo: MPEG DASH, HLS, Smooth Streaming, zonder dat u toore-pakket in een van deze streaming-indelingen hoeft.</span><span class="sxs-lookup"><span data-stu-id="67165-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="67165-111">Met dynamische pakketten hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="67165-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="67165-112">tootake profiteren van dynamische pakketten hoeft u tooencode uw bronbestand in een set multi-bitrate MP4-bestanden (Hallo coderingsstappen worden uitgelegd later in deze sectie).</span><span class="sxs-lookup"><span data-stu-id="67165-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="67165-113">tooscale media verwerking, Zie [dit](media-services-portal-scale-media-processing.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="67165-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="67165-114">Codeer Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="67165-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="67165-115">Deze sectie beschrijft Hallo mogelijke stappen tooencode uw inhoud met Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="67165-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="67165-116">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="67165-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="67165-117">In Hallo **instellingen** Selecteer **activa**.</span><span class="sxs-lookup"><span data-stu-id="67165-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="67165-118">In Hallo **activa** venster, selecteer Hallo asset dat u tooencode wilt.</span><span class="sxs-lookup"><span data-stu-id="67165-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="67165-119">Druk op Hallo **coderen** knop.</span><span class="sxs-lookup"><span data-stu-id="67165-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="67165-120">In Hallo **een asset coderen** venster, selecteer Hallo 'Media Encoder Standard' processor en een standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="67165-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="67165-121">Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="67165-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="67165-122">Als u van plan toocontrol welke codering definitie wordt gebruikt bent, houd hiermee rekening: het is belangrijk tooselect Hallo voorinstelling die het meest geschikt is voor uw invoervideo.</span><span class="sxs-lookup"><span data-stu-id="67165-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="67165-123">Bijvoorbeeld, als u weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kan u Hallo ' standaardinstelling H264 Multiple Bitrate 1080p ' vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="67165-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="67165-124">Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="67165-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="67165-125">Voor eenvoudiger beheer hebt u een optie bewerken Hallo-naam van de uitvoerasset hello en Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="67165-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="67165-127">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="67165-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="67165-128">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="67165-128">Next step</span></span>
<span data-ttu-id="67165-129">U kunt de voortgang codering taak Hello Azure-portal, zoals beschreven in [dit](media-services-portal-check-job-progress.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="67165-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="67165-130">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="67165-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="67165-131">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="67165-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

