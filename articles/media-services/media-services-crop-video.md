---
title: Het bijsnijden video's met Media Encoder Standard - Azure | Microsoft Docs
description: In dit artikel laat zien hoe bijsnijden video's met Media Encoder Standard.
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
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="fe6d0-103">Video’s bijsnijden met Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="fe6d0-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="fe6d0-104">Media Encoder Standard (MES) kunt u uw invoer video bijsnijden.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="fe6d0-105">Bijsnijden is het proces van een rechthoekig venster in het kader van de video te selecteren en alleen de pixels in dit venster codering.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="fe6d0-106">Het volgende diagram kunt u het proces wordt verduidelijkt.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-106">The following diagram helps illustrate the process.</span></span>

![Een video bijsnijden](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="fe6d0-108">Stel dat u hebt als invoer een video die een resolutie van 1920 x 1080 pixels (hoogte-breedteverhouding 16:9), maar wel met balken (pillar vakken) op de links, rechts, zodat alleen een venster 4:3 of 1440 x 1080 pixels active video bevat.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="fe6d0-109">U kunt MES bijsnijden of bewerken van de zwarte balken gebruiken en de regio 1440 x 1080 coderen.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="fe6d0-110">Bijsnijden in MES is een vooraf verwerken fase, zodat de bijsnijden parameters in de codering voorinstelling op de oorspronkelijke invoer video toepassen.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="fe6d0-111">Codering is een latere fase en de breedte en hoogte-instellingen toepassen op de *vooraf verwerkt* video en niet naar de oorspronkelijke video.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="fe6d0-112">Bij het ontwerpen van uw vooraf ingestelde moet u de volgende handelingen uit: (a) Selecteer de bijsnijden parameters op basis van de oorspronkelijke invoervideo en (b) Selecteer de instellingen op basis van de bijgesneden video coderen.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="fe6d0-113">Als u niet overeenkomt met de instellingen op de bijgesneden video coderen, de uitvoer niet zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="fe6d0-114">De [volgende](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) onderwerp wordt beschreven hoe u een codeertaak maakt met MES en het opgeven van een aangepaste voorinstelling voor de codering taak.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="fe6d0-115">Maken van een aangepaste voorinstelling</span><span class="sxs-lookup"><span data-stu-id="fe6d0-115">Creating a custom preset</span></span>
<span data-ttu-id="fe6d0-116">In het voorbeeld weergegeven in het diagram:</span><span class="sxs-lookup"><span data-stu-id="fe6d0-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="fe6d0-117">Oorspronkelijke invoer is 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="fe6d0-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="fe6d0-118">Deze moeten worden bijgesneden voor uitvoer van 1440 x 1080, die in de invoer frame wordt gecentreerd</span><span class="sxs-lookup"><span data-stu-id="fe6d0-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="fe6d0-119">Dit betekent dat een X-verschuiving van (1920 – 1440) / 2 = 240 en een Y-verschuiving van nul</span><span class="sxs-lookup"><span data-stu-id="fe6d0-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="fe6d0-120">De breedte en hoogte van de rechthoek bijsnijden zijn 1440 1080, respectievelijk en</span><span class="sxs-lookup"><span data-stu-id="fe6d0-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="fe6d0-121">In de fase coderen de vraag is voor het produceren van drie lagen, respectievelijk resoluties 1440 x 1080 960 x 720 en 480 x 360 zijn</span><span class="sxs-lookup"><span data-stu-id="fe6d0-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="fe6d0-122">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="fe6d0-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="fe6d0-123">Beperkingen voor bijsnijden</span><span class="sxs-lookup"><span data-stu-id="fe6d0-123">Restrictions on cropping</span></span>
<span data-ttu-id="fe6d0-124">De functie bijsnijden is bedoeld om handmatig zijn.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="fe6d0-125">U moet uw invoervideo laden in een geschikte bewerken hulpprogramma waarmee u frames van belang selecteren, plaatst u de cursor om te bepalen verschuivingen voor de rechthoek bijsnijden om te bepalen van de codering definitie die is afgestemd op die bepaalde video's, enzovoort. Deze functie is niet bedoeld om in te schakelen, bijvoorbeeld: automatische detectie en verwijderen van de zwarte letterbox/pillarbox randen in uw invoervideo.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="fe6d0-126">Volgende beperkingen zijn van toepassing op de bijsnijden functie.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="fe6d0-127">Als deze niet wordt voldaan, kan de coderen taak mislukt of er een onverwachte uitvoer geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="fe6d0-128">De coördinaten en de grootte van de rechthoek bijsnijden hebben om te passen binnen de invoer video</span><span class="sxs-lookup"><span data-stu-id="fe6d0-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="fe6d0-129">Zoals eerder vermeld, moet de breedte en hoogte in de instellingen voor het coderen overeenkomen met de bijgesneden video</span><span class="sxs-lookup"><span data-stu-id="fe6d0-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="fe6d0-130">Bijsnijden geldt voor video's die zijn vastgelegd in de liggende modus (d.w.z. niet van toepassing op video's die zijn geregistreerd met een smartphone ondergebracht verticaal of horizontaal of verticaal gebruik)</span><span class="sxs-lookup"><span data-stu-id="fe6d0-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="fe6d0-131">Het meest geschikt voor progressieve video vastgelegd met vierkante pixels</span><span class="sxs-lookup"><span data-stu-id="fe6d0-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="fe6d0-132">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="fe6d0-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="fe6d0-133">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="fe6d0-133">Next step</span></span>
<span data-ttu-id="fe6d0-134">Azure Media Services-leertrajecten voor meer informatie over de handige functies die worden aangeboden door AMS zien.</span><span class="sxs-lookup"><span data-stu-id="fe6d0-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
