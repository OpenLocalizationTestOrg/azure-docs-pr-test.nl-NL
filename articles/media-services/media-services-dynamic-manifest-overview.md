---
title: aaaFilters en dynamische manifesten | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toocreate gefilterd zodat de client deze toostream specifieke secties in een stream kunt gebruiken. Media Services dynamische manifesten tooarchive deze selectief streaming wordt gemaakt.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filters en dynamische manifesten
Vanaf versie 2.11, kunt u Media Services toodefine filters voor de activa. Deze filters zijn server side regels waarmee uw klanten toochoose toodo zaken als: afspelen alleen een gedeelte van een video (in plaats van afgespeeld Hallo hele video), of geef alleen een subset van audio en video vertoningen dat uw klant apparaat kan omgaan met () in plaats van alle Hallo vertoningen die zijn gekoppeld aan Hallo asset). Via dit filteren van uw assets wordt gearchiveerd **dynamische Manifest**s die een video van uw klant aanvraag toostream zijn gemaakt op basis van opgegeven filter.

In dit onderwerp wordt besproken algemene scenario's waarin zeer nuttige tooyour klanten en koppelingen tootopics die laten zien hoe toocreate programmatisch filtert met filters zijn (op dit moment kunt u filters maken met de REST-API's alleen).

## <a name="overview"></a>Overzicht
Bij het leveren van uw inhoud toocustomers (live streaming-gebeurtenissen of video-on-demand) het doel is toodeliver een hoogwaardige video toovarious apparaten met verschillende netwerkomstandigheden. tooachieve deze doelstelling Hallo te volgen:

* Codeer uw stream toomulti-bitrate ([adaptive bitrate](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) videostream (Dit zorgt voor kwaliteit en netwerkomstandigheden) en 
* Media Services gebruiken [dynamische pakketten](media-services-dynamic-packaging-overview.md) toodynamically opnieuw inpakken van uw stream in verschillende protocollen (Dit zorgt voor streaming op verschillende apparaten). Media Services ondersteunt de levering van de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming- en MPEG DASH. 

### <a name="manifest-files"></a>Manifestbestanden
Wanneer u een asset voor adaptive bitrate streaming coderen een **manifest** ()-afspeellijstbestand wordt gemaakt (Hallo-bestand is op basis van tekst of XML-indeling). Hallo **manifest** bestand bevat metagegevens zoals streaming: type (audio-, video- of tekst) bijhouden, naam, begintijd en eindtijd, bitrate (kenmerken), bijhouden talen, presentatievenster (sliding window van vaste duur), video bijhouden codec (code). Hallo player tooretrieve Hallo volgende fragment worden ook via op basis van informatie over Hallo volgende afgespeeld video fragmenten beschikbaar en de locatie. Fragmenten (of segmenten) zijn werkelijke Hallo 'reeksen' van een video-inhoud.

Hier volgt een voorbeeld van een manifestbestand: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Dynamische manifesten
Er zijn [scenario's](media-services-dynamic-manifest-overview.md#scenarios) wanneer de client moet meer flexibiliteit dan wat wordt beschreven in het manifestbestand Hallo standaard asset. Bijvoorbeeld:

* Apparaat in een bepaalde: leveren alleen Hallo vertoningen en/of opgegeven opgegeven taal nummers die worden ondersteund door het Hallo-apparaat dat is gebruikt tooplayback Hallo inhoud ('weergave filteren'). 
* Verminder Hallo manifest tooshow een submap illustratie van een live gebeurtenis ('onderliggende clip filteren').
* Trim Hallo begin van een video ('een video bijsnijden').
* Aanpassen presentatie venster (DVR) in de volgorde tooprovide een beperkte tijdsduur Hallo DVR venster in Hallo player ('aanpassen presentatievenster').

tooachieve deze flexibiliteit, de Media Services-aanbiedingen **dynamische manifesten** gebaseerd op vooraf gedefinieerde [filters](media-services-dynamic-manifest-overview.md#filters).  Wanneer u filters Hallo definieert, kunt uw clients ze toostream een specifieke weergave of subquery illustraties van uw video. Deze zou filters in Hallo streaming-URL opgeven. Filters kunnen worden toegepast tooadaptive bitrate streaming-protocollen die worden ondersteund door [dynamische pakketten](media-services-dynamic-packaging-overview.md): HLS, MPEG DASH en Smooth Streaming. Bijvoorbeeld:

URL voor MPEG-DASH met filter

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

Smooth Streaming-URL met filter

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Voor meer informatie over het toodeliver inhoud en build streaming-URL's, Zie [leveren van inhoud overzicht](media-services-deliver-content-overview.md).

> [!NOTE]
> Houd er rekening mee dat dynamische manifesten niet Hallo asset wijzigen en Hallo standaardmanifest voor de activa. De client kunt toorequest een stream met of zonder filters. 
> 
> 

### <a id="filters"></a>Filters
Er zijn twee typen asset filters: 

* Globale filters (kan worden toegepast tooany activa in hello Azure Media Services-account, hebben een levensduur van het Hallo-account) en 
* Lokale filters (kan alleen worden toegepast tooan asset met welke Hallo filter gekoppeld nadat deze is gemaakt is, hebben een levensduur van Hallo asset). 

Globale en lokale filtertypen zijn exact dezelfde eigenschappen Hallo. Hallo belangrijkste verschil tussen Hallo twee is voor welke scenario's voor welk type een filer beter geschikt is. Globale filters in het algemeen geschikt zijn voor de apparaatprofielen (weergave filteren) waarin lokale filters gebruikte tootrim specifiek activum kunnen worden.

## <a id="scenarios"></a>Algemene scenario 's
Zoals is vermeld voordat wanneer het doel van uw inhoud toocustomers (live streaming-gebeurtenissen of video-on-demand) leveren toodeliver video van hoge kwaliteit toovarious apparaten onder verschillende omstandigheden netwerk. Daarnaast biedt de mogelijk andere vereisten die betrekking hebben op uw assets te filteren en het gebruik van hebben **dynamische Manifest**s. Hallo volgende secties geven een kort overzicht van scenario's voor verschillende filteren.

* Geef alleen een subset van audio en video vertoningen dat bepaalde apparaten kunnen verwerken (in plaats van alle Hallo vertoningen die gekoppeld aan Hallo asset zijn). 
* Alleen een gedeelte van een video (in plaats van afgespeeld Hallo hele video) afspelen.
* DVR presentatievenster aanpassen.

## <a name="rendition-filtering"></a>Weergave filteren
U kunt tooencode uw asset toomultiple codering profielen (H.264 basislijn H.264 hoog, AACL, AACH, Dolby Digital Plus) en meerdere kwaliteit bitsnelheden. Niet alle clientapparaten ondersteunen echter van uw asset profielen en bitsnelheden. Oudere Android-apparaten ondersteunt bijvoorbeeld alleen H.264 basislijn + AACL. Verzenden van hogere bitsnelheden tooa inrichting Hallo voordelen kan niet ophalen, verspild bandbreedte en apparaat berekening. Dit apparaat moet decoderen alle Hallo gegeven informatie alleen tooscale het naar beneden om weer te geven.

Met dynamische Manifest, kunt u profielen van apparaten zoals mobile, console, HD/SD, enz. en Hallo houdt en kenmerken die u wilt dat toobe een onderdeel van elk profiel.

![Voorbeeld van de weergave filteren][renditions2]

Hallo voorbeeld te volgen, is een coderingsprogramma gebruikte tooencode een activum tussentijds in zeven ISO MP4s video vertoningen (van too1080p 180p). Hallo gecodeerde asset dynamisch verpakken in een van de volgende streaming protocollen Hallo: HLS, Smooth en MPEG DASH.  Hallo bovenaan Hallo diagram in Hallo HLS voor Hallo activum zonder filters manifest wordt weergegeven (bevat alle zeven vertoningen).  In de linkerbenedenhoek hello, wordt Hallo die HLS toowhich een filter met de naam 'ott manifest' is toegepast weergegeven. Hallo 'ott' filter geeft tooremove alle bitsnelheden lager dan 1 Mbps, wat tot Hallo onder twee kwaliteitsniveaus worden verwijderd leidde uit in het Hallo-antwoord.  In Hallo rechtsonder, Hallo HLS manifest toowhich een filter met de naam 'mobiel' is toegepast weergegeven. Hallo 'mobiel' filter geeft tooremove vertoningen waar hello resolutie groter dan 720p, wat tot Hallo twee 1080p vertoningen worden verwijderd is leidde uit.

![Weergave filteren][renditions1]

## <a name="removing-language-tracks"></a>Taal verwijderen
Uw assets kunnen meerdere audio talen zoals Engels, Spaans, Frans, enzovoort bevatten. Normaal gesproken Hallo Windows Media Player SDK managers-nummer standaardselectie en audio beschikbaar houdt per Gebruikersselectie. Het moeilijk is toodevelop dergelijke Player SDK's, verschillende implementaties over apparaatspecifieke-frameworks voor spelers is vereist. Ook op sommige platformen Neem Player-API's zijn beperkt en geen audio selectie functie waar gebruikers niet selecteren of Hallo standaard-nummer wijzigen. U kunt met asset filters Hallo gedrag beheren door te maken van de filters die alleen de gewenste audio talen opnemen.

![Taal houdt filteren][language_filter]

## <a name="trimming-start-of-an-asset"></a>Hoe worden ingekort begin van een asset
Sommige tests voordat de werkelijke gebeurtenis Hallo is in de meeste live streaming-gebeurtenissen, operators uitvoeren. Ze bevatten bijvoorbeeld een lei als volgt vóór Hallo begin van de gebeurtenis Hallo: "Programma begint tijdelijk worden". Als het archiveren van Hallo programma is Hallo test en lei gegevens ook worden gearchiveerd en worden opgenomen in het Hallo-presentatie. Echter, deze informatie moet niet worden weergegeven toohello clients. U kunt maken van een tijdfilter start en Hallo ongewenste gegevens verwijderen uit Hallo manifest met dynamische Manifest.

![Hoe worden ingekort starten][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Maken van onderliggende illustraties (weergaven) van een live-archief
Veel live gebeurtenissen zijn uitgevoerd en live archief meerdere gebeurtenissen kan bevatten. Nadat Hallo live gebeurtenis ends omroeporganisaties wil toobreak up Hallo archief live in logische programma moet worden gestart en reeksen stoppen. Vervolgens publiceren afzonderlijk deze virtuele programma's zonder post Hallo live archief verwerking en afzonderlijke elementen (die krijgt geen voordeel van het bestaande in de cache fragmenten Hallo in Hallo CDN) niet maken. Voorbeelden van dergelijke virtuele programma's (onderliggende illustraties) zijn Hallo kwartalen van een football of basketbalwedstrijd, Hallo innings in baseball of afzonderlijke gebeurtenissen van een 's middags van Olympische programma.

U kunt met dynamische Manifest keren beginnen of eindigen met filters maken en virtuele weergaven maken via Hallo boven aan het live archief. 

![Filter subclip][subclip_filter]

Gefilterde Asset:

![Skiën][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Presentatievenster (DVR) aan te passen
Azure Media Services biedt momenteel cirkelvormige archief waarop Hallo-duur kan worden geconfigureerd tussen 5 minuten: 25 uur. Manifest filteren, kunt gebruikte toocreate een rolling DVR-venster worden via Hallo bovenaan Hallo-archief zonder te verwijderen van media. Er zijn veel scenario's waar omroeporganisaties tooprovide een beperkte DVR venster dat wordt verplaatst met Hallo live rand en op Hallo hetzelfde moment een grotere archiveren venster houden. Een tv-station kunt toouse Hallo gegevens die buiten het Hallo DVR venster toohighlight illustraties of he\she tooprovide verschillende DVR vensters wilt voor verschillende apparaten. De meeste mobiele apparaten Hallo niet bijvoorbeeld big DVR windows (u kunt een venster van de DVR 2 minuten voor mobiele apparaten en 1 uur voor bureaublad-clients hebt) te verwerken.

![DVR venster][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Het aanpassen van LiveBackoff (live positie)
Manifest filteren kan worden gebruikt tooremove enkele seconden van Hallo live rand van een live programma. Hierdoor omroeporganisaties toowatch Hallo presentatie op Hallo preview publicatie wijst en aankondiging maken invoegen punten voordat Hallo viewers ontvangen Hallo stroom (meestal een back-uitgeschakeld met 30 seconden). Omroeporganisaties kunnen vervolgens push deze frameworks advertenties tootheir client in de tijd voor deze informatie over een tooreceived en proces Hallo voordat Hallo aankondiging kans.

Bovendien toohello aankondiging ondersteunen, LiveBackoff kan worden gebruikt voor het aanpassen van de client downloaden van live positie zodat wanneer clients nemen en druk op Hallo live rand nog steeds krijgen fragmenten van server in plaats van het ophalen van 404 of 412 HTTP-fouten.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Combineren van meerdere regels in een enkel filter
U kunt meerdere regels voor filteren in één filter combineren. U kunt bijvoorbeeld een bereik regel tooremove lei uit een live-archief definiëren en ook filteren bitsnelheden beschikbaar. Resultaat is voor meerdere filteren regels Hallo end Hallo samenstelling (alleen snijpunt) van deze regels.

![meerdere regels][multiple-rules]

## <a name="create-filters-programmatically"></a>Programmatisch filters maken
Hallo Volgend onderwerp wordt beschreven Media Services-entiteiten die gerelateerd toofilters zijn. Hallo-onderwerp wordt ook beschreven hoe tooprogrammatically filters maken.  

[Filters maken met de REST-API's](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Combineren van meerdere filters (filter samenstelling)
U kunt ook meerdere filters in één URL van een combineren. 

Hallo volgende scenario wordt uitgelegd waarom kunt u filters toocombine:

1. U moet uw video kenmerken toofilter voor mobiele apparaten, zoals Android of iPAD (in volgorde toolimit video kenmerken). tooremove Hallo ongewenste kenmerken, maakt u een globaal filter die geschikt is voor de apparaatprofielen. Zoals eerder vermeld, globale filters kunnen worden gebruikt voor alle activa onder Hallo dezelfde media services-account zonder verdere is gekoppeld. 
2. U ook wilt tootrim Hallo start en eindtijd van een actief. tooachieve, zou u een lokale filter maken en Hallo start-/ eindtijd niet instellen. 
3. Gewenste toocombine van deze filters (combinatie zou u zonder moeten tooadd kwaliteit filteren toohello bijsnijden met het filter dat wordt moeilijker filter gebruik).

toocombine filters, moet u tooset Hallo filter namen toohello manifest/afspeellijst-URL met door puntkomma's gescheiden. Stel u hebt een filter met de naam *MyMobileDevice* die eigenschappen filters en hebt u een andere naam *MyStartTime* tooset een bepaalde tijd starten. U kunt ze combineren als volgt:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

U kunt combineren too3 filters gedefinieerd. 

Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a name="know-issues-and-limitations"></a>Kent problemen en beperkingen
* Dynamische manifest draait in GOP grenzen (sleutel Frames) daarom bijsnijden GOP nauwkeurig is. 
* U kunt dezelfde filternaam voor lokale en globale filters gebruiken. Houd er rekening mee dat lokale filter hebben een hogere prioriteit en globale filters overschrijven.
* Als u een filter bijwerkt, kan het streaming-eindpunt toorefresh Hallo regels too2 minuten duren. Als Hallo inhoud is uitgevoerd met behulp van een aantal filters (en in het cachegeheugen van proxy's en CDN caches), kan het bijwerken van deze filters leiden tot player-fouten. Is het beste tooclear Hallo cache na het bijwerken van Hallo filter. Als deze optie niet mogelijk is, kunt u overwegen een ander filter.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Het leveren van inhoud tooCustomers overzicht](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
