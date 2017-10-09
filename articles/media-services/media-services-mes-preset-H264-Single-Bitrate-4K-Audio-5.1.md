---
title: aaaH264 Single-Bitrate 4K Audio 5.1 | Microsoft Docs
description: Hallo onderwerp een overzicht van Hallo ** standaardinstelling H264 Single-Bitrate 4K Audio 5.1* * taak definitie.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 72cb95ac-2cd6-4ef4-9938-8f22cea04920
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8ed5d85a0c58eaa9b076be667f4499659d90b19e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k-audio-51"></a>Geselecteerde instelling H264 Single-Bitrate 4K Audio 5.1
`Media Encoder Standard`definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering. Kunt u ofwel een `preset name` toospecify naar welke indeling u tooencode wilt dat uw mediabestand. U kunt maken met uw eigen JSON of XML gebaseerde standaardinstellingen (met UTF-8- of UTF-16-codering. U zou vervolgens Hallo aangepaste vooraf ingestelde toohello encoder doorgeven. Voorinstelling voor Hallo lijst met alle Hallo namen die worden ondersteund door dit `Media Encoder Standard` encoder, Zie [taak standaardinstellingen voor Media Encoder Standard](media-services-mes-presets-overview.md).  
  
 In dit onderwerp leest Hallo `H264 Single Bitrate 4K Audio 5.1` voorinstelling (in XML en JSON-indeling).  
  
 Deze definitie produceert één MP4-bestand met een bitrate van 18000 kbps en AAC 5.1 audio. Voor gedetailleerde informatie over het profiel bitrate, snelheid, enz. dit wordt vooraf ingestelde, onderzoekt Hallo XML- of JSON zoals hieronder gedefinieerd. Voor uitleg van elk element in welke betekent en Hallo geldige waarden voor elk element Zie Hallo [Media Encoder Standard schema](media-services-mes-schema.md).  
  
> [!NOTE]
>  Krijgt u Hallo Premium gereserveerd eenheidstype met 4K worden gecodeerd. Zie voor meer informatie [hoe tooScale codering](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
 XML  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
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
  
 JSON  
  
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
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
