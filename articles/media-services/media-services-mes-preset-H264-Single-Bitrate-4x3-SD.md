---
title: Single-Bitrate 4 x 3 SD Media Encoder Standard voorinstelling aaaH264 - Azure | Microsoft Docs
description: Hallo onderwerp een overzicht van Hallo ** standaardinstelling H264 Single-Bitrate 4 x 3 SD ** taak definitie.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 171689fe-7c4f-4d5a-b48e-281136d8ac97
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 212d76104b04217d99c1f199b63d3fe6c73b7419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4x3-sd"></a><span data-ttu-id="2f8e3-103">Geselecteerde instelling H264 Single-Bitrate 4 x 3 SD</span><span class="sxs-lookup"><span data-stu-id="2f8e3-103">H264 Single Bitrate 4x3 SD</span></span>
<span data-ttu-id="2f8e3-104">`Media Encoder Standard`definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="2f8e3-105">Kunt u ofwel een `preset name` toospecify naar welke indeling u tooencode wilt dat uw mediabestand.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="2f8e3-106">U kunt maken met uw eigen JSON of XML gebaseerde standaardinstellingen (met UTF-8- of UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="2f8e3-107">U zou vervolgens Hallo aangepaste vooraf ingestelde toohello encoder doorgeven.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="2f8e3-108">Voorinstelling voor Hallo lijst met alle Hallo namen die worden ondersteund door dit `Media Encoder Standard` encoder, Zie [taak standaardinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f8e3-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="2f8e3-109">In dit onderwerp leest Hallo `H264 Single Bitrate 4x3 SD` vooraf in XML en JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-109">This topic shows hello `H264 Single Bitrate 4x3 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="2f8e3-110">Deze vooraf ingestelde produceert een enkel MP4-bestand met een bitrate van 1800 kbps en aansluiting AAC audio.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-110">This preset produces a single MP4 file with a bitrate of 1800 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="2f8e3-111">Voor gedetailleerde informatie over het profiel bitrate, snelheid, enz. dit wordt vooraf ingestelde, onderzoekt Hallo XML- of JSON zoals hieronder gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="2f8e3-112">Zie voor uitleg van welke elk element in deze standaardinstellingen middelen en Hallo geldige waarden voor elk element Hallo [Media Encoder Standard schema](media-services-mes-schema.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="2f8e3-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="2f8e3-113">XML</span><span class="sxs-lookup"><span data-stu-id="2f8e3-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1800</Bitrate>  
          <Width>640</Width>  
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
          <MaxBitrate>1800</MaxBitrate>  
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
  
 <span data-ttu-id="2f8e3-114">JSON</span><span class="sxs-lookup"><span data-stu-id="2f8e3-114">JSON</span></span>  
  
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
          "Bitrate": 1800,  
          "MaxBitrate": 1800,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
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
