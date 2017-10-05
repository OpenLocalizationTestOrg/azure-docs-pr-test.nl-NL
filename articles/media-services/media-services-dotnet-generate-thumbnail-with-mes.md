---
title: Miniatuurweergaven genereren met Media Encoder Standard met .NET
description: Dit onderwerp leest hoe u .NET gebruikt voor een asset coderen en het genereren van miniaturen tegelijkertijd met Media Encoder Standard.
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
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="c4026-103">Miniatuurweergaven genereren met Media Encoder Standard met .NET</span><span class="sxs-lookup"><span data-stu-id="c4026-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="c4026-104">U kunt Media Encoder Standard voor het genereren van miniaturen voor een of meer van uw invoervideo in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), of [BMP](https://en.wikipedia.org/wiki/BMP_file_format) installatiekopie bestandsindelingen.</span><span class="sxs-lookup"><span data-stu-id="c4026-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="c4026-105">U kunt taken die alleen afbeeldingen produceren verzenden of u miniaturen generatie codering kunt combineren.</span><span class="sxs-lookup"><span data-stu-id="c4026-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="c4026-106">In dit onderwerp biedt een paar voorbeeld XML en JSON miniaturen standaardinstellingen voor dergelijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="c4026-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="c4026-107">Aan het einde van het onderwerp, er is een [voorbeeldcode](#code_sample) die laat zien hoe de Media Services .NET SDK gebruiken de codering taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c4026-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="c4026-108">Voor meer informatie over de elementen die worden gebruikt in de standaardinstellingen voorbeeld moet u nagaan [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c4026-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="c4026-109">Leest de [overwegingen](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4026-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="c4026-110">Voorbeeld: één PNG-bestand</span><span class="sxs-lookup"><span data-stu-id="c4026-110">Example – single PNG file</span></span>

<span data-ttu-id="c4026-111">De volgende JSON- en XML-definitie kan worden gebruikt voor het produceren van een één uitvoer PNG-bestand uit de eerste paar seconden van de video invoer waar het coderingsprogramma een poging best-effort is vinden van een 'interessante' frame.</span><span class="sxs-lookup"><span data-stu-id="c4026-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="c4026-112">Let op: de afbeeldingsgrootte uitvoer zijn ingesteld op 100%, wat betekent dat deze komt overeen met de afmetingen van de invoer video.</span><span class="sxs-lookup"><span data-stu-id="c4026-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="c4026-113">U ziet ook hoe de instelling 'Indeling' in 'Uitvoer' moet overeenkomen met het gebruik van 'PngLayers' in de sectie 'Codecs'.</span><span class="sxs-lookup"><span data-stu-id="c4026-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="c4026-114">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="c4026-115">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="c4026-116">Voorbeeld: een reeks JPEG-afbeeldingen</span><span class="sxs-lookup"><span data-stu-id="c4026-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="c4026-117">De volgende JSON- en XML-definitie kan worden gebruikt voor het produceren van een set 10 installatiekopieën op tijdstempels van 5% 15%,..., 95% van de invoer tijdlijn, waarbij de grootte van de installatiekopie is opgegeven voor een van de video invoer kwartaal.</span><span class="sxs-lookup"><span data-stu-id="c4026-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="c4026-118">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="c4026-119">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="c4026-120">Voorbeeld: een installatiekopie op een specifieke tijdstempel</span><span class="sxs-lookup"><span data-stu-id="c4026-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="c4026-121">De volgende JSON- en XML-definitie kan worden gebruikt voor het produceren van een enkele JPEG-afbeelding op de 30 tweede beginpositie van de invoer video.</span><span class="sxs-lookup"><span data-stu-id="c4026-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="c4026-122">Deze definitie verwacht de invoer moet meer dan 30 seconden duren (anders de taak mislukt).</span><span class="sxs-lookup"><span data-stu-id="c4026-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="c4026-123">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="c4026-124">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-124">XML preset</span></span>
    
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

## <span data-ttu-id="c4026-125"><a id="code_sample"></a>Voorbeeld: video coderen en miniatuur maken</span><span class="sxs-lookup"><span data-stu-id="c4026-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="c4026-126">Het volgende codevoorbeeld maakt gebruik van Media Services .NET SDK naar de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c4026-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="c4026-127">Maak een codeertaak.</span><span class="sxs-lookup"><span data-stu-id="c4026-127">Create an encoding job.</span></span>
* <span data-ttu-id="c4026-128">Een verwijzing naar de Media Encoder Standard encoder ophalen.</span><span class="sxs-lookup"><span data-stu-id="c4026-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="c4026-129">Laden van de vooraf ingestelde [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) die de codering vooraf ingesteld en de benodigde informatie voor het genereren van miniaturen bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4026-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="c4026-130">U kunt dit opslaan [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) of [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in bestands- en gebruik de volgende code om het bestand niet laden.</span><span class="sxs-lookup"><span data-stu-id="c4026-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="c4026-131">Een enkele codering taak toevoegen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="c4026-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="c4026-132">Geef de invoer asset moeten worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="c4026-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="c4026-133">Maak een uitvoerasset met de gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="c4026-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="c4026-134">Een gebeurtenis-handler voor het controleren van de voortgang van de taak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c4026-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="c4026-135">Verzenden van de taak.</span><span class="sxs-lookup"><span data-stu-id="c4026-135">Submit the job.</span></span>

<span data-ttu-id="c4026-136">Zie de [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md) onderwerp voor instructies over het instellen van uw Developer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="c4026-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

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
            // Read values from the App.config file.
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

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="c4026-137"><a id="json"></a>Miniaturen JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="c4026-138">Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c4026-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="c4026-139"><a id="xml"></a>Miniaturen XML-definitie</span><span class="sxs-lookup"><span data-stu-id="c4026-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="c4026-140">Zie voor meer informatie over schema [dit](https://msdn.microsoft.com/library/mt269962.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="c4026-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="c4026-141">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="c4026-141">Considerations</span></span>
<span data-ttu-id="c4026-142">Het volgende letten:</span><span class="sxs-lookup"><span data-stu-id="c4026-142">The following considerations apply:</span></span>

* <span data-ttu-id="c4026-143">Het gebruik van expliciete tijdstempels voor stap/beginbereik wordt ervan uitgegaan dat de invoerbron ten minste 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="c4026-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="c4026-144">Png-jpg/BmpImage elementen hebben starten, stap en bereik kenmerken string: deze kunnen worden geïnterpreteerd als:</span><span class="sxs-lookup"><span data-stu-id="c4026-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="c4026-145">Framenummer als ze niet-negatieve gehele getallen zijn, bijv.</span><span class="sxs-lookup"><span data-stu-id="c4026-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="c4026-146">'Start': '120'</span><span class="sxs-lookup"><span data-stu-id="c4026-146">"Start": "120",</span></span>
  * <span data-ttu-id="c4026-147">Relatieve duur van de bron als uitgedrukt als % voorafgegaan, bijv.</span><span class="sxs-lookup"><span data-stu-id="c4026-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="c4026-148">'Start': '15% ', of</span><span class="sxs-lookup"><span data-stu-id="c4026-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="c4026-149">Tijdstempel als uitgedrukt als: mm: ss...</span><span class="sxs-lookup"><span data-stu-id="c4026-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="c4026-150">de indeling.</span><span class="sxs-lookup"><span data-stu-id="c4026-150">format.</span></span> <span data-ttu-id="c4026-151">Bv.</span><span class="sxs-lookup"><span data-stu-id="c4026-151">Eg.</span></span> <span data-ttu-id="c4026-152">'Start': ' 00: 01:00 '</span><span class="sxs-lookup"><span data-stu-id="c4026-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="c4026-153">U kunt combineren en notaties als u moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="c4026-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="c4026-154">Daarnaast ondersteunt Start ook een speciale Macro: {Best}, die probeert om te bepalen van het eerste 'interessante' frame van de inhoud-NOTITIE: (stap en bereik worden genegeerd tijdens het starten is ingesteld op {beste})</span><span class="sxs-lookup"><span data-stu-id="c4026-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="c4026-155">Standaardwaarden: Starten: {Best}</span><span class="sxs-lookup"><span data-stu-id="c4026-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="c4026-156">De indeling van uitvoer moet expliciet worden opgegeven voor elke afbeeldingsindeling: Png-Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="c4026-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="c4026-157">Indien aanwezig, MES komt overeen met JpgVideo naar JpgFormat enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c4026-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="c4026-158">OutputFormat introduceert een nieuwe installatiekopie codec specifieke Macro: {Index}, welke moet aanwezig zijn (eenmaal en slechts één keer) voor de installatiekopie-uitvoerindelingen.</span><span class="sxs-lookup"><span data-stu-id="c4026-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4026-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4026-159">Next steps</span></span>

<span data-ttu-id="c4026-160">U kunt controleren de [taak uitgevoerd](media-services-check-job-progress.md) wanneer de coderingstaak in behandeling is.</span><span class="sxs-lookup"><span data-stu-id="c4026-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c4026-161">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c4026-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4026-162">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c4026-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c4026-163">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c4026-163">See Also</span></span>
[<span data-ttu-id="c4026-164">Media Services-codering overzicht</span><span class="sxs-lookup"><span data-stu-id="c4026-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

