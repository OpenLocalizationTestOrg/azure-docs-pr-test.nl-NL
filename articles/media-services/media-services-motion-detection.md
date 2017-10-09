---
title: aaaDetect bewegingen met Azure Media Analytics | Microsoft Docs
description: Hallo Azure Media beweging detectie media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Bewegingen met Azure Media Analytics detecteren
## <a name="overview"></a>Overzicht
Hallo **Azure Media beweging detectie** media processor (MP) kunt u tooefficiently secties van belang zijn binnen een video anders lang en probleemloze identificeren. Bewegingsdetectie kan worden gebruikt voor statische camera beeldmateriaal tooidentify secties van Hallo video waar beweging optreedt. Er wordt een JSON-bestand met een metagegevens met tijdstempels en de regio waar Hallo gebeurtenis heeft plaatsgevonden voor begrenzingsvak Hallo gegenereerd.

Gericht op beveiliging video feeds, is deze technologie kunnen toocategorize beweging in de relevante gebeurtenissen en fout-positieven zoals schaduwen en licht wijzigingen. Hiermee kunt u toogenerate beveiligingswaarschuwingen van de camera feeds zonder terwijl tooextract kunnen momenten van belang van zeer lange toezicht video's met oneindige irrelevante gebeurtenissen, spam.

Hallo **Azure Media beweging detectie** MP is momenteel in Preview.

Dit onderwerp bevat informatie over **Azure Media beweging detectie** en ziet u hoe toouse met Media Services SDK voor .NET

## <a name="motion-detector-input-files"></a>Beweging detectie invoerbestanden
Videobestanden. Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.

## <a name="task-configuration-preset"></a>Taken configureren (standaardoptie)
Bij het maken van een taak met **Azure Media beweging detectie**, moet u een configuratie-definitie opgeven. 

### <a name="parameters"></a>Parameters
U kunt Hallo volgende parameters:

| Naam | Opties | Beschrijving | Standaard |
| --- | --- | --- | --- |
| sensitivityLevel |Tekenreeks: 'laag', 'Gemiddeld', 'hoog' |Hiermee stelt Hallo gevoeligheid niveau op welke bewegingen wordt gerapporteerd. Deze fout-positieven tooadjust hoeveelheid aanpassen. |'Gemiddeld' |
| frameSamplingValue |Positief geheel getal |Hiermee stelt u Hallo frequentie op waaronder de algoritme wordt uitgevoerd. elk frame gelijk aan-1, 2 betekent dat elke 2e frame, enzovoort. |1 |
| detectLightChange |Boolean-waarde: 'true', 'onwaar' |Hiermee wordt ingesteld of lichte wijzigingen worden gerapporteerd in Hallo resultaten |'False' |
| mergeTimeThreshold |Tijd voor xs:: Mm: ss<br/>Voorbeeld: 00:00:03 |Hiermee geeft u het tijdvenster Hallo tussen beweging gebeurtenissen waarbij 2 gebeurtenissen wordt gecombineerd en gerapporteerd als 1. |00:00:00 |
| detectionZones |Een matrix van zones voor detectie:<br/>-Zone detectie is een matrix met punten 3 of meer<br/>-Punt is een x en y van 0 too1 coördinaat. |Hierin wordt beschreven Hallo lijst met detectie van veelhoekige zones toobe gebruikt.<br/>Resultaten met Hallo zones worden vermeld als een ID, eerst een wordt 'id' Hello: 0 |Enkele zone die de hele frame Hallo dekt. |

### <a name="json-example"></a>JSON-voorbeeld
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Beweging detectie uitvoerbestanden
Een motion detection-taak retourneren een JSON-bestand in Hallo uitvoerasset waarin Hallo beweging waarschuwingen en hun categorieën, binnen Hallo video worden beschreven. Hallo-bestand bevat informatie over het Hallo-tijd en de duur van gedetecteerd in Hallo video motion.

Hallo beweging detectie API biedt indicatoren zodra er objecten in beweging in een vaste achtergrond video (bijvoorbeeld een toezicht video zijn). Hallo beweging detectie is getraind tooreduce gegeven, zoals licht en wijzigingen van de schaduwkopie. Huidige beperkingen van Hallo algoritmen zijn nacht visie video's, semi-transparante objecten en kleine objecten.

### <a id="output_elements"></a>Elementen van Hallo uitvoer JSON-bestand
> [!NOTE]
> In de meest recente release Hallo Hallo uitvoer JSON-indeling is gewijzigd en een belangrijke wijziging voor sommige klanten kan vertegenwoordigen.
> 
> 

Hallo beschrijft volgende tabel de elementen van Hallo uitvoer JSON-bestand.

| Element | Beschrijving |
| --- | --- |
| Versie |Dit verwijst toohello versie Hallo Video API. Er is een fout opgetreden in de huidige versie Hallo 2. |
| Tijdschaal |'Maatstreepjes' per seconde van Hallo video. |
| Offset |Hallo tijdverschil voor tijdstempels in 'maatstreepjes'. Versie 1.0 van Video-API's, zal dit altijd 0 zijn. In de toekomst scenario's die wordt ondersteund, deze waarde kan worden gewijzigd. |
| framesnelheid |Frames per seconde van Hallo video. |
| Breedte, hoogte |Verwijst toohello breedte en hoogte van Hallo video in pixels. |
| Starten |Hallo start tijdstempel in 'maatstreepjes'. |
| Duur |Hallo-lengte van Hallo-gebeurtenis in 'maatstreepjes'. |
| Interval |elk item in het Hallo-gebeurtenis in 'maatstreepjes' Hello tijdsinterval. |
| Gebeurtenissen |Elke gebeurtenis fragment bevat Hallo beweging binnen deze tijdsduur gedetecteerd. |
| Type |In de huidige versie hello is dit altijd '2' voor algemene beweging. Dit label biedt Video-API's Hallo flexibiliteit toocategorize beweging in toekomstige versies. |
| RegionID |Zoals hierboven vermeld, zal dit altijd 0 in deze versie zijn. Dit label biedt Video API Hallo flexibiliteit toofind beweging in verschillende regio's in toekomstige versies. |
| Regio's |Gebied van de toohello in uw video waarin u het belangrijkst over beweging verwijst. <br/><br/>-Hallo regio gebied 'id' aangeeft: in deze versie er is slechts één ID 0. <br/>-'type' hello vorm van Hallo regio die u voor beweging interesseren vertegenwoordigt. Op dit moment worden 'rechthoek' en 'veelhoek' ondersteund.<br/> Als u 'rechthoek' hebt opgegeven, heeft Hallo regio dimensies in X, Y, Width en Height. Hallo X en Y-coördinaten vertegenwoordigen Hallo bovenste linkerkant Xyserver coördinaten van Hallo gebied in een genormaliseerde schaal van 0,0 too1.0. Hallo breedte en hoogte vertegenwoordigen Hallo grootte van Hallo gebied in een genormaliseerde schaal van 0,0 too1.0. In de huidige versie hello, zijn X, Y, Width en Height altijd vast op 0, 0 en 1, 1. <br/>Als u 'veelhoek' hebt opgegeven, heeft Hallo regio dimensies in punten. <br/> |
| fragmenten |Hallo metagegevens is up chunked in verschillende segmenten fragmenten aangeroepen. Elke fragment bevat een start, duur, Intervalnummer en gebeurtenis(sen). Een fragment met er zijn geen gebeurtenissen betekent dat er geen beweging is aangetroffen tijdens die begintijd en duur. |
| []-Haken |Elke accolade vertegenwoordigt één interval in Hallo-gebeurtenis. Lege haakjes voor dat interval betekent dat er geen beweging is gedetecteerd. |
| Locaties |Deze nieuwe vermelding onder gebeurtenissen bevat Hallo-locatie waar Hallo beweging zich heeft voorgedaan. Dit is meer specifieke dan Hallo detectie zones. |

Hallo Hier volgt een voorbeeld van een JSON-uitvoer

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Beperkingen
* Hallo ondersteund video-invoerindelingen zijn MP4 MOV en WMV.
* Bewegingsdetectie is geoptimaliseerd voor stilstaan achtergrond video's. Hallo-algoritme is gericht op het verminderen van gegeven, zoals licht wijzigingen en schaduwen.
* Sommige beweging mogelijk niet gedetecteerd vanwege tootechnical uitdagingen; bijvoorbeeld 's avonds visie video's, semi-transparante objecten en kleine objecten.

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende programma toont hoe:

1. Maak een asset en upload een mediabestand naar Hallo asset.
2. Een taak maken met een video motion detection-taak op basis van een configuratiebestand met Hallo json-definitie te volgen. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Azure Media Services beweging detectie-blog](https://azure.microsoft.com/blog/motion-detector-update/)

[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[Azure Media Analytics-demo 's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

