---
title: aaaAvanced Media Encoder Premium werkstroom zelfstudies
description: Dit document bevat scenario's die laten zien hoe tooperform geavanceerde taken met Media Encoder Premium Workflow en ook hoe toocreate complexe werkstromen met Workflow Designer.
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Geavanceerde werkstroom voor Media Encoder Premium zelfstudies
## <a name="overview"></a>Overzicht
Dit document bevat scenario's die laten zien hoe toocustomize werkstromen met **Workflow Designer**. U vindt Hallo werkelijke Werkstroombestanden [hier](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>INHOUDSOPGAVE
Hallo volgende onderwerpen komen aan bod:

* [MXF naar een single-bitrate MP4-codering](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Een nieuwe werkstroom starten](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Met behulp van Hallo Media bestandsinvoer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Streaming media te bekijken](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Toevoegen van een video encoder voor. MP4-bestand genereren](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Codering Hallo audiostroom](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Audio en Video-streams multiplex in een MP4-container](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Hallo MP4-bestand schrijven](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Maken van een Media Services-activum van Hallo-bestand voor uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Test Hallo lokaal werkstroom is voltooid](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [MXF in multibitrate MP4s - codering dynamische pakketten ingeschakeld](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Toevoegen van een of meer extra MP4-uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Configureren Hallo uitvoer bestandsnamen](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Toevoegen van een afzonderlijke-nummer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Hallo toe te voegen. ISM SMIL-bestand](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [MXF in multibitrate MP4 - verbeterde blauwdruk codering](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Werkstroom overzicht tooenhance](#workflow-overview-to-enhance)
  * [Naamgevingsregels voor bestanden](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Eigenschappen van onderdeel op Hallo werkstroom hoofdmap publiceren](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Uitvoerbestand namen zijn afhankelijk van de gepubliceerde eigenschapswaarden hebt gegenereerd](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Miniaturen toomultibitrate MP4 uitvoer toevoegen](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Werkstroom overzicht tooadd miniatuurweergaven voor](#workflow-overview-to-add-thumbnails-to)
  * [Toe te voegen JPG-codering](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Omgaan met de conversie van de werkruimte](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Schrijven Hallo miniaturen](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Fouten opsporen in een werkstroom](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Werkstroom is voltooid](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Op basis van tijd worden ingekort door multibitrate MP4-uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Werkstroom overzicht toostart bijsnijden aan toe te voegen](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Hallo stroom Trimmer gebruiken](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Werkstroom is voltooid](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Introducing hello onderdeel in een script vastgelegd](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Uitvoeren van scripts in een werkstroom: Hallo wereld](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Op basis van het frame worden ingekort door multibitrate MP4-uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Blauwdruk overzicht toostart bijsnijden aan toe te voegen](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Met behulp van Hallo Clip lijst XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Hallo clip lijst van een onderdeel in een script vastgelegd wijzigen](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [De eigenschap van een ClippingEnabled gemak toe te voegen](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>MXF naar een single-bitrate MP4-codering
In dit scenario maakt u een single bitrate. MP4-bestand met AAC HE gecodeerde audio van een. Het invoerbestand MXF.

### <a id="MXF_to_MP4_start_new"></a>Een nieuwe werkstroom starten
Workflow Designer openen en selecteer 'File '-' nieuwe werkruimte'-' transcoderen blauwdruk'

de nieuwe werkstroom Hello wordt 3 elementen weergeven:

* Primaire bronbestand
* Clip XML-lijst
* Uitvoerasset bestand  

![Nieuwe codering werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Nieuwe codering werkstroom*

### <a id="MXF_to_MP4_with_file_input"></a>Met behulp van Hallo Media bestandsinvoer
In de volgorde tooaccept onze invoer mediabestand een begint met Media bestand invoer onderdelen toevoegen. tooadd een onderdeel toohello werkstroom, zoekt in het zoekvak Hallo-opslagplaats en sleep Hallo gewenst vermelding op Hallo designer deelvenster. Dit doen voor Hallo Media bestand invoer en Hallo primaire bronbestand onderdeel toohello Filename invoer pincode vanaf Media bestand invoer Hallo verbinding te maken.

![Verbonden mediabestand invoer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Verbonden mediabestand invoer*

Voordat we veel anders doen kunt, moet u eerst tooindicate toohello werkstroomontwerper welke voorbeeldbestand willen we graag toouse toodesign onze werkstroom met. toodo geval is, klikt u op Hallo designer deelvenster achtergrond en te bekijken voor Hallo primaire bronbestand-eigenschap op Hallo eigenschap rechter deelvenster. Klik op Hallo mappictogram en selecteer Hallo gewenst bestand tootest Hallo werkstroom met. Zodra dit is gebeurd, wordt de Hallo Media bestandsinvoer onderdeel Hallo bestand controleren en de zijn pincodes tooreflect Hallo uitvoerbestand die deze geïnspecteerd vullen.

![Invoer van mediabestand ingevuld](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Invoer van mediabestand ingevuld*

Terwijl u hiermee met wat willen we graag toowork met invoer, niet duidelijk nog waar Hallo gecodeerde uitvoer moet gaan. Vergelijkbare toohow Hallo primaire bestand van de bron is geconfigureerd, worden nu Hallo uitvoer map variabele eigenschap, net onder configureren.

![Geconfigureerde invoer en uitvoer eigenschappen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Geconfigureerde invoer en uitvoer eigenschappen*

### <a id="MXF_to_MP4_streams"></a>Streaming media te bekijken
Vaak het gewenst tooknow Hallo stroom weergave die loopt via Hallo-werkstroom. tooinspect een stroom op elk gewenst moment in de werkstroom hello, klik op een uitvoer- of invoer van de pincode op Hallo-onderdelen. In dit geval probeert te klikken op Hallo niet-gecomprimeerde Video uitvoer pincode van de invoer van onze Media-bestand. Een dialoogvenster wordt geopend waarmee tooinspect Hallo uitgaande video.

![Niet-gecomprimeerde Video uitvoer inspecteren Hallo pincode](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Niet-gecomprimeerde Video uitvoer inspecteren Hallo pincode*

In ons geval vertelt ons bijvoorbeeld dat we je omgaan met een invoer 1920 x 1080 op 24 frames per seconde in 4:2:2 steekproeven voor een video van bijna 2 minuten.

### <a id="MXF_to_MP4_file_generation"></a>Toevoegen van een video encoder voor. MP4-bestand genereren
Houd er rekening mee dat nu, een niet-gecomprimeerde Video's en meerdere niet-gecomprimeerde Audio-uitvoer pincodes zijn beschikbaar voor gebruik van onze invoer Media-bestand. In de volgorde tooencode Hallo inkomende video, moeten we een codering onderdeel - in dit geval voor het genereren van. MP4-bestanden.

tooencode Hallo videostream tooH.264, Hallo AVC Video Encoder onderdeel toohello ontwerpoppervlak toevoegen. Dit onderdeel wordt een decomprimeren videostream als invoer en biedt een gecomprimeerde AVC-videostream op de pincode van de uitvoer.

![Niet-verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Niet-verbonden AVC-codering*

De eigenschappen kunt u bepalen hoe Hallo codering precies wordt uitgevoerd. We hebben een overzicht van enkele Hallo meer belangrijke instellingen:

* Uitvoer breedte en hoogte van de uitvoer: deze Hallo resolutie van Hallo gecodeerde video bepalen. In ons geval gaan we met 640 x 360
* Framesnelheid: wanneer set toopassthrough gewoon Hallo bron framesnelheid aannemen, is het mogelijk toooverride dit al. Houd er rekening mee dat dergelijke framesnelheid conversie is niet beweging-gecompenseerd.
* Profiel en het niveau: deze bepalen Hallo AVC-profiel en niveau. tooconveniently u meer informatie over de verschillende niveaus Hallo en -profielen, klikt u op Hallo vraagteken Hallo AVC Video Encoder onderdeel en Hallo help-pagina meer details over elk Hallo niveaus wordt weergegeven. Voor onze voorbeeld we kiezen Main-profiel op niveau 3.2 (Hallo standaard).
* Beoordeel besturingselement modus en Bitrate (kbps): in ons scenario we kiezen voor een constante uitvoer voor 1200 kbps bitrate (CBR)
* Video-indeling: dit is over Hallo VUI (Video bruikbaarheid informatie) die in Hallo H.264 stroom wordt geschreven (side-informatie die kan worden gebruikt door een decoder tooenhance Hallo weergave, maar niet essentieel toocorrectly te decoderen):
* NTSC (standaard voor VS of Japan, met behulp van 30 fps)
* PAL (standaard voor Europa, met behulp van 25 fps)
* Modus van de grootte GOP: geconfigureerd vaste GOP grootte voor onze toepassing met een Interval van twee seconden van de sleutel met GOPs gesloten. Dit zorgt voor compatibiliteit met Hallo die dynamische pakketten Azure Media Services biedt.

toofeed onze encoder AVC Hallo niet-gecomprimeerde Video-uitvoer pincode vanaf Hallo Media bestand invoer onderdeel toohello niet-gecomprimeerde Video invoer pincode van Hallo AVC coderingsprogramma verbinding te maken.

![Verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Verbonden AVC Main-codering*

### <a id="MXF_to_MP4_audio"></a>Codering Hallo audiostroom
Op dit moment hebben we video gecodeerd maar Hallo oorspronkelijke niet-gecomprimeerde audiostroom moet nog steeds toobe gecomprimeerd. Voor dit gaan we met AAC codering door Hallo onderdeel AAC codering (Dolby). Deze werkstroom toohello toevoegen.

![Niet-verbonden AVC-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Niet-verbonden AAC codering*

Nu is er een incompatibiliteit: Er is alleen een één niet-gecomprimeerde audio-invoer pincode van Hallo AAC Encoder terwijl meer dan waarschijnlijk Hallo Media bestand invoer heeft twee verschillende audiostroom beschikbaar ongecomprimeerde: één voor Hallo audio kanaal en één voor Hallo links recht. (Als u bent omgaan met rond geluid, dat is 6 kanalen.) Zodat het is niet mogelijk verbinding toodirectly Hallo audio van Hallo Media bestand invoerbron naar Hallo AAC audio-codering. Hallo AAC onderdeel verwacht een zogenaamde 'interleaved' audiostroom: één stream met beide Hallo links en Hallo rechts kanalen interleaved met elkaar. Wanneer we weten uit onze media-bronbestand wat welke audio-nummers zijn in welke positie in de bron hello, kunnen we correct dergelijke interleaved audiostroom Hello genereren spreker posities voor links of rechts toegewezen.

Eerst moet een toogenerated een interleaved stroom uit Hallo vereist bron audio-kanalen. Hallo Audio Stream Interleaver onderdeel verwerken dit voor ons. Deze werkstroom toohello toevoegen en maak verbinding Hallo audio-uitvoer van Hallo Media bestandsinvoer in de App.

![Verbonden audiostroom Interleaver](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Verbonden audiostroom Interleaver*

Nu dat we een interleaved audiostroom hebben, opgeven we nog steeds niet waar tooassign Hallo naar links of rechts spreker posities aan. In de volgorde van toospecify dit, we kunnen gebruikmaken van Hallo spreker positie wel statusrapporten.

![Toevoegen van een spreker positie wel statusrapporten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Toevoegen van een spreker positie wel statusrapporten*

Hallo spreker positie wel statusrapporten voor gebruik met een aansluiting invoerstroom configureren via een Encoder vooraf ingestelde Filter van 'Custom' en Hallo kanaal voorinstelling "2.0 (L, R)" genoemd. (Dit wordt Hallo links spreker positie toochannel 1 en Hallo rechts spreker positie toochannel 2 toewijzen).

Verbinding maken met uitvoer Hallo van Hallo spreker positie wel statusrapporten toohello invoer Hallo AAC Encoder. Vervolgens geeft u op Hallo AAC Encoder toowork met een '2.0 (L, R)' kanaal vooraf ingesteld, zodat deze toodeal met stereogeluid als invoer.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Audio en Video-streams multiplex in een MP4-container
Gegeven onze AVC gecodeerde videostream en onze AAC gecodeerd audiostroom, kunnen we beide in vastleggen een. MP4-container. Hallo-proces van de combinatie van verschillende stromen in een enkel wordt 'multiplex' (of 'muxing') genoemd. In dit geval bent we Hallo audio en video streams Hallo in één samenhangende interleaving. MP4-pakket. Hallo-onderdeel dat coördineert dit voor een. MP4-container wordt Hallo Multiplexer ISO MPEG-4 genoemd. Toevoegen van een toohello ontwerpoppervlak en verbind Hallo AVC Video Encoder zowel Hallo AAC Encoder tooits invoer.

![Verbonden MPEG4 Multiplexer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Verbonden MPEG4 Multiplexer*

### <a id="MXF_to_MP4_writing_mp4"></a>Hallo MP4-bestand schrijven
Bij het schrijven van een bestand voor uitvoer wordt Hallo bestand Output-component gebruikt. We kunnen deze uitvoer toohello Hallo ISO MPEG-4 Multiplexer verbinding maken zodat de uitvoer opgehaald toodisk geschreven. toodo, verbinding maken met de Hallo Container (MPEG-4) uitvoer pincode toohello schrijven invoer pincode Hallo uitvoer in een bestand.

![Verbonden uitvoer in een bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Verbonden uitvoer in een bestand*

Hallo filename die wordt gebruikt, wordt bepaald door Hallo bestandseigenschap. Die eigenschap kan hardcoded tooa gegeven waarde zijn, kan een tooset zult deze via een expressie in plaats daarvan.

toohave hello werkstroom automatisch bepalen Hallo uitvoer bestand van de eigenschap name van een expressie, klikt u op Hallo buton volgende toohello bestandsnaam (volgende toohello mappictogram). Van Hallo vervolgkeuzemenu en selecteer vervolgens 'Expressie'. Er verschijnt nu Hallo expressie-editor. Schakel eerst Hallo-inhoud van het Hallo-editor.

![Lege expressie-Editor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Lege expressie-Editor*

Hallo expressie-editor kunt tooenter een letterlijke waarde, gecombineerd met een of meer variabelen. Variabelen beginnen met een dollarteken. Als u Hallo $ sleutel raakt, ziet Hallo editor vervolgkeuzelijst met beschikbare variabelen met een keuze. In ons geval gebruikt u een combinatie van Hallo uitvoer directory en Hallo base invoerbestand naamvariabele:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Gevuld uit de expressie-Editor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Gevuld uit de expressie-Editor*

> [!NOTE]
> In volgorde Raadpleeg toosee een bestand voor uitvoer van de coderingstaak in Azure, moet u een waarde in de expressie-editor Hallo opgeven.
>
>

Als u Hallo expressie bevestigt door roept ok, voorbeeld Hallo eigenschappenvenster op dit moment van deze toowhat waarde Hallo bestand eigenschap wordt omgezet.

![Expressie voor uitvoer dir wordt opgelost](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Expressie voor uitvoer dir wordt opgelost*

### <a id="MXF_to_MP4_asset_from_output"></a>Maken van een Media Services-activum van Hallo-bestand voor uitvoer
Terwijl we een MP4-bestand voor uitvoer geschreven hebben, moeten we nog steeds tooindicate dat dit bestand toohello hoort uitvoer asset welke mediaservices wordt gegenereerd als gevolg van deze werkstroom wordt uitgevoerd. toothis einde Hallo Uitvoerasset bestand knooppunt op Hallo werkstroom canvas wordt gebruikt. Alle binnenkomende bestanden in dit knooppunt maakt deel uit van Hallo resulterende Azure Media Services actief zijn.

Verbinding maken met Hallo uitvoer in een bestand onderdeel toohello Uitvoerasset bestand onderdeel toofinish Hallo werkstroom.

![Werkstroom is voltooid](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Werkstroom is voltooid*

### <a id="MXF_to_MP4_test"></a>Test Hallo lokaal werkstroom is voltooid
lokaal tootest Hallo-werkstroom bereikt Hallo afspeelknop in de werkbalk boven Hallo Hallo. Als de werkstroom Hallo uitgevoerd, inspecteren Hallo uitvoer wordt gegenereerd in de uitvoermap Hallo geconfigureerd. U ziet Hallo MP4-bestand voor uitvoer die is gecodeerd uit Hallo MXF invoerbron bestand is voltooid.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Codering MXF in MP4 - multibitrate dynamische pakketten ingeschakeld
In dit scenario maakt u een set van meerdere bitrate MP4-bestanden met AAC gecodeerde audio van één. Het invoerbestand MXF.

Wanneer een multi-bitrate asset uitvoer vereist is voor gebruik in combinatie met Hallo dynamische pakketten functies die worden aangeboden door Azure Media Services, meerdere GOP uitgelijnde MP4-bestanden van elk een andere bitrate en de resolutie toobe gegenereerd moet. toodo dus Hallo [MXF naar een single-bitrate MP4-codering](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) scenario bevat ons een goed uitgangspunt.

![Werkstroom starten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Werkstroom starten*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Toevoegen van een of meer extra MP4-uitvoer
Alle MP4-bestanden in onze resulterende Azure Media Services actief wordt ondersteuning voor een andere bitrate en resolutie. Stel een of meer MP4 uitvoer bestanden toohello werkstroom toevoegen.

toomake ervoor dat we hebben alle onze video coderingsprogramma's die zijn gemaakt met dezelfde instellingen Hallo, de meest geschikte tooduplicate Hallo al bestaande AVC Video Encoder en configureer een andere combinatie van de resolutie en bitrate (we toevoegen van een van de 960 x 540 op 25 frames per seconde op 2,5 Mbps). bestaande encoder tooduplicate hello, kopie plakt u deze op Hallo ontwerpoppervlak.

Verbinding maken met Hallo niet-gecomprimeerde Video-uitvoer pincode Hallo Media bestandsinvoer in onze nieuwe AVC-component.

![Tweede AVC encoder verbonden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Tweede AVC encoder verbonden*

Nu aan te passen Hallo-configuratie voor onze nieuwe AVC encoder toooutput 960 x 540 met 2,5 Mbps. (Gebruik de eigenschappen 'uitvoer breedte', 'Uitvoer hoogte' en 'Bitrate (kbps)' voor deze.)

Opgegeven willen we toouse Hallo resulterende asset samen met Azure Media Services dynamische pakketten, Hallo streaming-eindpunt moet toobe geschikt is voor het genereren van deze MP4-bestanden HLS/Fragmented MP4/DASH-fragmenten die exact uitgelijnde tooeach andere op een manier zijn dat clients die zijn schakelen tussen verschillende bitsnelheden een enkele smooth continue video en audio-ervaring krijgen. toomake die optreden, moeten we dat in de eigenschappen van beide encoders AVC Hallo Hallo GOP ('groep afbeeldingen')-grootte voor beide MP4-bestanden is ingesteld tooensure too2 seconden, dat kunnen worden gedaan door:

* Hallo GOP grootte modus tooFixed GOP grootte wordt ingesteld en
* Hallo sleutel Frame Interval tootwo in seconden.
* Hallo GOP IDR besturingselement tooClosed GOP tooensure alle GOP permanent zijn ook instellen op hun eigen zonder afhankelijkheden

toomake onze handige toounderstand werkstroom Hallo eerste AVC encoder te wijzigen "AVC Video Encoder 640 x 360 1200kbps ' en het tweede AVC-encoder Hallo ' AVC-Video Encoder 960 x 540 2500 kbps '.

Een tweede ISO MPEG-4 Multiplexer en de uitvoer van een tweede bestand toevoegen. Hallo multiplexer toohello nieuwe AVC encoder verbinding en zorg ervoor dat de uitvoer naar Hallo uitvoer in een bestand wordt geleid. Sluit ook Hallo AAC audio encoder uitvoer toohello nieuwe multiplexer van invoer. Hallo uitvoer in een bestand op zijn beurt vervolgens kan worden verbonden toohello Uitvoerasset bestand knooppunt tooadd het toohello Media Services Asset die wordt gemaakt.

![Tweede mixer en uitvoer in een bestand verbonden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Tweede mixer en uitvoer in een bestand verbonden*

Voor compatibiliteit met Azure Media Services dynamische pakketten, configureer Hallo multiplexer van Chunk modus tooGOP aantal of de duur en Hallo GOPs per segment too1 ingesteld. (Dit is standaard Hallo.)

![Mixer Chunk modi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Mixer Chunk modi*

Opmerking: u kunt toorepeat dit proces voor alle andere bitrate en resolutie combinaties die u wilt dat toohave toohello asset uitvoer toegevoegd.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configureren Hallo uitvoer bestandsnamen
Er is meer dan één enkel bestand toegevoegde toohello uitvoerasset. Dit biedt een noodzaak toomake ervoor Hallo bestandsnamen voor elk Hallo bestanden zijn van elkaar verschillen en mogelijk zelfs van toepassing een naamgevingsconventie daarom het wissen van de bestandsnaam Hallo bent u omgaan is met uitvoer.

Uitvoer benoemen kan worden beheerd via de expressies in Hallo designer. Open Hallo deelvenster met de eigenschap voor een van de onderdelen van Hallo-uitvoer in een bestand en open Hallo expressie-editor voor Hallo bestandseigenschap. Ons eerste uitvoerbestand via de volgende expressie Hallo is geconfigureerd (Zie Hallo-zelfstudie voor het beste van [MXF tooa single-bitrate MP4-uitvoer](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Dit betekent dat onze filename wordt bepaald door twee variabelen: Hallo uitvoer directory toowrite in en hello basisnaam van bron. Hallo voormalige wordt blootgesteld als eigenschap op Hallo werkstroom hoofdmap en Hallo laatstgenoemde wordt bepaald door de inkomende hello-bestand. Houd er rekening mee dat uitvoermap hello wordt gebruikt voor het lokale testen; Deze eigenschap wordt overschreven door Hallo workflowengine wanneer Hallo werkstroom door Hallo cloud-gebaseerde Mediaprocessor in Azure Media Services wordt uitgevoerd.
toogive beide onze uitvoerbestanden aan de naamgeving van een consistente uitvoer, wijziging Hallo naming expressie voor het eerst bestandsnaam:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

en de tweede Hallo naar:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Uitvoeren van een tussenliggende testuitvoering toomake ervoor dat beide MP4-bestanden voor uitvoer correct worden gegenereerd.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Toevoegen van een afzonderlijke-nummer
Later zullen we zien wanneer er een ISM-bestand toogo met onze MP4-bestanden voor uitvoer gegenereerd, wordt ook moet een MP4-bestand alleen audio als Hallo-nummer voor onze adaptief streamen. toocreate dit bestand, een extra mixer toohello-werkstroom (ISO-MPEG-4 Multiplexer) toevoegen en Hallo AAC encoder uitvoer pincode verbinden met de pincode van de invoer voor Track 1.

![Audio mixer toegevoegd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Audio mixer toegevoegd*

Maken van een derde bestand onderdeel toooutput Hallo uitgaande uitvoerstroom van Hallo mixer en Hallo bestand naming expressie als configureren:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Audio mixer maken van de uitvoer van bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Audio mixer maken van de uitvoer van bestand*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Hallo toe te voegen. ISM SMIL-bestand
Voor Hallo dynamische pakketten toowork in combinatie met beide MP4-bestanden (en alleen audio MP4 Hallo) in onze asset Media Services moet er ook een manifestbestand (ook wel een 'SMIL'-bestand: Synchronized Multimedia Integration Language). Dit bestand geeft tooAzure Media Services aan welke MP4-bestanden zijn beschikbaar voor dynamische pakketten en welke van deze tooconsider voor Hallo audio streaming. Een typische manifestbestand voor een set MP4 van met een enkele audiostroom ziet er als volgt:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

Hallo ISM-bestand bevat binnen een switch-instructie een verwijzing tooeach van Hallo afzonderlijke MP4 videobestanden en daarnaast audiobestand toothose ook een (of meer) verwijst naar tooan MP4 alleen met Hallo audio.

Hallo manifestbestand voor onze van MP4-set kan worden gedaan door middel van een component Hallo 'AMS Manifest Writer' genoemd. toouse, sleep deze naar het oppervlak Hallo en Hallo 'Schrijven voltooid' uitvoer pincodes vanaf Hallo drie uitvoer in een bestand onderdelen toohello AMS Manifest Writer invoer verbinding te maken. Controleer zeker tooconnect Hallo-uitvoer van Hallo AMS Manifest Writer toohello Uitvoerasset bestand.

Net als bij onze andere bestand uitvoer-onderdelen, Hallo ISM uitvoer bestandsnaam configureren met een expressie:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Onze klaar werkstroom ziet er Hallo hieronder:

![Voltooide MXF toomultibitrate MP4-werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Voltooide MXF toomultibitrate MP4-werkstroom*

## <a id="MXF_to__multibitrate_MP4"></a>MXF in multibitrate MP4 - verbeterde blauwdruk codering
In Hallo [vorige werkstroom procedure](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we hebt gezien hoe een enkel MXF invoer actief kan worden geconverteerd naar een uitvoerasset met multi-bitrate MP4-bestanden, een alleen-audio MP4-bestand en een manifestbestand voor gebruik in combinatie met Azure Media Services dynamische pakketten.

In dit scenario wordt weergegeven hoe sommige aspecten van Hallo kunnen worden verbeterd en eenvoudiger gemaakt.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Werkstroom overzicht tooenhance
![Multibitrate MP4 werkstroom tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 werkstroom tooenhance*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Naamgevingsregels voor bestanden
In de vorige werkstroom Hallo we een eenvoudige expressie als Hallo basis voor het genereren van bestandsnamen uitvoer opgegeven. We enkele duplicatie al hebben: Hallo Hallo afzonderlijke uitvoer bestand componenten opgegeven dergelijke expressie.

Bijvoorbeeld: onze onderdeel bestand uitvoer voor de eerste videobestand hello wordt geconfigureerd met deze expressie:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Voor de tweede uitvoer voor Hallo is video, hebben we een expressie zoals:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Zou niet het schonere minder fout foutgevoelige en gemakkelijker als we kan Verwijder enkele van deze duplicaten en dingen in plaats daarvan meer configureerbaar maken? Gelukkig kunnen we: Hallo designer van expressie mogelijkheden in combinatie met Hallo mogelijkheid toocreate aangepaste eigenschappen in de hoofdmap van de werkstroom Geef ons een extra beveiligingslaag gemak.

Stel, dat we je filename configuratie-station van Hallo bitsnelheden Hallo afzonderlijke MP4-bestanden. Deze bitsnelheden beogen wij tooconfigure op één centrale plaats (op Hallo root van onze grafiek), vanaf waar zij gebruikte tooconfigure en het station genereren bestandsnaam moeten worden. toodo, begin met het publiceren van Hallo bitrate eigenschap vanuit beide AVC coderingsprogramma's toohello hoofdmap van de werkstroom, zodat deze toegankelijk is vanaf beide Hallo-hoofdmap ook vanuit Hallo AVC coderingsprogramma's. (Zelfs als in twee verschillende plaatsen weergegeven, er is slechts één onderliggende waarde.)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Eigenschappen van onderdeel op Hallo werkstroom hoofdmap publiceren
Hallo eerste AVC encoder openen, toohello Bitrate (kbps) eigenschap gaat en kies uit de vervolgkeuzelijst Hallo publiceren.

![Publicatie Hallo bitrate-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Publicatie Hallo bitrate-eigenschap*

Hallo configureren dialoogvenster toopublish toohello basis van onze grafiek werkstroom met een gepubliceerde naam 'video1bitrate' en 'Video 1 Bitrate' de leesbare weergavenaam publiceren. Configureren van een aangepaste groepsnaam 'Bitsnelheden Streaming' genoemd en publiceren bereikt.

![Publicatie Hallo bitrate-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Publishing dialoogvenster voor de eigenschap bitrate*

Herhaal Hallo dezelfde voor Hallo bitrate eigenschap Hallo tweede AVC-codering en noem deze 'video2bitrate' met de weergavenaam 'Bitrate Video 2', in Hallo dezelfde aangepaste 'Bitsnelheden Streaming' groeperen.

Als we nu Hallo hoofdmap werkstroomeigenschappen controleren, zien we onze aangepaste groep Hello twee gepubliceerde eigenschappen worden weergegeven. Beide zijn opgetreden bij het Hallo-waarde van hun respectieve AVC encoder bitrate weergeven.

![Eigenschappen van gepubliceerde bitrate op basis van de werkstroom](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Wanneer we tooaccess deze eigenschappen van code of van een expressie willen, kunnen we dit doen als volgt:

* vanuit Inlinecode van een onderdeel direct onder de hoofdmap Hallo: node.getPropertyAsString('.. / video1bitrate', null)
* in een expressie: ${ROOT_video1bitrate}

Laten we onze-nummer bitrate ook op deze publicatie volledig Hallo 'Bitsnelheden Streaming' groep. In de eigenschappen van de Hallo Hallo AAC codering, Hallo Bitrate instelling zoekt en selecteert u publiceren in Hallo dropdown volgende tooit. Toohello hoofdmap van de grafiek met de naam 'audio1bitrate' Hallo publiceren en naam "Bitrate Audio 1" in onze aangepaste groep 'Bitsnelheden Streaming' weergegeven.

![Publishing dialoogvenster voor audio bitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Publishing dialoogvenster voor audio bitrate*

![Resulterende video en audio-eigenschappen in de hoofdmap van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Resulterende video en audio-eigenschappen in de hoofdmap van*

Houd er rekening mee dat als u een van deze drie wijzigt ook opnieuw configureert waarden en wijzigingen Hallo waarden op de betreffende onderdelen Hallo ze zijn gekoppeld aan (en indien gepubliceerd vanuit).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Uitvoerbestand namen zijn afhankelijk van de gepubliceerde eigenschapswaarden hebt gegenereerd
In plaats van hardcoderen onze gegenereerde bestandsnamen we kunnen nu wijzigen onze expressie filename op elk Hallo uitvoer in een bestand onderdelen toorely op Hallo bitrate eigenschappen die we zojuist hebt gepubliceerd op basis van Hallo-grafiek. Beginnen met het eerste bestandsuitvoer, Hallo bestandseigenschap vinden en bewerken Hallo expressie als volgt:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

Hallo andere parameters in deze expressie kunnen worden geopend en die zijn ingevoerd door roept Hallo dollarteken op Hallo toetsenbord in Hallo expressievenster. Een van de beschikbare parameters Hallo is onze video1bitrate-eigenschap die we eerder hebt gepubliceerd.

![Toegang tot de parameters in een expressie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Toegang tot de parameters in een expressie*

Hallo dezelfde voor Hallo bestandsuitvoer voor onze tweede video:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

en voor Hallo bestand met alleen audio-uitvoer:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Als we nu Hallo bitrate voor Hallo video of audio-bestanden wijzigen, de respectieve encoder Hallo opnieuw wordt geconfigureerd en Hallo bitrate-bestand naamconventie gehonoreerd alle automatische.

## <a id="thumbnails_to__multibitrate_MP4"></a>Miniaturen toomultibitrate MP4 uitvoer toevoegen
Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we nu zoeken in de miniaturen toohello uitvoer toevoegen.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Werkstroom overzicht tooadd miniatuurweergaven voor
![Multibitrate MP4 werkstroom toostart uit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 werkstroom toostart uit*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Toe te voegen JPG-codering
Hallo hart van onze miniaturen generatie worden Hallo JPG-Encoder onderdeel, kunnen toooutput JPG-bestanden.

![JPG-codering](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*JPG-codering*

Kan geen echter rechtstreeks verbinding wordt gemaakt onze stroom niet-gecomprimeerde Video van Hallo Media bestandsinvoer in Hallo JPG-codering. In plaats daarvan verwacht het toobe doorgegeven afzonderlijke frames. Dit we kunt doen via Hallo Video Frame-Gate onderdeel.

![Verbinding maken met een frame-gate toohello JPG-encoder](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Verbinding maken met een frame-gate toohello JPG-encoder*

Hallo frame-gate nadat elke zoveel seconden of frames kunt een video frame toopass. Hallo interval en Hallo tijdzoneverschil met waarop dit gebeurt, kan worden geconfigureerd in de eigenschappen van Hallo.

![Eigenschappen van video Frame-Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Eigenschappen van video Frame-Gate*

Laten we een miniatuur van elke minuut door in te stellen Hallo modus tooTime (seconden) maken en Hallo too60 Interval.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Omgaan met de conversie van de werkruimte
Hoewel lijkt het logisch zowel niet-gecomprimeerde Video pincodes van Hallo frame-gate en de Hallo Media bestandsinvoer kunnen nu worden verbonden, zouden we krijg een waarschuwing als er zou doen.

![Invoerkleur ruimte fout](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Invoerkleur ruimte fout*

Dit is omdat Hallo manier in welke kleur informatie wordt weergegeven in de oorspronkelijke onbewerkte niet-gecomprimeerde videostream, afkomstig zijn van onze MXF wijkt af van wat Hallo JPG-codering verwacht. Meer specifiek, een zogenaamde ' kleur ruimte ' van 'RGB-' of 'Grijswaarden' tooflow in verwacht. Dit betekent dat Hallo Video Frame-Gate van inkomende videostream moet toohave een conversie met betrekking tot de kleurenruimte als eerste toegepast.

Sleep Hallo werkstroom Hallo kleur ruimte Converter - Intel en verbind deze tooour frame-gate.

![Verbinding maken met een conversieprogramma voor kleur ruimte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Verbinding maken met een conversieprogramma voor kleur ruimte*

Kies in het venster Eigenschappen Hallo Hallo BGR 24 vermelding uit de lijst met vooraf ingestelde Hallo.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Schrijven Hallo miniaturen
Verschillende op onze MP4-video, Hallo JPG-Encoder onderdeel wordt de uitvoer van meer dan één bestand. In de volgorde toodeal dit, een onderdeel van de schrijver Scene zoeken JPG-bestand kan worden gebruikt: wordt Hallo binnenkomende JPG miniaturen nemen en geschreven, elke bestandsnaam wordt voorafgegaan door een ander nummer. (Hallo getal wordt gewoonlijk aangeeft Hallo aantal seconden/eenheden in welke miniatuur Hallo is afkomstig van Hallo-stroom)

![Inleiding tot Hallo Writer Scene zoeken JPG-bestand](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Inleiding tot Hallo Writer Scene zoeken JPG-bestand*

Hallo map uitvoerpad eigenschap configureren met de Hallo expressie: ${ROOT_outputWriteDirectory}

en Hallo eigenschap Filename voorvoegsel met:

    ${ROOT_sourceFileBaseName}_thumb_

Hallo voorvoegsel wordt bepalen hoe de miniatuur Hallo-bestanden worden wordt genoemd. Ze wordt voorafgegaan door een aantal die duiden Hallo miniatuur van positie in Hallo-stroom.

![Eigenschappen van de zoekopdracht JPG-bestand Writer Scene](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Eigenschappen van de zoekopdracht JPG-bestand Writer Scene*

Verbinding maken met Hallo Scene zoeken JPG-bestand Writer toohello Uitvoerasset bestand knooppunt.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Fouten opsporen in een werkstroom
Verbinding maken met invoer Hallo van Hallo kleur ruimte converter toohello onbewerkte niet-gecomprimeerde video-uitvoer. Nu een lokale test uitvoeren voor Hallo werkstroom uitvoeren. Er is een goede kans Hallo werkstroom plotseling wordt niet langer uitgevoerd en geven met een rode omtrek op Hallo-onderdeel dat is een fout opgetreden:

![Kleur ruimte Converter fout](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Kleur ruimte Converter fout*

Klikt u op Hallo enigszins red "E" pictogram in Hallo rechtsboven Hallo kleur ruimte Converter onderdeel toosee wat is Hallo reden Hallo codering poging is mislukt.

![Kleur ruimte Converter foutberichtvenster](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Kleur ruimte Converter foutberichtvenster*

Het blijkt, zoals u kunt zien, dat Hallo binnenkomende kleurruimte standaard voor Hallo kleur ruimte converter toobe rec601 voor onze aangevraagde conversie van YUV tooRGB heeft. Onze stroom wordt niet blijkbaar van rec601 aangegeven. (Rec 601 is een standaard voor het coderen van elkaar kruisende analoge video signalen in digitale video vorm. Hiermee wordt een actieve regio die betrekking hebben op 720 helderheid voorbeelden en 360 chrominantie voorbeelden per regel. Hallo kleur system codering wordt ook wel YCbCr 4:2:2.)

toofix, geven we je op Hallo metagegevens van onze stroom die we je rec601 inhoud betreft. toodo gebruiken we een Video gegevens Type Updater onderdeel, die we Between onze onbewerkte bron- en Hallo kleur ruimte conversieonderdeel hebt geplaatst. Dit type gegevens updater kunt u handmatig bijwerken van bepaalde video gegevens Hallo type-eigenschappen. Een kleur ruimte Standard van 'Rec 601' tooindicate configureren. Als er geen kleurruimte nog gedefinieerd is, wordt hierdoor Hallo Video gegevens Type Updater tootag Hallo stream met Hallo 'Rec 601' kleurruimte. (Niet overschrijft alle bestaande metagegevens als Hallo onderdrukking selectievakje is ingeschakeld.)

![Bijwerken van kleur ruimte standaard op Hallo gegevens Type Updater](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Bijwerken van kleur ruimte standaard op Hallo gegevens Type Updater*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Werkstroom is voltooid
Nu ons onze werkstroom is voltooid, doet u een andere testuitvoering toosee deze aan.

![Voltooide werkstroom voor meerdere mp4-uitvoer met miniaturen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Voltooide werkstroom voor meerdere mp4-uitvoer met miniaturen*

## <a id="time_based_trim"></a>Op basis van tijd worden ingekort door multibitrate MP4-uitvoer
Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we wordt nu op zoek zijn naar bijsnijden Hallo bronvideo op basis van tijdstempels.

### <a id="time_based_trim_start"></a>Werkstroom overzicht toostart bijsnijden aan toe te voegen
![Werkstroom tooadd bijsnijden te starten](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Werkstroom tooadd bijsnijden te starten*

### <a id="time_based_trim_use_stream_trimmer"></a>Hallo stroom Trimmer gebruiken
Hallo stroom Trimmer component kunt tootrim Hallo begin en einde van een invoerstroom op basis van informatie over de tijdsinstellingen (seconden, minuten,...). Hallo trimmer biedt geen ondersteuning voor op basis van het frame-opmaak.

![Stroom Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Stroom Trimmer*

In plaats van rechtstreeks Hallo AVC coderingsprogramma's en spreker positie wel statusrapporten toohello Media bestandsinvoer koppelt, moet we tussen deze stroom Hallo trimmer plaatsen. (Één voor de video signaal Hallo en één voor Hallo interleaved audio signaal).

![Stroom Trimmer tussen plaatsen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Stroom Trimmer tussen plaatsen*

Laten we Hallo trimmer zodanig configureren dat we alleen video en audio tussen 15 en 60 seconden in Hallo video verwerkt.

Ga toohello eigenschappen van Hallo Video stroom Trimmer en zowel de begintijd (15s) en de eigenschappen van de eindtijd (60s) configureren. toomake zorgen zowel onze trimmer audio en video altijd geconfigureerde toohello dezelfde beginnen en eindigen waarden, komen we deze hoofdmap toohello van Hallo-werkstroom.

![Start tijdeigenschap van stroom Trimmer publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Start tijdeigenschap van stroom Trimmer publiceren*

![Dialoogvenster Eigenschappen voor de begintijd publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Dialoogvenster Eigenschappen voor de begintijd publiceren*

![Dialoogvenster Eigenschappen voor de eindtijd publiceren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Dialoogvenster Eigenschappen voor de eindtijd publiceren*

Als we nu Hallo hoofdmap van de werkstroom controleren, beide eigenschappen worden netjes weergegeven en kunnen worden geconfigureerd vanaf daar.

![Gepubliceerde eigenschappen die beschikbaar zijn in de hoofdmap van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Gepubliceerde eigenschappen die beschikbaar zijn in de hoofdmap van*

Nu Hallo bijsnijden eigenschappen openen vanuit Hallo audio trimmer en zowel begin- en eindtijden configureren met een expressie die toohello verwijst eigenschappen op basis van onze werkstroom Hallo gepubliceerd.

Voor Hallo audio bijsnijden begintijd:

    ${ROOT_TrimmingStartTime}

en voor de eindtijd:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Werkstroom is voltooid
![Werkstroom is voltooid](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Werkstroom is voltooid*

## <a id="scripting"></a>Introducing hello onderdeel in een script vastgelegd
Script onderdelen kunnen willekeurige scripts uitvoeren tijdens Hallo uitvoering fasen van de werkstroom. Er zijn vier verschillende scripts die kunnen worden uitgevoerd, elk met specifieke kenmerken en hun eigen plaats in Hallo werkstroom levenscyclus:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

Hallo documentatie Hallo onderdeel in een script vastgelegd gaat in meer detail voor elk van de bovenstaande Hallo. In [Hallo volgende sectie](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Hallo **realizeScript** scripting onderdeel is gebruikte tooconstruct een cliplist xml op Hallo snel wanneer Hallo werkstroom wordt gestart. Dit script wordt aangeroepen tijdens setup Hallo onderdelen die slechts één keer wordt uitgevoerd in de levenscyclus.

### <a id="scripting_hello_world"></a>Uitvoeren van scripts in een werkstroom: Hallo wereld
Sleep een onderdeel in een script vastgelegd naar het ontwerpoppervlak Hallo en wijzig de naam (bijvoorbeeld ' SetClipListXML').

![Script onderdelen toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Script onderdelen toevoegen*

Wanneer u de eigenschappen van Hallo inspecteert Hallo Component in een script vastgelegd, Hallo vier verschillende scripttypen worden weergegeven, elk ander configureerbare tooa-script.

![Eigenschappen van scripts](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Eigenschappen van scripts*

Wissen Hallo processInputScript en open de editor voor Hallo realizeScript Hallo. Nu we alles hebt ingesteld en klaar toostart scripting.

Scripts worden geschreven in Groovy, een dynamisch gecompileerde scripttaal voor Hallo Java-platform die compatibel is met Java behoudt. De meeste Java-code is daadwerkelijk, geldige Groovy code.

We gaan een eenvoudige hello world groovy script schrijven in de context van onze realizeScript Hallo. Voer Hallo volgende in Hallo-editor:

    node.log("hello world");

Een lokale testuitvoering nu uitvoeren. Controleer na het uitvoeren (via het tabblad voor het systeem op Hallo Hallo onderdeel in een script vastgelegd) Hallo logboeken-eigenschap.

![Hello world logboekuitvoer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Hello world logboekuitvoer*

Hallo knooppuntobject we Hallo logboek methode niet aanroepen voor, verwijst tooour huidige 'knooppunt' of we je scripting binnen Hallo-onderdeel. Elk onderdeel heeft als zodanig Hallo mogelijkheid toooutput logboekgegevens, beschikbaar via het tabblad Hallo-systeem. In dit geval uitvoer we Hallo string literal "Hallo wereld". Belangrijke toounderstand hier is dat dit toobe een foutopsporing waardevol hulpmiddel bewijzen kan, zonder dat u inzicht in welke script Hallo daadwerkelijk doet.

Van in onze scriptomgeving hebben we ook toegang tooproperties van andere onderdelen. Probeer dit:

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

Onze logboekvenster weergeven ons hello te volgen:

![De uitvoer voor toegang tot de Knooppuntpaden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*De uitvoer voor toegang tot de Knooppuntpaden*

## <a id="frame_based_trim"></a>Op basis van het frame worden ingekort door multibitrate MP4-uitvoer
Een werkstroom die wordt gegenereerd vanaf [een multibitrate MP4-uitvoer van een invoer MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we wordt nu op zoek zijn naar bijsnijden Hallo bronvideo op basis van het frame.

### <a id="frame_based_trim_start"></a>Blauwdruk overzicht toostart bijsnijden aan toe te voegen
![Werkstroom toostart bijsnijden aan toe te voegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Werkstroom toostart bijsnijden aan toe te voegen*

### <a id="frame_based_trim_clip_list"></a>Met behulp van Hallo Clip lijst XML
In alle vorige werkstroom zelfstudies gebruikt we Hallo Media bestand invoer onderdeel als onze video-invoerbron. Voor dit specifieke scenario echter worden gebruikt Hallo Clip lijst brononderdeel in plaats daarvan. Houd er rekening mee dat dit mag geen Hallo voorkeur manier van werken; Hallo Clip lijst bron alleen gebruiken wanneer er een echte reden toodo dus (Hallo hieronder geval waar we doorvoeren, zoals gebruik van Hallo clip lijst bijsnijden mogelijkheden).

tooswitch van onze Media bestandsinvoer toohello Clip lijst bron, Hallo Clip lijst brononderdeel naar het ontwerpoppervlak Hallo slepen en maak verbinding Hallo Clip lijst XML pincode toohello Clip lijst XML-knooppunt van Hallo workflow designer. Dit Hallo Clip lijst bron met uitvoer pincodes, tooour invoervideo op basis van gegevens moet voorzien. Hallo niet-gecomprimeerde Video en Audio van niet-gecomprimeerde pincodes nu verbinding te maken van Hallo Hallo Clip lijst bron toohello respectieve AVC coderingsprogramma's en Audio-stroom Interleaver. Verwijder nu Hallo Media bestandsinvoer.

![Hallo Media bestandsinvoer vervangen door Hallo Clip lijst bron](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Hallo Media bestandsinvoer vervangen door Hallo Clip lijst bron*

Hallo Clip lijst brononderdeel neemt als invoer een 'Clip lijst XML'. Als u lokaal Hallo bron bestand tootest met, is deze clip lijst xml automatisch ingevuld voor u.

![Automatisch ingevuld Clip lijst XML-eigenschap](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Automatisch ingevuld Clip lijst XML-eigenschap*

Zoek een beetje dichter toohello xml, is dit hoe het eruit:

![Dialoogvenster met de lijst clip bewerken](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Dialoogvenster met de lijst clip bewerken*

Dit echter doorgevoerd niet Hallo-mogelijkheden van XML-Hallo clip lijst. Een optie die we hebben is tooadd een element 'Trim' onder Hallo video en audio-bron, als volgt:

![Een lijst van element knippen toohello clip toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Een lijst van element knippen toohello clip toevoegen*

Als u XML-lijst van Hallo-clip als volgt hierboven wijzigen en uitvoeren van een lokale test uitgevoerd, ziet u Hallo video correct zijn afgekapt tussen 10 en 20 seconden in Hallo video.

Strijdig toowhat gebeurt wanneer u een lokale uitvoering doen, hoewel deze zeer dezelfde cliplist xml geen Hallo hetzelfde effect als toegepast in een werkstroom die wordt uitgevoerd in Azure Media Services. Wanneer Azure Premium-codering wordt gestart, Hallo cliplist xml wordt gegenereerd telkens opnieuw op basis van het Hallo invoerbestand Hallo codering is taak opgegeven. Dit betekent dat eventuele wijzigingen die we op Hallo xml doen helaas zou worden overschreven.

toocounter hello cliplist xml wordt gewist wanneer een codeertaak wordt gestart, we kunt opnieuw gegenereerd op Hallo snel direct na Hallo begin van de werkstroom. Deze aangepaste acties kunnen worden uitgevoerd via wat een 'in een script vastgelegd onderdeel' wordt genoemd. Zie voor meer informatie [Introducing hello onderdeel in een script vastgelegd](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Sleep een onderdeel in een script vastgelegd naar het ontwerpoppervlak Hallo en wijzig deze te 'SetClipListXML'.

![Script onderdelen toevoegen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Script onderdelen toevoegen*

Wanneer u de eigenschappen van Hallo inspecteert Hallo Component in een script vastgelegd, Hallo vier verschillende scripttypen worden weergegeven, elk ander configureerbare tooa-script.

![Eigenschappen van scripts](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Eigenschappen van scripts*

### <a id="frame_based_trim_modify_clip_list"></a>Hallo clip lijst van een onderdeel in een script vastgelegd wijzigen
Voordat we Hallo cliplist XML-bestand dat wordt gegenereerd tijdens het opstarten van de werkstroom opnieuw schrijven kunt, moeten we toohave access toohello cliplist xml-eigenschap en de inhoud. We kunnen dit doen als volgt:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Binnenkomende clip lijst aan te melden](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Binnenkomende clip lijst aan te melden*

Eerst moet u een manier toodetermine vanaf dat moment tot dat moment we tootrim willen Hallo video. toomake deze handige toohello minder technische gebruiker van de werkstroom hello, publiceren twee eigenschappen toohello root van Hallo-grafiek. toodo dit ontwerpoppervlak Hallo Klik met de rechtermuisknop en selecteer 'Eigenschap toevoegen':

* Eerste eigenschap: 'ClippingTimeStart' van het type: 'TIJDCODE'
* Tweede eigenschap: 'ClippingTimeEnd' van het type: 'TIJDCODE'

![Dialoogvenster van eigenschappen toevoegen voor de begintijd knippen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Dialoogvenster van eigenschappen toevoegen voor de begintijd knippen*

![Gepubliceerde eigenschappen van de tijd knipsel in de hoofdmap van de werkstroom van](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Gepubliceerde eigenschappen van de tijd knipsel in de hoofdmap van de werkstroom van*

Beide eigenschappen tooa geschikte waarde configureren:

![Hallo knipsel begin- en eigenschappen configureren](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Hallo knipsel begin- en eigenschappen configureren*

Nu uit in onze script we hebben toegang tot beide eigenschappen, als volgt:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Venster van het logboek met begin en einde van knippen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Venster van het logboek met begin en einde van knippen*

Laten we parseren Hallo tijdcode tekenreeksen in een handiger toouse formulier, met behulp van een eenvoudige reguliere expressie:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Het venster met de uitvoer van de geparseerde tijdcode](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Het venster met de uitvoer van de geparseerde tijdcode*

Met deze informatie bij de hand we nu Hallo cliplist xml tooreflect Hallo start kunt wijzigen en eindtijden voor Hallo frame nauwkeurige paginaknipsel van Hallo film gewenst.

![Script code tooadd trim-elementen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Script code tooadd trim-elementen*

Dit is gedaan door de normale tekenreeks bestandsbewerkingen. Hallo resulterende gewijzigde illustratie lijst xml teruggeschreven toohello clipListXML-eigenschap op basis van Hallo-werkstroom via de methode 'setProperty' Hallo. Hallo logboekvenster na het uitvoeren van een andere test zou ons Hallo volgende weergegeven:

![Hallo resulterende clip lijst logboekregistratie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Hallo resulterende clip lijst logboekregistratie*

Voer een test uitgevoerd toosee hoe Hallo video en audio-stromen hebben is afgekapt. Als u meer dan één testuitvoering met verschillende waarden voor Hallo bijsnijden punten doet, ziet u dat deze wordt geen rekening worden gehouden echter! Hallo reden hiervoor is dat designer hello, in tegenstelling tot hello Azure runtime, niet overschrijven Hallo cliplist xml elke gebeurt. Dit betekent dat alleen hello zeer eerste keer dat u hebt ingesteld Hallo in en uit punten zullen Hallo xml tootransform, alle andere tijden onze component guard Hallo (als (clipListXML.indexOf ('<trim>') == van -1)) verhindert dat Hallo werkstroom toe te voegen op een andere knippen element als er al een aanwezig.

toomake onze werkstroom handige tootest lokaal we best house-keeping code die als een beperkende element aanwezig was inspecteert toevoegen. Als dit het geval is, kunnen we deze verwijderen voordat u doorgaat doordat Hallo xml met Hallo nieuwe waarden. In plaats van gewone tekenreeksmanipulatie, is het waarschijnlijk veiliger toodo dit via echte xml-object model parseren.

Voordat we deze code toebehoort echter toevoegen kunt, moeten we een aantal importinstructies op Hallo eerst van onze script starten tooadd:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Hierna kunt we Hallo vereist reinigen code toevoegen:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Deze code gaat erboven Hallo punt waarop we Hallo trim elementen toohello cliplist xml toevoegen.

We kunnen op dit moment worden uitgevoerd en onze werkstroom zoals net als we willen dat bij dat Hallo wijzigingen toegepast ooit tijd wijzigen.    

### <a id="frame_based_trim_clippingenabled_prop"></a>De eigenschap van een ClippingEnabled gemak toe te voegen
Als u wilt u mogelijk niet altijd bijsnijden toohappen, gaan we voltooien uit onze werkstroom door toe te voegen een handige Booleaanse vlag die aangeeft of we wilt tooenable knippen / knipsel.

Publiceren voordat u, net zoals een nieuwe eigenschap toohello basis van onze werkstroom aangeroepen 'ClippingEnabled' van het type 'BOOLEAN'.

![Een eigenschap voor het inschakelen van knipsel gepubliceerd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Een eigenschap voor het inschakelen van knipsel gepubliceerd*

Met Hallo hieronder eenvoudige guard component, kunnen we controleren of bijsnijden vereist is en beslissen of u onze lijst clip toobe gewijzigd of niet als zodanig moet.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Volledige code
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Zie ook
[Inleiding tot Premium codering in Azure Media Services](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Hoe tooUse Premium codering in Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Codering van inhoud op aanvraag met Azure mediaservice](media-services-encode-asset.md#media-encoder-premium-workflow)

[Indelingen en codecs voor Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md)

[Werkstroom voorbeeldbestanden](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Azure Media Services Explorer-hulpprogramma](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
