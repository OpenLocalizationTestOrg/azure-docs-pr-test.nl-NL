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
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="7c002-103">Hoe toogenerate miniaturen met Media Encoder Standard met .NET</span><span class="sxs-lookup"><span data-stu-id="7c002-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="7c002-104">U kunt Media Encoder Standard toogenerate miniaturen voor een of meer van uw invoervideo in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), of [BMP](https://en.wikipedia.org/wiki/BMP_file_format) installatiekopie bestandsindelingen.</span><span class="sxs-lookup"><span data-stu-id="7c002-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="7c002-105">U kunt taken die alleen afbeeldingen produceren verzenden of u miniaturen generatie codering kunt combineren.</span><span class="sxs-lookup"><span data-stu-id="7c002-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="7c002-106">In dit onderwerp biedt een paar voorbeeld XML en JSON miniaturen standaardinstellingen voor dergelijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="7c002-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="7c002-107">Aan het einde van de Hallo van Hallo onderwerp, er is een [voorbeeldcode](#code_sample) die weergeeft hoe toouse Hallo Media Services .NET SDK tooaccomplish Hallo codering taak.</span><span class="sxs-lookup"><span data-stu-id="7c002-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="7c002-108">Voor meer informatie over het Hallo-elementen die worden gebruikt in als voorbeeld voorkeur, moet u nagaan [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7c002-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="7c002-109">Zorg ervoor dat tooreview hello [overwegingen](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sectie.</span><span class="sxs-lookup"><span data-stu-id="7c002-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="7c002-110">Voorbeeld: één PNG-bestand</span><span class="sxs-lookup"><span data-stu-id="7c002-110">Example – single PNG file</span></span>

<span data-ttu-id="7c002-111">Hallo volgende JSON en XML-definitie mag gebruikte tooproduce één uitvoer PNG eerst het bestand buiten Hallo enkele seconden van de invoervideo hello, waar Hallo codering een poging best-effort wordt vinden van een 'interessante' frame.</span><span class="sxs-lookup"><span data-stu-id="7c002-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="7c002-112">Houd er rekening mee dat de afmetingen van de afbeelding uitvoer Hallo too100%, wat betekent dat deze wordt overeenkomen met de Hallo dimensies van Hallo invoervideo zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7c002-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="7c002-113">U ziet ook hoe Hallo ' indeling' in 'Uitvoer' niet is vereist toomatch Hallo gebruik van 'PngLayers' Hallo 'Codecs' onder.</span><span class="sxs-lookup"><span data-stu-id="7c002-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="7c002-114">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="7c002-115">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="7c002-116">Voorbeeld: een reeks JPEG-afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="7c002-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="7c002-117">Hallo volgende JSON en XML-definitie mag gebruikte tooproduce een reeks 10 afbeeldingen op tijdstempels van 5% 15%,..., 95% van invoer tijdlijn hello, waarbij Hallo afbeeldingsgrootte is opgegeven toobe een vierde die Hallo video invoer.</span><span class="sxs-lookup"><span data-stu-id="7c002-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="7c002-118">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="7c002-119">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="7c002-120">Voorbeeld: een installatiekopie op een specifieke tijdstempel</span><span class="sxs-lookup"><span data-stu-id="7c002-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="7c002-121">Hallo volgende JSON en XML-definitie mag gebruikte tooproduce JPEG-afbeelding op Hallo 30 seconden markeren van Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="7c002-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="7c002-122">Deze definitie verwacht invoer toobe Hallo duurt langer dan 30 seconden (anders Hallo taak mislukt).</span><span class="sxs-lookup"><span data-stu-id="7c002-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="7c002-123">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="7c002-124">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-124">XML preset</span></span>
    
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

## <span data-ttu-id="7c002-125"><a id="code_sample"></a>Voorbeeld: video coderen en miniatuur maken</span><span class="sxs-lookup"><span data-stu-id="7c002-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="7c002-126">Hallo volgende codevoorbeeld maakt gebruik van Media Services .NET SDK tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="7c002-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="7c002-127">Maak een codeertaak.</span><span class="sxs-lookup"><span data-stu-id="7c002-127">Create an encoding job.</span></span>
* <span data-ttu-id="7c002-128">Een verwijzing toohello Media Encoder Standard encoder ophalen.</span><span class="sxs-lookup"><span data-stu-id="7c002-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="7c002-129">Load Hallo voorinstelling [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) die Hallo encoding preset evenals informatie nodig toogenerate miniaturen bevatten.</span><span class="sxs-lookup"><span data-stu-id="7c002-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="7c002-130">U kunt dit opslaan [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in een bestand en het gebruik Hallo codebestand tooload hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="7c002-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="7c002-131">Een codering taak toohello van de taak niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7c002-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="7c002-132">Geef Hallo invoer asset toobe gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="7c002-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="7c002-133">Maak een uitvoerasset met Hallo gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="7c002-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="7c002-134">Toevoegen van een gebeurtenis-handler toocheck Hallo taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7c002-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="7c002-135">Verzenden van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="7c002-135">Submit hello job.</span></span>

<span data-ttu-id="7c002-136">Zie Hallo [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md) onderwerp voor instructies over het tooset van uw Developer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7c002-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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

## <span data-ttu-id="7c002-137"><a id="json"></a>Miniaturen JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="7c002-138">Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7c002-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="7c002-139"><a id="xml"></a>Miniaturen XML-definitie</span><span class="sxs-lookup"><span data-stu-id="7c002-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="7c002-140">Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7c002-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="7c002-141">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="7c002-141">Considerations</span></span>
<span data-ttu-id="7c002-142">Hallo overwegingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="7c002-142">hello following considerations apply:</span></span>

* <span data-ttu-id="7c002-143">Hallo gebruik van expliciete tijdstempels voor stap/beginbereik wordt ervan uitgegaan dat Hallo-invoerbron is minimaal 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="7c002-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="7c002-144">Png-jpg/BmpImage elementen hebben starten, stap en bereik kenmerken string: deze kunnen worden geïnterpreteerd als:</span><span class="sxs-lookup"><span data-stu-id="7c002-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="7c002-145">Framenummer als ze niet-negatieve gehele getallen zijn, bijv.</span><span class="sxs-lookup"><span data-stu-id="7c002-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="7c002-146">'Start': '120'</span><span class="sxs-lookup"><span data-stu-id="7c002-146">"Start": "120",</span></span>
  * <span data-ttu-id="7c002-147">Duur van de relatieve toosource uitgedrukt in % voorafgegaan, bijv.</span><span class="sxs-lookup"><span data-stu-id="7c002-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="7c002-148">'Start': '15% ', of</span><span class="sxs-lookup"><span data-stu-id="7c002-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="7c002-149">Tijdstempel als uitgedrukt als: mm: ss...</span><span class="sxs-lookup"><span data-stu-id="7c002-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="7c002-150">de indeling.</span><span class="sxs-lookup"><span data-stu-id="7c002-150">format.</span></span> <span data-ttu-id="7c002-151">Bv.</span><span class="sxs-lookup"><span data-stu-id="7c002-151">Eg.</span></span> <span data-ttu-id="7c002-152">'Start': ' 00: 01:00 '</span><span class="sxs-lookup"><span data-stu-id="7c002-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="7c002-153">U kunt combineren en notaties als u moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="7c002-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="7c002-154">Daarnaast ondersteunt Start ook een speciale Macro: {Best}, die probeert toodetermine Hallo eerste 'interessante' frame van Hallo inhoud Opmerking: (stap en bereik worden genegeerd tijdens het starten is ingesteld, te {Best})</span><span class="sxs-lookup"><span data-stu-id="7c002-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="7c002-155">Standaardwaarden: Starten: {Best}</span><span class="sxs-lookup"><span data-stu-id="7c002-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="7c002-156">De indeling van uitvoer moet expliciet worden opgegeven voor elke afbeeldingsindeling toobe: Png-Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="7c002-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="7c002-157">Indien aanwezig, MES komt overeen met JpgVideo tooJpgFormat enzovoort.</span><span class="sxs-lookup"><span data-stu-id="7c002-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="7c002-158">OutputFormat introduceert een nieuwe installatiekopie codec specifieke Macro: {Index}, moeten toobe aanwezig (eenmaal en slechts één keer) voor de installatiekopie-uitvoerindelingen.</span><span class="sxs-lookup"><span data-stu-id="7c002-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c002-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c002-159">Next steps</span></span>

<span data-ttu-id="7c002-160">U kunt controleren Hallo [taak uitgevoerd](media-services-check-job-progress.md) tijdens het Hallo coderingstaak in behandeling is.</span><span class="sxs-lookup"><span data-stu-id="7c002-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7c002-161">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="7c002-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7c002-162">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="7c002-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="7c002-163">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7c002-163">See Also</span></span>
[<span data-ttu-id="7c002-164">Media Services-codering overzicht</span><span class="sxs-lookup"><span data-stu-id="7c002-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

