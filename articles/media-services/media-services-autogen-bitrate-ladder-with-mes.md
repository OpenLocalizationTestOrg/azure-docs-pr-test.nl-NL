---
title: Azure Media Encoder Standard tooauto aaaUse-genereren van een ladder bitrate | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toouse Media Encoder Standard (MES) tooauto-een bitrate ladder op basis van Hallo invoer resolutie en bitrate genereren. Hallo invoer resolutie en bitrate wordt nooit worden overschreden. Bijvoorbeeld, als Hallo-invoer is 720p op 3 Mbps, uitvoer wordt met de beste 720p blijven en wordt gestart volgens de tarieven voor lager is dan 3 Mbps.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="54fc0-105">Gebruik Azure Media Encoder Standard tooauto-een ladder bitrate genereren</span><span class="sxs-lookup"><span data-stu-id="54fc0-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="54fc0-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="54fc0-106">Overview</span></span>

<span data-ttu-id="54fc0-107">Dit onderwerp wordt beschreven hoe toouse Media Encoder Standard (MES) tooauto-een bitrate ladder (bitrate resolutie paren) op basis van Hallo invoer resolutie en bitrate genereren.</span><span class="sxs-lookup"><span data-stu-id="54fc0-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="54fc0-108">Hallo wordt automatisch gegenereerde voorinstelling nooit overschrijden, Hallo invoer resolutie en bitsnelheid.</span><span class="sxs-lookup"><span data-stu-id="54fc0-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="54fc0-109">Bijvoorbeeld, als Hallo-invoer is 720p op 3 Mbps, uitvoer wordt met de beste 720p blijven en wordt gestart volgens de tarieven voor lager is dan 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="54fc0-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="54fc0-110">Voor Streaming alleen codering</span><span class="sxs-lookup"><span data-stu-id="54fc0-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="54fc0-111">Als uw bedoeling tooencode is vooraf de bron-alleen voor streaming video u moeten 'Adaptief streamen' hello gebruiken bij het maken van een taak die voor codering.</span><span class="sxs-lookup"><span data-stu-id="54fc0-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="54fc0-112">Wanneer u Hallo **adaptief streamen** definitie Hallo MES codering wordt op intelligente wijze cap een ladder bitrate.</span><span class="sxs-lookup"><span data-stu-id="54fc0-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="54fc0-113">Echter, u zich niet kunnen toocontrol Hallo codering kosten, aangezien hoeveel lagen toouse Hallo-service bepaalt en met welke resolutie.</span><span class="sxs-lookup"><span data-stu-id="54fc0-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="54fc0-114">Ziet u voorbeelden van lagen van uitvoer geproduceerd door MES als gevolg van codering met Hallo **adaptief streamen** vooraf ingesteld op Hallo einde van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="54fc0-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="54fc0-115">Hallo uitvoer Asset MP4-bestanden bevat waar audio en video niet interleaved.</span><span class="sxs-lookup"><span data-stu-id="54fc0-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="54fc0-116">Codering in voor streamen en progressief downloaden</span><span class="sxs-lookup"><span data-stu-id="54fc0-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="54fc0-117">Als uw bedoeling tooencode is vooraf de bronvideo voor streaming en tooproduce MP4-bestanden voor progressieve download u moeten 'Inhoud adaptieve meerdere Bitrate MP4' hello gebruiken bij het maken van een taak die voor codering.</span><span class="sxs-lookup"><span data-stu-id="54fc0-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="54fc0-118">Wanneer u Hallo **inhoud adaptieve meerdere Bitrate MP4** definitie Hallo MES encoder toepassing hello dezelfde codering logica als hierboven, maar nu Hallo uitvoerasset bevat MP4-bestanden waar audio en video interleaved zijn.</span><span class="sxs-lookup"><span data-stu-id="54fc0-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="54fc0-119">U kunt een van deze MP4-bestanden (bijvoorbeeld Hallo hoogste bitrate versie) gebruiken als een bestand progressief downloaden.</span><span class="sxs-lookup"><span data-stu-id="54fc0-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="54fc0-120"><a id="encoding_with_dotnet"></a>Codering met mediaservices .NET SDK</span><span class="sxs-lookup"><span data-stu-id="54fc0-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="54fc0-121">Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="54fc0-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="54fc0-122">Maak een codeertaak.</span><span class="sxs-lookup"><span data-stu-id="54fc0-122">Create an encoding job.</span></span>
- <span data-ttu-id="54fc0-123">Een verwijzing toohello Media Encoder Standard encoder ophalen.</span><span class="sxs-lookup"><span data-stu-id="54fc0-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="54fc0-124">Een codeertaak taak toohello toevoegen en geef toouse hello **adaptief streamen** vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="54fc0-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="54fc0-125">Maak een uitvoerasset met Hallo gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="54fc0-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="54fc0-126">Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54fc0-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="54fc0-127">Verzenden van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="54fc0-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="54fc0-128">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="54fc0-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="54fc0-129">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="54fc0-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="54fc0-130">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="54fc0-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
            default:
                break;
            }
        }
        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
        }
    }

## <span data-ttu-id="54fc0-131"><a id="output"></a>Uitvoer</span><span class="sxs-lookup"><span data-stu-id="54fc0-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="54fc0-132">Deze sectie ziet u drie voorbeelden van lagen van uitvoer geproduceerd door MES als gevolg van codering met Hallo **adaptief streamen** vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="54fc0-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="54fc0-133">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="54fc0-133">Example 1</span></span>
<span data-ttu-id="54fc0-134">Bron met hoogte '1080' en '29.970' framesnelheid produceert 6 video lagen:</span><span class="sxs-lookup"><span data-stu-id="54fc0-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="54fc0-135">Laag</span><span class="sxs-lookup"><span data-stu-id="54fc0-135">Layer</span></span>|<span data-ttu-id="54fc0-136">Hoogte</span><span class="sxs-lookup"><span data-stu-id="54fc0-136">Height</span></span>|<span data-ttu-id="54fc0-137">Breedte</span><span class="sxs-lookup"><span data-stu-id="54fc0-137">Width</span></span>|<span data-ttu-id="54fc0-138">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="54fc0-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="54fc0-139">1</span><span class="sxs-lookup"><span data-stu-id="54fc0-139">1</span></span>|<span data-ttu-id="54fc0-140">1080</span><span class="sxs-lookup"><span data-stu-id="54fc0-140">1080</span></span>|<span data-ttu-id="54fc0-141">1920</span><span class="sxs-lookup"><span data-stu-id="54fc0-141">1920</span></span>|<span data-ttu-id="54fc0-142">6780</span><span class="sxs-lookup"><span data-stu-id="54fc0-142">6780</span></span>|
|<span data-ttu-id="54fc0-143">2</span><span class="sxs-lookup"><span data-stu-id="54fc0-143">2</span></span>|<span data-ttu-id="54fc0-144">720</span><span class="sxs-lookup"><span data-stu-id="54fc0-144">720</span></span>|<span data-ttu-id="54fc0-145">1280</span><span class="sxs-lookup"><span data-stu-id="54fc0-145">1280</span></span>|<span data-ttu-id="54fc0-146">3520</span><span class="sxs-lookup"><span data-stu-id="54fc0-146">3520</span></span>|
|<span data-ttu-id="54fc0-147">3</span><span class="sxs-lookup"><span data-stu-id="54fc0-147">3</span></span>|<span data-ttu-id="54fc0-148">540</span><span class="sxs-lookup"><span data-stu-id="54fc0-148">540</span></span>|<span data-ttu-id="54fc0-149">960</span><span class="sxs-lookup"><span data-stu-id="54fc0-149">960</span></span>|<span data-ttu-id="54fc0-150">2210</span><span class="sxs-lookup"><span data-stu-id="54fc0-150">2210</span></span>|
|<span data-ttu-id="54fc0-151">4</span><span class="sxs-lookup"><span data-stu-id="54fc0-151">4</span></span>|<span data-ttu-id="54fc0-152">360</span><span class="sxs-lookup"><span data-stu-id="54fc0-152">360</span></span>|<span data-ttu-id="54fc0-153">640</span><span class="sxs-lookup"><span data-stu-id="54fc0-153">640</span></span>|<span data-ttu-id="54fc0-154">1150</span><span class="sxs-lookup"><span data-stu-id="54fc0-154">1150</span></span>|
|<span data-ttu-id="54fc0-155">5</span><span class="sxs-lookup"><span data-stu-id="54fc0-155">5</span></span>|<span data-ttu-id="54fc0-156">270</span><span class="sxs-lookup"><span data-stu-id="54fc0-156">270</span></span>|<span data-ttu-id="54fc0-157">480</span><span class="sxs-lookup"><span data-stu-id="54fc0-157">480</span></span>|<span data-ttu-id="54fc0-158">720</span><span class="sxs-lookup"><span data-stu-id="54fc0-158">720</span></span>|
|<span data-ttu-id="54fc0-159">6</span><span class="sxs-lookup"><span data-stu-id="54fc0-159">6</span></span>|<span data-ttu-id="54fc0-160">180</span><span class="sxs-lookup"><span data-stu-id="54fc0-160">180</span></span>|<span data-ttu-id="54fc0-161">320</span><span class="sxs-lookup"><span data-stu-id="54fc0-161">320</span></span>|<span data-ttu-id="54fc0-162">380</span><span class="sxs-lookup"><span data-stu-id="54fc0-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="54fc0-163">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="54fc0-163">Example 2</span></span>
<span data-ttu-id="54fc0-164">Bron met hoogte '720' en '23.970' framesnelheid produceert 5 video lagen:</span><span class="sxs-lookup"><span data-stu-id="54fc0-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="54fc0-165">Laag</span><span class="sxs-lookup"><span data-stu-id="54fc0-165">Layer</span></span>|<span data-ttu-id="54fc0-166">Hoogte</span><span class="sxs-lookup"><span data-stu-id="54fc0-166">Height</span></span>|<span data-ttu-id="54fc0-167">Breedte</span><span class="sxs-lookup"><span data-stu-id="54fc0-167">Width</span></span>|<span data-ttu-id="54fc0-168">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="54fc0-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="54fc0-169">1</span><span class="sxs-lookup"><span data-stu-id="54fc0-169">1</span></span>|<span data-ttu-id="54fc0-170">720</span><span class="sxs-lookup"><span data-stu-id="54fc0-170">720</span></span>|<span data-ttu-id="54fc0-171">1280</span><span class="sxs-lookup"><span data-stu-id="54fc0-171">1280</span></span>|<span data-ttu-id="54fc0-172">2940</span><span class="sxs-lookup"><span data-stu-id="54fc0-172">2940</span></span>|
|<span data-ttu-id="54fc0-173">2</span><span class="sxs-lookup"><span data-stu-id="54fc0-173">2</span></span>|<span data-ttu-id="54fc0-174">540</span><span class="sxs-lookup"><span data-stu-id="54fc0-174">540</span></span>|<span data-ttu-id="54fc0-175">960</span><span class="sxs-lookup"><span data-stu-id="54fc0-175">960</span></span>|<span data-ttu-id="54fc0-176">1850</span><span class="sxs-lookup"><span data-stu-id="54fc0-176">1850</span></span>|
|<span data-ttu-id="54fc0-177">3</span><span class="sxs-lookup"><span data-stu-id="54fc0-177">3</span></span>|<span data-ttu-id="54fc0-178">360</span><span class="sxs-lookup"><span data-stu-id="54fc0-178">360</span></span>|<span data-ttu-id="54fc0-179">640</span><span class="sxs-lookup"><span data-stu-id="54fc0-179">640</span></span>|<span data-ttu-id="54fc0-180">960</span><span class="sxs-lookup"><span data-stu-id="54fc0-180">960</span></span>|
|<span data-ttu-id="54fc0-181">4</span><span class="sxs-lookup"><span data-stu-id="54fc0-181">4</span></span>|<span data-ttu-id="54fc0-182">270</span><span class="sxs-lookup"><span data-stu-id="54fc0-182">270</span></span>|<span data-ttu-id="54fc0-183">480</span><span class="sxs-lookup"><span data-stu-id="54fc0-183">480</span></span>|<span data-ttu-id="54fc0-184">600</span><span class="sxs-lookup"><span data-stu-id="54fc0-184">600</span></span>|
|<span data-ttu-id="54fc0-185">5</span><span class="sxs-lookup"><span data-stu-id="54fc0-185">5</span></span>|<span data-ttu-id="54fc0-186">180</span><span class="sxs-lookup"><span data-stu-id="54fc0-186">180</span></span>|<span data-ttu-id="54fc0-187">320</span><span class="sxs-lookup"><span data-stu-id="54fc0-187">320</span></span>|<span data-ttu-id="54fc0-188">320</span><span class="sxs-lookup"><span data-stu-id="54fc0-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="54fc0-189">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="54fc0-189">Example 3</span></span>
<span data-ttu-id="54fc0-190">Bron met hoogte '360' en '29.970' framesnelheid produceert 3 video lagen:</span><span class="sxs-lookup"><span data-stu-id="54fc0-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="54fc0-191">Laag</span><span class="sxs-lookup"><span data-stu-id="54fc0-191">Layer</span></span>|<span data-ttu-id="54fc0-192">Hoogte</span><span class="sxs-lookup"><span data-stu-id="54fc0-192">Height</span></span>|<span data-ttu-id="54fc0-193">Breedte</span><span class="sxs-lookup"><span data-stu-id="54fc0-193">Width</span></span>|<span data-ttu-id="54fc0-194">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="54fc0-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="54fc0-195">1</span><span class="sxs-lookup"><span data-stu-id="54fc0-195">1</span></span>|<span data-ttu-id="54fc0-196">360</span><span class="sxs-lookup"><span data-stu-id="54fc0-196">360</span></span>|<span data-ttu-id="54fc0-197">640</span><span class="sxs-lookup"><span data-stu-id="54fc0-197">640</span></span>|<span data-ttu-id="54fc0-198">700</span><span class="sxs-lookup"><span data-stu-id="54fc0-198">700</span></span>|
|<span data-ttu-id="54fc0-199">2</span><span class="sxs-lookup"><span data-stu-id="54fc0-199">2</span></span>|<span data-ttu-id="54fc0-200">270</span><span class="sxs-lookup"><span data-stu-id="54fc0-200">270</span></span>|<span data-ttu-id="54fc0-201">480</span><span class="sxs-lookup"><span data-stu-id="54fc0-201">480</span></span>|<span data-ttu-id="54fc0-202">440</span><span class="sxs-lookup"><span data-stu-id="54fc0-202">440</span></span>|
|<span data-ttu-id="54fc0-203">3</span><span class="sxs-lookup"><span data-stu-id="54fc0-203">3</span></span>|<span data-ttu-id="54fc0-204">180</span><span class="sxs-lookup"><span data-stu-id="54fc0-204">180</span></span>|<span data-ttu-id="54fc0-205">320</span><span class="sxs-lookup"><span data-stu-id="54fc0-205">320</span></span>|<span data-ttu-id="54fc0-206">230</span><span class="sxs-lookup"><span data-stu-id="54fc0-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="54fc0-207">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="54fc0-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="54fc0-208">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="54fc0-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="54fc0-209">Zie ook</span><span class="sxs-lookup"><span data-stu-id="54fc0-209">See Also</span></span>
[<span data-ttu-id="54fc0-210">Media Services-codering overzicht</span><span class="sxs-lookup"><span data-stu-id="54fc0-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

