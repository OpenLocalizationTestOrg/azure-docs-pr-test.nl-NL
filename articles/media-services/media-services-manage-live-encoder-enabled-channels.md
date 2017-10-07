---
title: aaaLive streamen met Azure Media Services toocreate multi-bitrate streams | Microsoft Docs
description: 'Dit onderwerp wordt beschreven hoe tooset van een kanaal dat u een single bitrate ontvangt livestream van een on-premises coderingsprogramma en voert deze live codering tooadaptive bitrate stream met Media Services. Hallo stream kan vervolgens worden geleverd tooclient afspelen toepassingen via een of meer Streaming-eindpunten, met behulp van een Hallo adaptieve streaming protocollen te volgen: MPEG-DASH HLS, Smooth Stream.'
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Live streamen met Azure Media Services toocreate multi-bitrate streams
## <a name="overview"></a>Overzicht
Azure Media Services (AMS) een **kanaal** vertegenwoordigt een pijplijn voor het verwerken van live streaming inhoud. Een **kanaal** live invoer streams ontvangt op twee manieren:

* Een on-premises live codering verzendt een single-bitrate stream toohello-kanaal dat is ingeschakeld tooperform live codering met Media Services in een Hallo volgende indelingen: RTP (MPEG-TS), RTMP of Smooth Streaming (gefragmenteerde MP4). Hallo kanaal voert live codering Hallo binnenkomende single-bitrate stream tooa multi-bitrate (adaptieve) videostream. Desgevraagd levert Media Services Hallo stroom toocustomers.
* Een on-premises live codering verzendt een multi-bitrate **RTMP** of **Smooth Streaming** tooperform live codering met AMS (gefragmenteerde MP4) toohello kanaal dat niet is ingeschakeld. Hallo ingenomen streams doorgeven **kanaal**s zonder verdere verwerking. Deze methode wordt aangeroepen **pass-through**. U kunt Hallo volgende live coderingsprogramma's die multi-bitrate Smooth Streaming uitvoeren: MediaExcel, Ateme, stel communicatie, Envivio, Cisco en Elemental. Hallo volgende live coderingsprogramma's voeren RTMP: Adobe Flash Media Live coderingsprogramma (FMLE), Telestream Wirecast, Haivision, Teradek en Tricaster coderingsprogramma's.  Een live coderingsprogramma kan ook een single-bitrate stream tooa kanaal dat niet is ingeschakeld voor live codering, maar dit wordt niet aanbevolen verzenden. Desgevraagd levert Media Services Hallo stroom toocustomers.
  
  > [!NOTE]
  > Een Pass Through-methode is de meest voordelige manier Hallo toodo live te streamen.
  > 
  > 

Vanaf versie Hallo Media Services 2.10, wanneer u een kanaal maakt, kunt u opgeven op welke manier u wenst de invoerstroom van kanaal tooreceive hello en of u wilt voor Hallo kanaal tooperform live codering van uw stream. U hebt hiervoor twee opties:

* **Geen** : deze waarde opgeven als u van plan toouse een on-premises live coderingsprogramma die multi-bitrate stream (Pass Through-stream bent) wordt uitgevoerd. In dit geval stroom voor inkomende hello doorgegeven via toohello zonder alle codering. Dit is Hallo gedrag van een versie van de voorafgaande too2.10 kanaal.  Zie voor meer informatie over het werken met kanalen van dit type, [Live streamen met on-premises-coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md).
* **Standaard** – Selecteer deze waarde als u van plan toouse Media Services tooencode bent uw single-bitrate livestream toomulti-bitrate stream. Let erop dat er een facturering invloed voor live codering en u rekening mee houden moet dat een live codering kanaal waardoor de status 'Actief' hello wordt facturering worden kosten in rekening.  Het is raadzaam uw actieve kanalen onmiddellijk te beëindigen nadat uw live-streaming gebeurtenis is voltooid tooavoid extra per uur kosten.

> [!NOTE]
> In dit onderwerp worden de kenmerken van de kanalen die zijn ingeschakeld tooperform live codering (**standaard** coderingstype). Zie voor informatie over het werken met kanalen die niet zijn ingeschakeld tooperform live codering, [Live streamen met on-premises-coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md).
> 
> Zorg ervoor dat tooreview hello [overwegingen](media-services-manage-live-encoder-enabled-channels.md#Considerations) sectie.
> 
> 

## <a name="billing-implications"></a>De implicaties van facturering
Een kanaal voor live codering begint zodra de status te verandert 'actief' via Hallo API facturering.   U kunt ook Hallo status weergeven in hello Azure-portal of in hello Azure Media Services Explorer hulpprogramma (http://aka.ms/amse).

Hallo volgende tabel toont hoe kanaal statussen worden toegewezen toobilling statussen in Hallo API en de Azure-portal. Houd er rekening mee Hallo statussen verschillen enigszins tussen Hallo API en UX-Portal Als u een kanaal Hallo 'Actief' status via Hallo API, of in Hallo 'Gereed' of 'Streaming' status in hello Azure-portal, facturering actief zijn.
Hallo-kanaal toostop van u verdere facturering, hebt u tooStop Hallo kanaal via Hallo API of in hello Azure-portal.
U bent zelf verantwoordelijk voor het stoppen van de kanalen wanneer u klaar bent met het Hallo-kanaal voor live codering.  Fout toostop een codering kanaal leidt tot voortdurende facturering.

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

### <a name="automatic-shut-off-for-unused-channels"></a>Automatisch afsluiten uit voor ongebruikte kanalen
Beginnen met 25 januari 2016 Media Services uitgerold een update die automatisch een kanaal (met live codering ingeschakeld) gestopt nadat deze in een niet-gebruikte status actief is geweest gedurende een lange periode. Dit geldt tooChannels die geen actieve programma's hebben en die een invoer bijdrage-kanaal voor langere tijd niet hebben ontvangen.

Hallo-drempelwaarde voor een niet-gebruikte periode is nominaal 12 uur, maar onderwerp toochange is.

## <a name="live-encoding-workflow"></a>Werkstroom voor Live codering
Hallo onderstaande diagram ziet u een live streaming-werkstroom waarbij een kanaal een single-bitrate stream ontvangt in een van de volgende protocollen Hallo: RTMP, Smooth Streaming of RTP (MPEG-TS); het codeert Hallo-stroom tooa multi-bitrate stream vervolgens. 

![Live-werkstroom][live-overview]

## <a id="scenario"></a>Algemeen Scenario voor Live streamen
Hallo hieronder vindt u algemene stappen voor het maken van algemene toepassingen voor live streamen.

> [!NOTE]
> Hallo maximum is aanbevolen duur van een live gebeurtenis op dit moment acht uur. Neem contact op met amslived op Microsoft.com als u toorun een kanaal voor langere tijd nodig. Let erop dat er een facturering invloed voor live codering en u rekening mee houden moet dat een live codering kanaal waardoor de status 'Actief' hello wordt elk uur facturering worden kosten in rekening.  Het is raadzaam uw actieve kanalen onmiddellijk te beëindigen nadat uw live-streaming gebeurtenis is voltooid tooavoid extra per uur kosten. 
> 
> 

1. Sluit een videocamera tooa-computer. Start en configureer een on-premises live coderingsprogramma dat een **één** bitrate stream in een van de volgende protocollen Hallo: RTMP, Smooth Streaming of RTP (MPEG-TS). 
   
    Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.
2. Maak en start een kanaal. 
3. URL voor opnemen ophalen Hallo kanaal. 
   
    Hallo URL voor opnemen wordt gebruikt door Hallo live coderingsprogramma toosend Hallo stroom toohello kanaal.
4. Hallo kanaal preview URL niet ophalen. 
   
    Gebruik deze URL tooverify dat Hallo livestream goed door het kanaal wordt ontvangen.
5. Maak een programma. 
   
    Wanneer met behulp van hello Azure-portal, het maken van een programma ook een asset gemaakt. 
   
    Wanneer u SDK voor .NET of REST u toocreate een asset als moet toouse dit activum bij het maken van een programma. 
6. Hallo-asset die zijn gekoppeld aan het Hallo-programma publiceren.   
   
    >[!NOTE]
    >Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud heeft toobe in Hallo **met** status. 
    
7. Start Hallo programma wanneer u bent klaar toostart streamen en te archiveren.
8. Hallo live coderingsprogramma kan desgewenst gesignaleerde toostart een advertentie zijn. Hallo advertentie wordt ingevoegd in de uitvoerstroom Hallo.
9. Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.
10. Verwijder Hallo programma (en verwijder desgewenst Hallo asset).   

> [!NOTE]
> Het is heel belangrijk niet tooforget tooStop een Live Encoding-kanaal. Let er is een uur facturering gevolgen voor live codering en u moet rekening mee houden dat een live codering kanaal waardoor de status 'Actief' hello wordt facturering worden kosten in rekening.  Het is raadzaam uw actieve kanalen onmiddellijk te beëindigen nadat uw live-streaming gebeurtenis is voltooid tooavoid extra per uur kosten. 
> 
> 

## <a id="channel"></a>De invoer-kanaal (opnemen) configuraties
### <a id="Ingest_Protocols"></a>Streaming-opnameprotocol
Als hello **coderingstype** te is ingesteld,**standaard**, geldige opties zijn:

* **RTP** (MPEG-TS): MPEG-2-transportstroom via RTP.  
* Single-bitrate **RTMP**
* Single-bitrate **gefragmenteerde MP4** (Smooth Streaming)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) - MPEG-2-transportstroom via RTP.
Typische gebruiksscenario's: 

Professionele omroeporganisaties werken doorgaans met geavanceerde lokale live coderingsprogramma's van leveranciers zoals elementair technologieën, Ericsson, Ateme, Imagine of Envivio toosend een stroom. Vaak wordt gebruikt in combinatie met een IT-afdeling en particuliere netwerken.

Overwegingen:

* Hallo-gebruik van een bepaald programma-transportstroom (SharePoint Team Services) invoer wordt sterk aanbevolen. 
* U kunt invoeren van too8 audio-stromen met MPEG-2 TS via RTP. 
* Hallo videostream moet een gemiddelde bitrate hieronder 15 Mbps
* cumulatieve gemiddelde bitrate Hallo van Hallo audio streams moeten uit minder dan 1 Mbps
* Hieronder worden de ondersteunde codecs Hallo:
  
  * MPEG-2 / H.262 Video 
    
    * Belangrijkste profiel (4:2:0)
    * Hoge-profiel (4:2:0, 4:2:2)
    * 422 profiel (4:2:0, 4:2:2)
  * MPEG-4 AVC / H.264-Video  
    
    * Basislijn, Main, hoge-profiel (8-bits versie 4:2:0)
    * Profiel voor maximaal 10 (10-bits versie 4:2:0)
    * Hoge 422 profiel (10-bits versie 4:2:2)
  * AAC MPEG-2-Kredietbrief Audio 
    
    * Mono, Stereo, rond (5.1, 7.1)
    * MPEG-2-stijl ADTS verpakking
  * Dolby Digital (AC-3) Audio 
    
    * Mono, Stereo, rond (5.1, 7.1)
  * MPEG-Audio (laag II en III) 
    
    * Mono, Stereo
* Aanbevolen uitzending coderingsprogramma's omvatten:
  
  * Stel communicatie Selenio ENC 1
  * Stel communicatie Selenio ENC 2
  * Live elemental

#### <a id="single_bitrate_RTMP"></a>Single-bitrate RTMP
Overwegingen:

* Hallo binnenkomende stream mag niet multi-bitrate video
* Hallo videostream moet een gemiddelde bitrate hieronder 15 Mbps
* Hallo audiostroom moet een gemiddelde bitrate lager dan 1 Mbps
* Hieronder worden de ondersteunde codecs Hallo:
* MPEG-4 AVC / H.264-Video
* Basislijn, Main, hoge-profiel (8-bits versie 4:2:0)
* Profiel voor maximaal 10 (10-bits versie 4:2:0)
* Hoge 422 profiel (10-bits versie 4:2:2)
* AAC MPEG-2-Kredietbrief Audio
* Mono, Stereo, rond (5.1, 7.1)
* 44,1 kHz samplefrequentie
* MPEG-2-stijl ADTS verpakking
* Aanbevolen coderingsprogramma's zijn onder andere:
* Telestream Wirecast
* Media Flash Live codering

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>Single-bitrate Fragmented MP4 (Smooth Streaming);
Typische gebruiksscenario's:

Gebruik een on-premises live coderingsprogramma's van leveranciers zoals elementair technologieën, Ericsson Ateme, Envivio toosend Hallo invoerstroom via Hallo open internet tooa in de buurt van Azure-Datacenter.

Overwegingen:

Hetzelfde als voor [single-bitrate RTMP](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Andere overwegingen
* U kunt Hallo invoerprotocol tijdens het Hallo kanaal niet wijzigen of de gekoppelde programma's worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u afzonderlijke kanalen voor elk invoerprotocol.
* Maximale resolutie voor binnenkomende videostream Hallo 1920 x 1080 is en maximaal 60 velden/seconde als interlaced of 30 frames per seconde als progressief.

### <a name="ingest-urls-endpoints"></a>URL's (eindpunten) voor opnemen
Een kanaal biedt een invoereindpunt (de URL voor opnemen) dat u in Hallo live codering, opgeeft zodat Hallo encoder kunt push streams tooyour kanalen.

U krijgt Hallo URL's voor opnemen wanneer u een kanaal hebt gemaakt. tooget deze URL's, Hallo kanaal heeft geen toobe in Hallo **met** status. Wanneer u klaar toostart gegevens worden gepusht naar Hallo kanaal bent, moet dit Hallo **met** status. Zodra Hallo kanaal ophalen van gegevens start, kunt u uw stream via de voorbeeld-URL Hallo bekijken.

Hebt u een optie voor het opnemen van gefragmenteerde MP4 (Smooth Streaming) livestream via een SSL-verbinding. tooingest via SSL, zorg ervoor dat tooupdate hello tooHTTPS URL voor opnemen. Houd er rekening mee dat op dit moment AMS biedt geen ondersteuning voor SSL met aangepaste domeinen.  

### <a name="allowed-ip-addresses"></a>Toegestane IP-adressen
U kunt Hallo IP-adressen die zijn toegestaan toopublish video toothis kanaal definiëren. Toegestane IP-adressen kunnen worden opgegeven als een enkel IP-adres (bijvoorbeeld 10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22) of een IP-adresbereik met een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld '10.0.0.1(255.255.252.0)').

Als geen IP-adressen zijn opgegeven en er geen regeldefinitie bestaat, zijn er geen IP-adressen toegestaan. tooallow elk IP-adres, maakt u een regel en stelt u 0.0.0.0/0.

## <a name="channel-preview"></a>Kanaal preview
### <a name="preview-urls"></a>Voorbeeld-URL 's
Kanalen bieden een preview-eindpunt (preview URL) toopreview te gebruiken en uw stream te valideren voordat verdere verwerking en levering.

Wanneer u Hallo kanaal hebt gemaakt, kunt u de voorbeeld-URL Hallo ophalen. tooget Hallo-URL, Hallo kanaal heeft geen toobe in Hallo **met** status.

Zodra Hallo kanaal ophalen van gegevens start, kunt u uw stream te bekijken.

> [!NOTE]
> Hallo preview stroom momenteel alleen kan worden aangeboden in Fragmented MP4 (Smooth Streaming) indeling ongeacht Hallo opgegeven type invoer. U kunt Hallo [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest Hallo Smooth Stream. U kunt ook een speler gehost in Azure portal tooview Hallo uw stream.
> 
> 

### <a name="allowed-ip-addresses"></a>Toegestane IP-adressen
U kunt definiëren Hallo IP-adressen die zijn toegestaan tooconnect toohello preview-eindpunt. Als er geen IP-adressen worden opgegeven elk IP-adres krijgt. Toegestane IP-adressen kunnen worden opgegeven als een enkel IP-adres (bijvoorbeeld 10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22) of een IP-adresbereik met een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld 10.0.0.1(255.255.252.0)).

## <a name="live-encoding-settings"></a>Live codering instellingen
Deze sectie wordt beschreven hoe Hallo-instellingen voor Hallo live coderingsprogramma binnen Hallo kanaal kunnen worden aangepast wanneer Hallo **Type codering** van een kanaal is ingesteld te**standaard**.

> [!NOTE]
> Wanneer meerdere taal nummers invoeren en tijdens het doorzoeken van live codering met Azure, alleen RTP voor invoer van meerdere talen wordt ondersteund. U kunt definiëren up too8 audio-stromen met MPEG-2 TS via RTP. Meerdere audio houdt met RTMP of Smooth streaming opnemen wordt momenteel niet ondersteund. Bij het uitvoeren van live codering met [lokale live coderen](media-services-live-streaming-with-onprem-encoders.md), geldt er geen dergelijke beperking, omdat een kanaal verzonden ongeacht tooAMS passeren zonder verdere verwerking.
> 
> 

### <a name="ad-marker-source"></a>AD-markering bron
U kunt opgeven dat Hallo bron voor advertentiemarkeringssignalen opgeven. Standaardwaarde is **Api**, wat aangeeft dat Hallo live coderingsprogramma binnen Hallo kanaal moet luisteren tooan asynchrone **Advertentiemarkerings-API**.

Hallo andere geldige optie is **Scte35** (alleen toegestaan als Hallo opnemen tooRTP (MPEG-TS) streaming-protocol is ingesteld. Wanneer Scte35 wordt opgegeven, wordt het live coderingsprogramma Hallo SCTE 35 signalen uit Hallo invoerstroom RTP (MPEG-TS) parseren.

### <a name="cea-708-closed-captions"></a>CEA 708 bijschriften gesloten
Een optionele vlag Hallo live coderingsprogramma tooignore CEA 708 bijschriften gegevens wordt ingesloten in inkomende hello-video. Wanneer het Hallo-vlag is ingesteld toofalse (standaard), Hallo encoder detecteert en opnieuw CEA 708 gegevens invoegen in video uitvoerstromen Hallo.

### <a name="video-stream"></a>Video-Stream
Optioneel. Hierin wordt beschreven Hallo invoer videostream. Als dit veld niet is opgegeven, wordt de standaardwaarde Hallo gebruikt. Deze instelling is alleen toegestaan als Hallo invoer protocol voor streaming (MPEG-TS) tooRTP is ingesteld.

#### <a name="index"></a>Index
Een op nul gebaseerde index die aangeeft welke video invoerstroom Hallo live coderingsprogramma binnen Hallo Channel moet worden verwerkt. Deze instelling geldt alleen als opnemen streaming-protocol is RTP (MPEG-TS).

Standaardwaarde is nul. Het verdient aanbeveling toosend in een bepaald programma transportstroom (SharePoint Team Services). Als Hallo invoerstroom meerdere programma's bevat, Hallo live codering parseert Hallo programma kaart tabel (bet) in de invoer Hallo Hallo invoer met een naam van het type stream van MPEG-2-Video of H.264 identificeert en in volgorde van Hallo vervaldatum Hallo tabelindeling geschikt Hallo op nul gebaseerde index wordt vervolgens gebruikt toopick up Hallo n-de vermelding in de overeenkomst.

### <a name="audio-stream"></a>Audio-Stream
Optioneel. Hierin wordt beschreven Hallo invoer audio stromen. Als dit veld niet is opgegeven, wordt Hallo standaardwaarden opgegeven toepassing. Deze instelling is alleen toegestaan als Hallo invoer protocol voor streaming (MPEG-TS) tooRTP is ingesteld.

#### <a name="index"></a>Index
Het verdient aanbeveling toosend in een bepaald programma transportstroom (SharePoint Team Services). Als Hallo invoerstroom bevat meerdere programma's, hello live coderingsprogramma binnen Hallo kanaal parseert Hallo programma kaart tabel (bet) in de invoer hello, identificeert Hallo invoer met een naam van het type stream van MPEG-2 AAC ADTS of systeem A AC-3 of systeem AC-3-B of persoonlijke MPEG-2 PES of Audio MPEG-1 of Audio MPEG-2, en worden in volgorde van Hallo vervaldatum Hallo Hallo op nul gebaseerde index wordt vervolgens gebruikt toopick up Hallo n-de vermelding in de overeenkomst.

#### <a name="language"></a>Taal
taal-id van de audiostroom hello, conform tooISO 639-2, zoals eng Hallo Als deze niet aanwezig is, is standaard Hallo en (niet-gedefinieerd).

Er mag up too8 audiostroom sets opgegeven als Hallo invoer toohello kanaal MPEG-2 TS via RTP. Echter, kunnen er geen twee vermeldingen Hello dezelfde waarde voor Index.

### <a id="preset"></a>Systeem-definitie
Hiermee geeft u op Hallo voorinstelling toobe die wordt gebruikt door Hallo live coderingsprogramma binnen dit kanaal. Op dit moment Hallo enige toegestane waarde is **Default720p** (standaard).

Houd er rekening mee dat als u aangepaste standaardinstellingen moet, u neemt contact op met amslived op Microsoft.com.

**Default720p** Hallo video wordt coderen in Hallo 7 lagen te volgen.

#### <a name="output-video-stream"></a>Video uitvoerstroom
| BitRate | Breedte | Hoogte | MaxFPS | Profiel | Naam voor uitvoer van stroom |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Hoog |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Main |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Main |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Main |Video_512x288_850kbps |
| 550 |384 |216 |30 |Main |Video_384x216_550kbps |
| 350 |340 |192 |30 |Basislijn |Video_340x192_350kbps |
| 200 |340 |192 |30 |Basislijn |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Audio-uitvoerstroom
Audio is gecodeerde toostereo AAC Kredietbrief op 64 kbps, wordt de frequentie van 44,1 kHz.

## <a name="signaling-advertisements"></a>Advertenties-signalering
Wanneer het kanaal Live Encoding is ingeschakeld heeft, moet u een onderdeel in de pipeline die verwerking video hebben en kunt bewerken. U kunt signaal voor Hallo kanaal tooinsert slates en/of aankondigingen in Hallo uitgaande adaptieve bitrate stream. Smartphones zijn nog steeds afbeeldingen waarmee u toocover up invoer live feed Hallo in bepaalde gevallen (bijvoorbeeld tijdens een commerciële einde kunt). Reclame signalen zijn tijd gesynchroniseerd signalen die u in Hallo uitgaande stroom tootell Hallo-speler tootake speciale actie – zoals tooswitch tooan advertentie op het juiste moment Hallo insluiten. Zie dit [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) voor een overzicht van Hallo SCTE 35 signalering mechanisme dat wordt gebruikt voor dit doel. Hieronder volgt een typisch scenario dat u in uw live gebeurtenis kan implementeren.

1. Hebben de doelgroep ophalen van een installatiekopie van een pre-gebeurtenissen voordat Hallo gebeurtenis wordt gestart.
2. De doelgroep ophalen van een installatiekopie van een post-gebeurtenissen na afloop van de gebeurtenis Hallo hebben.
3. De doelgroep ophalen van een installatiekopie van een FOUTGEBEURTENIS als er een probleem opgetreden tijdens het Hallo-gebeurtenis (bijvoorbeeld stroomstoring in Hallo stadium) hebben.
4. Een AD-BREAK installatiekopie toohide Hallo live gebeurtenis verzenden tijdens een commerciële einde feed.

Hallo volgen Hallo-eigenschappen die u instellen kunt wanneer-signalering advertenties. 

### <a name="duration"></a>Duur
Hallo duur in seconden van commerciële Hallo-einde. Dit heeft een positieve waarde dan nul toobe in volgorde toostart Hallo commerciële einde. Wanneer een commerciële einde in voortgang en Hallo duur is set toozero Hello CueId die overeenkomt met Hallo continu commerciële einde, en vervolgens die pauze wordt geannuleerd.

### <a name="cueid"></a>CueId
Een unieke ID voor Hallo commerciële break toobe die wordt gebruikt door downstream-toepassing tootake geschikte actie (s). Er moet een positief geheel getal toobe. U kunt deze waarde tooany willekeurige positief geheel getal zijn ingesteld of een upstream system tootrack Hallo hint-ID's gebruiken. Controleer bepaalde toonormalize alle id's toopositive gehele getallen vóór het verzenden via Hallo API.

### <a name="show-slate"></a>Lei weergeven
Optioneel. Hallo live coderingsprogramma tooswitch toohello signalen [standaard lei](media-services-manage-live-encoder-enabled-channels.md#default_slate) installatiekopie tijdens een commerciële einde en binnenkomende videofeed Hallo verbergen. Audio gedempt is ook tijdens lei. Standaard is **false**. 

Hallo-installatiekopie die wordt gebruikt worden Hallo opgegeven via Hallo standaard lei asset Id-eigenschap op Hallo moment Hallo kanaal gemaakt. Hallo lei worden uitgerekt toofit Hallo weergavegrootte installatiekopie. 

## <a name="insert-slate--images"></a>Lei afbeeldingen invoegen
Hallo live coderingsprogramma binnen Hallo kanaal kan gesignaleerde tooswitch tooa lei installatiekopie zijn. Het kan ook gesignaleerde tooend een continu lei zijn. 

Hallo live coderingsprogramma worden geconfigureerde tooswitch tooa lei installatiekopie en Hallo binnenkomende video signaal in bepaalde situaties, bijvoorbeeld tijdens een pauze ad verbergen. Als een dergelijke lei niet is geconfigureerd, wordt niet invoervideo tijdens die pauze ad gemaskeerd.

### <a name="duration"></a>Duur
Hallo de duur van Hallo lei in seconden. Dit heeft een positieve waarde dan nul toobe in volgorde toostart Hallo lei. Als er een continu lei is en een duur van nul is opgegeven, wordt die lei continu worden beëindigd.

### <a name="insert-slate-on-ad-marker"></a>Slate invoegen op advertentiemarkering
Set tootrue, deze instelling configureert als Hallo live coderingsprogramma tooinsert een installatiekopie lei tijdens een pauze ad. Hallo-standaardwaarde is true. 

### <a id="default_slate"></a>Standaard lei Asset-Id

Optioneel. Hiermee geeft u Hallo Asset-Id van Hallo Media Services actief die Hallo lei installatiekopie bevat. De standaardwaarde is null. 


>[!NOTE] 
>Voordat u Hallo kanaal maakt, moet hello lei installatiekopie met de Hallo volgen beperkingen worden geüpload als een toegewezen actief (er worden geen andere bestanden moet in deze asset). Deze afbeelding wordt alleen wanneer Hallo live coderingsprogramma een lei vanwege tooan ad-einde wordt ingevoegd of expliciet is gesignaleerd tooinsert een lei gebruikt. Hallo live coderingsprogramma kan ook gaan in een modus lei tijdens bepaalde foutcondities – bijvoorbeeld als invoer signaal hello verbroken wordt. Er is momenteel geen optie toouse een aangepaste installatiekopie wanneer Hallo live coderingsprogramma die een 'invoer signaal vermist' staat invoert. U kunt stemmen voor deze functie [hier](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Maximaal 1920 x 1080 in resolutie.
* Maximaal 3 MB groot.
* Hallo-bestandsnaam moet de extensie *.jpg hebben.
* Hallo afbeelding moet worden geüpload naar een Asset als Hallo die alleen AssetFile in dat actief en deze AssetFile moeten worden gemarkeerd als primaire Hallo-bestand. Hallo Asset niet opslag versleuteld.

Als hello **standaard leistenen Asset Id** niet is opgegeven, en **lei op ad-markering invoegen** te is ingesteld**true**, een standaardinstallatiekopie van het Azure Media Services worden gebruikt toohide Hallo invoer videostream. Audio gedempt is ook tijdens lei. 

## <a name="channels-programs"></a>Programma's van kanaal
Een kanaal is gekoppeld aan programma's waarmee u toocontrol Hallo publiceren en opslaan van segmenten in een live stream. Kanalen beheren programma's. Hallo is kanaal- en programma-relatie heel vergelijkbaar tootraditional media waarbij een kanaal een constante stream met inhoud heeft en een programma bereik toosome getimede gebeurtenis op dat kanaal.

Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **archiefvenster** lengte. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur. Lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Programma's kunnen uitvoeren in de opgegeven tijdsduur hello, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elk programma dat is gekoppeld aan een Asset die inhoud voor gestreamd Hallo opslaat. Een asset is toegewezen tooa blok-blob-container in hello Azure Storage-account en Hallo-bestanden in Hallo activa zijn opgeslagen als blobs in de container. toopublish hello programma zodat uw klanten kunnen bekijken Hallo stroom moet u een OnDemand-locator voor Hallo gekoppelde asset. Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.

Een kanaal biedt ondersteuning voor maximaal toothree gelijktijdig actieve programma's, zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte. De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een programma, maar toobroadcast alleen de laatste tien minuten. tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate. Een programma wordt ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd. Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

Gebruik bestaande programma's niet voor nieuwe gebeurtenissen. In plaats daarvan maakt en start een nieuw programma voor elke gebeurtenis, zoals beschreven in de sectie van Hallo Programming Live Streaming-toepassingen.

Start Hallo programma wanneer u bent klaar toostart streamen en te archiveren. Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren. 

toodelete gearchiveerde inhoud, stoppen en Hallo programma verwijderen en verwijder vervolgens de gekoppelde asset Hallo. Een asset kan niet worden verwijderd als deze wordt gebruikt door een programma. Hallo programma moet eerst worden verwijderd. 

Zelfs na het stoppen en verwijderen van programma hello, Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd.

Als u tooretain Hallo gearchiveerde inhoud wilt, maar niet langer voor streaming beschikbaar, verwijdert u Hallo streaming-locator.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Een voorbeeld van een live feed ophalen
Wanneer Live Encoding is ingeschakeld, kunt u nu een voorbeeld van live Hallo-feed ophalen, zoals het Hallo-kanaal is bereikt. Dit is een waardevol hulpmiddel toocheck of uw live feed daadwerkelijk Hallo kanaal bereikt. 

## <a id="states"></a>Kanaal statussen en hoe toohello modus facturering in statussen worden toegewezen
Hallo huidige status van een kanaal. Mogelijke waarden:

* **Gestopt**. Dit is de beginstatus Hallo Hallo kanaal na het maken ervan. Hallo kanaaleigenschappen kunnen worden bijgewerkt in deze toestand is, maar streaming is niet toegestaan.
* **Starten van**. Hallo-kanaal wordt gestart. In deze status zijn streaming en updates niet toegestaan. Als een fout optreedt, retourneert Hallo kanaal toohello status gestopt.
* **Met**. Hallo kanaal is geschikt voor het verwerken van live gegevensstromen.
* **Stoppen van**. Hallo-kanaal wordt gestopt. In deze status zijn streaming en updates niet toegestaan.
* **Verwijderen van**. Hallo-kanaal wordt verwijderd. In deze status zijn streaming en updates niet toegestaan.

Hallo volgende tabel toont hoe kanaal kaart toohello facturering modus staat. 

| Kanaalstatus | Portal UI-indicatoren | In rekening gebracht? |
| --- | --- | --- |
| Starting |Starting |Nee (overgangsstatus) |
| Running |Ready (er worden geen programma's uitgevoerd)<br/>of<br/>Streaming (er wordt ten minste een programma uitgevoerd) |Ja |
| Stopping |Stopping |Nee (overgangsstatus) |
| Stopped |Stopped |Nee |

> [!NOTE]
> Op dit moment Hallo kanaal start gemiddelde ongeveer 2 minuten, maar tijd tot tijd kan duren voordat too20 + minuten. Opnieuw instellen van kanaal kunnen too5 minuten duren.
> 
> 

## <a id="Considerations"></a>Overwegingen
* Wanneer een kanaal van **standaard** coderingstype optreedt in een verlies van invoer bron/bijdrage feed, wordt deze gecompenseerd door te Hallo bron video en audio vervangen door een fout lei en stilte. Hallo kanaal blijven tooemit een lei totdat Hallo invoer/bijdrage feed wordt hervat. Het is raadzaam om een kanaal live niet ingesteld blijven status langer dan 2 uur. Hallo-gedrag van Hallo kanaal op opnieuw verbinden met invoer voorbij dat punt, kan niet worden gegarandeerd, is het gedrag in antwoord tooa Reset-opdracht. U toostop Hallo kanaal hebt, verwijderen en een nieuwe maken.
* U kunt Hallo invoerprotocol tijdens het Hallo kanaal niet wijzigen of de gekoppelde programma's worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u afzonderlijke kanalen voor elk invoerprotocol.
* Telkens wanneer u de configuratie van het live coderingsprogramma hello, roepen Hallo **opnieuw** methode op het Hallo-kanaal. Voordat u Hallo kanaal opnieuw instelt, kunt u toostop Hallo programma hebben. Nadat u opnieuw Hallo kanaal, start u Hallo programma opnieuw.
* Een kanaal kan worden gestopt, alleen wanneer deze zich in de uitvoeringsstatus van Hallo en alle programma's op Hallo kanaal zijn gestopt.
* Standaard kunt u alleen 5 kanalen tooyour Media Services-account toevoegen. Dit is een dynamische quota voor alle nieuwe accounts. Zie voor meer informatie [quota's en beperkingen](media-services-quotas-and-limitations.md).
* U kunt Hallo invoerprotocol tijdens het Hallo kanaal niet wijzigen of de gekoppelde programma's worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u afzonderlijke kanalen voor elk invoerprotocol.
* U wordt alleen gefactureerd als het kanaal in Hallo **met** status. Voor meer informatie raadpleegt u te[dit](media-services-manage-live-encoder-enabled-channels.md#states) sectie.
* Hallo maximum is aanbevolen duur van een live gebeurtenis op dit moment acht uur. Neem contact op met amslived op Microsoft.com als u toorun een kanaal voor langere tijd nodig.
* Zorg ervoor dat toohave Hallo streaming-eindpunt van waaruit u wilt dat de inhoud toostream in Hallo **met** status.
* Wanneer meerdere taal nummers invoeren en tijdens het doorzoeken van live codering met Azure, alleen RTP voor invoer van meerdere talen wordt ondersteund. U kunt definiëren up too8 audio-stromen met MPEG-2 TS via RTP. Meerdere audio houdt met RTMP of Smooth streaming opnemen wordt momenteel niet ondersteund. Bij het uitvoeren van live codering met [lokale live coderen](media-services-live-streaming-with-onprem-encoders.md), geldt er geen dergelijke beperking, omdat een kanaal verzonden ongeacht tooAMS passeren zonder verdere verwerking.
* Hallo maakt gebruik van vooraf ingestelde Hallo begrip 'max framesnelheid' van 30 fps codering. Dus als hello invoer 60fps / 59.97i, Hallo ingevoerde frames verwijderd/de-interlaced too30/29,97 fps zijn. Als het Hallo-invoer is 50fps/50i, zijn Hallo ingevoerde frames verwijderd/de-interlaced too25 fps. Als invoer Hallo 25 fps is, wordt de uitvoer blijft bij 25 fps.
* Vergeet niet tooSTOP YOUR kanalen wanneer u klaar bent. Als u dit niet, blijven facturering.

## <a name="known-issues"></a>Bekende problemen
* Opstarttijd-kanaal is verbeterd tooan gemiddelde van 2 minuten, maar soms van toegenomen vraag nog steeds too20 + minuten kan duren.
* RTP ondersteuning is voor professionele omroeporganisaties geleverd. Controleer op Hallo opmerkingen bij RTP in [dit](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Lei afbeeldingen moeten voldoen toorestrictions beschreven [hier](media-services-manage-live-encoder-enabled-channels.md#default_slate). Als u probeert maakt u een kanaal met een lei die groter is dan 1920 x 1080 hello uiteindelijk wordt de aanvraag-standaardfout optreedt.
* Nogmaals... Vergeet niet de tooSTOP YOUR kanalen wanneer u klaar bent streaming. Als u dit niet, blijven facturering.

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Verwante onderwerpen
[Live Streaming-gebeurtenissen met Azure mediaservices leveren](media-services-overview.md)

[Kanalen waarmee live codering van een afzonderlijke bitrate tooadaptive bitrate stream met Portal maken](media-services-portal-creating-live-encoder-enabled-channel.md)

[Maken van kanalen waarmee live codering van een afzonderlijke bitrate tooadaptive bitrate stream met .NET SDK](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Kanalen met REST API beheren](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Media Services-concepten](media-services-concepts.md)

[Azure mediaservices gefragmenteerde MP4 Live opnemen specificatie](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

