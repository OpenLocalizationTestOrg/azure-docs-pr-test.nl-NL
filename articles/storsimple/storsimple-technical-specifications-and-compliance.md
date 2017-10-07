---
title: de technische specificaties aaaStorSimple | Microsoft Docs
description: Beschrijft Hallo technische specificaties en wettelijke normen compatibiliteitsinformatie voor Hallo StorSimple hardware-onderdelen.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 17ebf6b3-0872-4332-ac6e-074cc20a2b8e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: bb73661105dee7f6020a91f8c4f5abd6583023ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>Technische specificaties en naleving voor Hallo StorSimple-apparaat
## <a name="overview"></a>Overzicht
Hallo hardware-onderdelen van uw Microsoft Azure StorSimple-apparaat voldoen toohello technische specificaties en wettelijke normen die in dit artikel wordt beschreven. Hallo technische specificaties beschrijven opslagcapaciteit Hallo stroom en koeling Modules (PCMs) harde schijven en behuizingen. informatie over de compatibiliteit van Hallo bevat informatie over zaken als internationale normen, veiligheid en uitstoot en kabels.

## <a name="power-and-cooling-module-specifications"></a>Stroom en koeling Module specificaties
Hallo StorSimple-apparaat heeft twee 100-240 v dual ventilator SBB-compatibele Power koeling Modules (PCMs). Dit biedt een redundant vermogen-configuratie. Als een PCM mislukt, Hallo apparaat heeft nog steeds toooperate normaal gesproken op Hallo andere PCM totdat Hallo module kan niet worden vervangen.  

Hallo EBOD behuizing gebruikt een 580 W PCM en primaire behuizing gebruikt een 764 W PCM. Hallo volgende tabellen lijst Hallo technische specificaties die zijn gekoppeld aan Hallo PCMs.

| Specificatie | 580 W PCM (EBOD) | 764 W PCM (primair) |
| --- | --- | --- |
| Maximale vermogen |580 W |764 |
| Frequentie |50/60 Hz |50/60 Hz |
| Selectie voor bereik van spanning |Automatische variërend: 90 – 264 V AC, 47/63 Hz |Automatische variërend: 90-264 V AC, 47/63 Hz |
| Maximale stroomoverbelasting huidige |20 A |20 A |
| Power factor correctie |> 95% nominaal ingangsvoltage |> 95% nominaal ingangsvoltage |
| Harmonischen |Voldoet aan EN61000-3-2 |Voldoet aan EN61000-3-2 |
| Uitvoer |Stand-by-spanning 5v @ 2.0 A |Stand-by-spanning 5v @ 2.7 A |
| + 5V BIJ 42 A |+ 5V BIJ 40 A | |
| + 12 V @ 38 A |+ 12 V @ 38 A | |
| Hot pluggable |Ja |Ja |
| Switches en LED 's |AC in-of-switch en de status van de vier LED |AC in-of-switch en de status van de zes LED |
| Behuizing koeling |Ene koeling ventilatoren met variabele ventilatorbesturing voor snelheid |Ene koeling ventilatoren met variabele ventilatorbesturing voor snelheid |

## <a name="power-consumption-statistics"></a>Power verbruiksstatistieken
Hallo volgende tabel geeft een lijst Hallo typische energieverbruiksgegevens (de werkelijke waarden kunnen afwijken van Hallo gepubliceerd) voor Hallo verschillende modellen van StorSimple-apparaat. 

| Voorwaarden | 240 V AC | 240 V AC | 240 V AC | 110 V AC | 110 V AC | 110 V AC |
| --- | --- | --- | --- | --- | --- | --- |
|  Ventilatoren traag, stations inactief |1,45 A |0.31 kW |1057.76 BTU/uur |3.19 A |0.34 kW |1160.13 BTU/uur |
|  Ventilatoren vertragen, stations openen |1,54 A |0,33 kW |1126.01 BTU/uur |3.27 A |0.36 kW |1228.37 BTU/uur |
|  Snel, stations voor ventilatoren is niet actief, twee PSUs ingeschakeld |2.14 A |0.49 kW |1671.95 BTU/uur |4,99 A |0.54 kW |1842.56 BTU/uur |
|  Ventilatoren snel, niet-actieve stations, een voeding van stroom voorzien van een niet-actieve |2.05 A |0.48 kW |1637.83 BTU/uur |4,58 A |0,50 kW |1706.07 BTU/uur |
|  Ventilatoren snel, stations, toegang tot twee PSUs ingeschakeld |2,26 A |0,51 kW |1740.19 BTU/uur |4,95 A |0.54 kW |1842.56 BTU/uur |
|  Snelle ventilatoren, stations openen, een voeding ingeschakeld een niet-actieve |2.14 A |0.49 kW |1671.95 BTU/uur |4.81 A |0.53 kW |1808.44 BTU/uur |

## <a name="disk-drive-specifications"></a>Schijf-specificaties
Uw StorSimple-apparaat biedt ondersteuning voor maximaal too12 3.5 inch formulier factor seriële gekoppelde SCSI (SAS) harde schijven. Hallo werkelijke stations kunnen een combinatie van SSD-schijven (SSD's) of harde schijven (HDD's), afhankelijk van de productconfiguratie Hallo zijn. Hallo 12 schijfstation sleuven bevinden zich in een configuratie met 3 bij 4 voor Hallo behuizing. Hallo EBOD behuizing kunt u extra opslagruimte voor een andere 12 schijfstations. Dit zijn altijd HDD's.  

## <a name="storage-specifications"></a>Opslag-specificaties
Hallo StorSimple-apparaten hebben een combinatie van harde schijven en SSD-stations voor beide Hallo 8100 en 8600. Hallo totale bruikbare capaciteit voor Hallo 8100 en 8600 zijn ongeveer 15 TB en 38 TB respectievelijk. Hallo volgende tabel worden details op Hallo van SSD en HDD cloudcapaciteit in de context van Hallo Hallo StorSimple-oplossing capaciteit.

| Apparaatmodel / capaciteit | 8100 | 8600 |
| --- | --- | --- |
| Het aantal harde schijven (HDD's) |8 |19 |
| Aantal SSD-schijven (SSD's) |4 |5 |
| Één schijfcapaciteit |4 TB |4 TB |
| Één SSD-capaciteit |400 GB |800 GB |
| Reservecapaciteit |4 TB |4 TB |
| Bruikbare schijfcapaciteit |14 TB |36 TB |
| Bruikbare SSD-capaciteit |800 GB |2 TB |
| Totale bruikbare capaciteit * |~ 15 TB |~ 38 TB |
| Maximale oplossing capaciteit (met inbegrip van de cloud) |200 TB |500 TB |

<sup>* </sup>- *de totale bruikbare capaciteit Hallo bevat Hallo-capaciteit die beschikbaar zijn voor gegevens, metagegevens en buffers.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>Behuizing dimensies en gewicht specificaties
Hallo tabellenlijst na Hallo verschillende behuizing specificaties voor dimensies en gewicht.  

### <a name="enclosure-dimensions"></a>Behuizing dimensies
Hallo bevat volgende tabel Hallo dimensies van Hallo behuizing in millimeters en inches.

| Behuizing | Millimeters | Inches |
| --- | --- | --- |
| Hoogte |87.9 |3.46 |
| Breedte over flens koppelen |483 |19.02 |
| De breedte in de hoofdtekst van de behuizing |443 |17.44 |
| Diepte van front koppelen flens tooextremity van behuizing instantie |577 |22.72 |
| Diepte van bewerkingen van het deelvenster toofurthest uiteinde van behuizing |630.5 |24.82 |
| Diepte van het koppelen van flens toofurthest uiteinde van behuizing |603 |23.74 |

### <a name="enclosure-weight"></a>Behuizing gewicht
Afhankelijk van het Hallo-configuratie, een volledig geladen primaire behuizing wegen van 21 too33 kg en vereist dat twee personen toohandle deze. 

| Behuizing | Gewicht |
| --- | --- |
| Maximale gewicht (afhankelijk van Hallo configuratie) |30 kg – 33 kg |
| Leeg (geen stations gemonteerd) |21 – 23 kg |

## <a name="enclosure-environment-specifications"></a>Behuizing omgeving specificaties
Deze sectie vindt Hallo specificaties gerelateerde toohello behuizing omgeving. Hallo temperatuur, vochtigheid hoogte, gebruik, trillingen, richting, veiligheid en elektromagnetische compatibiliteit (EMC) zijn opgenomen in deze categorie.  

### <a name="temperature-and-humidity"></a>Temperatuur en vochtigheid
| Behuizing | Temperatuurbereik | De relatieve vochtigheid | Maximale NAT bol |
| --- | --- | --- | --- |
| Operationele |5 TEMPERATUUR - 35° C (41° F - 95° F) |20% tot 80% niet-voegen tot- |28° C (82° F) |
| Niet-operationeel |-40 TEMPERATUUR - 70° C (40° F - 158° F) |5-100% niet-voegen tot |29° C (84° F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>Luchtstroom, hoogte, gebruik, trillingen, richting, veiligheid en EMC
| Behuizing | Operationele specificaties |
| --- | --- |
| Luchtstroom |Systeem luchtstroom is front toorear. Systeem moet worden gebruikt met een low-pressure, achterzijde uitlaatgas installatie. Vorige druk gemaakt door rackdeuren en obstakels mag niet meer dan 5 Pascal (0,5 mm water meter). |
| Hoogte, operationele |-30 meters too3045 meters (too10-100 voet, 000 voeten) met maximaal temperatuur ongedaan door 5 ° C hierboven 7000 voeten beoordeeld. |
| Hoogte, niet-operationeel |-305 meters too12, 192 meters (-1,000 voeten too40, 000 voeten) |
| Gebruik, operationele |5g 10 ms ½ sinus |
| Gebruik, niet-operationeel |30g 10 ms ½ sinus |
| Trillingen, operationele |0.21g RMS 5 tot 500 Hz willekeurige |
| Trillingen, niet-operationeel |1.04g RMS 2 tot 200 Hz willekeurige |
| Trillingen, verplaatsing |3g 2 tot 200 Hz sinus |
| Richting en koppelen |19-inch rek monteren (2 EIA eenheden) |
| Rackrails |minimale 700 mm (31.50 inch) diepte rekken toofit compatibel zijn met IEC 297 |
| Veiligheid en goedkeuringen |CE en UL nl 61000-3, IEC 61000-3, UL 61000 3 |
| EMC |EN55022 (CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>Internationale normen naleving
Uw Microsoft Azure StorSimple-apparaat voldoet aan de Hallo internationale normen te volgen:  

* CE - EN 60950-1  
* CB rapport tooIEC 60950-1  
* UL en cUL tooUL 60950-1  

## <a name="safety-compliance"></a>Veiligheid naleving
Uw Microsoft Azure StorSimple-apparaat voldoet aan Hallo veiligheid classificaties te volgen:  

* Systeem productgoedkeuring: UL, cUL, CE  
* Naleving van de veiligheid: UL 60950 IEC 60950, EN 60950  

## <a name="emc-compliance"></a>Naleving van EMC
Uw Microsoft Azure StorSimple-apparaat voldoet aan de Hallo EMC classificaties te volgen.  

### <a name="emissions"></a>Uitstoot
Hallo-apparaat is compatibel met EMC voor die wordt uitgevoerd en uitgezonden niveaus.  

* Uitgevoerde uitstoot beperken niveaus: CFR 47 Part 15B klasse A EN55022 klasse A CISPR klasse A  
* Uitgezonden uitstoot beperken niveaus: CFR 47 Part 15B klasse A EN55022 klasse A CISPR klasse A   

### <a name="harmonics-and-flicker"></a>Harmonischen en knipperen
Hallo-apparaat voldoet aan de EN61000-3-2/3.  

### <a name="immunity-limit-levels"></a>Limiet immuniteitsgrenzen
Hallo-apparaat voldoet aan de EN55024.  

## <a name="ac-power-cord-compliance"></a>AC power kabel naleving
Hallo plug en Hallo voltooid power kabel assembly moet voldoen aan de Hallo geschikt is voor Hallo land in welke Hallo apparaat wordt gebruikt, en deze veiligheid goedkeuringen die geaccepteerd in dat land worden moeten hebben. Hallo volgende tabellen lijst standaarden voor Hallo Verenigde Staten van Amerika en Europa.  

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>Stroomkabels AC - Verenigde Staten (moet NRTL vermeld zijn)
| Onderdeel | Specificatie |
| --- | --- |
| Type van de kabel |Maximale lengte van AVP of SVT, 18 AWG minimum, 3 geleider 2.0 meters |
| Plug |NEMA 5 tot 15P basiskennis type bijlage plug beoordeeld 120 V, 10 A; of IEC 320 C14 250 V, 10 A |
| Socket |IEC 320 C-13, 250 V, 10 A |

### <a name="ac-power-cords---europe"></a>Stroomkabels AC - Europa
| Onderdeel | Specificatie |
| --- | --- |
| Type van de kabel |Geharmoniseerde, H05-VVF-3G1.0 |
| Socket |IEC 320 C-13, 250 V, 10 A |

## <a name="supported-network-cables"></a>Ondersteunde netwerkkabels
Raadpleeg toohello voor Hallo 10 GbE-netwerkinterfaces DATA 2 en DATA 3 [lijst met ondersteunde netwerkkabels en modules](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).

## <a name="next-steps"></a>Volgende stappen
U bent nu klaar toodeploy een StorSimple-apparaat in uw datacenter. Zie voor meer informatie [implementeren van uw on-premises apparaat](storsimple-deployment-walkthrough-u2.md).  

