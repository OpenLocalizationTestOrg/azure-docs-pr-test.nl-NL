---
title: aaaAzure Media Services dynamische pakketten overzicht | Microsoft Docs
description: Hallo onderwerp biedt en overzicht van dynamische pakketten.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Dynamische verpakking
## <a name="overview"></a>Overzicht
Microsoft Azure Media Services kunnen worden gebruikt toodeliver veel media bron bestandsindelingen, media streaming-indelingen en beveiliging van inhoud indelingen tooa verschillende technologieën van de client (bijvoorbeeld iOS-, XBOX, Silverlight, Windows 8). Deze clients begrijpen verschillende protocollen, bijvoorbeeld iOS een HTTP Live Streaming (HLS)-V4-indeling heeft en Silverlight en Xbox vereisen Smooth Streaming. Als u een set adaptive bitrate (multi-bitrate) hebt MP4-bestanden (ISO Base Media 14496-12) of een set adaptive bitrate Smooth Streaming-bestanden die u wilt dat tooserve tooclients die MPEG DASH, HLS of Smooth Streaming begrijpen, moet u ook te profiteren van Media Services dynamische pakketten.

Met dynamische verpakking alles wat die u nodig is toocreate een asset die een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden bevat. Vervolgens, op basis van de opgegeven indeling in het manifest Hallo Hallo of fragment aanvraag, Hallo On-Demand Streaming server zorgt ervoor dat u Hallo stream ontvangt in Hallo protocol dat u hebt gekozen. Hierdoor hoeft u alleen toostore en betalen voor Hallo-bestanden in één opslagindeling en Media Services-service bouwt en levert de juiste reactie Hallo op basis van aanvragen van een client.

Hallo volgende diagram toont Hallo traditionele codering en werkstroom voor statische pakketten.

![Statische codering](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Hallo toont volgende diagram Hallo dynamische pakketten werkstroom.

![Dynamische codering](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Gangbare scenario
1. Upload een invoerbestand (een tussentijds bestand genoemd). Bijvoorbeeld, H.264 MP4 of WMV (Zie voor een lijst met ondersteunde indelingen Hallo [indelingen ondersteund door de Media Encoder Standard Hallo](media-services-media-encoder-standard-formats.md).
2. Codeer uw tussentijds bestand tooH.264 MP4 adaptive bitrate sets.
3. Publiceer Hallo asset met Hallo adaptive bitrate MP4-set Hallo On Demand Locator maken.
4. Hallo streaming-URL's tooaccess bouwen en de inhoud streamen.

## <a name="preparing-assets-for-dynamic-streaming"></a>Activa voorbereiden voor dynamische streaming
tooprepare uw asset voor dynamische streaming-u hebt twee opties:

1. [Een master-bestand uploaden](media-services-dotnet-upload-files.md).
2. [Hallo Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets gebruiken](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [De inhoud streamen](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>De opmaak die niet worden ondersteund door dynamische pakketten
Hallo worden volgende bron indelingen niet ondersteund voor dynamische pakketten.

* Dolby digitale mp4-bestanden.
* Dolby digitale smooth bestanden.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

