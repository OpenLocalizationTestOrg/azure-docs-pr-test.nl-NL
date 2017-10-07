---
title: aaaComparison van Azure op aanvraag media encoders | Microsoft Docs
description: Dit onderwerp worden Hallo codering mogelijkheden van ** Media Encoder Standard ** en ** Media Encoder Premium werkstroom **.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: ee04ad10d8e7c5f4f3c6e91e9b7679c2aba82c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Vergelijking van Azure op aanvraag media coderingsprogramma 's

Dit onderwerp worden Hallo codering mogelijkheden van **Media Encoder Standard** en **Media Encoder Premium werkstroom**.

## <a name="video-and-audio-processing-capabilities"></a>Mogelijkheden voor de verwerking van video en audio

Hallo volgende tabel vergelijkt Hallo functionaliteit tussen Media Encoder Standard (MES) en Media Encoder Premium werkstroom (MEPW). 

|Mogelijkheid|Media Encoder Standard|Media Encoder Premium Workflow|
|---|---|---|
|Voorwaardelijke logica wordt toegepast tijdens het coderen<br/>(bijvoorbeeld als invoer Hallo HD is, klikt u vervolgens coderen 5.1 audio)|Nee|Ja|
|Ondertiteling|Nee|[Ja](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Correctie van Dolby® Professional volume](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> met de dialoog Intelligence™|Nee|Ja|
|Deselecteer ineengestrengeld, inverse telecine|Basic|Quality-broadcast|
|Detecteren en zwarte randen verwijderen <br/>(pillarboxes postbussen)|Nee|Ja|
|Genereren van miniaturen|[Ja](media-services-dotnet-generate-thumbnail-with-mes.md)|[Ja](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|Knippen/inkorten en foto van video 's|[Ja](media-services-advanced-encoding-with-mes.md#trim_video)|Ja|
|Overlays van audio en video|[Ja](media-services-advanced-encoding-with-mes.md#overlay)|[Ja](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|Overlays van afbeeldingen|Van de installatiekopie van bronnen|Afbeelding en de tekst bronnen|
|Meerdere audio taal|Beperkt|[Ja](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>Facturering meter gebruikt door elke encoder
| De naam van de Media-Processor | Geldende prijzen | Opmerkingen |
| --- | --- | --- |
| **Media Encoder Standard** |CODERING |Codering taken worden in rekening gebracht op basis van Hallo totale duur in minuten, alle Hallo mediabestanden geproduceerd als uitvoer met Hallo frequentie opgegeven [hier][1], onder Hallo ENCODER kolom. |
| **Media Encoder Premium Workflow** |PREMIUM-CODERING |Codering taken worden in rekening gebracht op basis van Hallo totale duur in minuten, alle Hallo mediabestanden geproduceerd als uitvoer met Hallo frequentie opgegeven [hier][1], onder Hallo PREMIUM ENCODER kolom. |

## <a name="input-containerfile-formats"></a>Invoer container/bestandsindelingen
| Invoer Container/bestandsindelingen | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| Adobe® Flash® F4V |Ja |Ja |
| MXF/SMPTE 377M |Ja |Ja |
| GXF |Ja |Ja |
| Streams MPEG-2-Transport |Ja |Ja |
| Streams MPEG-2-programma |Ja |Ja |
| MPEG-4/MP4 |Ja |Ja |
| Windows Media/AVP |Ja |Ja |
| AVI (niet-gecomprimeerde 8-bits/10 bits) |Ja |Ja |
| 3GPP/3GPP2 |Ja |Nee |
| Smooth Streaming-bestandsindeling (PIFF 1.3) |Ja |Nee |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) |Ja |Nee |
| Matroska/WebM |Ja |Nee |
| QuickTime (MOV) |Ja |Nee |

## <a name="input-video-codecs"></a>Video-codecs invoer
| Video-Codecs invoer | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| AVC 8-bits/10-bits, up too4:2:2, met inbegrip van AVCIntra |8-bits 4:2:0 en 4:2:2 |Ja |
| Avid DNxHD (in MXF) |Ja |Ja |
| DVCPro/DVCProHD (in MXF) |Ja |Ja |
| JPEG2000 |Ja |Ja |
| MPEG-2 (too422 profiel en een hoog niveau, inclusief varianten zoals XDCAM, XDCAM HD, XDCAM IMX, CableLabs® en D10) |Profiel voor de too422 van |Ja |
| MPEG-1 |Ja |Ja |
| Windows Media Video/VC-1 |Ja |Ja |
| Canopus hoofdkantoor/HQX |Nee |Nee |
| MPEG-4 Part 2 |Ja |Nee |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Ja |Nee |
| Apple ProRes 422 |Ja |Nee |
| Apple ProRes 422 LT |Ja |Nee |
| Apple ProRes 422 hoofdkantoor |Ja |Nee |
| Apple ProRes Proxy |Ja |Nee |
| Apple ProRes 4444 |Ja |Nee |
| Apple ProRes 4444 XQ |Ja |Nee |

## <a name="input-audio-codecs"></a>Audio-invoer codecs
| Audio-invoer Codecs | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| AES (SMPTE 331 M en 302 M, AES3 2003) |Nee |Ja |
| Dolby® E |Nee |Ja |
| Dolby® digitale (AC3) |Nee |Ja |
| Dolby® digitale Plus (E-AC3) |Nee |Ja |
| AAC (AAC Kredietbrief AAC HE en AAC-HEv2; up too5.1) |Ja |Ja |
| MPEG-laag 2 |Ja |Ja |
| MP3 (MPEG-1 Audio laag 3) |Ja |Ja |
| Windows Media Audio |Ja |Ja |
| WAV PCM / |Ja |Ja |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Ja |Nee |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |Ja |Nee |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Ja |Nee |

## <a name="output-containerfile-formats"></a>Container per bestand uitvoerindelingen
| Container per bestand uitvoerindelingen | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| Adobe® Flash® F4V |Nee |Ja |
| MXF (OP1a, XDCAM en AS02) |Nee |Ja |
| DPP (inclusief AS11) |Nee |Ja |
| GXF |Nee |Ja |
| MPEG-4/MP4 |Ja |Ja |
| MPEG-TS |Ja |Ja |
| Windows Media/AVP |Nee |Ja |
| AVI (niet-gecomprimeerde 8-bits/10 bits) |Nee |Ja |
| Smooth Streaming-bestandsindeling (PIFF 1.3) |Nee |Ja |

## <a name="output-video-codecs"></a>Video-codecs uitvoer
| Video-Codecs uitvoer | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| AVC (H.264; 8-bits; omhoog tooHigh profiel niveau 5.2; Ultra HD 4K; AVC Intra) |Alleen 8 bits 4:2:0 |Ja |
| Avid DNxHD (in MXF) |Nee |Ja |
| MPEG-2 (too422 profiel en een hoog niveau, inclusief varianten zoals XDCAM, XDCAM HD, XDCAM IMX, CableLabs® en D10) |Nee |Ja |
| MPEG-1 |Nee |Ja |
| Windows Media Video/VC-1 |Nee |Ja |
| Maken van JPEG-miniaturen |Ja |Ja |
| Maken van miniaturen PNG |Ja |Ja |
| Maken van miniaturen BMP |Ja |Nee |

## <a name="output-audio-codecs"></a>Audio-codecs uitvoer
| Audio-Codecs uitvoer | Media Encoder Standard | Media Encoder Premium Workflow |
| --- | --- | --- |
| AES (SMPTE 331 M en 302 M, AES3 2003) |Nee |Ja |
| Dolby® digitale (AC3) |Nee |Ja |
| Dolby® Digital Plus (E-AC3) up too7.1 |Nee |Ja |
| AAC (AAC Kredietbrief AAC HE en AAC-HEv2; up too5.1) |Ja |Ja |
| MPEG-laag 2 |Nee |Ja |
| MP3 (MPEG-1 Audio laag 3) |Nee |Ja |
| Windows Media Audio |Nee |Ja |

>[!NOTE]
>Als u tooDolby coderen® digitale (AC3) Hallo uitvoer kan alleen worden geschreven in een ISO MP4-bestand.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Verwante artikelen:
* [Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen](media-services-custom-mes-presets-with-dotnet.md)
* [Quota's en beperkingen](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
