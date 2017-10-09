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
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="840b2-103">Video’s bijsnijden met Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="840b2-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="840b2-104">U kunt uw invoervideo toocrop Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="840b2-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="840b2-105">Bijsnijden is Hallo proces een rechthoekig venster binnen Hallo video frame te selecteren en codering alleen Hallo pixels in dit venster.</span><span class="sxs-lookup"><span data-stu-id="840b2-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="840b2-106">Hallo volgende diagram kunt illustreren Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="840b2-106">hello following diagram helps illustrate hello process.</span></span>

![Een video bijsnijden](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="840b2-108">Stel dat u hebt een video die een resolutie van 1920 x 1080 pixels (hoogte-breedteverhouding 16:9), maar wel met balken (pillar vakken) op Hallo linker- en, zodat alleen een venster 4:3 of 1440 x 1080 pixels bevat actieve video als invoer.</span><span class="sxs-lookup"><span data-stu-id="840b2-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="840b2-109">U kunt MES toocrop gebruiken of uitgaand Hallo zwarte balken bewerken en coderen Hallo 1440 x 1080 regio.</span><span class="sxs-lookup"><span data-stu-id="840b2-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="840b2-110">Bijsnijden in MES is een vooraf verwerken fase, zodat Hallo bijsnijden parameters in Hallo codering voorinstelling toohello oorspronkelijke invoervideo toepassen.</span><span class="sxs-lookup"><span data-stu-id="840b2-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="840b2-111">Codering is een latere fase en Hallo breedte en hoogte-instellingen toepassen toohello *vooraf verwerkt* video en niet toohello oorspronkelijke video.</span><span class="sxs-lookup"><span data-stu-id="840b2-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="840b2-112">Bij het ontwerpen van uw vooraf ingestelde hebt u toodo Hallo volgende nodig: (a) selecteert Hallo bijsnijden parameters op basis van de oorspronkelijke invoervideo hello en (b) selecteert u uw instellingen op basis van Hallo bijgesneden video coderen.</span><span class="sxs-lookup"><span data-stu-id="840b2-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="840b2-113">Als u niet overeenkomt met uw instellingen toohello bijgesneden video coderen, Hallo uitvoer wordt niet zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="840b2-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="840b2-114">Hallo [volgende](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) onderwerp wordt beschreven hoe een codeertaak met MES toocreate en hoe toospecify een aangepaste voorinstelling voor codering taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="840b2-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="840b2-115">Maken van een aangepaste voorinstelling</span><span class="sxs-lookup"><span data-stu-id="840b2-115">Creating a custom preset</span></span>
<span data-ttu-id="840b2-116">In Hallo voorbeeld in Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="840b2-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="840b2-117">Oorspronkelijke invoer is 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="840b2-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="840b2-118">Het moet toobe bijgesneden tooan uitvoer van 1440 x 1080, die wordt gecentreerd in Hallo invoer frame</span><span class="sxs-lookup"><span data-stu-id="840b2-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="840b2-119">Dit betekent dat een X-verschuiving van (1920 – 1440) / 2 = 240 en een Y-verschuiving van nul</span><span class="sxs-lookup"><span data-stu-id="840b2-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="840b2-120">Hallo breedte en hoogte van Hallo bijsnijden rechthoek zijn 1440 1080, respectievelijk en</span><span class="sxs-lookup"><span data-stu-id="840b2-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="840b2-121">In Hallo coderen fase hello vragen tooproduce drie lagen is, zijn respectievelijk resoluties 1440 x 1080 960 x 720 en 480 x 360</span><span class="sxs-lookup"><span data-stu-id="840b2-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="840b2-122">JSON-definitie</span><span class="sxs-lookup"><span data-stu-id="840b2-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="840b2-123">Beperkingen voor bijsnijden</span><span class="sxs-lookup"><span data-stu-id="840b2-123">Restrictions on cropping</span></span>
<span data-ttu-id="840b2-124">Hallo bijsnijden functie bedoeld toobe handmatig.</span><span class="sxs-lookup"><span data-stu-id="840b2-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="840b2-125">U moet tooload uw invoer video in een geschikte bewerken hulpprogramma waarmee u frames van belang selecteren, plaatst u Hallo cursor toodetermine verschuivingen voor Hallo rechthoek bijsnijden, toodetermine Hallo codering voorinstelling die is afgestemd op die bepaalde video's, enzovoort. Deze functie is niet bedoeld voor tooenable zaken als: automatische detectie en verwijderen van de zwarte letterbox/pillarbox randen in uw invoervideo.</span><span class="sxs-lookup"><span data-stu-id="840b2-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="840b2-126">Volgende beperkingen van kracht toohello bijsnijden functie.</span><span class="sxs-lookup"><span data-stu-id="840b2-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="840b2-127">Als deze niet wordt voldaan, Hallo taak coderen kunt mislukt of er een onverwachte uitvoer geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="840b2-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="840b2-128">Hallo hebben coördinaten en de grootte van Hallo bijsnijden rechthoek toofit binnen Hallo invoervideo</span><span class="sxs-lookup"><span data-stu-id="840b2-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="840b2-129">Zoals eerder vermeld, Hallo breedte en hoogte in Hallo coderen instellingen hebben toocorrespond toohello bijgesneden video</span><span class="sxs-lookup"><span data-stu-id="840b2-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="840b2-130">Bijsnijden geldt toovideos vastgelegd in de liggende modus (d.w.z. niet van toepassing toovideos geregistreerd met een smartphone ondergebracht verticaal of in staand)</span><span class="sxs-lookup"><span data-stu-id="840b2-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="840b2-131">Het meest geschikt voor progressieve video vastgelegd met vierkante pixels</span><span class="sxs-lookup"><span data-stu-id="840b2-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="840b2-132">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="840b2-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="840b2-133">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="840b2-133">Next step</span></span>
<span data-ttu-id="840b2-134">Zie Azure Media Services paden toohelp die u meer informatie over de handige functies die worden aangeboden door AMS leren.</span><span class="sxs-lookup"><span data-stu-id="840b2-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
