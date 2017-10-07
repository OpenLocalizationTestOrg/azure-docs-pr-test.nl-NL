---
title: Media-bestanden met Azure Media Indexer 2 Preview aaaIndexing | Microsoft Docs
description: Azure Media Indexer kunt u toomake inhoud van uw doorzoekbare mediabestanden en toogenerate de tekst van een volledige-tekstindex voor ondertiteling en trefwoorden gesloten. In dit onderwerp toont hoe toouse Media Indexer 2 bekijken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indexeren van Media-bestanden met Azure Media Indexer 2 Preview
## <a name="overview"></a>Overzicht
Hallo **Azure Media Indexer 2 Preview** Mediaprocessor (MP) kunt u toomake media-bestanden en inhoud kan worden doorzocht, evenals gesloten closed captioning houdt genereren. Vorige versie van vergeleken toohello [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 Preview** voert sneller te indexeren en biedt taalondersteuning voor uitgebreidere. Ondersteunde talen zijn Engels, Spaans, Frans, Duits, Italiaans, Chinees (Mandarijn, vereenvoudigd), Portugees, Arabisch en Japans.

Hallo **Azure Media Indexer 2 Preview** MP is momenteel in Preview.

Dit onderwerp wordt beschreven hoe toocreate indexeren taken met **Azure Media Indexer 2 Preview**.

> [!NOTE]
> Hallo overwegingen volgende van toepassing:
> 
> Indexer 2 wordt niet ondersteund in Azure voor China en Azure Government.
> 
> Wanneer inhoud indexeren, moet u ervoor dat toouse mediabestanden die duidelijk speech (zonder achtergrondmuziek, ruis, effecten of microfoon hiss) hebben. Enkele voorbeelden van de betreffende inhoud zijn: vastgelegd vergaderingen, lezingen en presentaties. Hallo volgende inhoud mogelijk niet meer geschikt is voor het indexeren: films, televisieprogramma alles met gemengde Beeld en geluid effecten slecht opgenomen inhoud met achtergrondruis (hiss).
> 
> 

Dit onderwerp bevat informatie over **Azure Media Indexer 2 Preview** en ziet u hoe toouse met Media Services SDK voor .NET

## <a name="input-and-output-files"></a>Invoer- en bestanden
### <a name="input-files"></a>Invoerbestanden
Audio- of -bestanden

### <a name="output-files"></a>Uitvoerbestanden
Een indexing-taak kan ondertitelingsbestanden bestanden in de volgende indelingen Hallo genereren:  

* **SAMI**
* **TTML**
* **WebVTT**

Gesloten bijschrift (CC)-bestanden in de volgende indelingen kunnen worden gebruikt toomake audio en video bestanden toegankelijk toopeople met handicap horen.

## <a name="task-configuration-preset"></a>Taken configureren (standaardoptie)
Wanneer een taak maken van een indexering met **Azure Media Indexer 2 Preview**, moet u een configuratie-definitie opgeven.

Hallo stelt volgende JSON beschikbare parameters.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Ondersteunde talen
Azure Media Indexer 2 Preview ondersteunt spraak-naar-tekst voor Hallo talen te volgen (bij het opgeven van Hallo taalnaam in Hallo taakconfiguratie met 4 tekens code Gebruik haakjes zoals hieronder wordt weergegeven):

* Engels [EnUs]
* Spaans [EsEs]
* Chinees (Mandarijn, vereenvoudigd) [ZhCn]
* Frans [FrFr]
* Duits [DeDe]
* Italiaans [ItIt]
* Portugees [PtBr]
* Arabisch (Egyptisch) [ArEg]
* Japans [JaJp]
* Russisch [RuRu]
* Brits Engels [EnGb]
* Spaans (Mexico) [EsMx] 

## <a name="supported-file-types"></a>Ondersteunde bestandstypen

Zie voor informatie over ondersteunde bestandstypen Hallo [ondersteunde codecs/indelingen](media-services-media-encoder-standard-formats.md#input-containerfile-formats) sectie.

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende programma toont hoe:

1. Maak een asset en upload een mediabestand naar Hallo asset.
2. Een taak maken met een taak die op basis van een configuratiebestand met de volgende json-definitie Hallo voor indexering.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Hallo uitvoerbestanden downloaden. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Voorbeeld

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[Azure Media Analytics-demo 's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

