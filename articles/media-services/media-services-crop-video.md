---
title: aaaHow toocrop video's met Media Encoder Standard - Azure | Microsoft Docs
description: Dit artikel laat zien hoe toocrop video's met Media Encoder Standard.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a>Video’s bijsnijden met Media Encoder Standard
U kunt uw invoervideo toocrop Media Encoder Standard (MES). Bijsnijden is Hallo proces een rechthoekig venster binnen Hallo video frame te selecteren en codering alleen Hallo pixels in dit venster. Hallo volgende diagram kunt illustreren Hallo-proces.

![Een video bijsnijden](./media/media-services-crop-video/media-services-crop-video01.png)

Stel dat u hebt een video die een resolutie van 1920 x 1080 pixels (hoogte-breedteverhouding 16:9), maar wel met balken (pillar vakken) op Hallo linker- en, zodat alleen een venster 4:3 of 1440 x 1080 pixels bevat actieve video als invoer. U kunt MES toocrop gebruiken of uitgaand Hallo zwarte balken bewerken en coderen Hallo 1440 x 1080 regio.

Bijsnijden in MES is een vooraf verwerken fase, zodat Hallo bijsnijden parameters in Hallo codering voorinstelling toohello oorspronkelijke invoervideo toepassen. Codering is een latere fase en Hallo breedte en hoogte-instellingen toepassen toohello *vooraf verwerkt* video en niet toohello oorspronkelijke video. Bij het ontwerpen van uw vooraf ingestelde hebt u toodo Hallo volgende nodig: (a) selecteert Hallo bijsnijden parameters op basis van de oorspronkelijke invoervideo hello en (b) selecteert u uw instellingen op basis van Hallo bijgesneden video coderen. Als u niet overeenkomt met uw instellingen toohello bijgesneden video coderen, Hallo uitvoer wordt niet zoals verwacht.

Hallo [volgende](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) onderwerp wordt beschreven hoe een codeertaak met MES toocreate en hoe toospecify een aangepaste voorinstelling voor codering taak Hallo. 

## <a name="creating-a-custom-preset"></a>Maken van een aangepaste voorinstelling
In Hallo voorbeeld in Hallo diagram:

1. Oorspronkelijke invoer is 1920 x 1080
2. Het moet toobe bijgesneden tooan uitvoer van 1440 x 1080, die wordt gecentreerd in Hallo invoer frame
3. Dit betekent dat een X-verschuiving van (1920 – 1440) / 2 = 240 en een Y-verschuiving van nul
4. Hallo breedte en hoogte van Hallo bijsnijden rechthoek zijn 1440 1080, respectievelijk en
5. In Hallo coderen fase hello vragen tooproduce drie lagen is, zijn respectievelijk resoluties 1440 x 1080 960 x 720 en 480 x 360

### <a name="json-preset"></a>JSON-definitie
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a>Beperkingen voor bijsnijden
Hallo bijsnijden functie bedoeld toobe handmatig. U moet tooload uw invoer video in een geschikte bewerken hulpprogramma waarmee u frames van belang selecteren, plaatst u Hallo cursor toodetermine verschuivingen voor Hallo rechthoek bijsnijden, toodetermine Hallo codering voorinstelling die is afgestemd op die bepaalde video's, enzovoort. Deze functie is niet bedoeld voor tooenable zaken als: automatische detectie en verwijderen van de zwarte letterbox/pillarbox randen in uw invoervideo.

Volgende beperkingen van kracht toohello bijsnijden functie. Als deze niet wordt voldaan, Hallo taak coderen kunt mislukt of er een onverwachte uitvoer geproduceerd.

1. Hallo hebben coördinaten en de grootte van Hallo bijsnijden rechthoek toofit binnen Hallo invoervideo
2. Zoals eerder vermeld, Hallo breedte en hoogte in Hallo coderen instellingen hebben toocorrespond toohello bijgesneden video
3. Bijsnijden geldt toovideos vastgelegd in de liggende modus (d.w.z. niet van toepassing toovideos geregistreerd met een smartphone ondergebracht verticaal of in staand)
4. Het meest geschikt voor progressieve video vastgelegd met vierkante pixels

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Volgende stap
Zie Azure Media Services paden toohelp die u meer informatie over de handige functies die worden aangeboden door AMS leren.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
