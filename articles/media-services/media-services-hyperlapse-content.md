---
title: Media-bestanden met Azure Media Hyperlapse aaaHyperlapse | Microsoft Docs
description: Azure Media Hyperlapse maakt smooth verstreken tijd video's van de eerste persoon of actie camera inhoud. Dit onderwerp wordt beschreven hoe toouse Media indexeerfunctie.
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="6b9e0-104">Hyperlapse Media-bestanden met Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="6b9e0-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="6b9e0-105">Azure Media Hyperlapse is een Media Processor (MP) die u smooth video's verstreken tijd van eerste persoon of actie camera inhoud maakt.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="6b9e0-106">cloud-gebaseerd op hetzelfde niveau te Hallo[van Microsoft Research bureaublad Hyperlapse Pro en Hyperlapse mobiele telefoon](http://aka.ms/hyperlapse), Hallo grootschalige Hallo Azure Media Services Media maakt gebruik van Microsoft Hyperlapse voor Azure Media Services De verwerking van platform toohorizontally schalen en bulksgewijs parallelize Hyperlapse verwerking.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b9e0-107">Microsoft Hyperlapse is ontworpen toowork geschikt is voor de eerste persoon inhoud met een zwevend camera.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="6b9e0-108">Hoewel u nog steeds camerabeelden kunt nog steeds werken, kunnen niet Hallo prestaties en kwaliteit van hello Azure Media Hyperlapse Media-Processor worden gegarandeerd voor andere typen inhoud.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="6b9e0-109">meer informatie over Microsoft Hyperlapse voor Azure Media Services toolearn en bekijk enkele voorbeeld-video's, bekijk Hallo [inleidende blogbericht](http://aka.ms/azurehyperlapseblog) van Hallo openbare preview.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="6b9e0-110">Een Azure Media Hyperlapse taak als neemt invoer een MP4, MOV of WMV assetbestand samen met een configuratiebestand dat Hiermee wordt aangegeven welke frames van video moeten verstreken tijd en toowhat snelheid (bijvoorbeeld de eerste 10.000 frames 2 x).</span><span class="sxs-lookup"><span data-stu-id="6b9e0-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="6b9e0-111">Hallo-uitvoer is een weergave gestabiliseerd en verstreken tijd van Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="6b9e0-112">Zie voor de meest recente Azure Media Hyperlapse updates hello, [Media Services-blogs](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="6b9e0-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="6b9e0-113">Hyperlapse een asset</span><span class="sxs-lookup"><span data-stu-id="6b9e0-113">Hyperlapse an asset</span></span>
<span data-ttu-id="6b9e0-114">Eerst moet u tooupload uw gewenste invoerbestand tooAzure Media Services.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="6b9e0-115">Hallo toolearn informatie over concepten die betrokken zijn bij het uploaden en beheren van inhoud, Hallo lezen [inhoudsbeheer artikel](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e0-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="6b9e0-116"><a id="configuration"></a>Definitie van de configuratie voor Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="6b9e0-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="6b9e0-117">Nadat de inhoud van uw Media Services-account is, moet u uw configuratie voorinstelling tooconstruct.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="6b9e0-118">Hallo volgende tabel wordt uitgelegd Hallo gebruiker opgegeven velden:</span><span class="sxs-lookup"><span data-stu-id="6b9e0-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="6b9e0-119">Veld</span><span class="sxs-lookup"><span data-stu-id="6b9e0-119">Field</span></span> | <span data-ttu-id="6b9e0-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6b9e0-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b9e0-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="6b9e0-121">StartFrame</span></span> |<span data-ttu-id="6b9e0-122">Hallo-frame bij welke Hallo Microsoft Hyperlapse verwerking moet beginnen.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="6b9e0-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="6b9e0-123">NumFrames</span></span> |<span data-ttu-id="6b9e0-124">aantal frames tooprocess Hallo</span><span class="sxs-lookup"><span data-stu-id="6b9e0-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="6b9e0-125">Snelheid</span><span class="sxs-lookup"><span data-stu-id="6b9e0-125">Speed</span></span> |<span data-ttu-id="6b9e0-126">Hallo factor met welke toospeed Hallo invoer video bestaat.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="6b9e0-127">Hallo Hieronder volgt een voorbeeld van een configuratiebestand overeenstemmende in XML en JSON:</span><span class="sxs-lookup"><span data-stu-id="6b9e0-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="6b9e0-128">**XML-definitie:**</span><span class="sxs-lookup"><span data-stu-id="6b9e0-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="6b9e0-129">**JSON-definitie:**</span><span class="sxs-lookup"><span data-stu-id="6b9e0-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="6b9e0-130"><a id="sample_code"></a>Microsoft Hyperlapse Hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6b9e0-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="6b9e0-131">Hallo volgende methode uploadt een mediabestand als een actief en maakt een taak Hello Azure Media Hyperlapse Media-Processor.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="6b9e0-132">U hebt al een CloudMediaContext binnen het bereik met Hallo-naam 'context' van deze toowork code.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="6b9e0-133">meer informatie over deze, lees Hallo toolearn [inhoudsbeheer artikel](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e0-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="6b9e0-134">tekenreeksargument Hallo 'hyperConfig' is een verwachte toobe een overeenstemmende configuratie vooraf in JSON of XML zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="6b9e0-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="6b9e0-135"><a id="file_types"></a>Ondersteunde bestandstypen</span><span class="sxs-lookup"><span data-stu-id="6b9e0-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="6b9e0-136">MP4</span><span class="sxs-lookup"><span data-stu-id="6b9e0-136">MP4</span></span>
* <span data-ttu-id="6b9e0-137">MOV</span><span class="sxs-lookup"><span data-stu-id="6b9e0-137">MOV</span></span>
* <span data-ttu-id="6b9e0-138">WMV</span><span class="sxs-lookup"><span data-stu-id="6b9e0-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6b9e0-139">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="6b9e0-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6b9e0-140">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="6b9e0-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6b9e0-141">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="6b9e0-141">Related links</span></span>
[<span data-ttu-id="6b9e0-142">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="6b9e0-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="6b9e0-143">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="6b9e0-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

