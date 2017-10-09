---
title: aaaOverview van Live streamen met Azure Media Services | Microsoft Docs
description: In dit onderwerp geeft een overzicht van live streamen met Azure Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Overzicht van Live streamen met Azure Media Services
## <a name="overview"></a>Overzicht
Bij het leveren van live zijn streaming-gebeurtenissen met Azure Media Services Hallo na onderdelen vaak betrokken:

* Een camera die wordt gebruikt toobroadcast een gebeurtenis.
* Een coderingsprogramma voor live video dat signalen van Hallo camera toostreams die worden verzonden tooa converteert live streaming service.

    Eventueel meerdere op tijd gesynchroniseerde coderingsprogramma’s. Voor bepaalde kritieke live gebeurtenissen zeer hoge beschikbaarheid en kwaliteit vereisen, kunt het tooemploy actieve redundante coderingsprogramma's met tijd synchronisatie tooachieve naadloze failover zonder verlies van gegevens wordt aanbevolen.
* Een service voor live streamen waarmee u toodo hello te volgen:

  * Live-inhoud met verschillende protocollen voor live streamen opnemen (bijvoorbeeld RTMP of Smooth Streaming).
  * (Optioneel) Uw stream coderen in een stream met een adaptieve bitsnelheid.
  * Een voorbeeld van uw livestream bekijken.
  * record- en store Hallo ingenomen inhoud in de volgorde toobe gestreamd later (Video-on-Demand)
  * Hallo leveren via algemene streaming protocollen (bijvoorbeeld MPEG DASH, Smooth, HLS) rechtstreeks tooyour klanten of tooa inhoud Delivery Network (CDN) voor verdere distributie.

**Microsoft Azure Media Services** (AMS) biedt de mogelijkheid tooingest hello, coderen, bekijken, opslaan en leveren van uw live-streaming inhoud.

Bij het leveren van uw inhoud toocustomers het doel is toodeliver een hoogwaardige video toovarious apparaten met verschillende netwerkomstandigheden. tooachieve, gebruik live coderingsprogramma's tooencode uw videostream van stroom tooa multi-bitrate (adaptieve bitrate).  tootake antwoord op verschillende apparaten streaming Media Services gebruiken [dynamische pakketten](media-services-dynamic-packaging-overview.md) toodynamically opnieuw verpakte uw stream toodifferent protocollen. Media Services ondersteunt de levering van de volgende adaptive bitrate streaming-technologieën Hallo: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

In Azure Media Services **kanalen**, **programma's**, en **streaming-eindpunten** ingang alle Hallo live streamen opnemen, opmaken, DVR, waaronder functies beveiliging, schaalbaarheid en redundantie.

Een **kanaal** vertegenwoordigt een pijplijn voor de verwerking van inhoud voor live-streaming. Een kanaal kan ontvangen een live invoerstromen in Hallo volgende manieren:

* Een on-premises live codering verzendt multi-bitrate **RTMP** of **Smooth Streaming** (gefragmenteerd MP4) toohello-kanaal dat is geconfigureerd voor **pass-through** levering. Hallo **pass-through** levering vindt plaats wanneer Hallo ingenomen streams doorgeven **kanaal**s zonder verdere verwerking. U kunt Hallo volgende live coderingsprogramma's die multi-bitrate Smooth Streaming uitvoeren: MediaExcel, Ateme, stel communicatie, Envivio, Cisco en Elemental. Hallo volgende live coderingsprogramma's voeren RTMP: Adobe Flash Media Live coderingsprogramma (FMLE), Telestream Wirecast, Haivision, Teradek en Tricaster-transcoders.  Een live coderingsprogramma kan ook een single-bitrate stream tooa kanaal dat niet is ingeschakeld voor live codering, maar dit wordt niet aanbevolen verzenden. Desgevraagd levert Media Services Hallo stroom toocustomers.

  > [!NOTE]
  > Een Pass Through-methode is de meest voordelige manier Hallo toodo live te streamen wanneer u meerdere gebeurtenissen gedurende een lange periode uitvoert en u al hebt geïnvesteerd in on-premises coderingsprogramma's. Zie de details over de [prijzen](https://azure.microsoft.com/pricing/details/media-services/).
  > 
  > 
* Een on-premises live codering verzendt een stream met één bitsnelheid toohello-kanaal dat is ingeschakeld tooperform live codering met Media Services in een van de volgende indelingen Hallo: RTMP of Smooth Streaming (gefragmenteerde MP4). RTP (MPEG-TS) wordt ook ondersteund, mits u een speciale verbinding toohello Azure-Datacenter. Hallo volgende live coderingsprogramma's met RTMP uitvoer bekend toowork met kanalen van dit type zijn: Telestream Wirecast, FMLE. Hallo kanaal voert live codering Hallo binnenkomende single-bitrate stream tooa multi-bitrate (adaptieve) videostream. Desgevraagd levert Media Services Hallo stroom toocustomers.

Vanaf versie Hallo Media Services 2.10, wanneer u een kanaal maakt, kunt u opgeven op welke manier u wenst de invoerstroom van kanaal tooreceive hello en of u wilt voor Hallo kanaal tooperform live codering van uw stream. U hebt hiervoor twee opties:

* **Geen** (pass-through): deze waarde opgeven als u van plan toouse een on-premises live coderingsprogramma die multi-bitrate stream (Pass Through-stream bent) wordt uitgevoerd. In dit geval stroom voor inkomende hello doorgegeven via toohello zonder alle codering. Dit is Hallo gedrag van een versie van de voorafgaande too2.10 kanaal.  
* **Standaard** – Selecteer deze waarde als u van plan toouse Media Services tooencode bent uw single-bitrate livestream toomulti-bitrate stream. Deze methode is voor het snel voor incidentele gebeurtenissen omhoog schalen voordeliger. Let erop dat er een facturering invloed voor live codering en u rekening mee houden moet dat een live codering kanaal waardoor de status 'Actief' hello wordt facturering worden kosten in rekening.  Het is raadzaam uw actieve kanalen onmiddellijk te beëindigen nadat uw live-streaming gebeurtenis is voltooid tooavoid extra per uur kosten.

## <a name="comparison-of-channel-types"></a>Vergelijking van kanaaltypen
Volgende tabel bevat een handleiding toocomparing Hallo twee kanaaltypen ondersteund in Media Services

| Functie | Pass Through-kanaal | Standard-kanaal |
| --- | --- | --- |
| Single-bitrate-invoer is gecodeerd in meerdere bitsnelheden in Hallo cloud |Nee |Ja |
| Maximale resolutie van het aantal lagen |1080p, 8 lagen 60 + fps |720p, 6 lagen 30 fps |
| Invoer-protocollen |RTMP, Smooth Streaming |RTMP, Smooth Streaming- en RTP |
| Prijs |Zie Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/media-services/) en klik op het tabblad 'Live Video' |Zie Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/media-services/) |
| Maximale uitvoeringstijd |24 x 7 |8 uur |
| Ondersteuning voor het invoegen van slates |Nee |Ja |
| Ondersteuning voor ad-signalering |Nee |Ja |
| Pass Through-CEA 608/708 bijschriften |Ja |Ja |
| Mogelijkheid toorecover van korte vertragingen in bijdrage feed |Ja |Nee (kanaal beginnen slating na 6 + seconden zonder invoergegevens) |
| Ondersteuning voor niet-uniforme GOPs invoer |Ja |Nee, invoer moet worden gecorrigeerd 2sec GOPs |
| Ondersteuning voor variabele frame snelheid invoer |Ja |Nee, moet dat invoer framesnelheid worden vastgesteld.<br/>Secundaire variaties zijn toegestaan, bijvoorbeeld tijdens hoge beweging schermen. Maar encoder too10 frames per seconde kan niet verwijderen. |
| Automatische-signalen kanalen als invoer feed is verbroken |Nee |Na 12 uur, als er is geen programma uitvoeren |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Werken met kanalen die een multi-bitrate livestream van on-premises encoders ontvangen (pass-through)
Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Hallo **pass-through** werkstroom.

![Live-werkstroom](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Zie [Werken met kanalen die een multi-bitrate livestream van on-premises coderingsprogramma’s ontvangen](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie.

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Werken met kanalen die zijn ingeschakeld tooperform live codering met Azure Media Services
Hallo volgende diagram toont Hallo belangrijke onderdelen van Hallo AMS-platform die betrokken zijn bij Live Streaming-werkstroom waarbij een kanaal is ingeschakeld tooperform live codering met Media Services.

![Live-werkstroom](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Beschrijving van een kanaal en de bijbehorende onderdelen
### <a name="channel"></a>Kanaal
In Media Services [kanaal](https://docs.microsoft.com/rest/api/media/operations/channel)s zijn verantwoordelijk voor het verwerken van live streaming inhoud. Een kanaal biedt een invoereindpunt (de URL voor opnemen) vervolgens live transcoder tooa te bieden. Hallo kanaal live invoer gegevensstromen van live transcoder Hallo ontvangt en wordt het beschikbaar gemaakt voor streaming via een of meer streaming-eindpunten. Kanalen bieden ook een preview-eindpunt (preview URL) toopreview te gebruiken en uw stream te valideren voordat verdere verwerking en levering.

U krijgt Hallo URL's en Hallo preview opnemen wanneer u Hallo kanaal hebt gemaakt. tooget deze URL's, Hallo kanaal heeft geen toobe status Hallo gestart. Wanneer u klaar toostart gegevens van een live transcoder in Hallo kanaal worden gepusht bent, moet Hallo kanaal worden gestart. Zodra de live transcoder Hallo ophalen van gegevens start, kunt u uw stream te bekijken.

Elke Media Services-account kan meerdere kanalen, meerdere programma's en meerdere streaming-eindpunten bevatten. Afhankelijk van Hallo bandbreedte en beveiliging behoeften zijn StreamingEndpoint services speciale tooone of meer kanalen. Alle StreamingEndpoint kunt halen uit een kanaal.

### <a name="program"></a>Programma
Een [programma](https://docs.microsoft.com/rest/api/media/operations/program) kunt u toocontrol Hallo publiceren en opslaan van segmenten in een live stream. Kanalen beheren programma's. Hallo is kanaal- en programma-relatie heel vergelijkbaar tootraditional media waarbij een kanaal een constante stream met inhoud heeft en een programma bereik toosome getimede gebeurtenis op dat kanaal.
Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **ArchiveWindowLength** eigenschap. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur.

ArchiveWindowLength bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Programma's kunnen uitvoeren in de opgegeven tijdsduur hello, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elk programma is gekoppeld aan een asset. toopublish hello programma moet u een locator voor Hallo gekoppelde asset. Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.

Een kanaal biedt ondersteuning voor maximaal toothree gelijktijdig actieve programma's, zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte. De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een programma, maar toobroadcast alleen de laatste tien minuten. tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate. Een programma wordt ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd. Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

## <a name="billing-implications"></a>De implicaties van facturering
Een kanaal begint zodra de status te verandert 'actief' via Hallo API facturering.  

Hallo volgende tabel toont hoe kanaal statussen worden toegewezen toobilling statussen in Hallo API en de Azure-portal. Houd er rekening mee Hallo statussen verschillen enigszins tussen Hallo API en UX-Portal Als u een kanaal Hallo 'Actief' status via Hallo API, of in Hallo 'Gereed' of 'Streaming' status in hello Azure-portal, facturering actief zijn.

Hallo-kanaal toostop van u verdere facturering, hebt u tooStop Hallo kanaal via Hallo API of in hello Azure-portal.
U bent zelf verantwoordelijk voor het stoppen van de kanalen wanneer u klaar bent met Hallo-kanaal. Fout toostop Hallo kanaal leidt tot voortdurende facturering.

> [!NOTE]
> Als u werkt met standaard kanalen, automatisch AMS signalen een kanaal dat nog in de status 'Actief' 12 uur nadat Hallo invoer feed verloren en wordt er zijn geen programma's uitvoeren. Echter, wordt u nog steeds worden gefactureerd voor Hallo tijd Hallo die kanaal status 'Actief' was.
>
>

### <a id="states"></a>Kanaal statussen en hoe deze worden toegewezen toohello modus facturering
Hallo huidige status van een kanaal. Mogelijke waarden:

* **Gestopt**. Dit is Hallo beginstatus Hallo kanaal na het maken ervan (tenzij autostart is geselecteerd in de portal Hallo.) Er is geen facturering treedt op in deze staat. Hallo kanaaleigenschappen kunnen worden bijgewerkt in deze toestand is, maar streaming is niet toegestaan.
* **Starten van**. Hallo-kanaal wordt gestart. Er is geen facturering treedt op in deze staat. In deze status zijn streaming en updates niet toegestaan. Als een fout optreedt, retourneert Hallo kanaal toohello status gestopt.
* **Met**. Hallo kanaal is geschikt voor het verwerken van live gegevensstromen. Het is nu gebruik facturering. Hallo kanaal tooprevent verdere facturering, moet u stoppen.
* **Stoppen van**. Hallo-kanaal wordt gestopt. Er is geen facturering treedt op in deze tijdelijke status. In deze status zijn streaming en updates niet toegestaan.
* **Verwijderen van**. Hallo-kanaal wordt verwijderd. Er is geen facturering treedt op in deze tijdelijke status. In deze status zijn streaming en updates niet toegestaan.

Hallo volgende tabel toont hoe kanaal kaart toohello facturering modus staat.

| Kanaalstatus | Portal UI-indicatoren | Is het facturering? |
| --- | --- | --- |
| Starting |Starting |Nee (overgangsstatus) |
| Running |Ready (er worden geen programma's uitgevoerd)<br/>of<br/>Streaming (er wordt ten minste een programma uitgevoerd) |JA |
| Stopping |Stopping |Nee (overgangsstatus) |
| Stopped |Stopped |Nee |

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Verwante onderwerpen
[Azure mediaservices gefragmenteerde MP4 Live opnemen specificatie](media-services-fmp4-live-ingest-overview.md)

[Werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)

[Werken met kanalen die een multi-bitrate livestream van on-premises encoders ontvangen](media-services-live-streaming-with-onprem-encoders.md)

[Quota's en beperkingen](media-services-quotas-and-limitations.md).  

[Media Services-concepten](media-services-concepts.md)
