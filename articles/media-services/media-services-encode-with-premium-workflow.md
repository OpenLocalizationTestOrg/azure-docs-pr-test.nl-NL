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
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Geavanceerde codering met Media Encoder Premium Workflow
> [!NOTE]
> Media Encoder Premium media werkstroomverwerking beschreven in dit onderwerp is niet beschikbaar in China.
>
>

Premium-encoder vragen, e-mepd op Microsoft.com.

## <a name="overview"></a>Overzicht
Microsoft Azure Media Services introduceert Hallo **Media Encoder Premium werkstroom** Mediaprocessor. Deze processor biedt geavanceerde mogelijkheden voor uw werkstromen premium-op-verzoek-codering.

Hallo volgende onderwerpen worden gegevens over te**Media Encoder Premium werkstroom**:

* [Ondersteunde indelingen door Hallo Media Encoder Premium werkstroom](media-services-premium-workflow-encoder-formats.md) – bespreekt Hallo bestandsindelingen en codecs ondersteund door **Media Encoder Premium werkstroom**.
* [Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma's](media-services-encode-asset.md) vergelijkt Hallo codering mogelijkheden van **Media Encoder Premium werkstroom** en **Media Encoder Standard**.

Dit onderwerp wordt beschreven hoe tooencode met **Media Encoder Premium werkstroom** met .NET.

Taken voor het Hallo-codering **Media Encoder Premium werkstroom** vereisen een afzonderlijke configuratie-bestand, een werkstroom wordt genoemd. Deze bestanden hebben de extensie .workflow en zijn gemaakt met de Hallo [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.

Ook kunt u opvragen Hallo standaard Werkstroombestanden [hier](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Hallo-map bevat ook Hallo beschrijving van deze bestanden.

Hallo Werkstroombestanden moeten toobe geüpload tooyour Media Services-account als een actief, en deze activa in toohello taak codering moet worden doorgegeven.

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Voorbeeld van de codering

Hallo volgende voorbeeld laat zien hoe tooencode met **Media Encoder Premium werkstroom**.

Hallo stappen worden uitgevoerd:

1. Maak een asset en upload het werkstroombestand van een.
2. Maak een asset en upload een bronbestand voor media.
3. Hallo 'Media Encoder Premium Workflow' Mediaprocessor ophalen.
4. Een taak en een taak maken.

    In de meeste gevallen Hallo configuratietekenreeks voor Hallo-taak is leeg (zoals in het volgende voorbeeld Hallo). Er zijn een aantal geavanceerde scenario's (waarvoor u tootooset runtime eigenschappen dynamisch) in dat geval zou u een taak toohello codering van XML-tekenreeks opgeven. Voorbeelden van dergelijke scenario's zijn: een overlay, parallelle en sequentiële media wilt, subtitling maken.
5. Twee invoer activa toohello taak toevoegen.

    1. 1e – Hallo werkstroom asset.
    2. 2e: Hallo video asset.

    >[!NOTE]
    >Hallo werkstroom asset moet worden toegevoegd als toohello taak voordat Hallo media asset.
   Hallo configuratietekenreeks voor deze taak mag niet leeg zijn.
   
6. Hallo coderingstaak verzenden.

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

Premium-encoder vragen, e-mepd op Microsoft.com.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
