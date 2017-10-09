---
title: aaaAzure Media Services gefragmenteerde MP4 live opnemen specificatie | Microsoft Docs
description: Deze specificatie beschrijft Hallo-protocol en de indeling voor gefragmenteerde MP4 gebaseerde live streaming opname voor Azure Media Services. U kunt Azure Media Services toostream live gebeurtenissen gebruiken en inhoud in realtime uitzenden met behulp van Azure als Hallo cloud-platform. Dit document wordt ook beschreven best practices voor het bouwen van maximaal redundante en robuuste live mechanismen opnemen.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Azure Media Services tot gefragmenteerde MP4 live opnemen specificatie
Deze specificatie beschrijft Hallo-protocol en de indeling voor gefragmenteerde MP4 gebaseerde live streaming opname voor Azure Media Services. Media Services biedt een service voor live streamen dat klanten kunnen toostream live gebeurtenissen gebruiken en inhoud in realtime uitzenden met behulp van Azure als Hallo cloud-platform. Dit document wordt ook beschreven best practices voor het bouwen van maximaal redundante en robuuste live mechanismen opnemen.

## <a name="1-conformance-notation"></a>1. Conformiteit notatie
Hallo woorden key 'moet' 'moet geen,' 'Is vereist,' 'Vermelde', 'wordt niet,"'SHOULD', 'Mag niet' zijn 'Aanbevolen', 'Kunnen' en 'Optioneel' in dit document toobe geïnterpreteerd als ze beschreven in RFC 2119 worden.

## <a name="2-service-diagram"></a>2. Diagram van de service
Hallo volgende diagram toont Hallo op hoog niveau architectuur Hallo live streaming-service in Media Services:

1. Een live coderingsprogramma duwt live-feeds toochannels die zijn gemaakt en ingericht via hello Azure Media Services SDK.
2. Cloud kanalen, programma's en streaming-eindpunten in Media Services-ingang alle Hallo live streaming-functionaliteiten, waaronder opnemen, opmaken, DVR, beveiliging, schaalbaarheid en redundantie op.
3. Eventueel kunnen klanten kiezen toodeploy een laag Azure Content Delivery Network tussen Hallo streaming-eindpunt en Hallo clienteindpunten.
4. Client-eindpunten stroom van Hallo streaming-eindpunt met behulp van protocollen HTTP adaptief streamen. Voorbeelden zijn Microsoft Smooth Streaming, dynamische adaptief streamen via HTTP (DASH of MPEG-DASH) en Apple HTTP Live Streaming (HLS).

![stroom opnemen][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. De indeling bitstream – ISO 14496 12 gefragmenteerd MP4
Hallo draadindeling voor live streamen opnemen die worden beschreven dit document is gebaseerd op [ISO 14496 12]. Zie voor een gedetailleerde uitleg van gefragmenteerde MP4-indeling en extensies zowel voor video-on-demand bestanden en live streaming opname [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Indeling definities voor Live opnemen
Hallo hieronder wordt beschreven speciale indeling definities die van toepassing zijn toolive in Azure Media Services opnemen:

1. Hallo **ftyp legt vast**, **vak Server Manifest Live**, en **moov** vakken bij elke aanvraag (HTTP POST) moeten worden verzonden. Deze vakken op Hallo begin van Hallo stroom moeten worden verzonden en elk gewenst moment Hallo encoder tooresume stroom moet verbinding opnemen. Zie de sectie 6 in [1] voor meer informatie.
2. Sectie 3.3.2 in [1] definieert een optioneel het zogenaamde **StreamManifestBox** voor live opnemen. Vervaldatum toohello routering logica hello Azure load balancer, is met behulp van dit vak afgeschaft. Hallo vak mag geen aanwezig wanneer opnemen in Media Services. Als dit selectievakje aanwezig is, Media Services achtergrond deze genegeerd.
3. Hallo **TrackFragmentExtendedHeaderBox** vak gedefinieerd in 3.2.3.2 in [1] moet aanwezig zijn voor elke fragment.
4. Versie 2 van Hallo **TrackFragmentExtendedHeaderBox** vak moet gebruikte toogenerate mediasegmenten met identieke URL's in meerdere datacenters. Hallo-fragment indexveld is REQUIRED voor cross-datacenter failover van een index gebaseerde streaming-indelingen zoals Apple HLS en MPEG-DASH op basis van een index. tooenable cross-datacenter failover, Hallo fragment index moet worden gesynchroniseerd tussen meerdere coderingsprogramma's en worden verhoogd met 1 voor elke fragment opeenvolgende media, zelfs in encoder opnieuw wordt opgestart of storingen.
5. Sectie 3.3.6 in [1] definieert een invoervak **MovieFragmentRandomAccessBox** (**mfra**) die kunnen worden verzonden aan Hallo einde van live opname tooindicate einde van stroom (EOS) toohello kanaal. Vervaldatum toohello opnemen logica van Media Services met behulp van EOS is afgeschaft en Hallo **mfra** vak voor live opname niet moet worden verzonden. Als verzonden, Media Services achtergrond deze genegeerd. status van de tooreset Hallo Hallo punt opnemen, is het raadzaam dat u [kanaal opnieuw](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). We raden u ook aan dat u [programma stoppen](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend een presentatie en de stream.
6. Hallo MP4-fragment duur moet een constante, tooreduce Hallo grootte van de clientmanifesten Hallo. Een constante MP4-fragment duur verbetert ook client downloaden methodiek via Hallo herhaaldelijk labels. Hallo-duur kan toocompensate voor niet-integere framesnelheid variëren.
7. Hallo MP4-fragment duur moet liggen tussen ongeveer 2 en 6 seconden.
8. MP4 fragment tijdstempels en indexen (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` en `fragment_index`) moeten in oplopende volgorde binnenkomen. Hoewel Media Services robuuste tooduplicate fragmenten is, is deze mogelijkheid tooreorder fragmenten op basis van toohello media tijdlijn beperkt.

## <a name="4-protocol-format--http"></a>4. Indeling protocol: HTTP
ISO gefragmenteerd MP4 gebaseerde live opnemen voor Media Services gebruikt een standaard langlopende HTTP POST-aanvraag tootransmit gecodeerd mediagegevens dat is gecomprimeerd tot gefragmenteerde MP4-indeling toohello service. Elke HTTP POST verstuurt een complete gefragmenteerd MP4 bitstream ('stream'), Hallo die begint met header vakken vanaf (**ftyp legt vast**, **vak Server Manifest Live**, en **moov** dialoogvensters), en wilt doorgaan met een reeks fragmenten (**moof** en **mdat** vakken). Zie de sectie 9.2 in [1] voor URL-syntaxis voor Hallo HTTP POST-aanvraag. Een voorbeeld van Hallo POST-URL is: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Vereisten
Hier vindt u gedetailleerde vereisten Hallo:

1. Hello codering moet worden gestart door het verzenden van een HTTP POST-aanvraag met een lege uitgezonden Hallo 'hoofdtekst' (nul inhoudslengte) met behulp van dezelfde URL voor opname Hallo. Zo kunt u snel opsporen of Hallo live opname eindpunt geldig is en of er zijn verificatie of andere voorwaarden Hallo-codering. Per HTTP-protocol kan niet Hallo-server teruggestuurd een HTTP-antwoord totdat hello volledige aanvraag, waaronder Hallo POST hoofdtekst is ontvangen. Gezien Hallo langlopende aard van een live gebeurtenis, zonder deze stap wordt Hallo encoder mogelijk niet meer kunnen toodetect fouten totdat het klaar is met het verzenden van gegevens van alle Hallo.
2. Hallo-codering moet eventuele fouten of verificatiecontroles verwerken vanwege (1). Als (1) is voltooid met een 200 antwoord worden voortgezet.
3. Hallo-codering moet een nieuwe HTTP POST-aanvraag beginnen met Hallo gefragmenteerd MP4-stream. Hallo nettolading moet beginnen met het Hallo-header vakken, gevolgd door fragmenten. Houd er rekening mee dat Hallo **ftyp legt vast**, **vak Server Manifest Live**, en **moov** vakken (in deze volgorde) moeten worden verzonden met elke aanvraag, zelfs als het Hallo-codering moet opnieuw verbinding maken omdat Hallo vorige aanvraag is beëindigd voorafgaande toohello einde van de Hallo-stroom. 
4. Hallo-codering moet gesegmenteerde overdrachtscodering voor het uploaden van gebruiken, omdat het onmogelijk toopredict Hallo gehele lengte van de inhoud van Hallo live gebeurtenis.
5. Wanneer gebeurtenis Hallo is afgelopen, na het verzenden van de laatste fragment hello, moet Hallo encoder probleemloos Hallo chunked overdrachtscodering-bericht sequence (de meeste HTTP-client stacks verwerkt; het automatisch) eindigen. Hallo-codering moet wacht Hallo tooreturn Hallo definitieve antwoord servicecode en vervolgens Hallo verbinding te verbreken. 
6. Hallo-codering moet niet gebruiken Hallo `Events()` zelfstandig naamwoord zoals beschreven in 9.2 in [1] voor live opname in Media Services.
7. Als Hallo HTTP POST-aanvraag wordt beëindigd of tijden uit met een TCP-fout voorafgaande toohello einde van stroom hello, Hallo-codering moet een nieuwe POST-aanvraag uitgeven met behulp van een nieuwe verbinding en volg Hallo voorafgaand aan de vereisten. Hallo-codering moet bovendien verzenden Hallo vorige twee MP4-fragmenten voor elk nummer in de stroom Hallo en hervatten zonder een onderbreking in Hallo media tijdlijn. Laatste twee MP4 fragmenten voor elk nummer opnieuw verzenden van Hallo zorgt ervoor dat er geen gegevens verloren gaan. Met andere woorden, als een stroom geen audio en video bijgehouden bevat en Hallo huidige POST-aanvraag is mislukt, Hallo-codering moet herstellen en opnieuw verzenden Hallo laatste twee fragmenten voor Hallo-nummer, die eerder met succes zijn verzonden, en Hallo laatste twee fragmenten voor Hallo video bijhouden, die eerder met succes zijn verzonden, tooensure dat er geen gegevens verloren gaan. Hallo-codering moet onderhouden een "forward" buffer van media fragmenten die het opnieuw verzendt wanneer verbinding wordt gemaakt.

## <a name="5-timescale"></a>5. Tijdschaal
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) beschrijft Hallo informatie over het gebruik van tijdschaal voor **SmoothStreamingMedia** (sectie 2.2.2.1) **StreamElement** (sectie 2.2.2.3) **StreamFragmentElement**(Punt 2.2.2.6), en **LiveSMIL** (punt 2.2.7.3.1). Als Hallo tijdschaal waarde niet aanwezig is, is het Hallo-standaardwaarde gebruikt 10,000,000 (10 MHz). Hoewel informatie over het gebruik van andere waarden tijdschaal Hallo Smooth Streaming-specificatie niet wordt geblokkeerd, de meeste implementaties van het coderingsprogramma deze standaardinstelling gebruiken waarde (10 MHz) toogenerate Smooth Streaming opnemen van gegevens. Vervaldatum toohello [Azure Media dynamische pakketten](media-services-dynamic-packaging-overview.md) functie, het is raadzaam een tijdschaal 90 KHz te gebruiken voor video stromen en 44,1 of 48.1 KHz voor audio stromen. Als andere tijdschaal waarden worden gebruikt voor verschillende stromen, moet Hallo stroom niveau tijdschaal worden verzonden. Zie voor meer informatie [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Definitie van 'stream'
De stroom is Hallo basiseenheid van bewerking in live opname voor het opstellen van live presentaties verwerken streaming failover en redundantie scenario's. Stroom wordt gedefinieerd als een unieke, gefragmenteerde MP4-bitstream met één track of meerdere nummers. Een volledige live presentatie kan een of meer stromen, afhankelijk van de configuratie Hallo van Hallo live coderingsprogramma's bevatten. Hallo volgen voorbeelden laten zien verschillende opties voor het gebruik van streams toocompose van een volledige live presentatie.

**Voorbeeld:** 

Een klant wil toocreate een live streaming presentatie met Hallo audio/video bitsnelheden te volgen:

Video – 3000 kbps, 1500 kbps, 750 kbps

Audio-128 k

### <a name="option-1-all-tracks-in-one-stream"></a>Optie 1: Alle nummers in één stroom
Bij deze optie geen enkele coderingsprogramma genereert alle audio/video-nummers en verzamelt ze in één gefragmenteerde MP4 bitstream. Hallo gefragmenteerd MP4 bitstream wordt verzonden via één HTTP POST-verbinding. In dit voorbeeld is er slechts één stream voor deze live presentatie.

![Streams-een bijhouden][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Optie 2: Elk nummer in een afzonderlijke stream
Bij deze optie Hallo encoder plaatst een nummer in elke bitstream fragment MP4 en plaatst alle Hallo streams via afzonderlijke HTTP-verbindingen. Dit kan worden gedaan met een coderingsprogramma of met meerdere coderingsprogramma's. Hallo live opname ziet deze live presentatie als bestaat uit vier stromen.

![Streams afzonderlijke houdt][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Optie 3:-Nummer met Hallo laagste bitrate video spoor bundelen in één stream
Bij deze optie kiest Hallo klant toobundle Hallo audio met Hallo laagste bitrate video bijhouden in een fragment MP4 bitstream bijhouden en laat de andere twee video sporen als afzonderlijke gegevensstromen Hallo. 

![Streams-audio en video-nummers][image4]

### <a name="summary"></a>Samenvatting
Dit is geen uitputtende lijst van alle mogelijke opname opties voor dit voorbeeld. Als een sterker nog, wordt een groepering van nummers in streams ondersteund door live opname. Klanten en leveranciers encoder kunt hun eigen implementaties op basis van de technische complexiteit, encoder-capaciteit en redundantie en overwegingen. In de meeste gevallen is er echter slechts één-nummer voor de hele live presentatie Hallo. De belangrijke tooensure Hallo gezondheid van Hallo opnemen dus stream met Hallo-nummer. Dit aandachtspunt vaak resulteert in het Hallo-nummer als in een eigen stroom (zoals in de optie 2) of het bundeling met Hallo laagste bitrate video bijhouden (zoals in de optie 3). Ook, voor betere redundantie en fouttolerantie verzenden Hallo dezelfde-nummer in twee verschillende stromen (optie 2 met redundant audio houdt) of bundelen Hallo-nummer met ten minste twee Hallo laagste bitrate video-nummers (optie 3 met audio gebundeld op minimaal twee streams video) wordt nadrukkelijk aanbevolen voor live opnemen in Media Services.

## <a name="7-service-failover"></a>7. Failover van de service
Goede failover-ondersteuning is gegeven Hallo aard van live streamen, essentieel voor het Hallo-beschikbaarheid van Hallo-service. Media Services is ontworpen toohandle verschillende typen fouten, waaronder netwerkfouten, server-fouten en opslagproblemen. Wanneer gebruikt in combinatie met de juiste failoverlogica van Hallo live coderingsprogramma kant, kunnen klanten een uiterst betrouwbare service voor live streamen vanuit de cloud Hallo kunnen bereiken.

In deze sectie bespreken we service failover-scenario's. In dit geval Hallo fout gebeurt er ergens in Hallo-service en het doet zich voor als een netwerkfout opgetreden. Hier volgen enkele aanbevelingen voor implementatie van Hallo-codering voor het verwerken van de service failover:

1. Gebruik een 10 seconden time-out voor Hallo TCP-verbinding tot stand brengen. Als een poging tooestablish Hallo verbinding langer dan 10 seconden duurt, Hallo bewerking afbreken en probeer het opnieuw. 
2. Gebruik een korte time-out voor het verzenden van bericht segmenten van Hallo HTTP-aanvraag. Als Hallo doel MP4-fragment duur N seconden, gebruikt u de time-out voor een verzenden tussen N en 2 N seconden; Als Hallo MP4-fragment duur 6 seconden, gebruikt u bijvoorbeeld een time-out van 6 too12 seconden. Als er een time-out optreedt, opnemen reset Hallo verbinding, open een nieuwe verbinding en hervatten stroom op Hallo nieuwe verbinding. 
3. Een rolling buffer met Hallo laatste twee fragmenten voor elk nummer dat correct en volledig toohello service verzonden is onderhouden.  Als Hallo HTTP POST-aanvraag voor een stroom wordt beëindigd of een optreedt voorafgaande toohello einde van stroom hello time-out, opent u een nieuwe verbinding en beginnen met een andere HTTP POST-aanvraag, Hallo stroom headers verzenden Hallo opnieuw verzenden die de laatste twee fragmenten voor elk nummer en Hallo stroom zonder hervatten Introductie van een onderbreking in Hallo media tijdlijn. Dit vermindert de kans op Hallo van gegevensverlies.
4. U wordt aangeraden dat Hallo-codering niet beperken het aantal nieuwe pogingen tooestablish verbinding Hallo of hervatten streaming nadat een TCP-fout is opgetreden.
5. Nadat een TCP-fout:
  
    a. de huidige verbinding Hallo moet worden gesloten en een nieuwe verbinding moet worden gemaakt voor een nieuwe HTTP POST-aanvraag.

    b. nieuwe HTTP POST-URL moet Hallo Hallo hetzelfde als de URL van de oorspronkelijke POST Hallo.
  
    c. Hallo nieuwe HTTP POST moet bestaan uit stroom kopteksten (**ftyp legt vast**, **vak Server Manifest Live**, en **moov** vakken) die zijn identiek toohello stroom kopteksten in Hallo initiële POST.
  
    d. de laatste twee fragmenten Hallo verzonden voor elk nummer moeten opnieuw worden verzonden en zonder een onderbreking in Hallo media tijdlijn streaming moet hervat. Hallo MP4-fragment tijdstempels toenemen continu, zelfs in een HTTP POST-aanvragen.
6. Hallo-codering moet Hallo HTTP POST-aanvraag beëindigd als er gegevens worden niet verzonden met een frequentie in overeenstemming met de Hallo MP4-fragment duur.  Een HTTP POST-aanvraag die geen gegevens verzendt kunt voorkomen dat Media Services verbreken snel Hallo-codering in Hallo-gebeurtenis van een service-update. Om deze reden Hallo HTTP POST voor sparse (ad signaal) houdt moeten worden kortstondig wordt beëindigd als sparse fragment hello wordt verzonden.

## <a name="8-encoder-failover"></a>8. codering-failover
Encoder failover is de tweede type Hallo van failover-scenario dat toobe geadresseerd voor de levering van end-to-end-live-streaming moet. In dit scenario optreedt Hallo fout op Hallo encoder aan clientzijde. 

![codering-failover][image5]

Hallo verwachtingen van het volgende van toepassing van Hallo live opname eindpunt als encoder failover gebeurt:

1. Een nieuw exemplaar van de codering moet worden gemaakt toocontinue streaming, zoals geïllustreerd in Hallo diagram (Stream voor 3000k video met stippellijn).
2. Hallo nieuwe encoder gebruik moet Hallo dezelfde URL voor HTTP POST-aanvragen als Hallo mislukt exemplaar.
3. Hallo nieuwe encoder POST-aanvraag vergezeld gaan van Hallo dezelfde gefragmenteerd MP4-header vakken zoals Hallo mislukt exemplaar.
4. nieuwe Hallo-codering moet juist worden gesynchroniseerd met alle andere actieve coderingsprogramma's voor hello dezelfde live presentatie toogenerate gesynchroniseerd audio/video-voorbeelden met uitgelijnde fragment grenzen.
5. Hallo nieuwe stream moet semantisch equivalent met Hallo vorige stream, en uitwisselbaar op Hallo-header en het fragment niveaus.
6. nieuwe Hallo-codering moet proberen toominimize gegevens verloren gaan. Hallo `fragment_absolute_time` en `fragment_index` Media fragmenten vanaf Hallo punt waar de Hallo encoder laatste gestopt moeten verhogen. Hallo `fragment_absolute_time` en `fragment_index` moet worden verhoogd met een ononderbroken wijze, maar het is een onderbreking van toegestane toointroduce indien nodig. Media Services negeert fragmenten dat al is ontvangen en verwerkt, dus is het beter tooerr Hallo-zijde van fragmenten dan toointroduce onderbrekingen in Hallo media tijdlijn opnieuw te verzenden. 

## <a name="9-encoder-redundancy"></a>9. codering redundantie
Voor bepaalde kritieke live gebeurtenissen dat verzoek zelfs hogere beschikbaarheid en kwaliteit vereisen, raden we u actieve redundante coderingsprogramma's tooachieve naadloze failover zonder verlies van gegevens.

![codering redundantie][image6]

Zoals wordt geïllustreerd in dit diagram, push twee groepen coderingsprogramma's twee exemplaren van elke stroom tegelijkertijd in Hallo live-service. Deze instelling wordt ondersteund, omdat Media Services dubbele fragmenten op basis van de stroom-ID en het fragment timestamp uitfilteren kunt. Hallo resulterende livestream en archief is één exemplaar van alle Hallo stromen die Hallo best mogelijke aggregatie van twee bronnen Hallo. Bijvoorbeeld in een hypothetische extreme geval is, zolang er een coderingsprogramma is (heeft geen toobe Hallo dezelfde) uitvoeren op elk gewenst moment in de tijd van elke stroom hello resulterende livestream van Hallo-service continue zonder gegevensverlies. 

Hallo-vereisten voor dit scenario zijn dezelfde bijna Hallo als vereisten in geval van Hallo 'Encoder failover' hello, met uitzondering van Hallo op Hallo Hallo tweede set coderingsprogramma's worden uitgevoerd dezelfde tijd als primaire encoders Hallo.

## <a name="10-service-redundancy"></a>10. redundantie van de service
Voor maximaal redundante globale distributie, moet u soms regio-overschrijdende back-toohandle regionale noodsituaties hebben. Voortbouwend op Hallo 'Encoder redundantie' topologie, kunnen klanten kiezen toohave een redundante service-implementatie in een andere regio die verbonden met Hallo tweede reeks coderingsprogramma's. Klanten ook kunnen werken met een Content Delivery Network provider toodeploy een globale Traffic Manager voor Hallo twee service implementaties tooseamlessly route-clientverkeer. Hallo-vereisten voor Hallo coderingsprogramma's zijn hetzelfde als 'Encoder redundantie' case Hallo Hallo. Hallo alleen uitzondering hierop is dat Hallo tweede set encoders behoeften toobe waarnaar wordt verwezen tooa verschillende live eindpunt opnemen. Hallo volgende diagram ziet u deze installatie:

![redundantie van de service][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Speciale soorten opname-indelingen
Deze sectie wordt beschreven speciale soorten live opname-indelingen die ontworpen toohandle specifieke scenario's zijn.

### <a name="sparse-track"></a>Sparse bijhouden
Wanneer u een live streaming presentatie met een interactieve ervaring, vaak wordt nodig tootransmit tijd gesynchroniseerd gebeurtenissen of signalen in-band met Hallo belangrijkste mediagegevens. Een voorbeeld hiervan is dynamische live ad invoegen. Dit type gebeurtenis-signalering wijkt af van reguliere audio/video-streaming vanwege de sparse aard. Met andere woorden, Hallo-signalering gegevens meestal gebeurt niet continu en hello-interval mag harde toopredict. Hallo-concept van sparse bijhouden was ontworpen tooingest en uitzenden band signalering van gegevens.

Hallo zijn volgende stappen een aanbevolen implementatie voor het opnemen van sparse bijhouden:

1. Maak een afzonderlijke gefragmenteerde MP4 bitstream met sparse houdt, zonder audio/video houdt.
2. In Hallo **vak Server Manifest Live** zoals gedefinieerd in de sectie 6 in [1], gebruik Hallo *parentTrackName* toospecify Hallo parameternaam van Hallo bovenliggende bijhouden. Zie voor meer informatie de sectie 4.2.1.2.1.2 in [1].
3. In Hallo **vak Server Manifest Live**, **manifestOutput** te moet worden ingesteld**true**.
4. Hallo sparse aard van Hallo-signalering gebeurtenis gezien, raden we Hallo volgende:
   
    a. Aan het begin van de Hallo van live gebeurtenis hello verzendt Hallo codering Hallo initiële header vakken toohello service, waarmee Hallo service tooregister Hallo sparse bijhouden in Hallo client manifest.
   
    b. Hallo HTTP POST-aanvraag Hallo codering moet worden beëindigd wanneer gegevens worden niet verzonden. Een langlopende HTTP POST die geen gegevens verzendt kunt voorkomen dat Media Services verbreken snel Hallo-codering in Hallo-gebeurtenis van een service-update of de server opnieuw opstarten. In dergelijke gevallen is Hallo mediaserver tijdelijk geblokkeerd in een ontvangstbewerking op Hallo socket.
   
    c. Tijdens het Hallo tijdstip waarop-signalering gegevens niet beschikbaar is, moet Hallo encoder Hallo HTTP POST-aanvraag sluiten. Terwijl de POST-aanvraag Hallo actief is, moet encoder hello gegevens verzenden.

    d. Bij het verzenden van sparse fragmenten instellen Hallo encoder een expliciete header content-length, als deze beschikbaar is.

    e. Bij het verzenden van sparse fragmenten op basis van een nieuwe verbinding moet Hallo-codering beginnen met het verzenden van Hallo header vakken, gevolgd door de nieuwe fragmenten Hallo. Dit is gevallen gebeurt in welke failover middenweg kiest en Hallo nieuwe sparse-verbinding tot stand gebrachte tooa nieuwe server die niet zichtbaar is voor Hallo sparse bijhouden voordat wordt.

    f. Hallo sparse bijhouden fragment wordt de client beschikbare toohello wanneer Hallo bijbehorende bovenliggende bijhouden fragment dat een tijdstempelwaarde groter of gelijk beschikbaar toohello client wordt uitgevoerd. Bijvoorbeeld, als sparse fragment Hallo een tijdstempel van t heeft = 1000, wordt verwacht dat nadat het Hallo-client ziet 'video' (ervan uitgaande Hallo bovenliggende bijhouden naam 'video') fragment tijdstempel 1000 of hoger, het kan downloaden Hallo sparse fragment t = 1000. Houd er rekening mee dat Hallo werkelijke signaal kan worden gebruikt voor een andere positie in Hallo presentatie tijdlijn voor het opgegeven doel. In dit voorbeeld wordt het mogelijk dat er Hallo sparse fragment van t = 1000 heeft een XML-nettolading is voor het invoegen van een ad dat een paar seconden later.

    g. Hallo-nettolading van sparse bijhouden fragmenten kan zijn in verschillende indelingen (zoals XML, tekst of binair), afhankelijk van Hallo scenario.

### <a name="redundant-audio-track"></a>Redundante-nummer
In een typische HTTP adaptieve streaming-scenario (bijvoorbeeld Smooth Streaming of streepje) vaak, is er slechts één-nummer in de hele presentatie Hallo. In tegenstelling tot de video houdt met meerdere kwaliteitsniveaus voor toochoose van client in foutcondities hello, mag Hallo-nummer een potentieel risico als hello opname van Hallo-stroom met Hallo-nummer verbroken is. 

Dit probleem op door Media Services ondersteunt toosolve live opname van redundante audio houdt. Hallo idee is dat Hallo dezelfde-nummer kan meerdere keren worden verzonden in verschillende stromen. Hoewel hello service alleen Hallo-nummer eenmaal in het manifest voor Hallo-client registreert, kan deze redundante audio houdt als back-ups gebruiken voor het ophalen van audio fragmenten als primaire-nummer Hallo problemen heeft. tooingest redundante audio houdt, Hallo-codering moet:

1. Hallo dezelfde audio bijhouden in meerdere fragment MP4 bitstreams maken. Hallo redundante audio houdt moet dezelfde, hello dezelfde fragment tijdstempels en uitwisselbaar op Hallo-header en het fragment niveaus.
2. Zorg ervoor dat 'audio' Hallo-item in Hallo Live Server Manifest (sectie 6 in [1]) is hello gelijk voor alle redundante audio houdt.

Hallo na implementatie wordt aanbevolen voor redundante audio houdt:

1. Elke unieke-nummer in een stream zelfstandig verzenden. Ook verzenden van een redundant stroom voor elk van deze stromen-nummer, waar de tweede stroom Hallo van Hallo eerst alleen door Hallo-id in Hallo HTTP POST-URL verschilt: {protocol} :// {server address} / {punt path}/Streams({identifier}) publiceren.
2. Gebruik afzonderlijke streams toosend Hallo twee laagste video bitsnelheden. Elk van deze stromen moet ook een kopie van elke unieke nummer bevatten. Wanneer er meerdere talen worden ondersteund, moeten deze stromen audio houdt voor elke taal bevatten.
3. Afzonderlijke server (coderingsprogramma) exemplaren tooencode gebruiken en Hallo redundante stromen die worden vermeld in (1) en (2) te verzenden. 

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
