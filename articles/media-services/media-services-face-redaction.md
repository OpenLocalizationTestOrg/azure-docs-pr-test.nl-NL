---
title: aaaRedact vlakken met Azure Media Analytics | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe tooredact bespreekt met Azure media analytics.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Redigeren vlakken met Azure Media Analytics
## <a name="overview"></a>Overzicht
**Azure Media Redactor** is een [Azure Media Analytics](media-services-analytics-overview.md) Mediaprocessor (MP) die schaalbare face redactie in Hallo cloud biedt. Face redactie kunt u toomodify uw video in volgorde tooblur vlakken van geselecteerde gebruikers. U kunt toouse Hallo face redactie service in openbare veiligheid en nieuws media scenario's. Een paar minuten beeldmateriaal waarin meerdere vlakken handmatig tooredact uur kunnen duren, maar met deze service Hallo face redactie proces een paar eenvoudige stappen is vereist. Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-redactor/) blog.

Dit onderwerp bevat informatie over **Azure Media Redactor** en ziet u hoe toouse met Media Services SDK voor .NET.

Hallo **Azure Media Redactor** MP is momenteel in Preview. Is beschikbaar in alle openbare Azure-regio's, evenals US Government en China datacenters. Dit voorbeeld is momenteel gratis. 

## <a name="face-redaction-modes"></a>Face redactie modi
Analyseert redactie werkt door vlakken opsporen in elke frame van video en bij te houden Hallo face object beide voorwaarts en achterwaarts in de tijd, zodat hello dezelfde persoon kan worden vervaagd vanuit andere hoeken ook. Hallo geautomatiseerde redactie proces is zeer complex en 100% van de gewenste uitvoer geen altijd om deze reden die Media Analytics u over een aantal manieren toomodify Hallo uiteindelijke uitvoer beschikt produceert.

In de toevoeging tooa volledig automatische modus is er een werkstroom twee keer waarmee Hallo selectie/de-selection gevonden vlakken via een lijst met id. Bovendien toomake willekeurige per frame aanpassingen Hallo MP maakt gebruik van een bestand met metagegevens in JSON-indeling. Deze werkstroom is onderverdeeld in **analyseren** en **Redact** modi. U kunt de twee modi Hallo in één iteratie die beide taken in één taak uitvoert; combineren Deze modus wordt aangeroepen **gecombineerde**.

### <a name="combined-mode"></a>Gecombineerde modus
Het resultaat is een geredigeerde mp4 automatisch zonder handmatige invoer.

| Fase | Bestandsnaam | Opmerkingen |
| --- | --- | --- |
| Invoer asset |foo.bar |Video in WMV, MOV of MP4-indeling |
| Invoer config |De configuratie van definitie |{{'version':'1.0 ","opties": {'mode': 'gecombineerd'}} |
| Uitvoerasset |foo_redacted.mp4 |Video met zorgt voor een vervaging toegepast |

#### <a name="input-example"></a>Voorbeeld van invoer:
[Bekijk deze video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Voorbeeld van uitvoer:
[Bekijk deze video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Modus analyseren
Hallo **analyseren** pass van Hallo twee keer werkstroom neemt een video-invoer en resulteert in een JSON-bestand van face locaties en jpg-afbeeldingen van elke face gedetecteerd.

| Fase | Bestandsnaam | Opmerkingen |
| --- | --- | --- |
| Invoer asset |foo.bar |Video in WMV, MPV of MP4-indeling |
| Invoer config |De configuratie van definitie |{{'version':'1.0 ","opties": {'mode': 'analyseren'}} |
| Uitvoerasset |foo_annotations.JSON |De gegevens van de aantekening van face locaties in JSON-indeling. Dit kan worden bewerkt met de Hallo gebruiker toomodify Hallo zorgt voor een vervaging begrenzingsvak vakken. Zie onderstaand voorbeeld. |
| Uitvoerasset |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Een bijgesneden jpg van elke gezicht, waarbij Hallo Hallo labelId van Hallo gezicht geeft gedetecteerd |

#### <a name="output-example"></a>Voorbeeld van uitvoer:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Modus Redigeren
tweede stap van de werkstroom Hallo Hallo duurt een groter aantal invoerwaarden die moeten worden samengevoegd in één element.

Dit omvat een lijst met id's tooblur Hallo oorspronkelijke video en Hallo aantekeningen JSON. Deze modus gebruikt Hallo aantekeningen tooapply vervaging op Hallo invoervideo.

Hallo omvat uitvoer van Hallo analyseren pass geen Hallo oorspronkelijke video. Hallo video moet toobe geüpload naar de invoer asset Hallo voor Hallo Redact modus taak en geselecteerd als primaire Hallo-bestand.

| Fase | Bestandsnaam | Opmerkingen |
| --- | --- | --- |
| Invoer asset |foo.bar |Video WMV, MPV of MP4-indeling. Hetzelfde als in stap 1 video. |
| Invoer asset |foo_annotations.JSON |metagegevensbestand aantekeningen uit stap 1, optionele wijzigingen. |
| Invoer asset |foo_IDList.txt (optioneel) |Optionele nieuwe regel gescheiden lijst van id's tooredact gezicht. Als dit leeg laat, vervaging dit alle vlakken. |
| Invoer config |De configuratie van definitie |{{'version':'1.0 ","opties": {'mode': 'Redigeren'}} |
| Uitvoerasset |foo_redacted.mp4 |Video met zorgt voor een vervaging toegepast op basis van aantekeningen |

#### <a name="example-output"></a>Voorbeeld van uitvoer
Dit is Hallo-uitvoer van een IDList met een ID die geselecteerd.

[Bekijk deze video](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Voorbeeld foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Typen vervagen

In Hallo **gecombineerde** of **Redact** modus, er zijn 5 vervaging verschillende modi u uit via Hallo JSON-invoer configuratie kiezen kunt: **laag**, **Med**, **Hoge**, **Debug**, en **zwart**. Standaard **Med** wordt gebruikt.

Vindt u voorbeelden van Hallo vervagen hieronder typen.

### <a name="example-json"></a>Voorbeeld JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Laag

![Laag](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Med

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Hoog

![Hoog](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Fouten opsporen

![Fouten opsporen](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Zwart

![Zwart](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Elementen van Hallo uitvoer JSON-bestand

Hallo redactie MP biedt hoge precisie face locatie detectie en bijhouden die up too64 menselijke vlakken in een video frame kan detecteren. Voorzijde vlakken bieden de beste resultaten Hallo tijdens vlakken kant- en kleine vlakken (minder dan of gelijk zijn aan too24x24 pixels) lastig zijn.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende programma toont hoe:

1. Maak een asset en upload een mediabestand naar Hallo asset.
2. Een taak maken met een face redactie taak op basis van een configuratiebestand met Hallo json-definitie te volgen. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[Azure Media Analytics-demo 's](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

