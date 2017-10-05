---
title: Geselecteerde instelling H264 Single-Bitrate 720p Audio 5.1 | Microsoft Docs
description: Het onderwerp een overzicht van de ** standaardinstelling H264 Single-Bitrate 720p Audio 5.1* * taak definitie.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ba2bfa57-3c87-4b1b-b91b-58f9108f4e85
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 629ef7690f25dc6de1773a83cf967544cdf16682
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-720p-audio-51"></a><span data-ttu-id="8d6e5-103">Geselecteerde instelling H264 Single-Bitrate 720p Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="8d6e5-103">H264 Single Bitrate 720p Audio 5.1</span></span>
<span data-ttu-id="8d6e5-104">`Media Encoder Standard`definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="8d6e5-105">Kunt u ofwel een `preset name` om op te geven naar welke indeling u wilt uw mediabestand coderen.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="8d6e5-106">U kunt maken met uw eigen JSON of XML gebaseerde standaardinstellingen (met UTF-8- of UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="8d6e5-107">U zou geeft u het aangepaste vooraf ingesteld op de encoder.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="8d6e5-108">Voor een overzicht van de vooraf ingestelde namen ondersteund door dit `Media Encoder Standard` encoder, Zie [taak standaardinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d6e5-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="8d6e5-109">In dit onderwerp leest de `H264 Single Bitrate 720p Audio 5.1` vooraf in XML en JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-109">This topic shows the `H264 Single Bitrate 720p Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="8d6e5-110">Deze definitie produceert één MP4-bestand met een bitrate van 4500 kbps en AAC 5.1 audio.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="8d6e5-111">Voor gedetailleerde informatie over profiel bitrate, snelheid, enz. dit wordt vooraf ingesteld, controleert u de XML- of JSON zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="8d6e5-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="8d6e5-112">Zie voor een uitleg van elk element in welke betekent en de geldige waarden voor elk element, het [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="8d6e5-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="8d6e5-113">XML</span><span class="sxs-lookup"><span data-stu-id="8d6e5-113">XML</span></span>  
  
```  
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
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="8d6e5-114">JSON</span><span class="sxs-lookup"><span data-stu-id="8d6e5-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 4500,  
          "MaxBitrate": 4500,  
          "BufferWindow": "00:00:05",  
          "Width": 1280,  
          "Height": 720,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
```
