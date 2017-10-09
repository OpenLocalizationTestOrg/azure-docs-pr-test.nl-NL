---
title: aaaAzure Media Services Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen (FAQ's)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Veelgestelde vragen

In dit artikel komen Veelgestelde vragen die worden gegenereerd door de gebruikersgemeenschap van hello Azure Media Services (AMS).

## <a name="general-ams-faqs"></a>Algemene AMS Veelgestelde vragen
V: hoe u de schaal van indexeren?

A: Hallo gereserveerde eenheden zijn hello dezelfde voor codering en taken te indexeren. Volg de instructies op [hoe tooScale met gereserveerde Coderingseenheden](media-services-scale-media-processing-overview.md). **Opmerking** prestaties van de indexeerfunctie wordt niet beïnvloed door gereserveerde eenheidstype.

V: ik geüpload, gecodeerd en u een video gepubliceerd. Wat Hallo reden Hallo video zou zijn niet afgespeeld wanneer ik probeer toostream deze?

A: een van de meest voorkomende redenen is er geen streaming-eindpunt van waaruit u tooplayback in Hallo probeert Hallo Hallo **met** status.  

V: kan ik samenstellen op een live stream doen?

A: samenstellen op live gegevensstromen is momenteel niet beschikbaar in Azure Media Services, dus u toopre moet-opstellen op uw computer.

V: kan ik Azure CDN gebruiken met Live Streaming

A: Media Services ondersteunt de integratie met Azure CDN (Zie voor meer informatie [hoe tooManage Streaming-eindpunten in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)).  U kunt Live streamen met CDN. Azure Media Services biedt Smooth Streaming, HLS en MPEG-DASH-uitvoer. Alle deze indelingen HTTP gebruiken voor het overbrengen van gegevens en voordelen van het HTTP-caching krijgen. In live streaming werkelijke video en audio-gegevens is onderverdeeld toofragments en deze afzonderlijke fragmenten ophalen in de cache opgeslagen in CDN. Alleen gegevens behoeften toobe vernieuwd is Hallo manifest gegevens. CDN worden regelmatig vernieuwd manifest gegevens.

V: biedt Azure Media services ondersteuning voor installatiekopieën van opslaan?

A: als u alleen toostore JPEG of PNG-afbeeldingen zoekt, moet u die in Azure Blob Storage behouden. Er is geen voordeel tooputting die ze op in uw Media Services-account, tenzij u ze die zijn gekoppeld aan uw Video of Audio activa tookeep wilt. Of als u nodig toouse Hallo afbeeldingen als overlays in Hallo video encoder wellicht. Media Encoder Standard ondersteunt hierbij afbeeldingen boven op video's en dat deze lijsten JPEG- en PNG-ondersteunde indelingen invoer. Zie voor meer informatie [Overlays maken](media-services-advanced-encoding-with-mes.md#overlay).

V: hoe kan ik de activa van een Media Services-account tooanother kopiëren.

A: toocopy activa van een Media Services-account tooanother met .NET, gebruik [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) uitbreidingsmethode beschikbaar in Hallo [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) opslagplaats. Zie voor meer informatie [dit](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.

V: wat zijn Hallo-ondersteunde tekens voor het benoemen van bestanden wanneer u werkt met AMS?

A: Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan. waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '. Bovendien kunnen alleen er een '.' Hallo bestandsnaamextensie.

V: hoe tooconnect met behulp van REST?

A: voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI. 

V: hoe kan ik een video draaien tijdens Hallo proces codering.

A: Hallo [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) draaihoek door hoeken van 180-90/270 ondersteunt. Hallo standaardgedrag is 'Auto', waarbij toodetect Hallo rotatie metagegevens in Hallo binnenkomende MP4/MOV-bestand probeert en compenseren voor het. Neem de volgende Hallo **bronnen** element tooone van Hallo json standaardinstellingen gedefinieerd [hier](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
