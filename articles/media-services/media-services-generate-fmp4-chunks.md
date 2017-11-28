---
title: een Azure Media Services codering taak die wordt gegenereerd fMP4 segmenten aaaCreate | Microsoft Docs
description: Dit onderwerp leest hoe toocreate dat door een codering taak die wordt gegenereerd fMP4 segmenten gedownload. Wanneer deze taak wordt gebruikt met Media Encoder Standard Hallo of codering met Media Encoder Premium werkstroom, bevat de uitvoerasset Hallo fMP4 segmenten in plaats van ISO MP4-bestanden.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 388f3ccb9865b5c4e159af86d5a9ee2f4e3f6120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="c52ba-104">Een codering taak maken die wordt gegenereerd fMP4 segmenten</span><span class="sxs-lookup"><span data-stu-id="c52ba-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="c52ba-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c52ba-105">Overview</span></span>

<span data-ttu-id="c52ba-106">Dit onderwerp wordt beschreven hoe een codering taak die wordt gegenereerd toocreate gefragmenteerd MP4 segmenten in plaats van ISO MP4-bestanden (fMP4).</span><span class="sxs-lookup"><span data-stu-id="c52ba-106">This topic shows how toocreate an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="c52ba-107">toogenerate fMP4 chunks gebruiken Hallo **Media Encoder Standard** of **Media Encoder Premium werkstroom** encoder toocreate een codering van de taak en geef ook op  **AssetFormatOption.AdaptiveStreaming** optie, zoals in dit codefragment:</span><span class="sxs-lookup"><span data-stu-id="c52ba-107">toogenerate fMP4 chunks, use hello **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder toocreate an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="c52ba-108"><a id="encoding_with_dotnet"></a>Codering met mediaservices .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c52ba-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="c52ba-109">Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="c52ba-109">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="c52ba-110">Maak een codeertaak.</span><span class="sxs-lookup"><span data-stu-id="c52ba-110">Create an encoding job.</span></span>
- <span data-ttu-id="c52ba-111">Ophalen van een verwijzing toohello **Media Encoder Standard** encoder.</span><span class="sxs-lookup"><span data-stu-id="c52ba-111">Get a reference toohello **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="c52ba-112">Een codeertaak taak toohello toevoegen en geef toouse hello **adaptief streamen** vooraf ingestelde.</span><span class="sxs-lookup"><span data-stu-id="c52ba-112">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="c52ba-113">Maak een uitvoerasset die fMP4 segmenten en een ISM-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="c52ba-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="c52ba-114">Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c52ba-114">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="c52ba-115">Verzenden van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="c52ba-115">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c52ba-116">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="c52ba-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c52ba-117">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c52ba-117">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c52ba-118">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c52ba-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
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
            // It is also specified toouse AssetFormatOption.AdaptiveStreaming, 
            // which means hello output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="c52ba-119">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c52ba-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c52ba-120">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c52ba-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c52ba-121">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c52ba-121">See Also</span></span>
[<span data-ttu-id="c52ba-122">Media Services-codering overzicht</span><span class="sxs-lookup"><span data-stu-id="c52ba-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

