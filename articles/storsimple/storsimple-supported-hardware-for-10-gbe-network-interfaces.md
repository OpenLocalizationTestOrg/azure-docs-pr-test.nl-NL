---
title: aaaHardware voor StorSimple 10 GbE-interfaces | Microsoft Docs
description: Beschrijft Hallo ondersteund kleine vormfactor pluggable (SFP) infraroodzenders, kabels en switches voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: df8d40c7-f5ad-4f84-93eb-779fbd5f7243
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 3e6769380040ab08d9a57ef7221bf62c6c855137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-hardware-for-hello-10-gbe-network-interfaces-on-your-storsimple-device"></a>Ondersteunde hardware voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Dit artikel bevat informatie over aanvullende hardware die geschikt is voor uw Microsoft Azure StorSimple-apparaat.

## <a name="list-of-devices-tested-by-microsoft"></a>Lijst met apparaten die door Microsoft getest
Microsoft heeft getest Hallo na het pluggable (SFP) infraroodzenders kleine vormfactor, kabels en switches tooensure optimaal worden werken met apparaten. (Hallo volgende tabellen worden bijgewerkt als nieuwe hardware wordt getest.)

### <a name="sfp-transceivers"></a>SFP + infraroodzenders
| Maken | Model |
| --- | --- |
| Cisco |SFP-10G-SR |

### <a name="cables"></a>Kabels
| S. Nee. | Maken | Model |
| --- | --- | --- |
| 1. |Cisco |SFP-H10GB-CU1M |
| 2. |Cisco |SFP-H10GB-CU2M |
| 3. |Cisco |SFP-H10GB-CU3M |
| 4. |Tripp Lite |N820 - 05-M (OM3) |

### <a name="switches"></a>Switches
| S. Nee. | Maken | Model |
| --- | --- | --- |
| 1. |Cisco |N3K-C3172PQ-10GE |
| 2. |Cisco |N3K-C3048-ZM-F |
| 3. |Cisco |N5K-C5596UP-VA |

## <a name="list-of-devices-tested-in-hello-field"></a>Lijst met apparaten die zijn getest in Hallo-veld
Deze sectie bevat Hallo-lijst met apparaten die u hebt geïmplementeerd in het veld Hallo van StorSimple-klanten. Deze zijn niet door Microsoft getest, maar zijn waarschijnlijk toowork met uw StorSimple-apparaat.

| Parameter | Waarde |
| --- | --- |
| Switch maken |Juniper |
| Switch-model |ex4550 32F |
| De versie van de switch-besturingssysteem |JunOS 12.3R9.4 |
| Blade-model |Poorten vrijgeven (PIC 0) |
| Zender maken |Juniper |
| Zender model |Onderdeelnummer 740 021308 <br></br> Onderdeelnummer 740 030658 |
| Zender firmwareversie |Rev. 01 versie 0,0 (gerapporteerd) |
| Model van de kabel |Duplex meestal LC/LC 50/125µ, OM3, LSZH |
| StorSimple-model |8600 |
| De softwareversie StorSimple |6.3.9600.17491 |

## <a name="list-of-devices-tested-by-oem-provider-mellanox"></a>Lijst met apparaten die zijn getest door OEM-provider (Mellanox)
Mellanox heeft getest Hallo na het pluggable (SFP) infraroodzenders kleine vormfactor, kabels en switches tooensure optimaal worden werken met Mellanox netwerkinterfaces zoals Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat.

### <a name="cables-and-modules-supported-by-mellanox"></a>Kabels en modules die worden ondersteund door Mellanox
Hallo volgende tabel bevat Hallo kabels en modules die worden ondersteund door Mellanox. Deze zijn niet door Microsoft getest, maar zijn waarschijnlijk toowork met uw StorSimple-apparaat.

| S. Nee. | Snelheid | Model | Beschrijving | Maken |
| --- | --- | --- | --- | --- |
| 1. |10 GbE |CAB-SFP-SFP - 1M |passieve koper kabel SFP + 10 Gb/s-1m |Arista |
| 2. |10 GbE |CAB-SFP-SFP - 2M |passieve koper kabel SFP + 10 Gb/s 2 MB |Arista |
| 3. |10 GbE |CAB-SFP-SFP - 3M |passieve koper kabel SFP + 10 Gb/s 3m |Arista |
| 4. |10 GbE |CAB-SFP-SFP - 5M |passieve koper kabel SFP + 10 Gb/s 5m |Arista |
| 5. |10 GbE |Cisco SFP-H10GBCU1M |Cisco SFP + kabel |Cisco |
| 6. |10 GbE |Cisco SFP-H10GBCU3M |Cisco SFP + kabel |Cisco |
| 7. |10 GbE |Cisco SFP-H10GBCU5M |Cisco SFP + kabel |Cisco |
| 8. |10 GbE |HP J9281B X242 10 G |SFP + tooSFP + 1m directe koppelen koper-kabel |HP |
| 9. |10 GbE |455883 B21 HP BLc |10Gb SR SFP + kiezen |HP |
| 10. |10 GbE |455886 B21 HP BLc |10Gb LR SFP + kiezen |HP |
| 11. |10 GbE |487649 B21 HP BLc |SFP + 0,5 m 10GbE koper kabel |HP |
| 12. |10 GbE |487652 B21 HP BLc |1m 10GbE SFP + koper kabel |HP |
| 13. |10 GbE |487655 B21 HP BLc |SFP + 3m 10GbE koper kabel |HP |
| 14. |10 GbE |487658 B21 HP BLc |SFP + 7m 10GbE koper kabel |HP |
| 15. |10 GbE |537963 B21 HP BLc |SFP + 5m 10GbE koper kabel |HP |
| 16. |10 GbE |HP AP784A |3m C-serie passieve koper SFP + kabel |HP |
| 17. |10 GbE |HP AP785A |5m C-serie passieve koper SFP + kabel |HP |
| 18. |10 GbE |HP AP818A |1m B-serie Active koper SFP + kabel |HP |
| 19. |10 GbE |HP AP819A |3m B-serie Active koper SFP + kabel |HP |
| 20. |10 GbE |HP J9150A |X132 10 G SFP + LC SR zender |HP |
| 21. |10 GbE |HP J9151A |X132 10 G SFP + LC LR zender |HP |
| 22. |10 GbE |HP J9283B |X242 10 G SFP + SFP + 3 m DAC-kabel |HP |
| 23. |10 GbE |HP J9285B |X242 10 G SFP + SFP + 7 m DAC-kabel |HP |
| 24. |10 GbE |HP JD095B |X240 10 G SFP + SFP + 0.65 m DAC-kabel |HP |
| 25. |10 GbE |HP JD096B |X240 10 G SFP + SFP + 1,2 m DAC-kabel |HP |
| 26. |10 GbE |HP JD097B |X240 10 G SFP + SFP + 3 m Pa-kabel |HP |
| 27. |10 GbE |MAM1Q00A QSA Mellanox |QSFP tooSFP + Adapter |Mellanox technologieën |
| 28. |10 GbE |MC2309124 006 Mt |Passieve koper kabel 1 x SFP + tooQSFP 10Gb/s 24awg 7m |Mellanox technologieën |
| 29. |10 GbE |MC2309124 007 Mt |Passieve koper kabel 1 x SFP + tooQSFP 10Gb/s 24awg 7m |Mellanox technologieën |
| 30. |10 GbE |MC2309130 003 Mt |Passieve koper kabel 1 x SFP + tooQSFP 10Gb/s 30awg 3m |Mellanox technologieën |
| 31. |10 GbE |MC2309130 00A Mt |Passieve koper kabel 1 x SFP + tooQSFP 10Gb/s 30awg 0,5 m |Mellanox technologieën |
| 32. |10 GbE |MC3309124 005 Mt |Passieve koper bekabelen 1 x SFP+ 10 Gb/s 24awg 5 m |Mellanox technologieën |
| 33. |10 GbE |MC3309124 007 Mt |Passieve koper bekabelen 1 x SFP+ 10 Gb/s 24awg 7 m |Mellanox technologieën |
| 34. |10 GbE |MC3309130 003 Mt |Passieve koper bekabelen 1 x SFP+ 10 Gb/s 30awg 3 m |Mellanox technologieën |
| 35. |10 GbE |MC3309130 00A Mt |Passieve koper bekabelen 1 x SFP+ 10 Gb/s 30awg 0,5 m |Mellanox technologieën |

### <a name="switches-supported-by-mellanox"></a>Switches die worden ondersteund door Mellanox
Hallo volgende tabel geeft een lijst wordt ondersteund door Mellanox Hallo-switches. Deze zijn niet door Microsoft getest, maar zijn waarschijnlijk toowork met uw StorSimple-apparaat.

| S. Nee. | Snelheid | Model | Beschrijving | Maken |
| --- | --- | --- | --- | --- |
| 1. |10GbE |516733 B21 |HP ProCurve 6120XG 10GbE Ethernet-Blade Switch |HP |
| 2. |10GbE |538113 B21 |HP 10GbE Pass-Through-Module (PTM) |HP |
| 3. |10GbE |EN4093 |IBM PureFlex Fabric EN4093 10 Gigabit schaalbare Switch Systeemmodule |IBM |
| 4. |1GbE |3020 |Cisco exemplaar 3020 1GbE switch blade |Cisco |
| 5. |1GbE |3020 X |Cisco exemplaar 3020 X 1GbE switch-blade |Cisco |
| 6. |1GbE |438030 B21 |1GbE switch-module voor HP - GbE2c Layer 2/3 Ethernet-Blade Switch |HP |
| 7. |1GbE |6120G |HP ProCurve 6120G/XG 1GbE switch-blade |HP |

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over de hardware-onderdelen StorSimple en status](storsimple-monitor-hardware-status.md).

