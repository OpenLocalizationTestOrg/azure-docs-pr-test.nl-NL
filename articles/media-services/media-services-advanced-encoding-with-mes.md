---
title: aaaPerform geavanceerde codering door aan te passen MES standaardinstellingen | Microsoft Docs
description: Dit onderwerp leest hoe tooperform geavanceerde codering met Media Encoder Standard standaardinstellingen van de taak aanpassen.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="12f4c-103">Uitvoeren van geavanceerde codering door aan te passen MES standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="12f4c-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="12f4c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="12f4c-104">Overview</span></span>

<span data-ttu-id="12f4c-105">Dit onderwerp leest hoe Media Encoder Standard toocustomize voorinstellingen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="12f4c-106">Hallo [codering met Media Encoder Standard met behulp van aangepaste standaardinstellingen](media-services-custom-mes-presets-with-dotnet.md) onderwerp wordt beschreven hoe toouse .NET toocreate een codering van de taak en een taak die met deze taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12f4c-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="12f4c-107">Wanneer u een vooraf ingestelde levering Hallo aangepaste standaardinstellingen toohello codering taak aanpassen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="12f4c-108">Als een XML-definitie, moet u ervoor dat toopreserve Hallo volgorde van elementen, zoals wordt weergegeven in de XML-voorbeelden hieronder (bijvoorbeeld KeyFrameInterval moet worden voorafgegaan door een SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="12f4c-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="12f4c-109">In dit onderwerp worden de Hallo aangepaste standaardinstellingen die Hallo na codering taken uitvoeren gedemonstreerd.</span><span class="sxs-lookup"><span data-stu-id="12f4c-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="12f4c-110">Ondersteuning voor relatieve grootten</span><span class="sxs-lookup"><span data-stu-id="12f4c-110">Support for relative sizes</span></span>

<span data-ttu-id="12f4c-111">Bij het genereren van miniaturen, hoeft u niet tooalways Geef uitvoer breedte en hoogte in pixels.</span><span class="sxs-lookup"><span data-stu-id="12f4c-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="12f4c-112">U kunt opgeven in percentages in Hallo bereik [% 1,..., 100%].</span><span class="sxs-lookup"><span data-stu-id="12f4c-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="12f4c-113">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="12f4c-114">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="12f4c-115"><a id="thumbnails"></a>Genereren van miniaturen</span><span class="sxs-lookup"><span data-stu-id="12f4c-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="12f4c-116">Deze sectie wordt beschreven hoe toocustomize een voorinstelling die miniaturen genereert.</span><span class="sxs-lookup"><span data-stu-id="12f4c-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="12f4c-117">Hallo bevat voorinstelling zoals hieronder gedefinieerd, informatie over hoe u wilt dat tooencode uw bestand evenals informatie nodig toogenerate miniatuurweergaven.</span><span class="sxs-lookup"><span data-stu-id="12f4c-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="12f4c-118">U kunt een van de Hallo MES standaardinstellingen beschreven nemen [dit](media-services-mes-presets-overview.md) sectie en code die wordt gegenereerd miniaturen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="12f4c-119">Hallo **SceneChangeDetection** -instelling in de volgende vooraf ingestelde Hallo kan alleen worden ingesteld tootrue als u tooa single-bitrate video coderen wilt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="12f4c-120">Als u tooa multi-bitrate coderen wilt video en stel **SceneChangeDetection** tootrue, Hallo codering wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="12f4c-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="12f4c-121">Zie voor meer informatie over schema [dit](media-services-mes-schema.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="12f4c-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="12f4c-122">Zorg ervoor dat tooreview hello [overwegingen](#considerations) sectie.</span><span class="sxs-lookup"><span data-stu-id="12f4c-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="12f4c-123"><a id="json"></a>JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-123"><a id="json"></a>JSON preset</span></span>
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="12f4c-124"><a id="xml"></a>XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-124"><a id="xml"></a>XML preset</span></span>
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="12f4c-125">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="12f4c-125">Considerations</span></span>

<span data-ttu-id="12f4c-126">Hallo overwegingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="12f4c-126">hello following considerations apply:</span></span>

* <span data-ttu-id="12f4c-127">Hallo gebruik van expliciete tijdstempels voor stap/beginbereik wordt ervan uitgegaan dat Hallo-invoerbron is minimaal 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="12f4c-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="12f4c-128">Png-jpg/BmpImage elementen moeten worden gestart, stap en bereik tekenreekskenmerken: deze kunnen worden geïnterpreteerd als:</span><span class="sxs-lookup"><span data-stu-id="12f4c-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="12f4c-129">Aantal frame als ze niet-negatieve gehele getallen zijn, bijvoorbeeld 'Start': '120'</span><span class="sxs-lookup"><span data-stu-id="12f4c-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="12f4c-130">Duur van de relatieve toosource uitgedrukt in % voorafgegaan, bijvoorbeeld 'Start': '15% ', of</span><span class="sxs-lookup"><span data-stu-id="12f4c-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="12f4c-131">Tijdstempel als uitgedrukt als: mm: ss...</span><span class="sxs-lookup"><span data-stu-id="12f4c-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="12f4c-132">indeling, bijvoorbeeld 'Start': ' 00: 01:00 '</span><span class="sxs-lookup"><span data-stu-id="12f4c-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="12f4c-133">U kunt combineren en notaties als u moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="12f4c-134">Daarnaast ondersteunt Start ook een speciale Macro: {Best}, die probeert toodetermine Hallo eerste 'interessante' frame van Hallo inhoud Opmerking: (stap en bereik worden genegeerd tijdens het starten is ingesteld, te {Best})</span><span class="sxs-lookup"><span data-stu-id="12f4c-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="12f4c-135">Standaardwaarden: Starten: {Best}</span><span class="sxs-lookup"><span data-stu-id="12f4c-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="12f4c-136">De indeling van uitvoer moet expliciet worden opgegeven voor elke afbeeldingsindeling toobe: Png-Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="12f4c-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="12f4c-137">Als aanwezig is, vergelijkt MES JpgVideo tooJpgFormat enzovoort.</span><span class="sxs-lookup"><span data-stu-id="12f4c-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="12f4c-138">OutputFormat introduceert een nieuwe installatiekopie codec specifieke Macro: {Index}, moeten toobe aanwezig (eenmaal en slechts één keer) voor de installatiekopie-uitvoerindelingen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="12f4c-139"><a id="trim_video"></a>Een video (paginaknipsel) knippen</span><span class="sxs-lookup"><span data-stu-id="12f4c-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="12f4c-140">Deze sectie vertelt over het wijzigen van Hallo encoder tooclip voorinstellingen of trim Hallo invoervideo waar Hallo-invoer een zogenaamde tussentijds of op aanvraag-bestand is.</span><span class="sxs-lookup"><span data-stu-id="12f4c-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="12f4c-141">Hello coderingsprogramma kan ook worden gebruikt tooclip of een asset, die is vastgelegd of van een live stream gearchiveerd trim – Hallo details voor deze zijn beschikbaar in [deze blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="12f4c-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="12f4c-142">tootrim uw video's, u een van de Hallo MES standaardinstellingen gedocumenteerd kunt nemen [dit](media-services-mes-presets-overview.md) sectie en Hallo wijzigen **bronnen** element (zoals hieronder wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="12f4c-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="12f4c-143">Hallo-waarde van StartTime moet toomatch Hallo absolute tijdstempels van Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="12f4c-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="12f4c-144">Bijvoorbeeld, als hello eerste frame van Hallo invoervideo een tijdstempel van 12:00:10.000 heeft, wordt StartTime moet ten minste 12:00:10.000 en hoger.</span><span class="sxs-lookup"><span data-stu-id="12f4c-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="12f4c-145">In Hallo onderstaand voorbeeld gaan we ervan uit dat Hallo invoervideo een eerste tijdstempel van nul heeft.</span><span class="sxs-lookup"><span data-stu-id="12f4c-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="12f4c-146">**Bronnen** aan Hallo begin van de vooraf ingestelde Hallo moeten worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="12f4c-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="12f4c-147"><a id="json"></a>JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="12f4c-148">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-148">XML preset</span></span>
<span data-ttu-id="12f4c-149">tootrim uw video's, u een van de Hallo MES standaardinstellingen gedocumenteerd kunt nemen [hier](media-services-mes-presets-overview.md) en Hallo wijzigen **bronnen** element (zoals hieronder wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="12f4c-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="12f4c-150"><a id="overlay"></a>Maken van een overlay</span><span class="sxs-lookup"><span data-stu-id="12f4c-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="12f4c-151">Hallo Media Encoder Standard kunt u een installatiekopie op een bestaande video toooverlay.</span><span class="sxs-lookup"><span data-stu-id="12f4c-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="12f4c-152">Op dit moment Hallo volgende indelingen worden ondersteund: png, jpg, gif, en bmp.</span><span class="sxs-lookup"><span data-stu-id="12f4c-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="12f4c-153">Hallo is voorinstelling zoals hieronder gedefinieerd, een eenvoudige voorbeeld van een video-overlay.</span><span class="sxs-lookup"><span data-stu-id="12f4c-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="12f4c-154">Bovendien toodefining een vooraf ingestelde bestand, hebt u ook toolet Media Services weten welk bestand Hallo actief in is Hallo overlay installatiekopie en waarop het bestand is Hallo bronvideo waarop u wilt dat toooverlay Hallo afbeelding.</span><span class="sxs-lookup"><span data-stu-id="12f4c-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="12f4c-155">Hallo videobestand heeft toobe hello **primaire** bestand.</span><span class="sxs-lookup"><span data-stu-id="12f4c-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="12f4c-156">Als u .NET gebruikt, voegt u twee functies toohello .NET-voorbeeld gedefinieerd in de volgende Hallo [dit](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="12f4c-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="12f4c-157">Hallo **UploadMediaFilesFromFolder** functie uploadt bestanden vanuit een map (bijvoorbeeld BigBuckBunny.mp4 en Image001.png) en sets Hallo mp4-bestand toobe Hallo primaire bestand Hallo actief in.</span><span class="sxs-lookup"><span data-stu-id="12f4c-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="12f4c-158">Hallo **EncodeWithOverlay** functie maakt gebruik van Hallo aangepaste vooraf ingestelde bestand dat is doorgegeven tooit (bijvoorbeeld Hallo die volgt voorinstelling) toocreate Hallo codering taak.</span><span class="sxs-lookup"><span data-stu-id="12f4c-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="12f4c-159">Huidige beperkingen:</span><span class="sxs-lookup"><span data-stu-id="12f4c-159">Current limitations:</span></span>
>
> <span data-ttu-id="12f4c-160">Hallo overlay dekkingsinstelling wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="12f4c-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="12f4c-161">Uw video bronbestand en Hallo overlay installatiekopiebestand hebben toobe in dezelfde asset Hallo en Hallo videobestand behoeften toobe instellen als primaire Hallo-bestand in deze activa.</span><span class="sxs-lookup"><span data-stu-id="12f4c-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="12f4c-162">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="12f4c-163">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="12f4c-164"><a id="silent_audio"></a>Invoegen van een achtergrond-nummer als invoer geen audio heeft</span><span class="sxs-lookup"><span data-stu-id="12f4c-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="12f4c-165">Standaard als u een coderingsprogramma invoer toohello met alleen video en geen audio verzendt bevat vervolgens Hallo uitvoerasset bestanden die alleen video gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="12f4c-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="12f4c-166">Sommige spelers mogelijk geen toohandle dergelijke uitvoerstromen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="12f4c-167">In dit scenario kunt u deze instelling tooforce Hallo encoder tooadd een achtergrond-nummer toohello uitvoer.</span><span class="sxs-lookup"><span data-stu-id="12f4c-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="12f4c-168">tooforce hello encoder tooproduce een activum met een achtergrond-nummer invoer bevat geen audio Hallo 'InsertSilenceIfNoAudio'-waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="12f4c-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="12f4c-169">U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:</span><span class="sxs-lookup"><span data-stu-id="12f4c-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="12f4c-170">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="12f4c-171">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="12f4c-172"><a id="deinterlacing"></a>Automatische de-interlacing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="12f4c-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="12f4c-173">Klanten hoeft niet toodo iets als ze zoals Hallo inhoud toobe automatisch ongedaan interlaced interliniëren.</span><span class="sxs-lookup"><span data-stu-id="12f4c-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="12f4c-174">Wanneer Hallo automatisch de-interlacing is ingeschakeld (standaard) Hallo die mes Hallo automatische detectie van geïnterlinieerde frames en gemarkeerd als geïnterlinieerde frames alleen ongedaan interlaces.</span><span class="sxs-lookup"><span data-stu-id="12f4c-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="12f4c-175">U kunt uitschakelen Hallo automatisch de-interlacing.</span><span class="sxs-lookup"><span data-stu-id="12f4c-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="12f4c-176">Deze optie wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="12f4c-177">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="12f4c-178">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="12f4c-179"><a id="audio_only"></a>Alleen audio standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="12f4c-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="12f4c-180">Deze sectie wordt gedemonstreerd twee alleen audio MES standaardinstellingen: AAC Audio- en AAC goede kwaliteit Audio.</span><span class="sxs-lookup"><span data-stu-id="12f4c-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="12f4c-181">AAC Audio</span><span class="sxs-lookup"><span data-stu-id="12f4c-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="12f4c-182">AAC goede kwaliteit Audio</span><span class="sxs-lookup"><span data-stu-id="12f4c-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="12f4c-183"><a id="concatenate"></a>Samenvoegen van twee of meer video bestanden</span><span class="sxs-lookup"><span data-stu-id="12f4c-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="12f4c-184">Hallo volgende voorbeeld ziet u het genereren van een vooraf ingestelde tooconcatenate twee of meer videobestanden.</span><span class="sxs-lookup"><span data-stu-id="12f4c-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="12f4c-185">meest voorkomende scenario Hallo is dat u tooadd een kop of een aanhangwagen toohello belangrijkste video wilt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="12f4c-186">Hallo bedoeld wordt gebruikt wanneer Hallo videobestanden samen wordt bewerkt eigenschappen (beeldschermresolutie, framesnelheid, count-nummer, enzovoort delen).</span><span class="sxs-lookup"><span data-stu-id="12f4c-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="12f4c-187">U moet behandelen niet toomix video's van verschillende framesnelheid of met een verschillend aantal audio houdt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="12f4c-188">Hallo huidige ontwerp van Hallo samenvoeging functie verwacht dat Hallo invoer videoclips zijn consistent in termen van resolutie framesnelheid enzovoort.</span><span class="sxs-lookup"><span data-stu-id="12f4c-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="12f4c-189">Vereisten en overwegingen</span><span class="sxs-lookup"><span data-stu-id="12f4c-189">Requirements and considerations</span></span>

* <span data-ttu-id="12f4c-190">Invoer video's mag alleen één-nummer hebben.</span><span class="sxs-lookup"><span data-stu-id="12f4c-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="12f4c-191">Invoer video's, moeten alle Hallo hebben dezelfde framesnelheid.</span><span class="sxs-lookup"><span data-stu-id="12f4c-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="12f4c-192">U moet uw video's uploaden naar afzonderlijke activa en Hallo video's instellen als primaire bestand Hallo in elke asset.</span><span class="sxs-lookup"><span data-stu-id="12f4c-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="12f4c-193">U moet tooknow Hallo duur van uw video's.</span><span class="sxs-lookup"><span data-stu-id="12f4c-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="12f4c-194">Hallo vooraf ingestelde in de volgende voorbeelden wordt ervan uitgegaan dat alle Hallo invoer video's starten met een tijdstempel van nul.</span><span class="sxs-lookup"><span data-stu-id="12f4c-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="12f4c-195">U moet toomodify Hallo StartTime waarden als Hallo video's verschillende begin timestamp hebben, zoals gewoonlijk Hallo geval met live archieven.</span><span class="sxs-lookup"><span data-stu-id="12f4c-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="12f4c-196">Hallo kunt JSON-definitie u expliciete verwijzingen toohello item-id hebt waarden van invoerbestand activa Hallo.</span><span class="sxs-lookup"><span data-stu-id="12f4c-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="12f4c-197">Hallo voorbeeldcode wordt ervan uitgegaan dat Hallo die JSON voorinstelling tooa lokaal bestand, zoals 'C:\supportFiles\preset.json' is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="12f4c-198">Ook wordt ervan uitgegaan dat twee activa zijn gemaakt door het uploaden van twee videobestanden, en dat u weet Hallo resulterende waarden van item-id hebt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="12f4c-199">Hallo codefragment en JSON voorinstelling toont een voorbeeld van twee video bestanden worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="12f4c-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="12f4c-200">U kunt ook toomore dan twee video's door:</span><span class="sxs-lookup"><span data-stu-id="12f4c-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="12f4c-201">Taak aanroepen. InputAssets.Add() herhaaldelijk tooadd meer video's, in volgorde.</span><span class="sxs-lookup"><span data-stu-id="12f4c-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="12f4c-202">Toohello 'bronnen'-element in Hallo JSON, waardoor het bijbehorende bewerkt door meer vermeldingen toe te voegen in Hallo dezelfde volgorde.</span><span class="sxs-lookup"><span data-stu-id="12f4c-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="12f4c-203">.NET-code</span><span class="sxs-lookup"><span data-stu-id="12f4c-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="12f4c-204">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-204">JSON preset</span></span>

<span data-ttu-id="12f4c-205">Uw aangepaste voorinstelling met id's van Hallo activa dat u wilt dat tooconcatenate en met Hallo tijdstip segment voor elke video bijwerken.</span><span class="sxs-lookup"><span data-stu-id="12f4c-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="12f4c-206"><a id="crop"></a>Bijsnijden video's met Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="12f4c-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="12f4c-207">Zie Hallo [video's met Media Encoder Standard bijsnijden](media-services-crop-video.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="12f4c-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="12f4c-208"><a id="no_video"></a>Invoegen van een video bijhouden als invoer geen video heeft</span><span class="sxs-lookup"><span data-stu-id="12f4c-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="12f4c-209">Standaard als u een coderingsprogramma invoer toohello met alleen audio en geen video verzendt bevat vervolgens Hallo uitvoerasset bestanden die alleen audiogegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="12f4c-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="12f4c-210">Sommige spelers, met inbegrip van Azure Media Player (Zie [dit](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) mogelijk niet kunnen toohandle dergelijke stromen.</span><span class="sxs-lookup"><span data-stu-id="12f4c-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="12f4c-211">U kunt deze instelling tooforce Hallo encoder tooadd een monochroom video bijhouden toohello uitvoer gebruiken in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="12f4c-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="12f4c-212">Hallo encoder tooinsert dwingen een uitvoer video bijhouden toeneemt Hallo grootte van Hallo Asset uitvoer en waardoor Hallo kosten in rekening gebracht voor Hallo taak codering.</span><span class="sxs-lookup"><span data-stu-id="12f4c-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="12f4c-213">U moet uitvoeren van tests tooverify die deze resulterende verhoging heeft alleen een matige impact op uw maandelijkse kosten.</span><span class="sxs-lookup"><span data-stu-id="12f4c-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="12f4c-214">Video op alleen Hallo laagste bitrate invoegen</span><span class="sxs-lookup"><span data-stu-id="12f4c-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="12f4c-215">Stel dat u gebruikt een meerdere bitrate encoding preset zoals [' standaardinstelling H264 Multiple Bitrate 720p '](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode uw hele invoer catalogus voor streaming, die een combinatie van video en audio alleen-lezen bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="12f4c-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="12f4c-216">In dit scenario wanneer Hallo invoer geen video heeft kunt u tooforce Hallo encoder tooinsert een video monochroom bijhouden op net Hallo laagste bitrate, als tegengestelde tooinserting video op elke bitrate uitvoer.</span><span class="sxs-lookup"><span data-stu-id="12f4c-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="12f4c-217">tooachieve, moet u toouse hello **InsertBlackIfNoVideoBottomLayerOnly** vlag.</span><span class="sxs-lookup"><span data-stu-id="12f4c-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="12f4c-218">U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:</span><span class="sxs-lookup"><span data-stu-id="12f4c-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="12f4c-219">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="12f4c-220">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-220">XML preset</span></span>

<span data-ttu-id="12f4c-221">Wanneer u XML, gebruikt u voorwaarde = 'InsertBlackIfNoVideoBottomLayerOnly' als een kenmerk toohello **H264Video** -element en de voorwaarde 'InsertSilenceIfNoAudio' te als een kenmerk =**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="12f4c-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="12f4c-222">Video helemaal invoegen uitvoer bitsnelheden</span><span class="sxs-lookup"><span data-stu-id="12f4c-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="12f4c-223">Stel dat u gebruikt een meerdere bitrate encoding preset zoals [' standaardinstelling H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode uw hele invoer catalogus voor streaming, die een combinatie van video en audio alleen-lezen bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="12f4c-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="12f4c-224">In dit scenario wanneer Hallo invoer geen video heeft kunt u tooforce Hallo encoder tooinsert monochroom video op alle Hallo uitvoer bitsnelheden bijhouden.</span><span class="sxs-lookup"><span data-stu-id="12f4c-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="12f4c-225">Dit zorgt ervoor dat de uitvoer activa zijn alle homogene met toonumber ten opzichte van houdt video en audio houdt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="12f4c-226">tooachieve, moet u toospecify Hallo 'InsertBlackIfNoVideo' vlag.</span><span class="sxs-lookup"><span data-stu-id="12f4c-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="12f4c-227">U kunt een van de Hallo MES standaardinstellingen gedocumenteerd in nemen [dit](media-services-mes-presets-overview.md) uit en breng Hallo wijziging:</span><span class="sxs-lookup"><span data-stu-id="12f4c-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="12f4c-228">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="12f4c-229">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-229">XML preset</span></span>

<span data-ttu-id="12f4c-230">Wanneer u XML, gebruikt u voorwaarde = 'InsertBlackIfNoVideo' als een kenmerk toohello **H264Video** -element en de voorwaarde 'InsertSilenceIfNoAudio' te als een kenmerk =**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="12f4c-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="12f4c-231"><a id="rotate_video"></a>Een video draaien</span><span class="sxs-lookup"><span data-stu-id="12f4c-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="12f4c-232">Hallo [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) draaihoek door hoeken van 0/90/180/270 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="12f4c-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="12f4c-233">Hallo standaardgedrag is 'Auto', waarbij toodetect Hallo rotatie metagegevens in de binnenkomende videobestand Hallo probeert en compenseren voor het.</span><span class="sxs-lookup"><span data-stu-id="12f4c-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="12f4c-234">Neem de volgende Hallo **bronnen** element tooone van Hallo standaardinstellingen die zijn gedefinieerd in [dit](media-services-mes-presets-overview.md) sectie:</span><span class="sxs-lookup"><span data-stu-id="12f4c-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="12f4c-235">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="12f4c-236">XML-definitie</span><span class="sxs-lookup"><span data-stu-id="12f4c-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="12f4c-237">Zie ook [dit](media-services-mes-schema.md#PreserveResolutionAfterRotation) onderwerp voor meer informatie over hoe Hallo encoder worden geïnterpreteerd Hallo breedte en hoogte-instellingen in Hallo definitie wanneer rotatie compensatie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="12f4c-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="12f4c-238">U kunt Hallo waarde '0' tooindicate toohello encoder tooignore rotatie van de metagegevens, indien aanwezig, in Hallo invoervideo.</span><span class="sxs-lookup"><span data-stu-id="12f4c-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="12f4c-239">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="12f4c-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="12f4c-240">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="12f4c-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="12f4c-241">Zie ook</span><span class="sxs-lookup"><span data-stu-id="12f4c-241">See Also</span></span>
[<span data-ttu-id="12f4c-242">Media Services-codering overzicht</span><span class="sxs-lookup"><span data-stu-id="12f4c-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
