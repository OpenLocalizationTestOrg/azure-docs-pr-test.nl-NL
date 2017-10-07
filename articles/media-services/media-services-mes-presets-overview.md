---
title: aaaTask standaardinstellingen voor MES (Media Encoder Standard) | Microsoft Docs
description: Hallo onderwerp biedt en overzicht van de standaardinstellingen van de taak voor MES (Media Encoder Standard).
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Taak standaardinstellingen voor MES (Media Encoder Standard)

**Media Encoder Standard** definieert een aantal standaardinstellingen die u gebruiken kunt bij het maken van codering taken codering. Het verdient aanbeveling toouse Hallo 'Adaptief streamen' voorinstelling als u wilt dat een video tooencode voor streaming met Media Services. Wanneer u opgeeft in deze vooraf ingestelde, Media Encoder Standard wordt [automatisch genereren een ladder bitrate](media-services-autogen-bitrate-ladder-with-mes.md). 

Als u een codering voorinstelling toocustomize nodig hebt, moet u een van de standaardinstellingen in deze sectie is gedefinieerd als een sjabloon voor de configuratie van uw aangepaste codering Hallo houden. Zie voor uitleg van welke elk element in deze standaardinstellingen middelen en Hallo geldige waarden voor elk element Hallo [Media Encoder Standard schema](media-services-mes-schema.md) onderwerp.  
  
> [!NOTE]
>  Wanneer u een definitie voor 4k codeert, krijgt u Hallo `S3` eenheidstype gereserveerd. Zie voor meer informatie [hoe tooScale codering](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Als u werkt met Media Encoder Standard, wordt rotatie standaard ingeschakeld. Als uw video is vastgelegd op een smartphone of andere mobiele apparaten in de modus Staand en vervolgens deze standaardinstellingen standaard deze tooLandscape modus voorafgaande tooencoding draait, (in tegenstelling tot, wanneer u met Azure Media Encoder werkt, waarbij video te draaien een handmatige bewerking is, zoals beschreven in [dit](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog onder 'Video rotatie').  
  
Beschikbare standaardinstellingen:  
  
 [Geselecteerde instelling H264 Multiple Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) levert een set van 8 GOP uitgelijnde MP4-bestanden, variërend van 6000 kbps too400 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) levert een set van 8 GOP uitgelijnde MP4-bestanden, variërend van 6000 kbps too400 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 16 x 9 voor iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) levert een set van 8 GOP uitgelijnde MP4-bestanden, variërend van 8500 kbps too200 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 16 x 9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) levert een set van 5 GOP uitgelijnde MP4-bestanden, variërend van 1900 kbps too400 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) levert een set van 5 GOP uitgelijnde MP4-bestanden, variërend van 1900 kbps too400 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) levert een set 12 GOP uitgelijnde MP4-bestanden, variërend van 20000 kbps too1000 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) levert een set 12 GOP uitgelijnde MP4-bestanden, variërend van 20000 kbps too1000 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 4 x 3 voor iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) levert een set van 8 GOP uitgelijnde MP4-bestanden, variërend van 8500 kbps too200 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 4 x 3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) levert een set van 5 GOP uitgelijnde MP4-bestanden, variërend van 1600 kbps too400 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) levert een set van 5 GOP uitgelijnde MP4-bestanden, variërend van 1600 kbps too400 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) levert een set 6 GOP uitgelijnde MP4-bestanden, variërend van 3400 kbps too400 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) levert een set 6 GOP uitgelijnde MP4-bestanden, variërend van 3400 kbps too400 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produceert één MP4-bestand met een bitrate van 6750 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produceert één MP4-bestand met een bitrate van 6750 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produceert één MP4-bestand met een bitrate van 18000 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produceert één MP4-bestand met een bitrate van 18000 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 4 x 3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produceert één MP4-bestand met een bitrate van 1800 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 4 x 3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produceert één MP4-bestand met een bitrate van 1800 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 16 x 9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produceert één MP4-bestand met een bitrate van 2200 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 16 x 9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produceert één MP4-bestand met een bitrate van 2200 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produceert één MP4-bestand met een bitrate van 4500 kbps en AAC 5.1 audio.  
  
 [Geselecteerde instelling H264 Single-Bitrate 720p voor Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) voorinstelling produceert één MP4-bestand met een bitrate van 2000 kbps en aansluiting AAC.  
  
 [Geselecteerde instelling H264 Single-Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produceert één MP4-bestand met een bitrate van 4500 kbps en aansluiting AAC audio.  
  
 [Geselecteerde instelling H264 één bitsnelheid van hoge kwaliteit SD voor Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produceert één MP4-bestand met een bitrate van 500 kbps en stereogeluid AAC...  
  
 [Geselecteerde instelling H264 Single Bitrate lage kwaliteit SD voor Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produceert één MP4-bestand met een bitrate van 56 kbps en aansluiting AAC audio.  
  
 Zie voor meer informatie gerelateerde tooMedia Services coderingsprogramma's, [codering op aanvraag met Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
