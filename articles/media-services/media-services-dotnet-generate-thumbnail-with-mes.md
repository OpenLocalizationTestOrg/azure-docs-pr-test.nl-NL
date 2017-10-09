---
title: aaaHow toogenerate miniaturen met Media Encoder Standard met .NET
description: Dit onderwerp wordt beschreven hoe toouse .NET tooencode een asset en genereren van miniaturen op Hallo tegelijkertijd met Media Encoder Standard.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>Hoe toogenerate miniaturen met Media Encoder Standard met .NET

U kunt Media Encoder Standard toogenerate miniaturen voor een of meer van uw invoervideo in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), of [BMP](https://en.wikipedia.org/wiki/BMP_file_format) installatiekopie bestandsindelingen. U kunt taken die alleen afbeeldingen produceren verzenden of u miniaturen generatie codering kunt combineren. In dit onderwerp biedt een paar voorbeeld XML en JSON miniaturen standaardinstellingen voor dergelijke scenario's. Aan het einde van de Hallo van Hallo onderwerp, er is een [voorbeeldcode](#code_sample) die weergeeft hoe toouse Hallo Media Services .NET SDK tooaccomplish Hallo codering taak.

Voor meer informatie over het Hallo-elementen die worden gebruikt in als voorbeeld voorkeur, moet u nagaan [Media Encoder Standard schema](media-services-mes-schema.md).

Zorg ervoor dat tooreview hello [overwegingen](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sectie.

## <a name="example--single-png-file"></a>Voorbeeld: één PNG-bestand

Hallo volgende JSON en XML-definitie mag gebruikte tooproduce één uitvoer PNG eerst het bestand buiten Hallo enkele seconden van de invoervideo hello, waar Hallo codering een poging best-effort wordt vinden van een 'interessante' frame. Houd er rekening mee dat de afmetingen van de afbeelding uitvoer Hallo too100%, wat betekent dat deze wordt overeenkomen met de Hallo dimensies van Hallo invoervideo zijn ingesteld. U ziet ook hoe Hallo ' indeling' in 'Uitvoer' niet is vereist toomatch Hallo gebruik van 'PngLayers' Hallo 'Codecs' onder. 

### <a name="json-preset"></a>JSON-definitie

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML-definitie

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a>Voorbeeld: een reeks JPEG-afbeeldingen

Hallo volgende JSON en XML-definitie mag gebruikte tooproduce een reeks 10 afbeeldingen op tijdstempels van 5% 15%,..., 95% van invoer tijdlijn hello, waarbij Hallo afbeeldingsgrootte is opgegeven toobe een vierde die Hallo video invoer.

### <a name="json-preset"></a>JSON-definitie

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a>XML-definitie
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a>Voorbeeld: een installatiekopie op een specifieke tijdstempel

Hallo volgende JSON en XML-definitie mag gebruikte tooproduce JPEG-afbeelding op Hallo 30 seconden markeren van Hallo invoervideo. Deze definitie verwacht invoer toobe Hallo duurt langer dan 30 seconden (anders Hallo taak mislukt).

### <a name="json-preset"></a>JSON-definitie

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML-definitie
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a id="code_sample"></a>Voorbeeld: video coderen en miniatuur maken

Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:

* Maak een codeertaak.
* Een verwijzing toohello Media Encoder Standard encoder ophalen.
* Load Hallo voorinstelling [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) die Hallo encoding preset evenals informatie nodig toogenerate miniaturen bevatten. U kunt dit opslaan [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in een bestand en het gebruik Hallo codebestand tooload hello te volgen.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* Een codering taak toohello van de taak niet toevoegen. 
* Geef Hallo invoer asset toobe gecodeerd.
* Maak een uitvoerasset met Hallo gecodeerde asset.
* Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.
* Verzenden van Hallo-taak.

Zie Hallo [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md) onderwerp voor instructies over het tooset van uw Developer-omgeving.

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

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

## <a id="json"></a>Miniaturen JSON-definitie
Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="xml"></a>Miniaturen XML-definitie
Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a>Overwegingen
Hallo overwegingen volgende van toepassing:

* Hallo gebruik van expliciete tijdstempels voor stap/beginbereik wordt ervan uitgegaan dat Hallo-invoerbron is minimaal 1 minuut.
* Png-jpg/BmpImage elementen hebben starten, stap en bereik kenmerken string: deze kunnen worden geïnterpreteerd als:
  
  * Framenummer als ze niet-negatieve gehele getallen zijn, bijv. 'Start': '120'
  * Duur van de relatieve toosource uitgedrukt in % voorafgegaan, bijv. 'Start': '15% ', of
  * Tijdstempel als uitgedrukt als: mm: ss... de indeling. Bv. 'Start': ' 00: 01:00 '
    
    U kunt combineren en notaties als u moet overeenkomen.
    
    Daarnaast ondersteunt Start ook een speciale Macro: {Best}, die probeert toodetermine Hallo eerste 'interessante' frame van Hallo inhoud Opmerking: (stap en bereik worden genegeerd tijdens het starten is ingesteld, te {Best})
  * Standaardwaarden: Starten: {Best}
* De indeling van uitvoer moet expliciet worden opgegeven voor elke afbeeldingsindeling toobe: Png-Jpg/BmpFormat. Indien aanwezig, MES komt overeen met JpgVideo tooJpgFormat enzovoort. OutputFormat introduceert een nieuwe installatiekopie codec specifieke Macro: {Index}, moeten toobe aanwezig (eenmaal en slechts één keer) voor de installatiekopie-uitvoerindelingen.

## <a name="next-steps"></a>Volgende stappen

U kunt controleren Hallo [taak uitgevoerd](media-services-check-job-progress.md) tijdens het Hallo coderingstaak in behandeling is.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Media Services-codering overzicht](media-services-encode-asset.md)

