---
title: aaaDetect gezichts- en Emotion met Azure Media Analytics | Microsoft Docs
description: In dit onderwerp wordt beschreven hoe toodetect bespreekt en emoties met Azure Media Analytics.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Face en Emotion met Azure Media Analytics detecteren
## <a name="overview"></a>Overzicht
Hallo **Azure Media Face detectie** Mediaprocessor (MP) kunt u toocount, de bewegingen bijhouden, en zelfs meter doelgroep deelname en reactie via bedacht. Deze service bevat twee functies: 

* **Face-detectie**
  
    Face-detectie zoekt en houdt menselijke vlakken binnen een video. Meerdere vlakken kunnen worden gedetecteerd en vervolgens worden bijgehouden als ze onderweg, met Hallo-metagegevens en de locatie geretourneerd in een JSON-bestand. Tijdens de bijhouden, wordt geprobeerd toogive een consistente ID toohello dezelfde geconfronteerd terwijl Hallo persoon is navigeren op het scherm, zelfs als ze zijn ondervindt hinder van obstakels of kort Hallo frame laat.
  
  > [!NOTE]
  > Deze service voert geen gezichtsherkenning. Een persoon die Hallo frame verlaat of ondervindt voor wordt hinder van obstakels te lang krijgt een nieuwe ID wanneer ze terugkeren.
  > 
  > 
* **Emotiedetectie**
  
    Emotiedetectie is een optioneel onderdeel van Hallo Face Detection Media Processor op dat analyse op meerdere emotionele kenmerken van Hallo vlakken gedetecteerd retourneert, met inbegrip van gelukkig, sadness bang, volgt uitzien en meer. 

Hallo **Azure Media Face detectie** MP is momenteel in Preview.

Dit onderwerp bevat informatie over **Azure Media Face detectie** en ziet u hoe toouse met Media Services SDK voor .NET.

## <a name="face-detector-input-files"></a>Detectie-invoerbestanden geconfronteerd
Videobestanden. Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.

## <a name="face-detector-output-files"></a>Detectie uitvoerbestanden geconfronteerd
Hallo face detection en bijhouden API biedt hoge precisie face locatie detectie en bijhouden die up too64 menselijke vlakken in een video kan detecteren. Voorzijde vlakken bieden de beste resultaten Hallo tijdens vlakken kant- en kleine vlakken (minder dan of gelijk zijn aan too24x24 pixels) mogelijk niet nauwkeurig.

Hallo gedetecteerde en bijgehouden vlakken worden geretourneerd met coördinaten (links, top, breedte en hoogte) Hallo-locatie van vlakken in Hallo afbeelding in pixels die aangeeft, evenals een face ID getal dat aangeeft dat afzonderlijke bijhouden Hallo. Face-id-nummers zijn foutgevoelige tooreset omstandigheden wanneer Hallo voorzijde face verloren is gegaan of elkaar overlappen in Hallo-frame, waardoor bepaalde personen ophalen van meerdere id's toegewezen.

## <a id="output_elements"></a>Elementen van Hallo uitvoer JSON-bestand

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Face-detectie maakt gebruik van technieken van fragmentatie (waarbij Hallo metagegevens kan worden opgesplitst in segmenten op basis van tijd en u kunt downloaden wat u nodig hebt) en segmentering (waarbij Hallo gebeurtenissen worden opgedeeld geval ze te groot krijgen). Enkele eenvoudige berekeningen kunt u Hallo gegevens transformeren. Bijvoorbeeld, als een gebeurtenis wordt gestart om 6300 (maten) met een tijdschaal van 2997 (ticks per seconde) en framesnelheid van vervolgens 29,97 (frames per seconde):

* Start/tijdschaal = 2.1 seconden
* Seconden x Framerate 63 frames =

## <a name="face-detection-input-and-output-example"></a>Geconfronteerd detectie invoer en uitvoer voorbeeld
### <a name="input-video"></a>Invoervideo
[Invoervideo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Taken configureren (standaardoptie)
Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven. Hallo na configuratie definitie is slechts voor face detection.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Beschrijvingen van kenmerken
| Naam van kenmerk | Beschrijving |
| --- | --- |
| Modus |Snel - verwerking snel van de snelheid, maar minder nauwkeurig (standaard).|

### <a name="json-output"></a>JSON-uitvoer
Voorbeeld van JSON-uitvoer na Hallo is afgebroken.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Emotiedetectie invoer en uitvoer voorbeeld
### <a name="input-video"></a>Invoervideo
[Invoervideo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Taken configureren (standaardoptie)
Bij het maken van een taak met **Azure Media Face detectie**, moet u een configuratie-definitie opgeven. Hallo na configuratie voorinstelling geeft toocreate die JSON op basis van Hallo emotiedetectie.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Beschrijvingen van kenmerken
| Naam van kenmerk | Beschrijving |
| --- | --- |
| Modus |Vlakken: Komen alleen voor detectie.<br/>PerFaceEmotion: Retourneren emotion onafhankelijk voor elke face-detectie.<br/>AggregateEmotion: Return gemiddelde emotion waarden voor alle vlakken in frame. |
| AggregateEmotionWindowMs |Gebruik deze optie als AggregateEmotion modus geselecteerd. Hiermee geeft u Hallo lengte van video gebruikte tooproduce elk cumulatieve resultaat in milliseconden. |
| AggregateEmotionIntervalMs |Gebruik deze optie als AggregateEmotion modus geselecteerd. Hiermee geeft u aan met welke frequentie tooproduce statistische functie resulteert. |

#### <a name="aggregate-defaults"></a>Cumulatieve standaardinstellingen
Hieronder worden aanbevolen waarden voor statistische vensterfunctie hello en intervalinstellingen. AggregateEmotionWindowMs mag niet langer zijn dan AggregateEmotionIntervalMs.

|| Standaardinstellingen (s) | Min(s) | Max(s) |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0.5 |2 |0.25|
| AggregateEmotionIntervalMs |0.5 |1 |0.25|

### <a name="json-output"></a>JSON-uitvoer
JSON-uitvoer voor cumulatieve emotion (afgekapt):

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Beperkingen
* Hallo ondersteund video-invoerindelingen zijn MP4 MOV en WMV.
* Hallo waarneembaar face grootte bereik is 24 x 24 too2048x2048 pixels. Hallo vlakken buiten dit bereik wordt niet gedetecteerd.
* Maximum aantal vlakken geretourneerd Hallo is voor elke video 64.
* Sommige vlakken mogelijk niet gedetecteerd vanwege tootechnical uitdagingen; bijvoorbeeld zeer grote face hoeken (head-ven) en grote Occlusie. Voorzijde en in de buurt binnen handbereik hebt Hallo krijgt de beste resultaten.

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende programma toont hoe:

1. Maak een asset en upload een mediabestand naar Hallo asset.
2. Een taak maken met een face detection-taak op basis van een configuratiebestand met Hallo json-definitie te volgen. 
   
        {
            "version": "1.0"
        }
3. Hallo uitvoer JSON-bestanden downloaden. 

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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Azure Media Analytics-demo 's](http://amslabs.azurewebsites.net/demos/Analytics.html)

