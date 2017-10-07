---
title: aaaH264 Single-Bitrate 1080p Audio 5.1 | Microsoft Docs
description: Hallo onderwerp een overzicht van Hallo ** standaardinstelling H264 Single-Bitrate 1080p Audio 5.1* * taak definitie.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: b42238de-2a3c-4683-ae7f-7ce19ad5162e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 8ee5f34f4fd84c615ca8c5e7554e9ec832f54a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-1080p-audio-51"></a><span data-ttu-id="cd966-103">Geselecteerde instelling H264 Single-Bitrate 1080p Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="cd966-103">H264 Single Bitrate 1080p Audio 5.1</span></span>
<span data-ttu-id="cd966-104">`Media Encoder Standard`definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering.</span><span class="sxs-lookup"><span data-stu-id="cd966-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="cd966-105">Kunt u ofwel een `preset name` toospecify naar welke indeling u tooencode wilt dat uw mediabestand.</span><span class="sxs-lookup"><span data-stu-id="cd966-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="cd966-106">U kunt maken met uw eigen JSON of XML gebaseerde standaardinstellingen (met UTF-8- of UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="cd966-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="cd966-107">U zou vervolgens Hallo aangepaste vooraf ingestelde toohello encoder doorgeven.</span><span class="sxs-lookup"><span data-stu-id="cd966-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="cd966-108">Voorinstelling voor Hallo lijst met alle Hallo namen die worden ondersteund door dit `Media Encoder Standard` encoder, Zie [taak standaardinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd966-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="cd966-109">In dit onderwerp leest Hallo `H264 Single Bitrate 1080p Audio 5.1` vooraf in XML en JSON-indeling...</span><span class="sxs-lookup"><span data-stu-id="cd966-109">This topic shows hello `H264 Single Bitrate 1080p Audio 5.1` preset in XML and JSON format..</span></span>  
  
 <span data-ttu-id="cd966-110">Deze definitie produceert één MP4-bestand met een bitrate van 6750 kbps en AAC 5.1 audio.</span><span class="sxs-lookup"><span data-stu-id="cd966-110">This preset produces a single MP4 file with a bitrate of 6750 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="cd966-111">Voor gedetailleerde informatie over het profiel bitrate, snelheid, enz. dit wordt vooraf ingestelde, onderzoekt Hallo XML- of JSON zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="cd966-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="cd966-112">Voor uitleg van elk element in welke betekent en Hallo geldige waarden voor elk element Zie Hallo [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cd966-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="cd966-113">XML</span><span class="sxs-lookup"><span data-stu-id="cd966-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>6750</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>6750</MaxBitrate>  
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
  
 <span data-ttu-id="cd966-114">JSON</span><span class="sxs-lookup"><span data-stu-id="cd966-114">JSON</span></span>  
  
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
          "Bitrate": 6750,  
          "MaxBitrate": 6750,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
          "Height": 1080,  
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
