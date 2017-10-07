---
title: aaaUse Azure Media Video Thumbnails tooCreate samenvatting van een Video | Microsoft Docs
description: Samenvatting van de video kan helpen u bij het maken van samenvattingen van lange video's door interessante codefragmenten automatisch selecteren van bronvideo Hallo. Dit is handig als u wilt dat een snel overzicht van welke tooexpect in een lange video tooprovide.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="b654a-104">Gebruik Azure Media Video Thumbnails tooCreate samenvatting van een Video</span><span class="sxs-lookup"><span data-stu-id="b654a-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="b654a-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b654a-105">Overview</span></span>
<span data-ttu-id="b654a-106">Hallo **Azure Media Video miniaturen** Mediaprocessor (MP) kunt u een samenvatting van een video die handig toocustomers die een overzicht van een lange video toopreview toocreate.</span><span class="sxs-lookup"><span data-stu-id="b654a-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="b654a-107">Klanten kunnen bijvoorbeeld toosee een korte 'Samenvatting video' wanneer ze Beweeg de muisaanwijzer over een miniatuur.</span><span class="sxs-lookup"><span data-stu-id="b654a-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="b654a-108">Door het Hallo-parameters van aanpassingen **Azure Media Video Thumbnails** via een voorinstelling configuratie kunt u krachtige schermopname detectie Hallo MP en samenvoeging technologie tooalgorithmically een beschrijvende subclip genereren.</span><span class="sxs-lookup"><span data-stu-id="b654a-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="b654a-109">Hallo **Azure Media Video miniatuur** MP is momenteel in Preview.</span><span class="sxs-lookup"><span data-stu-id="b654a-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="b654a-110">Dit onderwerp bevat informatie over **Azure Media Video miniatuur** en ziet u hoe toouse met Media Services SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="b654a-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="b654a-111">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="b654a-111">Limitations</span></span>

<span data-ttu-id="b654a-112">In sommige gevallen, als uw video niet uit verschillende scènes bestaat worden Hallo uitvoer pas een enkele opname.</span><span class="sxs-lookup"><span data-stu-id="b654a-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="b654a-113">Voorbeeld van video-overzicht</span><span class="sxs-lookup"><span data-stu-id="b654a-113">Video summary example</span></span>
<span data-ttu-id="b654a-114">Hier volgen enkele voorbeelden van welke hello Azure Media Video Thumbnails Mediaprocessor kunt doen:</span><span class="sxs-lookup"><span data-stu-id="b654a-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="b654a-115">Oorspronkelijke video</span><span class="sxs-lookup"><span data-stu-id="b654a-115">Original video</span></span>
[<span data-ttu-id="b654a-116">Oorspronkelijke video</span><span class="sxs-lookup"><span data-stu-id="b654a-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="b654a-117">Video miniaturen resultaat</span><span class="sxs-lookup"><span data-stu-id="b654a-117">Video thumbnail result</span></span>
[<span data-ttu-id="b654a-118">Video miniaturen resultaat</span><span class="sxs-lookup"><span data-stu-id="b654a-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="b654a-119">Taken configureren (standaardoptie)</span><span class="sxs-lookup"><span data-stu-id="b654a-119">Task configuration (preset)</span></span>
<span data-ttu-id="b654a-120">Bij het maken van een video miniaturen taak met **Azure Media Video miniaturen**, moet u een configuratie-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="b654a-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="b654a-121">Hallo hierboven miniaturen voorbeeld is gemaakt met de volgende JSON-basisconfiguratie Hallo:</span><span class="sxs-lookup"><span data-stu-id="b654a-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="b654a-122">Op dit moment kunt u Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="b654a-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="b654a-123">Param</span><span class="sxs-lookup"><span data-stu-id="b654a-123">Param</span></span> | <span data-ttu-id="b654a-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b654a-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b654a-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="b654a-125">outputAudio</span></span> |<span data-ttu-id="b654a-126">Hiermee geeft u op of de resulterende video Hallo audio bevat.</span><span class="sxs-lookup"><span data-stu-id="b654a-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="b654a-127">Toegestane waarden zijn: True of False.</span><span class="sxs-lookup"><span data-stu-id="b654a-127">Allowed values are: True or False.</span></span> <span data-ttu-id="b654a-128">De standaardwaarde is True.</span><span class="sxs-lookup"><span data-stu-id="b654a-128">Default is True.</span></span> |
| <span data-ttu-id="b654a-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="b654a-129">fadeInFadeOut</span></span> |<span data-ttu-id="b654a-130">Hiermee geeft u op of vervagen overgangen tussen Hallo afzonderlijke beweging miniaturen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b654a-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="b654a-131">Toegestane waarden zijn: True of False.</span><span class="sxs-lookup"><span data-stu-id="b654a-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="b654a-132">De standaardwaarde is True.</span><span class="sxs-lookup"><span data-stu-id="b654a-132">Default is True.</span></span> |
| <span data-ttu-id="b654a-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="b654a-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="b654a-134">Geheel getal dat hoe lang Hallo hele resulterende video aangeeft bedraagt.</span><span class="sxs-lookup"><span data-stu-id="b654a-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="b654a-135">Standaard is afhankelijk van duur van de oorspronkelijke video.</span><span class="sxs-lookup"><span data-stu-id="b654a-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="b654a-136">Hallo volgende tabel beschrijft de standaardduur Hallo wanneer **maxMotionThumbnailInSecs** wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b654a-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b654a-137">Duur van de video</span><span class="sxs-lookup"><span data-stu-id="b654a-137">Video duration</span></span> |<span data-ttu-id="b654a-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="b654a-138">d < 3 min</span></span> |<span data-ttu-id="b654a-139">3 min < d < 15 min.</span><span class="sxs-lookup"><span data-stu-id="b654a-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="b654a-140">Duur van de miniatuur</span><span class="sxs-lookup"><span data-stu-id="b654a-140">Thumbnail duration</span></span> |<span data-ttu-id="b654a-141">15 per seconde (2-3-scènes)</span><span class="sxs-lookup"><span data-stu-id="b654a-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="b654a-142">30 seconden (3-5-scènes)</span><span class="sxs-lookup"><span data-stu-id="b654a-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="b654a-143">Hallo stelt volgende JSON beschikbare parameters.</span><span class="sxs-lookup"><span data-stu-id="b654a-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="b654a-144">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="b654a-144">.NET sample code</span></span>

<span data-ttu-id="b654a-145">Hallo volgende programma toont hoe:</span><span class="sxs-lookup"><span data-stu-id="b654a-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="b654a-146">Maak een asset en upload een mediabestand naar Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="b654a-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="b654a-147">Maakt een taak met een video miniaturen taak op basis van een configuratiebestand met Hallo json-definitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="b654a-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="b654a-148">Hallo uitvoerbestanden downloadt.</span><span class="sxs-lookup"><span data-stu-id="b654a-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b654a-149">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="b654a-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b654a-150">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b654a-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="b654a-151">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b654a-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="b654a-152">Miniaturen video-uitvoer</span><span class="sxs-lookup"><span data-stu-id="b654a-152">Video thumbnail output</span></span>
[<span data-ttu-id="b654a-153">Miniaturen video-uitvoer</span><span class="sxs-lookup"><span data-stu-id="b654a-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="b654a-154">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="b654a-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b654a-155">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="b654a-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b654a-156">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="b654a-156">Related links</span></span>
[<span data-ttu-id="b654a-157">Azure Media Services Analytics-overzicht</span><span class="sxs-lookup"><span data-stu-id="b654a-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="b654a-158">Azure Media Analytics-demo 's</span><span class="sxs-lookup"><span data-stu-id="b654a-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

