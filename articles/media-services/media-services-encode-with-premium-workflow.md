---
title: Geavanceerde codering met Media Encoder Premium Workflow | Microsoft Docs
description: Informatie over het coderen met Media Encoder Premium Workflow. Codevoorbeelden zijn geschreven in C# en gebruiken van de Media Services SDK voor .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="ac1b5-104">Geavanceerde codering met Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="ac1b5-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="ac1b5-105">Media Encoder Premium media werkstroomverwerking beschreven in dit onderwerp is niet beschikbaar in China.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="ac1b5-106">Premium-encoder vragen, e-mepd op Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="ac1b5-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ac1b5-107">Overview</span></span>
<span data-ttu-id="ac1b5-108">Microsoft Azure Media Services introduceert de **Media Encoder Premium werkstroom** Mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="ac1b5-109">Deze processor biedt geavanceerde mogelijkheden voor uw werkstromen premium-op-verzoek-codering.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="ac1b5-110">De volgende onderwerpen worden gegevens over **Media Encoder Premium werkstroom**:</span><span class="sxs-lookup"><span data-stu-id="ac1b5-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="ac1b5-111">[Ondersteund door de werkstroom met Media Encoder Premium indelingen](media-services-premium-workflow-encoder-formats.md) : het bestand Discusses indelingen en codecs ondersteund door **Media Encoder Premium werkstroom**.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="ac1b5-112">[Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma's](media-services-encode-asset.md) vergelijkt de codering mogelijkheden van **Media Encoder Premium werkstroom** en **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="ac1b5-113">Dit onderwerp wordt beschreven hoe u coderen met **Media Encoder Premium werkstroom** met .NET.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="ac1b5-114">Codering van taken voor de **Media Encoder Premium werkstroom** vereisen een afzonderlijke configuratie-bestand, een werkstroom wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="ac1b5-115">Deze bestanden hebben de extensie .workflow en worden gemaakt met de [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="ac1b5-116">U kunt de standaard ook ophalen Werkstroombestanden [hier](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="ac1b5-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="ac1b5-117">De map bevat ook de beschrijving van deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="ac1b5-118">De Werkstroombestanden moeten worden geüpload naar uw Media Services-account als een actief en dit activum moet worden doorgegeven aan de codering taak.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ac1b5-119">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ac1b5-120">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ac1b5-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="ac1b5-121">Voorbeeld van de codering</span><span class="sxs-lookup"><span data-stu-id="ac1b5-121">Encoding example</span></span>

<span data-ttu-id="ac1b5-122">Het volgende voorbeeld laat zien hoe coderen met **Media Encoder Premium werkstroom**.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="ac1b5-123">De volgende stappen worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ac1b5-123">The following steps are performed:</span></span>

1. <span data-ttu-id="ac1b5-124">Maak een asset en upload het werkstroombestand van een.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="ac1b5-125">Maak een asset en upload een bronbestand voor media.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="ac1b5-126">De media-processor 'Media Encoder Premium Workflow' worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="ac1b5-127">Een taak en een taak maken.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-127">Create a job and a task.</span></span>

    <span data-ttu-id="ac1b5-128">In de meeste gevallen de configuratietekenreeks voor de taak is leeg (zoals in het volgende voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="ac1b5-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="ac1b5-129">Er zijn een aantal geavanceerde scenario's (waarvoor u dynamisch instellen van de eigenschappen van de runtime) in dat geval zou u een XML-tekenreeks voor de codering taak opgeven.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="ac1b5-130">Voorbeelden van dergelijke scenario's zijn: een overlay, parallelle en sequentiële media wilt, subtitling maken.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="ac1b5-131">Twee invoer elementen toevoegen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="ac1b5-132">1e: de werkstroom asset.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="ac1b5-133">2e: de video asset.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ac1b5-134">De asset werkstroom moet worden toegevoegd aan de taak voordat de asset media.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="ac1b5-135">De configuratietekenreeks voor deze taak mag niet leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="ac1b5-136">De coderingstaak verzenden.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-136">Submit the encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
                    }

                    return job.OutputMediaAssets[0];
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

<span data-ttu-id="ac1b5-137">Premium-encoder vragen, e-mepd op Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ac1b5-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ac1b5-138">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ac1b5-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac1b5-139">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ac1b5-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
