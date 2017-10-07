---
title: aaaStorSimple indicatoren | Microsoft Docs
description: Beschrijft Hallo Lichtdioden (LED's) en akoestisch alarmen gebruikt toomonitor Hallo status van Hallo StorSimple-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Gebruik StorSimple indicatoren toomanage bewaking van uw apparaat
## <a name="overview"></a>Overzicht
Uw StorSimple-apparaat bevat luminescentiedioden (LED's) en waarmee u toomonitor kunt alarmen Hallo-modules en de algehele status van Hallo StorSimple-apparaat. Hallo indicatoren kunt u vinden op Hallo hardware-onderdelen van de primaire ruimte Hallo-apparaat en Hallo EBOD behuizing. Hallo indicatoren kan LED's of akoestisch alarmen zijn.

Er zijn drie LED statussen gebruikt tooindicate Hallo status van een module: groen knippert groen toored-geel of rood oranje.  

* Groen LED's vertegenwoordigen een gezonde operationele status.  
* Groen toored-oranje knippert vertegenwoordigen LED's Hallo aanwezigheid van niet-kritieke voorwaarden waarvoor u mogelijk tussenkomst van de gebruiker.  
* Rood oranje LED's geven aan dat er een kritieke fout binnen Hallo module aanwezig is.  

Hallo rest van dit artikel beschrijft Hallo verschillende bewaking indicatielampjes, de locaties op Hallo StorSimple-apparaat en alle gekoppelde akoestisch alarmen Hallo Apparaatstatus op basis van Hallo LED statussen.

## <a name="front-panel-indicator-leds"></a>Voorpaneel LED
de voorpaneel Hello, ook wel bekend als Hallo *operations Configuratiescherm* of *ops Configuratiescherm*, wordt Hallo cumulatieve status van alle Hallo modules weergegeven in Hallo-systeem. Hallo voorpaneel identiek op Hallo StorSimple primaire en Hallo EBOD behuizing en hieronder wordt weergegeven.  

   ![Apparaat voorpaneel][1]

Hallo voorpaneel bevat Hallo indicatoren te volgen:  

1. Knop Dempen
2. Power indicator LED (rood-groen-geel)
3. Module-fout indicator geleid (in rood-oranje/uit)
4. Logische fout indicator geleid (in rood-oranje/OFF
5. Eenheid-ID weergeven  

Hallo het belangrijkste verschil tussen Hallo voorpaneel LED's voor Hallo-apparaat en die voor Hallo EBOD behuizing is Hallo **System eenheid-id-nummer** op Hallo LED beeldscherm wordt weergegeven. Hallo standaardeenheid weergegeven op Hallo apparaat-ID is **00**, terwijl Hallo standaard eenheid-ID weergegeven op Hallo EBOD behuizing **01**. Hiermee kunt u tooquickly onderscheid maken tussen Hallo-apparaat en Hallo EBOD behuizing wanneer Hallo-apparaat is ingeschakeld. Als uw apparaat is uitgeschakeld, gebruikt u Hallo informatie in [schakelt u een nieuw apparaat](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) toodifferentiate Hallo-apparaat bij Hallo EBOD behuizing.  

## <a name="front-panel-led-status"></a>Voorpaneel LED status
Gebruik Hallo tabel tooidentify Hallo status aangegeven door Hallo LED's op Hallo voorpaneel voor Hallo-apparaat of Hallo EBOD behuizing te volgen.  

| Inschakelen van het systeem | Module-fout | Logische-fout | Waarschuwing | Status |
| --- | --- | --- | --- | --- |
| Rood oranje |UIT |UIT |N.v.t. |Netstroom verloren, uitgevoerd op de back-stroom of Netstroom zijn aangesloten op en Hallo controller modules zijn verwijderd. |
| Groen |AAN |AAN |N.v.t. |OPS Configuratiescherm inschakelen (5s) status testen |
| Groen |UIT |UIT |N.v.t. |Power op alle functies goed |
| Groen |AAN |N.v.t. |Fout met betrekking tot PCM LED's, ventilator veroorzaakt LED 's |Alle PCM-fout ventilator fault, boven of onder temperatuur |
| Groen |AAN |N.v.t. |I/o-module LED 's |Een controller-fout module |
| Groen |AAN |N.v.t. |N.v.t. |Behuizing logica fouttolerantie |
| Groen |Flash |N.v.t. |Status van de module geleid voor module van de domeincontroller. Fout met betrekking tot PCM LED's, ventilator veroorzaakt LED 's |Onbekende controller moduletype geïnstalleerd, I2C bus mislukt, controller-module essentieel product data (VPD)-configuratiefout |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Voeding (PCM) module LED koeling
Power koeling module (PCM) LED vindt u op Hallo achterzijde van de primaire behuizing Hallo of EBOD behuizing op elke PCM-module. Dit onderwerp wordt beschreven hoe toouse Hallo LED's toomonitor Hallo status van uw StorSimple-apparaat te volgen.  

* PCM LED's voor de primaire behuizing Hallo
* PCM LED's voor Hallo EBOD behuizing

## <a name="pcm-leds-for-hello-primary-enclosure"></a>PCM LED's voor de primaire behuizing Hallo
Hallo StorSimple-apparaat heeft een 764W PCM-module met een extra batterij. Hallo volgende afbeelding ziet u Hallo LED Configuratiescherm voor Hallo-apparaat.  

   ![PCM LED's op de primaire behuizing Hallo][2]

LED legenda:

1. Fout in Echtheidsvoorwaarde power
2. Ventilator mislukt
3. Fout met betrekking tot accu
4. PCM OK
5. DC-fout
6. Goede accu  

Hallo-status van PCM wordt aangegeven op Hallo Hallo Configuratiescherm geleid. Hallo apparaat PCM LED Configuratiescherm heeft zes LED's. Vier van deze LED's weergeven Hallo-status van Hallo voeding en Hallo ventilator. Hallo resterende twee LED's geven de status Hallo Hallo back-up batterij module in Hallo PCM. U kunt Hallo tabellen toodetermine Hallo status Hallo PCM te volgen.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>PCM LED voor voeding en -ventilator
| Status | PCM orde (groen) | AC mislukken (geel) | Ventilator (geel) is mislukt | DC is mislukt (geel) |
| --- | --- | --- | --- | --- |
| Er is geen netstroom (tooenclosure) |UIT |UIT |UIT |UIT |
| Er is geen netstroom (alleen deze PCM) |UIT |AAN |UIT |AAN |
| AC presenteren aan PCM - OK |AAN |UIT |UIT |UIT |
| PCM mislukken (ventilator mislukken) |UIT |UIT |AAN |N.v.t. |
| PCM-fout (via amp via spanning via huidige) |UIT |AAN |AAN |AAN |
| PCM (ventilator buiten tolerantie) |AAN |UIT |UIT |AAN |
| Standby-modus |Knipperend |UIT |UIT |UIT |
| Download van de PCM-firmware |UIT |Knipperend |Knipperend |Knipperend |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>PCM LED voor Hallo back-up batterij
| Status | Accu goed (groen) | Fout met betrekking tot accu (geel) |
| --- | --- | --- |
| Accu niet aanwezig |UIT |UIT |
| Accu aanwezig zijn en worden in rekening gebracht |AAN |UIT |
| Het laden of onderhoud zuivering accu |Knipperend |UIT |
| Accu 'soft' fout (herstelbare) |UIT |Knipperend |
| Accu "harde" fout (niet-herstelbare) |UIT |AAN |
| Disarmed accu |Knipperend |UIT |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>PCM LED's voor Hallo EBOD behuizing
Hallo EBOD behuizing heeft een PCM 580 w bij en er geen extra accu. Hallo PCM-deelvenster voor Hallo EBOD behuizing heeft indicatielampjes alleen voor Hallo voedingen en Hallo ventilator. Hallo volgende afbeelding ziet u deze LED's.

   ![PCM LED's op Hallo EBOD behuizing][3] 

U kunt Hallo tabel toodetermine Hallo status Hallo PCM te volgen.  

| Status | PCM orde (groen) | AC mislukken (geel) | Ventilator (geel) is mislukt | DC is mislukt (geel) |
| --- | --- | --- | --- | --- |
| Er is geen netstroom (tooenclosure) |UIT |UIT |UIT |UIT |
| Er is geen netstroom (alleen deze PCM) |UIT |AAN |UIT |AAN |
| AC aanwezig PCM ON – OK |AAN |UIT |UIT |UIT |
| PCM mislukken (ventilator mislukken) |UIT |UIT |AAN |X |
| PCM-fout (via amp via spanning via huidige |UIT |AAN |AAN |AAN |
| PCM (ventilator buiten tolerantie) |AAN |UIT |UIT |AAN |
| Stand-by-model |Knipperend |UIT |UIT |UIT |
| Download van de PCM-firmware |UIT |Knipperend |Knipperend |Knipperend |

## <a name="controller-module-indicator-leds"></a>Controller module LED
Hallo StorSimple-apparaat bevat LED's voor de primaire domeincontroller Hallo en Hallo EBOD controller modules.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>Bewaking van LED's voor de primaire domeincontroller Hallo
Hallo kunt volgende afbeelding u Hallo LED's op de primaire domeincontroller Hallo identificeren. (Alle Hallo-onderdelen zijn vermelde tooaid afdrukstand).  

   ![Bewaking LED's - primaire domeincontroller][4]

Gebruik Hallo volgende tabel toodetermine of Hallo controllermodule correct wordt uitgevoerd.  

### <a name="controller-indicator-leds"></a>Controller LED
| LED | Beschrijving |
| --- | --- |
| ID-LED (blauw) |Hiermee wordt aangegeven dat die module hello wordt wordt geïdentificeerd. Als hello blauw LED op een actieve domeincontroller knippert, klikt u vervolgens hello controller Hallo actieve controller en hello andere één Hallo stand-by-controller. Zie voor meer informatie [identificeren Hallo actieve controller op uw apparaat](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| Fout met betrekking tot LED (geel) |Hiermee geeft u een fout in Hallo-controller. |
| OK LED (groen) |Constante groen geeft aan dat domeincontroller Hallo is OK. Knippert groen geeft aan een configuratiefout VPD-controller. |
| SAS activiteit LED's (groen) |Constante groen geeft aan dat een verbinding zonder huidige activiteit. Knippert groen geeft aan Hallo verbinding heeft lopende activiteiten. |
| Ethernet-status LED 's |Rechts wordt aangegeven koppeling/netwerkactiviteit: (constante groen) koppeling active (knippert groen) netwerkactiviteit. Links geeft Netwerksnelheid: (geel) 1000 Mb/s (groen) 100 Mb/s en (uit) 10 Mb/s. Deze licht mogelijk, afhankelijk van Hallo Onderdeelmodel knipperen zelfs als het Hallo-netwerkinterface niet is ingeschakeld. |
| POST LED 's |Voortgang Hallo opstarten wanneer de controller Hallo is ingeschakeld. Als Hallo StorSimple-apparaat tooboot mislukt, helpt dit LED Microsoft Support Hallo punt in Hallo opstartproces waarmee Hallo-fout is opgetreden te identificeren. |

> [!IMPORTANT]
> Als het Hallo-fout LED uit is, is er een probleem met Hallo controllermodule die mogelijk worden opgelost door Hallo domeincontroller opnieuw te starten. Neem contact op met Microsoft Support als dit probleem niet wordt verholpen door opnieuw te starten Hallo-controller.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Bewaking van LED's voor Hallo EBOD (EBOD behuizing)
Elk van Hallo 6 Gb/s EBOD SAS-controllers LED's die de status aan te geven, zoals wordt weergegeven in de volgende illustratie Hallo heeft.  

  ![Bewaking LED's - EBOD behuizing][5]

Gebruik Hallo volgende tabel toodetermine of Hallo EBOD controllermodule normaal functioneert.  

### <a name="ebod-controller-module-indicator-leds"></a>EBOD controller module-LED
| Status | I/o-module orde (groen) | I/o-module-fout (geel) | Host-poortactiviteit (groen) |
| --- | --- | --- | --- |
| Controllermodule OK |AAN |UIT |- |
| Controller module fouttolerantie |UIT |AAN |- |
| Er is geen externe host-poortverbinding |- |- |UIT |
| Externe host-poortverbinding – geen activiteit |- |- |AAN |
| Externe host-poortverbinding - activiteit |- |- |Knipperend |
| Fout in module metagegevens van domeincontroller |Knipperend |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Schijfstation LED voor primaire behuizing Hallo en EBOD behuizing
Hallo StorSimple-apparaat heeft schijfstations zich in zowel de primaire behuizing Hallo en Hallo EBOD behuizing. Elke harde schijf bevat de bewaking van indicatielampjes, zoals beschreven in deze sectie. 

Voor de schijfstations hello, Hallo stationsstatus wordt aangegeven met een groen LED en een rood oranje LED gekoppeld aan de voorzijde Hallo van elke schijf carrier-module. Hallo volgende afbeelding ziet u deze LED's.

  ![Schijfstation LED 's][6]

Gebruik Hallo tabel toodetermine Hallo status van elke harde schijf die op zijn beurt is van invloed op Hallo algemene voorpaneel LED status te volgen.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Schijfstation LED voor Hallo EBOD behuizing
| Status | Activiteit OK LED (groen) | Fout met betrekking tot LED (rood oranje) | Ops Configuratiescherm LED gekoppeld |
| --- | --- | --- | --- |
| Er is geen station is geïnstalleerd |UIT |UIT |Geen |
| Station geïnstalleerd en operationeel |Knipperend in-of uitschakelen met de activiteit |X |Geen |
| SCSI-behuizing Services (SE) apparaat identiteit instellen |AAN |Knippert 1 seconde op/1 seconde uitschakelen |Geen |
| SE apparaat veroorzaakt bit is ingesteld |AAN |AAN |Logische-fout (rood) |
| Stroomstoring besturingselement circuit |UIT |AAN |Module-fout (rood) |

## <a name="audible-alarms"></a>Akoestisch alarmen
Een StorSimple-apparaat bevat akoestisch alarmen die zijn gekoppeld aan zowel primaire behuizing Hallo Hallo EBOD behuizing. Een akoestisch alarm bevindt zich op Hallo voorpaneel (ook wel bekend als Hallo ops deelvenster) van beide behuizingen. Hallo akoestisch alarm geeft aan wanneer een fouttoestand aanwezig is. Hallo volgende voorwaarden wordt Hallo alarm activeren:  

* Ventilator fout of probleem
* Spanning buiten het bereik
* Boven of onder temperatuur voorwaarde
* Thermische overschrijding
* Systeemfout
* Logische-fout
* Geef stroomstoring
* Verwijderen van een macht koeling van module (PCM)  

Hallo volgende tabel beschrijft Hallo verschillende statussen waarschuwing.  

### <a name="alarm-states"></a>Waarschuwing statussen
| Status van waarschuwing | Actie | Actie knop Dempen ingedrukt |
| --- | --- | --- |
| S0 |Normale modus: achtergrond |Twee keer een piepgeluid laat horen |
| S1 |Modus voor fouten: 1 seconde op/1 seconde uitschakelen |Overgang tooS2 of S3 (Zie Opmerkingen) |
| S2 |Modus herinneren: onregelmatige geluid |Geen |
| S3 |Dempen modus: achtergrond |Geen |
| S4 |Kritieke fout modus: continue alarm |Niet beschikbaar: dempen niet actief |

> [!NOTE]
> * Waarschuwing status S1, als u niet op dempen binnen twee minuten overgezet Hallo status automatisch tooS2 of S3.  
> * Waarschuwing Staten S1 tooS4 tooS0 retourneren nadat Hallo fouttoestand is gewist.  
> * Kritieke fout status S4 kan worden ingevoerd vanuit een andere status.  


U kunt Hallo akoestisch alarm dempen Hallo dempen door knop te drukken op Hallo ops Configuratiescherm. Automatische dempen zal optreden na twee minuten als Hallo dempen niet handmatig wordt beheerd. Wanneer Hallo alarm gedempt is, wordt voortgezet toosound met korte onregelmatige pieptonen tooindicate die het probleem blijft optreden. Hallo alarm worden achtergrond wanneer alle problemen met de Hallo worden gewist.

Hallo volgende tabel beschrijft Hallo verschillende voorwaarden waarschuwing.

### <a name="alarm-conditions"></a>Waarschuwing-voorwaarden
| Status | Ernst | Waarschuwing | OPS deelvenster LED |
| --- | --- | --- | --- |
| Waarschuwing aan PCM: DC stroomstoring van een enkele PCM |Fout: Er is geen verlies van redundantie |S1 |Module-fout |
| Waarschuwing aan PCM: DC stroomstoring van een enkele PCM |Fout: verlies van redundantie |S1 |Module-fout |
| Mislukken van PCM-ventilator |Fout: verlies van redundantie |S1 |Module-fout |
| SBB module PCM-fout gedetecteerd |Fouttolerantie |S1 |Module-fout |
| PCM verwijderd |Fout in de configuratie |Geen |Module-fout |
| Configuratiefout behuizing |Fout: kritiek |S1 |Module-fout |
| Lage temperatuur waarschuwingsmelding |Waarschuwing |S1 |Module-fout |
| Hoge temperatuur waarschuwingsmelding |Waarschuwing |S1 |Module-fout |
| Via temperatuur |Fout: kritiek |S1 |Module-fout |
| I2C bus mislukt |Fout: verlies van redundantie |S1 |Module-fout |
| OPS deelvenster communicatiefout (I2C) |Fout: kritiek |S1 |Module-fout |
| Fout bij de domeincontroller |Fout: kritiek |S1 |Module-fout |
| SBB interface module fouttolerantie |Fout: kritiek |S1 |Module-fout |
| SBB interface module-fout: geen werkende modules resterende |Fout: kritiek |S4 |Module-fout |
| SBB interfacemodule verwijderd |Waarschuwing |Geen |Module-fout |
| Station besturingselement stroomstoring |Waarschuwing: zonder verlies van station power |S1 |Module-fout |
| Station besturingselement stroomstoring |Fout: essentiële; station stroomstoring |S1 |Module-fout |
| Station verwijderd |Waarschuwing |Geen |Module-fout |
| Onvoldoende stroom beschikbaar |Waarschuwing |Geen |Module-fout |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple hardwareonderdelen en status](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


