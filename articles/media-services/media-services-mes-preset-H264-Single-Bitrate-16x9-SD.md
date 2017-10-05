---
title: Geselecteerde instelling H264 Single-Bitrate 16 x 9 SD Media Encoder Standard voorinstelling - Azure | Microsoft Docs
description: Het onderwerp een overzicht van de ** standaardinstelling H264 Single-Bitrate 16 x 9 SD ** taak definitie.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ce0efc07-3461-44f6-a7bc-c4877bc09529
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 746dc845f1e32d6be3f207448523d8966da9f8a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-16x9-sd"></a><span data-ttu-id="37057-103">Geselecteerde instelling H264 Single-Bitrate 16 x 9 SD</span><span class="sxs-lookup"><span data-stu-id="37057-103">H264 Single Bitrate 16x9 SD</span></span>
<span data-ttu-id="37057-104">`Media Encoder Standard`definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering.</span><span class="sxs-lookup"><span data-stu-id="37057-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="37057-105">Kunt u ofwel een `preset name` om op te geven naar welke indeling u wilt uw mediabestand coderen.</span><span class="sxs-lookup"><span data-stu-id="37057-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="37057-106">U kunt maken met uw eigen JSON of XML gebaseerde standaardinstellingen (met UTF-8- of UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="37057-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="37057-107">U zou geeft u het aangepaste vooraf ingesteld op de encoder.</span><span class="sxs-lookup"><span data-stu-id="37057-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="37057-108">Voor een overzicht van de vooraf ingestelde namen ondersteund door dit `Media Encoder Standard` encoder, Zie [taak standaardinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37057-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="37057-109">In dit onderwerp leest de `H264 Single Bitrate 16x9 SD` vooraf in XML en JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="37057-109">This topic shows the `H264 Single Bitrate 16x9 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="37057-110">Deze vooraf ingestelde produceert een enkel MP4-bestand met een bitrate van 2200 kbps en aansluiting AAC audio.</span><span class="sxs-lookup"><span data-stu-id="37057-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="37057-111">Voor gedetailleerde informatie over profiel bitrate, snelheid, enz. dit wordt vooraf ingesteld, controleert u de XML- of JSON zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="37057-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="37057-112">Zie voor uitleg van welke elk element in deze standaardinstellingen middelen en de geldige waarden voor elk element in de [Media Encoder Standard schema](media-services-mes-schema.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="37057-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="37057-113">XML</span><span class="sxs-lookup"><span data-stu-id="37057-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>2200</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>2200</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 <span data-ttu-id="37057-114">JSON</span><span class="sxs-lookup"><span data-stu-id="37057-114">JSON</span></span>  
  
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
          "Bitrate": 2200,  
          "MaxBitrate": 2200,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
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
```
