---
title: aaaAdvanced codering met Media Encoder Premium Workflow | Microsoft Docs
description: Meer informatie over hoe tooencode met Media Encoder Premium Workflow. Codevoorbeelden zijn geschreven in C# en gebruiken van Hallo Media Services SDK voor .NET.
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
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="70022-104">Geavanceerde codering met Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="70022-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="70022-105">Media Encoder Premium media werkstroomverwerking beschreven in dit onderwerp is niet beschikbaar in China.</span><span class="sxs-lookup"><span data-stu-id="70022-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="70022-106">Premium-encoder vragen, e-mepd op Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="70022-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="70022-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="70022-107">Overview</span></span>
<span data-ttu-id="70022-108">Microsoft Azure Media Services introduceert Hallo **Media Encoder Premium werkstroom** Mediaprocessor.</span><span class="sxs-lookup"><span data-stu-id="70022-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="70022-109">Deze processor biedt geavanceerde mogelijkheden voor uw werkstromen premium-op-verzoek-codering.</span><span class="sxs-lookup"><span data-stu-id="70022-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="70022-110">Hallo volgende onderwerpen worden gegevens over te**Media Encoder Premium werkstroom**:</span><span class="sxs-lookup"><span data-stu-id="70022-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="70022-111">[Ondersteunde indelingen door Hallo Media Encoder Premium werkstroom](media-services-premium-workflow-encoder-formats.md) – bespreekt Hallo bestandsindelingen en codecs ondersteund door **Media Encoder Premium werkstroom**.</span><span class="sxs-lookup"><span data-stu-id="70022-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="70022-112">[Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma's](media-services-encode-asset.md) vergelijkt Hallo codering mogelijkheden van **Media Encoder Premium werkstroom** en **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="70022-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="70022-113">Dit onderwerp wordt beschreven hoe tooencode met **Media Encoder Premium werkstroom** met .NET.</span><span class="sxs-lookup"><span data-stu-id="70022-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="70022-114">Taken voor het Hallo-codering **Media Encoder Premium werkstroom** vereisen een afzonderlijke configuratie-bestand, een werkstroom wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="70022-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="70022-115">Deze bestanden hebben de extensie .workflow en zijn gemaakt met de Hallo [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="70022-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="70022-116">Ook kunt u opvragen Hallo standaard Werkstroombestanden [hier](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="70022-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="70022-117">Hallo-map bevat ook Hallo beschrijving van deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="70022-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="70022-118">Hallo Werkstroombestanden moeten toobe geüpload tooyour Media Services-account als een actief, en deze activa in toohello taak codering moet worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="70022-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="70022-119">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="70022-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="70022-120">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="70022-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="70022-121">Voorbeeld van de codering</span><span class="sxs-lookup"><span data-stu-id="70022-121">Encoding example</span></span>

<span data-ttu-id="70022-122">Hallo volgende voorbeeld laat zien hoe tooencode met **Media Encoder Premium werkstroom**.</span><span class="sxs-lookup"><span data-stu-id="70022-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="70022-123">Hallo stappen worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="70022-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="70022-124">Maak een asset en upload het werkstroombestand van een.</span><span class="sxs-lookup"><span data-stu-id="70022-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="70022-125">Maak een asset en upload een bronbestand voor media.</span><span class="sxs-lookup"><span data-stu-id="70022-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="70022-126">Hallo 'Media Encoder Premium Workflow' Mediaprocessor ophalen.</span><span class="sxs-lookup"><span data-stu-id="70022-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="70022-127">Een taak en een taak maken.</span><span class="sxs-lookup"><span data-stu-id="70022-127">Create a job and a task.</span></span>

    <span data-ttu-id="70022-128">In de meeste gevallen Hallo configuratietekenreeks voor Hallo-taak is leeg (zoals in het volgende voorbeeld Hallo).</span><span class="sxs-lookup"><span data-stu-id="70022-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="70022-129">Er zijn een aantal geavanceerde scenario's (waarvoor u tootooset runtime eigenschappen dynamisch) in dat geval zou u een taak toohello codering van XML-tekenreeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="70022-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="70022-130">Voorbeelden van dergelijke scenario's zijn: een overlay, parallelle en sequentiële media wilt, subtitling maken.</span><span class="sxs-lookup"><span data-stu-id="70022-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="70022-131">Twee invoer activa toohello taak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="70022-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="70022-132">1e – Hallo werkstroom asset.</span><span class="sxs-lookup"><span data-stu-id="70022-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="70022-133">2e: Hallo video asset.</span><span class="sxs-lookup"><span data-stu-id="70022-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="70022-134">Hallo werkstroom asset moet worden toegevoegd als toohello taak voordat Hallo media asset.</span><span class="sxs-lookup"><span data-stu-id="70022-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="70022-135">Hallo configuratietekenreeks voor deze taak mag niet leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="70022-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="70022-136">Hallo coderingstaak verzenden.</span><span class="sxs-lookup"><span data-stu-id="70022-136">Submit hello encoding job.</span></span>

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
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
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

<span data-ttu-id="70022-137">Premium-encoder vragen, e-mepd op Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="70022-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="70022-138">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="70022-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="70022-139">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="70022-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
