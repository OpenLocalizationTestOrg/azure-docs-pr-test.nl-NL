---
title: aaaDigitize tekst met Azure Media Analytics OCR | Microsoft Docs
description: Azure Media Analytics OCR (OCR) kunt u de tekstinhoud tooconvert in videobestanden naar bewerkbare, doorzoekbaar digitale tekst.  Hiermee kunt u tooautomate Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Gebruik Azure Media Analytics tooconvert tekstinhoud in videobestanden in digitale tekst
## <a name="overview"></a>Overzicht
Als u tekst tooextract inhoud van uw video's moet en een bewerkbare, doorzoekbaar digitale tekst wordt gegenereerd, moet u Azure Media Analytics OCR (OCR). Deze Azure Media Processor tekstinhoud detecteert in uw video's en genereert tekstbestanden voor het gebruik. OCR kunt u tooautomate Hallo extractie van zinvolle metagegevens van de video signaal Hallo van uw media.

Wanneer gebruikt in combinatie met een zoekmachine, kunt u eenvoudig uw media indexering van tekst en Hallo detectie van uw inhoud verbeteren. Dit is zeer nuttig zijn bij zeer tekstuele video, zoals een video-opname of een schermopname van een diavoorstelling. Hello Azure OCR Mediaprocessor is geoptimaliseerd voor digitale tekst.

Hallo **Azure Media OCR** Mediaprocessor is momenteel in Preview.

Dit onderwerp bevat informatie over **Azure Media OCR** en ziet u hoe toouse met Media Services SDK voor .NET. Zie voor meer informatie en voorbeelden [deze blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>De invoerbestanden OCR
Videobestanden. Op dit moment Hallo volgende indelingen worden ondersteund: MP4 MOV en WMV.

## <a name="task-configuration"></a>Taken configureren
Taken configureren (standaardoptie). Bij het maken van een taak met **Azure Media OCR**, moet u een configuratie met JSON of XML-definitie opgeven. 

>[!NOTE]
>Hallo OCR-engine duurt slechts een installatiekopie-regio met minimale 40 pixels toomaximum 32000 pixels als een geldige invoer in beide hoogte/breedte.
>

### <a name="attribute-descriptions"></a>Beschrijvingen van kenmerken
| Naam van kenmerk | Beschrijving |
| --- | --- |
|AdvancedOutput| Als u AdvancedOutput tootrue instelt, wordt in Hallo JSON-uitvoer positionele gegevens voor elke één woord (in aanvulling toophrases en regio's) bevatten. Als u niet dat toosee wilt vlag deze details kunt set Hallo toofalse. Hallo-standaardwaarde is false. Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Taal |(optioneel) beschrijft Hallo taal van de tekst voor welke toolook. Een van de volgende Hallo: AutoDetect (standaard), Arabisch, ChineseSimplified, ChineseTraditional, Tsjechisch Deens, Nederlands, Engels, Fins, Frans, Duits, Grieks, Hongaars, Italiaans, Japans, Koreaans, Noors, Pools, Portugees, Roemeens, Russisch, SerbianCyrillic, SerbianLatin, Slowaaks, Spaans, Zweeds, Turks. |
| TextOrientation |(optioneel) beschrijft Hallo richting van tekst voor welke toolook.  "Left" betekent dat Hallo boven aan alle letters worden waarnaar wordt verwezen naar Hallo links.  De standaardtekst (zoals die die kunnen worden gevonden in een boek) kan worden aangeroepen 'Van' objectgeoriënteerde.  Een van de volgende Hallo: AutoDetect (standaard), maximaal, rechts, omlaag, links. |
| TimeInterval |(optioneel) wordt de samplingfrequentie Hallo beschreven.  Standaard is elke seconde 1/2.<br/>JSON-indeling –: mm: ss. SSS (standaard 00:00:00.500)<br/>XML-indeling W3C XSD duur primitieve (standaard PT0.5) |
| DetectRegions |(optioneel) Een matrix met regio's binnen de video frame Hallo opgeven in welke tekst toodetect DetectRegion-objecten.<br/>Een object DetectRegion Hallo vier integerwaarden volgende bestaat:<br/>Links: pixels van Hallo linkermarge<br/>Top – pixels van Hallo bovenmarge<br/>Breedte – breedte van Hallo gebied in pixels<br/>Hoogte – hoogte van Hallo gebied in pixels |

#### <a name="json-preset-example"></a>Vooraf gedefinieerde JSON-voorbeeld

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Vooraf gedefinieerde XML-voorbeeld
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>De uitvoerbestanden OCR
Hallo-uitvoer van Hallo OCR Mediaprocessor is een JSON-bestand.

### <a name="elements-of-hello-output-json-file"></a>Elementen van Hallo uitvoer JSON-bestand
Hallo Video OCR uitvoer biedt gegevens tijd gesegmenteerd op Hallo-tekens in uw video zijn gevonden.  Kunt u kenmerken, zoals taal of toohone in stand op precies Hallo woorden dat u geïnteresseerd in analyseren bent. 

Hallo uitvoer bevat Hallo volgende kenmerken:

| Element | Beschrijving |
| --- | --- |
| Tijdschaal |'maatstreepjes' per seconde van Hallo video |
| Offset |tijdzoneverschil voor tijdstempels. Versie 1.0 van Video-API's, zal dit altijd 0 zijn. |
| framesnelheid |Frames per seconde van Hallo video |
| Breedte |breedte van Hallo video in pixels |
| Hoogte |hoogte van Hallo video in pixels |
| fragmenten |matrix van reeksen in welke Hallo metagegevens is chunked video op basis van tijd |
| start |Begintijd van een fragment in 'maatstreepjes' |
| Duur |lengte van een fragment in 'maatstreepjes' |
| interval |het interval van elke gebeurtenis binnen een gegeven fragment Hallo |
| events |matrix met regio 's |
| Regio |object dat vertegenwoordigt woorden of zinnen gedetecteerd |
| taal |taal van Hallo tekst binnen een regio gedetecteerd |
| afdrukstand |richting van Hallo tekst binnen een regio gedetecteerd |
| regels |matrix van regels tekst binnen een regio gedetecteerd |
| Tekst |de werkelijke tekst Hello |

### <a name="json-output-example"></a>Voorbeeld van JSON-uitvoer
Hallo bevat volgende voorbeeld van uitvoer algemene video informatie Hallo en verschillende video fragmenten. In elke video fragment bevat elke regio die wordt gedetecteerd door OCR MP met de Hallo taal en de richting van tekst. Hallo regio bevat ook elke regel woord in deze regio van Hallo regel tekst hello regelpositie en elke word-gegevens (word-inhoud, positie en vertrouwen) in deze regel. Hallo Hieronder volgt een voorbeeld en ik bepaalde inline opmerkingen plaatsen.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Voorbeeldcode voor .NET

Hallo volgende programma toont hoe:

1. Maak een asset en upload een mediabestand naar Hallo asset.
2. Een taak maken met een OCR configuration/voorinstelling-bestand.
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

