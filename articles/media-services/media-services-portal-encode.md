---
title: Een asset met Media Encoder Standard met de Azure-portal coderen | Microsoft Docs
description: Deze zelfstudie leert u de stappen voor het coderen van een activum met Media Encoder Standard met de Azure-portal.
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="3dd83-103">Een asset met Media Encoder Standard met de Azure-portal coderen</span><span class="sxs-lookup"><span data-stu-id="3dd83-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3dd83-104">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="3dd83-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3dd83-105">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dd83-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="3dd83-106">Wanneer er met Azure Media Services wordt gewerkt, wordt er meestal een Adaptive Bitrate Streaming aan uw clients geleverd.</span><span class="sxs-lookup"><span data-stu-id="3dd83-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="3dd83-107">Media Services ondersteunt de volgende Adaptive Bitrate Streaming-technologieën: HLS (HTTP Live Streaming), Smooth Streaming en MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="3dd83-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="3dd83-108">Als u video's wilt voorbereiden voor Adaptive Bitrate Streaming, moet u de bronvideo coderen in multi-bitrate-bestanden.</span><span class="sxs-lookup"><span data-stu-id="3dd83-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="3dd83-109">Gebruik het coderingsprogramma **Media Encoder Standard** om de video's te coderen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="3dd83-110">Media Services biedt ook dynamische pakketten zodat u kunt uw multi-bitrate MP4s in de volgende streaming-indelingen leveren: MPEG DASH, HLS, Smooth Streaming, zonder dat u opnieuw verpakken in een van deze streaming-indelingen hoeft.</span><span class="sxs-lookup"><span data-stu-id="3dd83-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="3dd83-111">Voor dynamische pakketten hoeft u voor slechts één opslagindeling de bestanden op te slaan en hiervoor te betalen. Media Services bouwt en levert de juiste reactie op basis van aanvragen van een client.</span><span class="sxs-lookup"><span data-stu-id="3dd83-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3dd83-112">Als u gebruik wilt maken van dynamische pakketten, moet u het bronbestand coderen in een set multi-bitrate MP4-bestanden (de coderingsstappen worden verderop in deze sectie uitgelegd).</span><span class="sxs-lookup"><span data-stu-id="3dd83-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="3dd83-113">Als u wilt schalen verwerking van de media, Zie [dit](media-services-portal-scale-media-processing.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3dd83-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="3dd83-114">Coderen met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3dd83-114">Encode with the Azure portal</span></span>
<span data-ttu-id="3dd83-115">In deze sectie wordt beschreven hoe u uw inhoud codeert met Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="3dd83-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="3dd83-116">Selecteer uw Azure Media Services-account in [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3dd83-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3dd83-117">Selecteer in het venster **Instellingen** de optie **Assets**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="3dd83-118">Selecteer in het venster **Assets** de asset die u wilt coderen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="3dd83-119">Klik op de knop **Coderen**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="3dd83-120">Selecteer in het venster **Een asset coderen** de processor Media Encoder Standard en een standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="3dd83-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="3dd83-121">Zie [automatisch een bitrate ladder genereren](media-services-autogen-bitrate-ladder-with-mes.md) en [Standaardinstellingen voor taken in MES](media-services-mes-presets-overview.md) voor informatie over standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="3dd83-122">Als u wilt bepalen welke standaardinstelling voor versleuteling wordt gebruikt, moet u er rekening mee houden dat het belangrijk is de standaardinstelling te selecteren die het meest geschikt is voor uw invoervideo.</span><span class="sxs-lookup"><span data-stu-id="3dd83-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="3dd83-123">Als u bijvoorbeeld weet dat uw invoervideo een resolutie van 1920 x 1080 pixels heeft, kunt u de standaardinstelling H264 Multiple Bitrate 1080p gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3dd83-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="3dd83-124">Als u een video met een lage resolutie (640 x 360) hebt, gebruikt u niet de standaardinstelling H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="3dd83-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="3dd83-125">Voor eenvoudiger beheer kunt u de naam van de uitvoerasset en de naam van de taak bewerken.</span><span class="sxs-lookup"><span data-stu-id="3dd83-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Assets coderen](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="3dd83-127">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="3dd83-128">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="3dd83-128">Next step</span></span>
<span data-ttu-id="3dd83-129">U kunt de voortgang codering taak met de Azure portal, zoals beschreven in [dit](media-services-portal-check-job-progress.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3dd83-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="3dd83-130">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="3dd83-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3dd83-131">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="3dd83-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

