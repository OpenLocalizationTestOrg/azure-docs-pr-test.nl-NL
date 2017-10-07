---
title: Azure Media Services aaaMicrosoft scenario's en beschikbaarheid van functies in datacenters | Microsoft Docs
description: In dit onderwerp vindt u informatie over Microsoft Azure Media Services-scenario's en over de beschikbaarheid van functies en services in datacenters.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Scenario's en de beschikbaarheid van Media Services-functies in datacenters

Microsoft Azure Media Services (AMS) kunt u toosecurely uploaden, opslaan, coderen en video of audio-inhoud van het pakket voor zowel op aanvraag en live streaming levering toovarious clients (bijvoorbeeld TV, PC en mobiele apparaten).

AMS draait in meerdere datacenters Hallo wereld. Deze datacenters worden gegroepeerd in toogeographic regio's, waardoor u flexibiliteit bij het kiezen waar toobuild uw toepassingen. U kunt bekijken Hallo [lijst met regio's en de locaties](https://azure.microsoft.com/regions/). 

Dit onderwerp bevat algemene scenario's voor het leveren van uw inhoud: [live](#live_scenarios) of [on-demand](#vod_scenarios). Hallo onderwerp bevat ook informatie over de beschikbaarheid van mediafuncties en services via datacenters.

## <a name="overview"></a>Overzicht

### <a name="prerequisites"></a>Vereisten

toostart met Azure Media Services, moet u de volgende Hallo hebben:

* Een Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com) voor meer informatie.
* Een Azure Media Services-account. Zie [Een account maken](media-services-portal-create-account.md) voor meer informatie.
* Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud heeft toobe in Hallo **met** status.

    Wanneer uw AMS-account is gemaakt, een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. toostart streaming van uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling, Hallo streaming-eindpunt heeft toobe in Hallo **met** status.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Veelgebruikte objecten bij het ontwikkelen van tegen Hallo AMS OData-model

Hallo volgende afbeelding ziet u enkele van de meest gebruikte Hallo-objecten bij het ontwikkelen van toepassingen met Media Services OData-model Hallo.

Klik op Hallo installatiekopie tooview het maximale grootte.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

U kunt hele model Hallo weergeven [hier](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Inhoud in de opslag beveiligen en Hallo streamingmedia leveren wissen (niet-versleutelde)

![VoD-werkstroom](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Upload een mediabestand van hoge kwaliteit naar een asset.

    Het verdient aanbeveling tooapply opslag versleuteling optie tooyour asset in volgorde tooprotect uw inhoud tijdens het uploaden en terwijl in rust in de opslag.
2. Codeer tooa set adaptive bitrate MP4-bestanden.

    Het is raadzaam om uw inhoud in rust voor uitvoer asset in volgorde tooprotect tooapply opslag versleuteling optie toohello.
3. Configureer het beleid voor de levering van assets (gebruikt voor dynamische pakketten).

    Als de opslag van uw asset is versleuteld, **moet** u een beleid voor assetlevering configureren.
4. Hallo asset publiceren door een OnDemand-locator te maken.
5. Stream de gepubliceerde inhoud.

Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>De inhoud in de opslag beveiligen, dynamisch versleutelde streamingmedia leveren

![Beveiligen met PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Upload een mediabestand van hoge kwaliteit naar een asset. Storage encryption optie toohello asset toepassen.
2. Codeer tooa set adaptive bitrate MP4-bestanden. Storage encryption optie toohello uitvoerasset toepassen.
3. Inhoud coderingssleutel voor Hallo asset die u toobe dynamisch worden versleuteld tijdens het afspelen wilt maken.
4. Configureer het autorisatiebeleid voor de inhoudssleutel.
5. Configureer het beleid voor de levering van assets (gebruikt door dynamische pakketten en dynamische versleuteling).
6. Hallo asset publiceren door een OnDemand-locator te maken.
7. Stream de gepubliceerde inhoud.

Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Media Analytics tooderive bruikbare inzicht in uw video's gebruiken

Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee het eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's. Zie [Overzicht van Azure Media Services Analytics](media-services-analytics-overview.md) voor meer informatie.

1. Upload een mediabestand van hoge kwaliteit naar een asset.
2. Uw video's verwerken met een Hallo Media Analytics-services die worden beschreven in Hallo [Media Analytics overzicht](media-services-analytics-overview.md) sectie.
3. Media Analytics-mediaprocessoren produceren MP4- of JSON-bestanden. Als een Mediaprocessor een MP4-bestand, kunt u Hallo bestand progressief downloaden. Als een Mediaprocessor een JSON-bestand, kunt u Hallo-bestand downloaden van hello Azure blob-opslag.

Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.

## <a name="deliver-progressive-download"></a>Een progressieve download leveren

1. Upload een mediabestand van hoge kwaliteit naar een asset.
2. Codeer tooa één MP4-bestand.
3. Hallo asset publiceren door een OnDemand- of SAS-locator te maken.

    Als u SAS-locator gebruikt, worden Hallo inhoud wordt gedownload van hello Azure blob-opslag. In dit geval hoeft niet toohave streaming-eindpunten in gestarte staat verkeert.
4. Download de inhoud op progressieve wijze.

## <a id="live_scenarios"></a>Evenementen live streamen 

1. Live-inhoud met verschillende protocollen voor live streamen opnemen (bijvoorbeeld RTMP of Smooth Streaming).
2. (Optioneel) Uw stream coderen in een stream met een adaptieve bitsnelheid.
3. Een voorbeeld van uw livestream bekijken.
4. Hallo leveren via algemene streaming protocollen (bijvoorbeeld MPEG DASH, Smooth, HLS) rechtstreeks tooyour klanten of tooa inhoud Delivery Network (CDN) voor verdere distributie.

    -of-

    Record- en store Hallo ingenomen inhoud in de volgorde toobe gestreamd later (Video-on-Demand).

Bij het uitvoeren van live streamen, kunt u een van de volgende Hallo van routes:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Werken met kanalen die een multi-bitrate livestream van on-premises encoders ontvangen (pass-through)

Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Hallo **pass-through** werkstroom.

![Live-werkstroom](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Zie [Werken met kanalen die een multi-bitrate livestream van on-premises coderingsprogramma’s ontvangen](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie.

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Werken met kanalen die zijn ingeschakeld tooperform live codering met Azure Media Services

Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Live Streaming-werkstroom waarbij een kanaal is ingeschakeld tooperform live codering met Media Services.

![Live-werkstroom](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Zie voor informatie over de beschikbaarheid van datacenters Hallo [beschikbaarheid](#availability) sectie.

## <a name="consuming-content"></a>Inhoud gebruiken

Azure Media Services biedt u hulpprogramma's voor Hallo moet toocreate rijke, dynamische clientspelertoepassingen voor de meeste platforms, waaronder: iOS-apparaten, Android-apparaten, Windows, Windows Phone, Xbox en Set-top vakken. Volgend onderwerp Hallo biedt koppelingen tooSDKs en Frameworks voor spelers die u kunt gebruiken toodevelop uw eigen clienttoepassingen die streamingmedia van Media Services kunnen gebruiken. Zie [Toepassingen voor het afspelen van video ontwikkelen](media-services-develop-video-players.md) voor meer informatie

## <a name="enabling-azure-cdn"></a>Azure CDN inschakelen

Media Services ondersteunt de integratie met Azure CDN. Voor meer informatie over Azure CDN tooenable Zie [hoe tooManage Streaming-eindpunten in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Een Media Services-account schalen

AMS-klanten kunnen streaming-eindpunten, de mediaverwerking en de opslag in hun AMS-accounts schalen.

* Media Services-klanten kunnen een **Standard**-streaming-eindpunt of een Premium-**streaming**-eindpunt kiezen. **Standard**-streaming-eindpunten zijn geschikt voor de meeste streaming-workloads. Het Hallo dezelfde functies als bevat een **Premium** automatisch streaming-eindpunten en kan worden geschaald uitgaande bandbreedte. 

    **Premium**-streaming-eindpunten zijn geschikt voor geavanceerde workloads omdat er gebruik wordt gemaakt van toegewezen, schaalbare bandbreedtecapaciteit. Klanten met een **Premium**-streaming-eindpunt krijgen standaard één streaming-eenheid (SU). Hallo streaming-eindpunt kan worden uitgebreid door SUs toe te voegen. Elke SU biedt extra bandbreedte capaciteit toohello toepassing. Voor meer informatie over het schalen van **Premium** Hallo streaming-eindpunten, Zie [streaming-eindpunten schalen](media-services-portal-scale-streaming-endpoints.md) onderwerp.

* Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt. U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**. Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type.

    Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden** (RUs). het aantal ingerichte RUs Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account.

    >[!NOTE]
    >RU's werken voor het parallel verwerken van alle media, waaronder indexeringstaken via Azure Media Indexer. Indexeringstaken worden echter niet sneller verwerkt met snellere gereserveerde eenheden, terwijl dit bij coderen wel het geval is.

    Zie [Mediaverwerking schalen](media-services-portal-scale-media-processing.md) voor meer informatie.
* U kunt ook uw Media Services-account schalen door storage accounts tooit toe te voegen. Elk opslagaccount is beperkt too500 TB. tooexpand uw opslag buiten de standaardbeperkingen hello, kunt u tooattach meerdere storage accounts tooa enkel Media Services-account. Zie [Opslagaccounts beheren](meda-services-managing-multiple-storage-accounts.md) voor meer informatie.

##<a id="availability"></a> De beschikbaarheid van Media Services-functies in datacenters

Deze sectie bevat informatie over de beschikbaarheid van Media Services-functies in datacenters.

### <a name="ams-accounts"></a>AMS-accounts

#### <a name="availability"></a>Beschikbaarheid

U kunt Media Services accounts maken in Hallo gebieden te volgen: Noord-Europa, West-Europa, VS-West, VS-Oost, Zuidoost-Azië, Oost-Azië, Japan-West, Japan-Oost, Brazilië-Zuid, India-West, Zuid-India en India, midden. 

### <a name="streaming-endpoints"></a>Streaming-eindpunten 

Media Services-klanten kunnen een **Standard**-streaming-eindpunt of een Premium-**streaming**-eindpunt kiezen. Zie voor meer informatie, Hallo [schalen](#scaling) sectie.

#### <a name="availability"></a>Beschikbaarheid

|Naam|Status|Datacenters
|---|---|---|
|Standard|Algemene beschikbaarheid|Alle|
|Premium|Algemene beschikbaarheid|Alle|

### <a name="live-encoding"></a>Live Encoding

#### <a name="availability"></a>Beschikbaarheid

Beschikbaar in alle datacenters, behalve in: Duitsland, Zuid-Brazilië, West-India, Zuid-India en Centraal-India. 

### <a name="encoding-media-processors"></a>Mediaprocessors coderen

AMS biedt twee coderingsprogramma's die op basis van behoefte kunnen worden gebruikt: **Media Encoder Standard** en **Media Encoder Premium Workflow**. Zie [Overzicht en een vergelijking van Azure-mediacoderingsprogramma's die op basis van behoefte kunnen worden gebruikt](media-services-encode-asset.md) voor meer informatie. 

#### <a name="availability"></a>Beschikbaarheid

|Naam van mediaprocessor|Status|Datacenters
|---|---|---|
|Media Encoder Standard|Algemene beschikbaarheid|Alle|
|Media Encoder Premium Workflow|Algemene beschikbaarheid|Overal behalve China|

### <a name="analytics-media-processors"></a>Mediaprocessors voor analyse

Media Analytics is een verzameling spraakonderdelen en visuele onderdelen waarmee eenvoudiger voor organisaties en bedrijven tooderive bruikbare inzichten aan hun video's. Zie [Overzicht van Azure Media Services Analytics](media-services-analytics-overview.md) voor meer informatie.

#### <a name="availability"></a>Beschikbaarheid

|Naam van mediaprocessor|Status|Datacenters
|---|---|---|
|Azure Media Face Detector|Preview|Alle|
|Azure Media Hyperlapse|Preview|Alle|
|Azure Media Indexer|Algemene beschikbaarheid|Alle|
|Azure Media Motion Detector|Preview|Alle|
|Azure Media OCR|Preview|Alle|
|Azure Media Redactor|Preview|Alle|
|Azure Media Stabilizer|Preview|Alle|
|Azure Media Video Thumbnails|Preview|Alle|
|Azure Media Indexer 2|Preview|Overal behalve China en regio federale overheid|

### <a name="protection"></a>Beveiliging

Microsoft Azure Media Services kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering. Zie [AMS-inhoud beveiligen](media-services-content-protection-overview.md) voor meer informatie.

#### <a name="availability"></a>Beschikbaarheid

|Versleuteling|Status|Datacenters|
|---|---|---| 
|Storage|Algemene beschikbaarheid|Alle|
|AES-128-sleutels|Algemene beschikbaarheid|Alle|
|FairPlay|Algemene beschikbaarheid|Alle|
|PlayReady|Algemene beschikbaarheid|Alle|
|Widevine|Algemene beschikbaarheid|Overal behalve in Duitsland, bij overheden en in China.

### <a name="reserved-units-rus"></a>Gereserveerde eenheden (RU's)

het aantal ingerichte gereserveerde eenheden Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account. 

Zie voor meer informatie, Hallo [schalen](#scaling) sectie.

#### <a name="availability"></a>Beschikbaarheid

Beschikbaar in alle datacenters.

### <a name="reserved-unit-ru-type"></a>Gereserveerde-eenheidstype (RU)

Een Media Services-account is gekoppeld aan een gereserveerde eenheidstype, waarmee wordt bepaald Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt. U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: S1, S2 of S3.

Zie voor meer informatie, Hallo [schalen](#scaling) sectie.

#### <a name="availability"></a>Beschikbaarheid

|RU-typenaam|Status|Datacenters
|---|---|---|
|S1|Algemene beschikbaarheid|Alle|
|S2|Algemene beschikbaarheid|Overal behalve in Zuid-Brazilië en West-India|
|S3|Algemene beschikbaarheid|Overal behalve in West-India|

## <a name="next-steps"></a>Volgende stappen

Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

