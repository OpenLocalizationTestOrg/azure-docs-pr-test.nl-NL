---
title: aaaOverview en vergelijking van Azure op vraag media coderingsprogramma's | Microsoft Docs
description: In dit onderwerp biedt een overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma's.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Overzicht en een vergelijking van Azure op aanvraag media coderingsprogramma 's
## <a name="encoding-overview"></a>Overzicht van de codering
Azure Media Services biedt meerdere opties voor het Hallo-codering van media in Hallo cloud.

Wanneer u begint met Media Services, is het belangrijk toounderstand Hallo verschil tussen codecs en bestandsindelingen.
Codecs zijn Hallo-software die Hallo compressie/decompressie algoritmen implementeert dat bestandsindelingen zijn containers waarin Hallo gecomprimeerd video.

Media Services biedt dynamische pakketten zodat u uw adaptive bitrate MP4- of Smooth Streaming inhoud gecodeerde in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) toodeliver zonder dat u hoeft toore-pakket in een van deze streaming-indelingen.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. tootake profiteren van [dynamische pakketten](media-services-dynamic-packaging-overview.md), hebt u toodo Hallo volgende nodig:
>
>Bovendien moet u uw bronbestand coderen in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden (Hallo coderingsstappen worden verderop in deze zelfstudie uitgelegd).

Media Services ondersteunt de volgende Hallo op aanvraag coderingsprogramma's die worden beschreven in dit artikel:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

Dit artikel bevat een kort overzicht van op verzoek media coderingsprogramma's en koppelingen tooarticles waarmee u meer gedetailleerde informatie bevat. Hallo-onderwerp bevat ook een vergelijking van Hallo coderingsprogramma's.

>[!NOTE]
>Standaard hebben elke Media Services-account een actieve codering taak tegelijk. Meerdere codering taken gelijktijdig uitgevoerd, één voor elke codering gereserveerde eenheid die u hebt gekocht, kunt u codering eenheden waarmee u toohave reserveren. Zie voor informatie [codering eenheden schalen](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-toouse"></a>Hoe toouse
[Hoe tooencode met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Indelingen
[Indelingen en codecs](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Standaardinstellingen
Media Encoder Standard is geconfigureerd met behulp van een Hallo encoder standaardinstellingen beschreven [hier](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Invoer en uitvoer van metagegevens
Hallo encoders invoer metagegevens wordt beschreven [hier](media-services-input-metadata-schema.md).

Hallo encoders uitvoer metagegevens wordt beschreven [hier](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Genereren van miniaturen
Zie voor informatie [hoe toogenerate miniaturen met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Trim video's (paginaknipsel)
Zie voor informatie [hoe tootrim video's met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Overlays maken
Zie voor informatie [hoe toocreate overlays met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Zie ook
[Hallo Media Services-blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Media Encoder Premium Workflow
### <a name="overview"></a>Overzicht
[Inleiding tot Premium codering in Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Hoe toouse
Werkstroom voor Media Encoder Premium is geconfigureerd met behulp van complexe werkstromen. Werkstroombestanden kan worden gemaakt en bijgewerkt met Hallo [Workflow Designer](media-services-workflow-designer.md) hulpprogramma.

[Hoe tooUse Premium codering in Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Bekende problemen
Als uw invoervideo bevat geen ondertiteling, uitvoer Hallo dat Asset bevatten nog steeds een leeg TTML-bestand.


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Verwante artikelen:
* [Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen](media-services-custom-mes-presets-with-dotnet.md)
* [Quota's en beperkingen](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
