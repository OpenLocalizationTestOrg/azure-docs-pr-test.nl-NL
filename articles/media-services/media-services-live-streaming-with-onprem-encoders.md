---
title: aaaStream live met lokale coderingsprogramma's die multi-bitrate streams - Azure maken | Microsoft Docs
description: 'Dit onderwerp wordt beschreven hoe tooset van een kanaal dat u een multi-bitrate ontvangt livestream van een on-premises coderingsprogramma. Hallo stream kan vervolgens worden geleverd tooclient afspelen toepassingen via een of meer streaming-eindpunten, met behulp van een Hallo adaptieve streaming protocollen te volgen: HLS, Smooth Streaming streepje.'
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Live streamen met on-premises-coderingsprogramma's die multi-bitrate streams maken
## <a name="overview"></a>Overzicht
In Azure Media Services een *kanaal* vertegenwoordigt een pijplijn voor het verwerken van inhoud live-streaming. Een kanaal ontvangt live invoer gegevensstromen in twee manieren:

* Een on-premises live codering verzendt een multi-bitrate RTMP of Smooth Streaming (gefragmenteerde MP4) stroom toohello kanaal dat is niet ingeschakeld tooperform live codering met Media Services. Hallo ingenomen streams pass through-kanalen zonder verdere verwerking. Deze methode wordt aangeroepen *pass-through*. U kunt Hallo volgende live coderingsprogramma's die multi-bitrate Smooth Streaming als uitvoer hebt: Media Excel, Ateme, stel communicatie, Envivio, Cisco en Elemental. Hallo volgende live coderingsprogramma's hebben RTMP als uitvoer: Adobe Flash Live Mediacoderingsprogramma, Telestream Wirecast Haivision, Teradek en TriCaster. Een live coderingsprogramma kan ook een single-bitrate stream tooa kanaal dat niet is ingeschakeld voor live codering verzenden, maar niet aangeraden. Media Services biedt Hallo stroom toocustomers die deze vragen.

  > [!NOTE]
  > Een Pass Through-methode is de meest voordelige manier Hallo toodo live te streamen.


* Een on-premises live codering verzendt een single-bitrate stream toohello kanaal dat is ingeschakeld tooperform live codering met Media Services in een Hallo volgende indelingen: RTP (MPEG-TS), RTMP of Smooth Streaming (gefragmenteerde MP4). Hallo kanaal voert vervolgens live codering van Hallo binnenkomende single-bitrate stream tooa multi-bitrate (adaptieve) videostream. Media Services biedt Hallo stroom toocustomers die deze vragen.

Vanaf Media Services 2.10 Hallo release, wanneer u een kanaal maakt, kunt u opgeven hoe u wilt dat de invoerstroom van kanaal tooreceive Hallo. U kunt ook opgeven of u wilt dat Hallo kanaal tooperform live codering van uw stream. U hebt hiervoor twee opties:

* **Doorgeven**: deze waarde opgeven als u van plan bent toouse een on-premises live coderingsprogramma die een multi-bitrate stream (Pass Through-stream) als uitvoer hebben. In dit geval Hallo binnenkomende stream wordt doorgegeven via toohello zonder alle codering. Dit is Hallo gedrag van een kanaal vóór Hallo 2.10 release. In dit onderwerp biedt informatie over het werken met kanalen van dit type.
* **Live Encoding**: Kies deze waarde als u van plan toouse Media Services tooencode uw single-bitrate livestream tooa multi-bitrate stream bent. Houd er rekening mee dat als u een live codering kanaal in een **met** staat, worden kosten. Het is raadzaam uw actieve kanalen onmiddellijk te beëindigen nadat uw live-streaming-gebeurtenis is voltooid tooavoid extra per uur kosten. Media Services biedt Hallo stroom toocustomers die deze vragen.

> [!NOTE]
> In dit onderwerp worden de kenmerken van de kanalen die niet zijn ingeschakeld tooperform live codering. Zie voor informatie over het werken met kanalen die zijn ingeschakeld tooperform live codering, [Live streamen met Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).
>
>

Hallo volgende diagram geeft een live-streaming-werkstroom die gebruikmaakt van een lokale live coderingsprogramma toohave multi-bitrate RTMP of gefragmenteerde MP4 (Smooth Streaming) streams als uitvoer.

![Live-werkstroom][live-overview]

## <a id="scenario"></a>Algemeen scenario voor live-streaming
Hallo volgende stappen worden de taken beschreven die zijn betrokken bij het maken van algemene toepassingen voor live-streaming.

1. Sluit een videocamera tooa-computer. Start en configureer een on-premises live coderingsprogramma dat een multi-bitrate RTMP of gefragmenteerde MP4 (Smooth Streaming) stroom als uitvoer. Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.

    U kunt deze stap ook uitvoeren nadat u uw kanaal hebt gemaakt.
2. Een kanaal maken en starten.

3. URL voor opnemen ophalen Hallo kanaal.

    Hallo live coderingsprogramma gebruikt Hallo opnemen URL toosend Hallo stroom toohello kanaal.
4. Hallo kanaal preview URL niet ophalen.

    Gebruik deze URL tooverify dat Hallo livestream goed door het kanaal wordt ontvangen.
5. Maak een programma.

    Wanneer u hello Azure-portal gebruikt, een programma maken ook een asset gemaakt.

    Als u Hallo SDK voor .NET of REST gebruikt, kunt u een asset toocreate moet en geeft toouse dit activum bij het maken van een programma.
6. Hallo asset die is gekoppeld aan het Hallo-programma publiceren.   

    >[!NOTE]
    >Wanneer uw Azure Media Services-account is gemaakt, een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud heeft toobe in Hallo **met** status.

7. Start Hallo programma wanneer u bent klaar toostart streamen en te archiveren.

8. Hallo live coderingsprogramma kan desgewenst gesignaleerde toostart een advertentie zijn. Hallo advertentie wordt ingevoegd in de uitvoerstroom Hallo.

9. Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.

10. Verwijder Hallo programma (en verwijder desgewenst Hallo asset).     

## <a id="channel"></a>Beschrijving van een kanaal en de bijbehorende onderdelen
### <a id="channel_input"></a>Channel-invoer (opnemen) configuraties
#### <a id="ingest_protocols"></a>Streaming-opnameprotocol
Media Services ondersteunt live-feeds opnemen met behulp van multi-bitrate gefragmenteerd MP4 en multi-bitrate RTMP als protocollen voor streaming. Wanneer Hallo RTMP opnemen streaming-protocol is ingeschakeld, worden twee eindpunten (invoer) opnemen voor Hallo kanaal worden gemaakt:

* **Primaire URL**: Hiermee geeft u op Hallo volledige URL van de primaire RTMP Hallo-kanaal eindpunt opnemen.
* **Secundaire URL** (optioneel): Hiermee geeft u op Hallo volledige URL van de secundaire RTMP Hallo-kanaal eindpunt opnemen.

Gebruik secundaire Hallo-URL als u wilt dat tooimprove Hallo duurzaamheid en Foutentolerantie van uw opnemen stroom (evenals encoder failover en Foutentolerantie), met name voor Hallo volgen scenario's:

- Één encoder double pushen tooboth primaire en secundaire URL's:

    Hallo belangrijkste doel van dit scenario is tooprovide meer tolerantie toonetwork schommelingen en geleidelijk. Sommige RTMP coderingsprogramma's niet verwerken netwerk goed wordt verbroken. Als een netwerk verbinding verbreken gebeurt, kan een coderingsprogramma stoppen met coderen en verzend de Hallo buffer opgeslagen gegevens niet in als een reconnect gebeurt. Dit zorgt ervoor dat wijzigingen en verlies van gegevens. Netwerk wordt verbroken vanwege een onjuiste netwerk of onderhoud kan gebeuren op Hallo Azure aan clientzijde. Primaire en secundaire URL's Hallo netwerkproblemen verkleinen en te profiteren van een gecontroleerde upgradeproces. Telkens wanneer een geplande netwerk verbinding verbreken gebeurt, Media Services beheert Hallo primaire en secundaire verbroken en biedt een vertraagde tussen twee Hallo verbreken. Tijd tookeep verzenden van gegevens zijn vervolgens coderingsprogramma's en deze opnieuw. Hallo-volgorde van Hallo verbroken kan willekeurig, maar er is een vertraging optreden tussen primaire en secundaire of secundaire/primaire URL's. In dit scenario is Hallo encoder nog steeds Hallo potentieel risico.

- Meerdere coderingsprogramma's, met elke encoder pushen tooa toegewezen beheerpunt:

    Dit scenario biedt zowel codering en redundantie voor opnemen. In dit scenario encoder1 pushes toohello primaire URL en encoder2 pushes toohello secundaire URL. Wanneer een coderingsprogramma is mislukt, kunt hello andere encoder houden verzenden van gegevens. Redundantie van de gegevens kan worden beheerd omdat Media Services niet primaire en secundaire URL's op Hallo verbroken wordt hetzelfde moment. Dit scenario wordt ervan uitgegaan dat coderingsprogramma's gesynchroniseerd zijn en exact bieden dezelfde gegevens Hallo.  

- Meerdere encoders double pushen tooboth primaire en secundaire URL's:

    In dit scenario push beide coderingsprogramma's gegevens tooboth primaire en secundaire URL's. Dit biedt Hallo best betrouwbaarheid en fouttolerantie, evenals gegevensredundantie. In dit scenario kan tolereren beide storingen van de codering en de verbinding verbreekt, zelfs als een encoder niet meer werkt. Hierbij wordt ervan uitgegaan dat coderingsprogramma's gesynchroniseerd zijn en precies bieden Hallo dezelfde gegevens.  

Zie voor meer informatie over het live coderingsprogramma's RTMP [Azure Media Services RTMP-ondersteuning en Live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>URL's (eindpunten) voor opnemen
Een kanaal biedt een invoereindpunt (de URL voor opnemen) dat u in Hallo live codering, opgeeft zodat Hallo encoder kunt push streams tooyour kanalen.   

U krijgt Hallo URL's voor opnemen wanneer u Hallo kanaal hebt gemaakt. Voor u tooget deze URL's, Hallo kanaal heeft geen toobe in Hallo **met** status. Wanneer u klaar toostart toohello gegevenskanaal worden gepusht bent, Hallo kanaal moet Hallo **met** status. Nadat het Hallo-kanaal wordt gestart ophalen van gegevens, kunt u uw stream via de voorbeeld-URL Hallo bekijken.

Hebt u een optie voor het opnemen van een gefragmenteerde MP4 (Smooth Streaming) livestream via een SSL-verbinding. tooingest via SSL, zorg ervoor dat tooupdate hello tooHTTPS URL voor opnemen. U kan niet op dit moment RTMP opnemen via SSL.

#### <a id="keyframe_interval"></a>Keyframe interval
Wanneer u een lokale live coderingsprogramma toogenerate multi-bitrate stream, bevat Hallo keyframe interval Hallo duur van Hallo groep afbeeldingen (GOP) gebruikt door deze externe encoder. Nadat Hallo-kanaal deze binnenkomende stroom ontvangen, u kunt leveren uw live stream tooclient afspelen toepassingen in een van de volgende indelingen Hallo: Smooth Streaming, dynamische adaptief streamen via HTTP-(KOPPELTEKEN) en HTTP Live Streaming (HLS). Wanneer u bezig bent met het live streamen wordt dynamisch HLS altijd geleverd. Standaard berekend automatisch Hallo HLS segment verpakking verhouding (fragmenten per segment) op basis van Hallo keyframe interval dat ontvangen van het live coderingsprogramma Hallo Media Services.

Hallo volgende tabel ziet u hoe Hallo segment duur wordt berekend:

| Keyframe interval | HLS segment verpakking verhouding (FragmentsPerSegment) | Voorbeeld |
| --- | --- | --- |
| Kleiner dan of gelijk zijn aan too3 seconden |3:1 |Als KeyFrameInterval (of GOP) 2 seconden, is Hallo HLS segment verpakking breedteverhouding 3 too1. Hiermee maakt u een HLS 6 seconde segment. |
| 3 too5 seconden |2:1 |Als KeyFrameInterval (of GOP) 4 seconden, is Hallo HLS segment verpakking breedteverhouding 2 too1. Hiermee maakt u een HLS-segment 8 seconde. |
| Meer dan 5 seconden |1:1 |Als KeyFrameInterval (of GOP) 6 seconden, is Hallo HLS segment verpakking breedteverhouding 1 too1. Hiermee maakt u een HLS 6 seconde segment. |

U kunt wijzigen Hallo fragmenten per segment verhouding door de uitvoer en de instelling FragmentsPerSegment op ChannelOutputHls configureren Hallo-kanaal.

U kunt ook Hallo keyframe intervalwaarde door Hallo KeyFrameInterval eigenschap op ChanneInput wijzigen. Als u KeyFrameInterval expliciet is ingesteld, Hallo HLS segment verpakking verhouding die fragmentspersegment wordt berekend via Hallo regels die hierboven is beschreven.  

Als u zowel KeyFrameInterval als FragmentsPerSegment expliciet instelt, gebruikt Media Services Hallo-waarden die u instelt.

#### <a name="allowed-ip-addresses"></a>Toegestane IP-adressen
U kunt Hallo IP-adressen die zijn toegestaan toopublish video toothis kanaal definiëren. Een toegestane IP-adres kan worden opgegeven als een van de volgende Hallo:

* Een enkel IP-adres (bijvoorbeeld: 10.0.0.1)
* Een IP-adresbereik die gebruikmaakt van een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22)
* Een IP-adresbereik die gebruikmaakt van een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld 10.0.0.1(255.255.252.0))

Als geen IP-adressen zijn opgegeven en er geen regeldefinitie bestaat, wordt geen IP-adres toegestaan. tooallow elk IP-adres, maakt u een regel en stelt u 0.0.0.0/0.

### <a name="channel-preview"></a>Kanaal preview
#### <a name="preview-urls"></a>Voorbeeld-URL 's
Kanalen bieden een preview-eindpunt (preview URL) toopreview te gebruiken en uw stream te valideren voordat verdere verwerking en levering.

Wanneer u Hallo kanaal hebt gemaakt, kunt u de voorbeeld-URL Hallo ophalen. Voor u tooget Hallo URL Hallo kanaal heeft geen toobe in Hallo **met** status. Nadat het Hallo-kanaal wordt gestart ophalen van gegevens, kunt u uw stream bekijken.

Op dit moment Hallo preview stroom kan worden geleverd alleen in gefragmenteerde MP4 (Smooth Streaming) indeling, ongeacht Hallo invoertype opgegeven. U kunt Hallo [Smooth Streaming Health Monitor](http://smf.cloudapp.net/healthmonitor) player tootest Hallo smooth stream. Ook kunt u een speler die is gehost in Azure portal tooview Hallo uw stream.

#### <a name="allowed-ip-addresses"></a>Toegestane IP-adressen
U kunt definiëren Hallo IP-adressen die zijn toegestaan tooconnect toohello preview-eindpunt. Als geen IP-adressen worden opgegeven, wordt elk IP-adres krijgt. Een toegestane IP-adres kan worden opgegeven als een van de volgende Hallo:

* Een enkel IP-adres (bijvoorbeeld: 10.0.0.1)
* Een IP-adresbereik die gebruikmaakt van een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22)
* Een IP-adresbereik die gebruikmaakt van een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>Kanaal-uitvoer
Zie voor informatie over channel uitvoer Hallo [Keyframe interval](#keyframe_interval) sectie.

### <a name="channel-managed-programs"></a>Programma's van Channel beheerd
Een kanaal is gekoppeld aan programma's die u toocontrol Hallo publiceren en opslaan van segmenten in een live stream kunt gebruiken. Kanalen beheren programma's. Hallo is kanaal- en programma-relatie heel vergelijkbaar tootraditional media, waarbij een kanaal een constante stream met inhoud heeft en een programma bereik toosome getimede gebeurtenis op dat kanaal.

Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **archiefvenster** lengte. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur. Lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Programma's kunnen uitvoeren in de opgegeven tijdsduur hello, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elk programma dat is gekoppeld aan een asset die Hallo gestreamde inhoud is opgeslagen. Een asset is toegewezen tooa blok-blob-container in hello Azure storage-account en Hallo-bestanden in Hallo activa zijn opgeslagen als blobs in de container. toopublish hello programma zodat uw klanten Hallo stream kunnen bekijken, moet u een OnDemand-locator voor Hallo gekoppeld asset maken. U kunt deze locator toobuild een streaming-URL die u tooyour clients kunt leveren.

Een kanaal biedt ondersteuning voor maximaal toothree gelijktijdig actieve programma's, zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. U kunt publiceren en archiveren van verschillende onderdelen van een gebeurtenis naar behoefte. Stel bijvoorbeeld dat uw bedrijf nodig tooarchive zes uur van een programma, maar alleen Hallo toobroadcast afgelopen 10 minuten is. tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate. Een programma wordt ingesteld tooarchive zes uur van Hallo gebeurtenis, maar Hallo programma wordt niet gepubliceerd. Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

Gebruik bestaande programma's niet voor nieuwe gebeurtenissen. Maak in plaats daarvan een nieuw programma voor elke gebeurtenis. Start Hallo programma wanneer u bent klaar toostart streamen en te archiveren. Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.

toodelete gearchiveerde inhoud, stoppen en Hallo programma verwijderen en verwijder vervolgens de gekoppelde asset Hallo. Een asset kan niet worden verwijderd als deze wordt gebruikt door een programma. Hallo programma moet eerst worden verwijderd.

Zelfs na het stoppen en verwijderen van programma hello, kunnen gebruikers de gearchiveerde inhoud als video op aanvraag streamen, totdat u Hallo-asset verwijderd. Als u tooretain Hallo gearchiveerde inhoud wilt, maar niet langer voor streaming beschikbaar, verwijdert u Hallo streaming-locator.

## <a id="states"></a>Kanaal statussen en facturering
Mogelijke waarden voor de huidige status van een kanaal Hallo zijn:

* **Gestopt**: dit Hallo beginstatus Hallo-kanaal is na het maken ervan. Hallo kanaaleigenschappen kunnen worden bijgewerkt in deze toestand is, maar streaming is niet toegestaan.
* **Starten van**: Hallo kanaal wordt gestart. In deze status zijn streaming en updates niet toegestaan. Als er een fout optreedt Hallo kanaal toohello retourneert **gestopt** status.
* **Met**: Hallo kanaal live gegevensstromen kan verwerken.
* **Stoppen van**: Hallo-kanaal is wordt gestopt. In deze status zijn streaming en updates niet toegestaan.
* **Verwijderen van**: Hallo kanaal wordt verwijderd. In deze status zijn streaming en updates niet toegestaan.

Hallo volgende tabel toont hoe kanaal kaart toohello facturering modus staat.

| Kanaalstatus | Portal indicatoren van de gebruikersinterface | In rekening gebracht? |
| --- | --- | --- | --- |
| **Starten** |**Starten** |Nee (overgangsstatus) |
| **Uitgevoerd** |**Gereed** (Er zijn geen actieve programma)<p><p>of<p>**Streaming** (ten minste één actieve programma) |Ja |
| **Stoppen** |**Stoppen** |Nee (overgangsstatus) |
| **Gestopt** |**Gestopt** |Nee |

## <a id="cc_and_ads"></a>Gesloten ondertiteling en ad invoegen
Hallo volgende tabel ziet u ondersteunde standaarden voor ondertiteling en ad invoegen.

| Standard | Opmerkingen |
| --- | --- |
| CEA 708 en EIA 608 (708/608) |CEA 708 en EIA 608 zijn gesloten ondertiteling standaarden voor Hallo Verenigde Staten en Canada.<p><p>Op dit moment wordt ondertiteling alleen ondersteund als uitgevoerd in de gecodeerde invoerstroom Hallo. U moet toouse een live media encoder die 608 of 708 bijschriften kunt invoegen in gecodeerde Hallo-stroom die tooMedia Services heeft verzonden. Media Services biedt Hallo inhoud met ingevoegde bijschriften tooyour viewers. |
| TTML binnen .ismt (tekst houdt Smooth Streaming) |Media Services dynamische pakketten ervoor zorgt dat uw clients toostream-inhoud in een van de volgende indelingen Hallo: DASH, HLS of Smooth Streaming. Echter, als u wilt opnemen gefragmenteerd MP4 (Smooth Streaming) met bijschriften binnen .ismt (tekst houdt Smooth Streaming), kunt u Hallo stroom tooonly Smooth Streaming clients leveren. |
| SCTE 35 |SCTE 35 is een digitale signalering systeem die toocue reclame invoegen wordt gebruikt. Downstream ontvangers gebruik Hallo signaal toosplice reclame Hallo stroom voor Hallo tijd die is toegewezen. SCTE 35 moet worden verzonden als een sparse spoor in Hallo-invoerstroom.<p><p>Op dit moment alleen ondersteund Hallo invoerstroom indeling die zijn voor de ad-signalen is gefragmenteerd MP4 (Smooth Streaming). alleen ondersteund Hallo uitvoerindeling is ook Smooth Streaming. |

## <a id="considerations"></a>Overwegingen
Wanneer u een lokale live coderingsprogramma toosend een multi-bitrate stream tooa kanaal, toepassing hello volgende beperkingen:

* Zorg ervoor dat er voldoende vrije Internet connectiviteit toosend gegevens toohello punten opnemen.
* URL voor opnemen met behulp van een secundaire extra bandbreedte vereist.
* Hallo binnenkomende multi-bitrate stream kan maximaal 10 videokwaliteit niveaus (lagen) en maximaal 5 audio houdt hebben.
* hoogste gemiddelde bitrate Hallo voor elk van Hallo videokwaliteit niveaus moeten uit minder dan 10 Mbps.
* Hallo moeten statistische functie van gemiddelde bitsnelheden Hallo voor alle Hallo video en audio-gegevensstromen uit minder dan 25 Mbps.
* U kunt Hallo invoerprotocol tijdens het Hallo-kanaal niet wijzigen of de gekoppelde programma's worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u afzonderlijke kanalen voor elk invoerprotocol.
* U kunt een single bitrate opnemen in het kanaal op. Maar omdat Hallo kanaal geen Hallo stroom verwerkt, Hallo clienttoepassingen ontvangt ook een single-bitrate stream. (Wordt niet aanbevolen deze optie.)

Hier volgen andere overwegingen gerelateerde tooworking met kanalen en gerelateerde onderdelen:

* Telkens wanneer u de configuratie van het live coderingsprogramma hello, roepen Hallo **opnieuw** methode op het Hallo-kanaal. Voordat u Hallo kanaal opnieuw instelt, kunt u toostop Hallo programma hebben. Nadat u opnieuw Hallo kanaal, start u Hallo programma opnieuw.
* Een kanaal kan worden gestopt, alleen wanneer deze Hallo **met** status en alle programma's op Hallo kanaal zijn gestopt.
* Standaard kunt u alleen 5 kanalen tooyour Media Services-account toevoegen. Zie voor meer informatie [quota's en beperkingen](media-services-quotas-and-limitations.md).
* U wordt gefactureerd alleen wanneer het kanaal in Hallo **met** status. Raadpleeg voor meer informatie, toohello [Channel statussen en facturering](media-services-live-streaming-with-onprem-encoders.md#states) sectie.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Verwante onderwerpen
[Azure Media Services tot gefragmenteerde MP4 live opnemen specificatie](media-services-fmp4-live-ingest-overview.md)

[Overzicht van Azure Media Services en algemene scenario 's](media-services-overview.md)

[Media Services-concepten](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
