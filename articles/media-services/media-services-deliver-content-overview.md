---
title: de inhoud toocustomers aaaDelivering | Microsoft Docs
description: In dit onderwerp geeft een overzicht van wat is betrokken bij het leveren van uw inhoud met Azure Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Inhoud toocustomers leveren
Wanneer u uw inhoud toocustomers streamen of video-on-demand bevat, is het doel toodeliver hoogwaardige video toovarious apparaten met verschillende netwerkomstandigheden.

tooachieve deze doelstelling krijgen die u kunt:

* Codeer uw videostream van stroom tooa multi-bitrate (adaptieve bitrate). Dit zorgt voor kwaliteit en netwerkomstandigheden.
* Gebruik Microsoft Azure Media Services [dynamische pakketten](media-services-dynamic-packaging-overview.md) toodynamically opnieuw inpakken van uw stream in verschillende protocollen. Dit zorgt voor streaming op verschillende apparaten. Media Services ondersteunt de levering van de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming- en MPEG-DASH.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

In dit artikel biedt een overzicht van belangrijke contentlevering concepten.

bekende problemen, toocheck Zie [bekende problemen](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Dynamische verpakking
Dynamische hello-pakketten die Media Services biedt, dat kunt u uw adaptive bitrate MP4- of Smooth Streaming gecodeerde inhoud in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) leveren zonder toore-pakket in deze streaming-indelingen. We raden aan met het leveren van uw inhoud met dynamische pakketten.

tootake profiteren van dynamische pakketten hoeft u tooencode uw tussentijds (bron) bestand in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden.

Dynamische pakketten, opslaan en betaalt voor één opslagindeling Hallo bestanden. Media Services bouwt en levert de juiste reactie Hallo op basis van uw aanvragen.

Dynamische pakketten is beschikbaar voor standard en premium streaming-eindpunten. 

Zie voor meer informatie [dynamische pakketten](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filters en dynamische manifesten
U kunt filters definiëren voor de activa met Media Services. Deze filters zijn serverzijde regels waarmee uw klanten acties als het afspelen van een specifieke sectie van een video- of een subset van audio en video vertoningen dat uw klant apparaat kan verwerken (in plaats van alle Hallo vertoningen die gekoppeld aan asset Hallo zijn opgeven ). Dit filteren wordt bereikt door *dynamische manifesten* die worden gemaakt wanneer de klant toostream video op basis van een aanvragen of meer filters hebt opgegeven.

Zie voor meer informatie [Filters en dynamische manifesten](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Locators
tooprovide uw gebruikers met een URL die kan worden gebruikt toostream of uw inhoud downloaden, moet u eerst toopublish uw asset door een locator te maken. Een locator biedt een vermelding punt tooaccess Hallo bestanden in een asset. Media Services ondersteunt twee typen locators:

* OnDemandOrigin-locators. Deze zijn gebruikte toostream media (bijvoorbeeld MPEG DASH, HLS of Smooth Streaming) of bestanden progressief te downloaden.
* Locators voor Shared access signature (SAS)-URL. Dit zijn de gebruikte toodownload media-bestanden tooyour lokale computer.

Een *toegangsbeleid* gebruikte toodefine Hallo machtigingen op (zoals lezen, schrijven en lijst) is en duur waarvoor een client toegang voor een bepaalde asset heeft. Houd er rekening mee dat Hallo lijst machtiging (AccessPermissions.List) niet moet worden gebruikt bij het maken van een locator OrDemandOrigin.

Locators hebben een verloopdatum. Hello Azure-portal stelt een vervaldatum van 100 jaar in Hallo toekomstige voor locators.

> [!NOTE]
> Als u hello Azure portal toocreate locators vóór maart 2015 gebruikt, zijn deze locators tooexpire ingesteld na twee jaar.
> 
> 

tooupdate een vervaldatum op een locator, gebruik [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) of [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API's. Houd er rekening mee dat wanneer u de vervaldatum Hallo van een SAS-locator bijwerkt, Hallo URL gewijzigd.

Locators zijn niet ontworpen toomanage per gebruiker toegangsbeheer. U kunt verschillende toegang tooindividual gebruikers met rechten geven met behulp van oplossingen voor beheer van digitale rechten (DRM). Zie voor meer informatie [Media beveiligen](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Wanneer u een locator maakt, is er mogelijk een vertraging van 30 seconden vanwege toorequired opslag en doorgifte processen in Azure Storage.

## <a name="adaptive-streaming"></a>Adaptief streamen
Adaptive bitrate technologieën toestaan-speler toepassingen toodetermine netwerkomstandigheden en selecteer in meerdere bitsnelheden. Wanneer vermindert de netwerkcommunicatie kunt Hallo-client een lagere bitrate selecteren zodat afspelen kunt doorgaan met de lagere videokwaliteit. Als netwerkomstandigheden verbeteren, kunt Hallo client tooa hogere bitrate met verbeterde videokwaliteit overschakelen. Azure Media Services ondersteunt de volgende adaptive bitrate technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming- en MPEG-DASH.

tooprovide gebruikers met streaming-URL's, moet u eerst maken een OnDemandOrigin-locator. Hallo locator biedt u basispad toohello asset met daarin de inhoud Hallo Hallo maken u toostream. Echter, toobe kunnen toostream deze inhoud, moet u toomodify na dit pad verder. een volledige URL toohello manifestbestand streamen, moet u Hallo-locator pad samenvoegen tooconstruct (filename.ism) naam van waarde en Hallo manifestbestand. Voeg **/Manifest** en een geschikte indeling (indien nodig) toohello locator-pad.

> [!NOTE]
> U kunt ook de inhoud streamen via een SSL-verbinding. toodo, zorg ervoor dat uw streaming URL's starten met HTTPS. Houd er rekening mee dat op dit moment AMS biedt geen ondersteuning voor SSL met aangepaste domeinen.  
> 


U kunt alleen streamen via SSL als Hallo streaming-eindpunt van waaruit u uw inhoud wilt leveren na 10 September 2014 werd gemaakt. Als uw streaming-URL's zijn gebaseerd op het streaming-eindpunten die zijn gemaakt na 10 September 2014 Hallo bevat Hallo-URL 'streaming.mediaservices.windows.net'. Streaming-URL's die 'origin.mediaservices.windows.net' (oude Hallo-indeling bevatten) bieden geen ondersteuning voor SSL. Als de URL de oude indeling Hallo heeft en toobe kunnen toostream via SSL gewenste, maakt u een nieuwe streaming-eindpunt. URL's op basis van nieuwe streaming-eindpunt toostream uw inhoud via SSL hello gebruiken.

## <a name="streaming-url-formats"></a>Streaming-URL-indelingen
### <a name="mpeg-dash-format"></a>MPEG-DASH-indeling
{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=MPD-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Apple HTTP Live Streaming (HLS)-V4-indeling
{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Apple HTTP Live Streaming (HLS) V3-indeling
{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Apple HTTP Live Streaming (HLS)-indeling met alleen audio-filter
Alleen audio-nummers zijn standaard opgenomen in Hallo die HLS manifest. Dit is vereist voor Apple Store certificeringsinstantie voor mobiele netwerken. Als een client beschikt niet over voldoende bandbreedte of is verbonden via een verbinding 2G, switches afspelen in dit geval tooaudio alleen-lezen. Dit helpt tookeep inhoud zonder buffer streaming, maar er is geen video. In sommige scenario's mogelijk player buffer voorkeur worden via alleen audio. Als u tooremove Hallo alleen audio bijhouden wilt, Voeg **alleen audio = false** toohello URL.

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=m3u8-aapl-v3,audio-Only=False)

Zie voor meer informatie [ondersteuning voor dynamische samenstelling Manifest- en HLS uitvoer aanvullende functies](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Smooth Streaming-indeling
{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest

Voorbeeld:

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest

### <a id="fmp4_v20"></a>Smooth Streaming 2.0-manifest (verouderde manifest)
Standaard bevat manifest indeling Smooth Streaming Hallo herhaaldelijk label (r-code). Sommige spelers ondersteunen echter geen Hallo r-tag. Clients met deze spelers kunnen een indeling die wordt uitgeschakeld Hallo r-tag gebruiken:

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Progressief downloaden
Met progressief downloaden, kunt u beginnen met het afspelen van media voordat Hallo hele bestand is gedownload. U downloaden niet ISM * (isma ismv ismt of ismc)-bestanden progressief.

tooprogressively inhoud downloaden, Hallo OnDemandOrigin type locator. Hallo toont volgende voorbeeld Hallo-URL die is gebaseerd op Hallo OnDemandOrigin type locator:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

U moet elke gewenste toostream van Hallo oorsprong service voor progressief downloaden opslag versleuteld activa decoderen.

## <a name="download"></a>Downloaden
toodownload uw inhoud tooa client-apparaat, moet u een SAS-Locator maken. Hallo SAS-locator biedt u toegang krijgen tot toohello Azure Storage-container waarin het bestand zich bevindt. toobuild hello download-URL, u hebt het Hallo-bestandsnaam tooembed tussen Hallo host en SAS-handtekening.

Hallo toont volgende voorbeeld Hallo-URL die is gebaseerd op Hallo SAS-locator:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

Hallo overwegingen volgende van toepassing:

* U moet elke gewenste toostream van Hallo oorsprong service voor progressief downloaden opslag versleuteld activa decoderen.
* Een download die nog niet voltooid binnen de 12 uur zal mislukken.

## <a name="streaming-endpoints"></a>Streaming-eindpunten

Een streaming-eindpunt vertegenwoordigt een streaming-service die inhoud leveren kunt direct tooa client player toepassing of tooa content delivery network (CDN voor) verdere distributie. Hallo uitgaande stroom van een streaming-eindpunt-service is een live stream of een activum video-on-demand in uw Media Services-account. Er zijn twee soorten streaming-eindpunten, **standaard** en **premium**. Zie voor meer informatie [Streaming-eindpunten overzicht](media-services-streaming-endpoints-overview.md).

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

## <a name="known-issues"></a>Bekende problemen
### <a name="changes-toosmooth-streaming-manifest-version"></a>Wijzigingen tooSmooth Streaming versie van het clustermanifest
Conform de voordat Hallo juli 2016 servicerelease--wanneer de activa die is geproduceerd met Media Encoder Standard Media Encoder Premium werkstroom of Hallo eerdere Azure Media Encoder zijn gestreamd met behulp van dynamische pakketten--Hallo Smooth Streaming manifest geretourneerd tooversion 2.0. In versie 2.0 gebruik Hallo fragment duur niet Hallo zogenaamde herhalen (r)-tags. Bijvoorbeeld:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

In juli 2016 servicerelease hello voldoet Hallo gegenereerd Smooth Streaming manifest tooversion 2.2, met een fragment duur met herhalingen tags. Bijvoorbeeld:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Sommige Hallo verouderde Smooth Streaming-clients mogelijk niet ondersteund op Hallo herhaaldelijk tags en tooload Hallo manifest zal mislukken. toomitigate dit probleem kunt u Hallo verouderde manifest indelingsparameter **(indeling = fmp4 v20)** of bijwerken van de meest recente versie toohello van de client, die ondersteuning biedt voor herhaaldelijk labels. Zie voor meer informatie [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Verwante onderwerpen
[Media Services-locators na rolling opslagsleutels bijwerken](media-services-roll-storage-access-keys.md)

