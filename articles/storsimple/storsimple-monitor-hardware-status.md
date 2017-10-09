---
title: aaaStorSimple hardwareonderdelen en status | Microsoft Docs
description: Meer informatie over hoe toomonitor Hallo hardware-onderdelen van uw StorSimple-apparaat via Hallo StorSimple Manager-service.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>Gebruik Hallo StorSimple Manager-service toomonitor hardware-onderdelen en status
## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven Hallo verschillende fysieke en logische onderdelen in uw on-premises StorSimple-apparaat. Ook wordt uitgelegd hoe toomonitor Onderdeelstatus apparaat via Hallo Hallo **onderhoud** pagina in Hallo StorSimple Manager-service. 

Hallo **onderhoud** pagina status van de hardware van alle onderdelen van het StorSimple-apparaat Hallo Hallo bevat. 

Onder de lijst met onderdelen 8100 Hallo zijn er drie secties waarin wordt beschreven:

* **Gedeelde onderdelen** – deze maken geen deel uit van Hallo-controllers, zoals harde schijven, behuizing, PCM-onderdelen en PCM temperatuur, regel spanning en huidige sensoren regel.
* **Onderdelen van de controller 0** – Hallo-onderdelen die zich bevinden op Controller 0, zoals domeincontrollers, SAS-uitbreidingsmodule en connector temperatuursensors domeincontroller, en verschillende Hallo netwerkinterfaces.
* **Onderdelen van de controller 1** – Hallo onderdelen die deel uitmaken van de Controller 1, vergelijkbare toothose gedetailleerde voor Controller 0.

Een 8600-apparaat heeft extra onderdelen die overeenkomen met toohello behuizing uitgebreid Bunch van schijven (EBOD). Er zijn vijf secties onder Hallo lijst van onderdelen. Er zijn van deze drie secties die identiek toohello die hierboven worden beschreven voor 8100 Hallo-onderdelen in de primaire behuizing Hallo bevat. Er zijn twee extra secties voor Hallo EBOD behuizing waarin wordt beschreven:

* **EBOD behuizing gedeelde onderdelen** – Hallo onderdelen aanwezig zijn op Hallo EBOD enclosure en PCM die geen deel uitmaken van Hallo EBOD controller.
* **EBOD Controller 0 onderdelen** – Hallo onderdelen die zich op EBOD behuizing, 0, zoals Hallo EBOD controller temperatuursensors SAS uitbreidingsmodule en de connector en de domeincontroller bevinden.
* **Onderdelen van EBOD Controller 1** – onderdelen die deel uitmaken van EBOD behuizing 1, Hallo vergelijkbare toothose gedetailleerde voor EBOD behuizing 0.

> [!NOTE]
> **Hallo hardware status sectie is niet aanwezig in Hallo onderhoudspagina voor een virtueel StorSimple-apparaat (1100).**
> 
> 

## <a name="monitor-hello-hardware-status"></a>Hallo hardwarestatus controleren
Voer Hallo stappen tooview Hallo status van de hardware van een apparaatonderdeel te volgen:

1. Navigeer te**apparaten**, selecteert u een specifieke StorSimple-apparaat. Toogo in Hallo op apparaatniveau menu en klik op **onderhoud**. 
2. Zoek Hallo **hardwarestatus** sectie en kies uit de beschikbare onderdelen Hallo (zoals hierboven beschreven). Klik op een pijl Hallo label tooexpand Hallo lijst en bekijkt hello Onderdeelstatus Hallo voorafgaand aan verschillende Apparaatonderdelen. Zie Hallo [lijst met gedetailleerde onderdelen voor de primaire behuizing Hallo](#component-list-for-primary-enclosure-of-storsimple-device) en Hallo [lijst met gedetailleerde onderdelen voor Hallo EBOD behuizing](#component-list-for-ebod-enclosure-of-storsimple-device).
3. Gebruik Hallo kleurcodering schema toointerpret Hallo onderdeelstatus te volgen:
   
   * **Selectievakje groen** – Denotes een **goed** of **OK** onderdeel.
   * **Gele** – geeft aan een onderdeel in **waarschuwing** status.
   * **Rood uitroepteken** – Denotes een onderdeel dat heeft een **fout** of **aandacht** status.
   * **Met de zwarte tekst wit** – geeft aan een onderdeel dat is niet aanwezig.
4. Als er een onderdeel dat zich niet in een **goed** status, neem contact op met Microsoft Support. Als u waarschuwingen op het apparaat zijn ingeschakeld, ontvangt u een e-mailmelding. Als u een mislukte hardwareonderdeel tooreplace moet, Zie [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Lijst met onderdelen voor primaire behuizing van StorSimple-apparaat
Hallo Hallo volgende overzichten van de tabel fysieke en logische onderdelen die zijn opgenomen in de primaire behuizing Hallo van uw on-premises StorSimple-apparaat.

| Onderdeel | Module | Type | Locatie | Veld FRU (replaceable unit)? | Beschrijving |
| --- | --- | --- | --- | --- | --- |
| Station in sleuf [0-11] |Harde schijven |Fysieke |Gedeeld |Ja |Één lijn wordt weergegeven voor elke Hallo SSD of Hallo HDD-schijven in Hallo primaire behuizing. |
| Ambient-temperatuursensor |Behuizing |Fysieke |Gedeeld |Nee |Metingen Hallo temperatuur in Hallo chassis. |
| Halverwege vlak-temperatuursensor |Behuizing |Fysieke |Gedeeld |Nee |Metingen Hallo temperatuur van Hallo halverwege vlak. |
| Akoestisch alarm |Behuizing |Fysieke |Gedeeld |Nee |Hiermee wordt aangegeven of Hallo akoestisch alarm subsysteem in Hallo chassis functioneel. |
| Behuizing |Behuizing |Fysieke |Gedeeld |Ja |Hallo aanwezigheid van een chassis aangeeft. |
| Bijlage-instellingen |Behuizing |Fysieke |Gedeeld |Nee |Toohello voorpaneel van Hallo chassis verwijst. |
| Regel spanning sensoren |PCM |Fysieke |Gedeeld |Nee |Talrijke regel spanning sensoren hebben hun status wordt weergegeven, waarin wordt aangegeven of Hallo gemeten spanning binnen de tolerantie. |
| De huidige sensoren regel |PCM |Fysieke |Gedeeld |Nee |Talrijke regel huidige sensoren hebben hun status wordt weergegeven, waarin wordt aangegeven of hello gemeten huidige binnen de tolerantie. |
| Temperatuursensors in PCM |PCM |Fysieke |Gedeeld |Nee |Talrijke temperatuursensors zoals Inlet en Hotspot sensoren hebben hun status wordt weergegeven, die aangeeft of Hallo temperatuur gemeten valt binnen de tolerantie. |
| Voeding [0-1] |PCM |Fysieke |Gedeeld |Ja |Één lijn wordt weergegeven voor elke stroom wordt voorzien in Hallo Hallo twee PCMs zich in Hallo achterzijde Hallo-apparaat. |
| Koeling [0-1] |PCM |Fysieke |Gedeeld |Ja |Een regel wordt weergegeven voor elke Hallo vier ventilatoren die zich in Hallo twee PCMs. |
| Accu [0-1] |PCM |Fysieke |Gedeeld |Ja |Een regel wordt weergegeven voor elke Hallo back-up batterij modules die zijn aangebracht in Hallo PCM. |
| Metis |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo-status van Hallo batterijen: Hiermee wordt aangegeven of ze moeten in rekening gebracht en naderen einde van de levenscyclus. |
| Cluster |N.v.t. |Logische |Gedeeld |N.v.t. |Geeft de status van Hallo-cluster dat wordt gemaakt tussen de twee geïntegreerde controller modules Hallo Hallo. |
| Clusterknooppunt |N.v.t. |Logische |Gedeeld |N.v.t. |Geeft de status Hallo van Hallo controller als onderdeel van Hallo-cluster. |
| Clusterquorum |N.v.t. |Logische | |N.v.t. |Hiermee wordt aangegeven Hallo aanwezigheid van het Hallo meerderheid schijf lidmaatschap van Hallo HDD-opslaggroep. |
| HDD gegevensruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo-opslagruimte die wordt gebruikt voor gegevens in Hallo harde schijf (HDD)-opslaggroep. |
| HDD management ruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo-ruimte is gereserveerd in Hallo HDD-opslaggroep voor beheertaken. |
| Harde schijf quorum ruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo-ruimte is gereserveerd in Hallo HDD-opslaggroep voor het clusterquorum. |
| HDD vervanging ruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo-ruimte is gereserveerd in Hallo HDD-opslaggroep voor vervanging van de domeincontroller. |
| SSD gegevensruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo opslagruimte die wordt gebruikt voor gegevens in de opslaggroep van Hallo Solid-State station (SSD). |
| SSD NVRAM ruimte |N.v.t. |Logische |Gedeeld |N.v.t. |Hallo opslagruimte in Hallo SSD opslaggroep die is toegewezen voor NVRAM logica. |
| HDD-opslaggroep |N.v.t. |Logische |Gedeeld |N.v.t. |Geeft de status van Hallo logische opslaggroep die wordt gemaakt van apparaat HDD's Hallo. |
| SSD-opslaggroep |N.v.t. |Logische |Gedeeld |N.v.t. |Geeft de status van Hallo logische opslaggroep die wordt gemaakt van apparaat SSD's Hallo. |
| Controller [0-1] [state] |I/O 'S |Fysieke |Domeincontroller |Ja |Hallo-status van het Hallo-controller, en of deze in de actieve of stand-by-modus in Hallo chassis. |
| Temperatuursensors in netwerkcontroller |I/O 'S |Fysieke |Domeincontroller |Nee |Talrijke temperatuursensors zoals i/o-module, CPU-temperatuur, DIMM en PCIe sensoren hebben hun status wordt weergegeven, waarin wordt aangegeven of Hallo temperatuur aangetroffen binnen de tolerantie. |
| SAS uitbreidingsmodule |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo seriële gekoppelde SCSI (SAS) uitbreidingsmodule, namelijk gebruikte tooconnect Hallo geïntegreerde toohello opslagcontroller. |
| SAS-connector [0-1] |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van elke SAS-connector, gebruikte tooconnect geïntegreerd opslag toohello SAS uitbreidingsmodule. |
| SBB halverwege vlak tussen geheugenonderdelen |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft Hallo status Hallo halverwege vlak connector, gebruikte tooconnect is elke domeincontroller toohello halverwege vlak. |
| Processorcore |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van processor-cores Hallo binnen elke domeincontroller. |
| Behuizing electronics power |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo power systeem die wordt gebruikt door Hallo behuizing. |
| Behuizing electronics diagnostische gegevens |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo diagnostics subsystemen geleverd door het Hallo-controller. |
| Bmc (Baseboard Management Controller) |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo baseboard management controller (BMC) Dit is een speciale serviceprocessor Hallo hardwareapparaat bewaakt door sensoren en communiceert met de systeembeheerder Hallo via een onafhankelijke verbinding. |
| Ethernet |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van elke Hallo netwerkinterfaces, dat wil zeggen Hallo management en gegevenspoorten op Hallo-domeincontroller. |
| NVRAM |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van NVRAM, een niet-vluchtige RAM-geheugen back-up gemaakt door Hallo accu dat tooretain toepassing kritieke informatie in het Hallo-gebeurtenis van stroomstoring. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Lijst met onderdelen voor EBOD behuizing van StorSimple-apparaat
Hallo Hallo volgende overzichten van de tabel fysieke en logische onderdelen die zijn opgenomen in Hallo EBOD behuizing van uw on-premises StorSimple-apparaat.

| Onderdeel | Module | Type | Locatie | FRU? | Beschrijving |
| --- | --- | --- | --- | --- | --- |
| Station in sleuf [0-11] |Harde schijven |Fysieke |Gedeeld |Ja |Één lijn wordt weergegeven voor elke Hallo die HDD-aan de voorzijde Hallo Hallo EBOD behuizing schijven. |
| Ambient-temperatuursensor |Behuizing |Fysieke |Gedeeld |Nee |Metingen Hallo temperatuur in Hallo chassis. |
| Halverwege vlak-temperatuursensor |Behuizing |Fysieke |Gedeeld |Nee |Metingen Hallo temperatuur van Hallo halverwege vlak. |
| Akoestisch alarm |Behuizing |Fysieke |Gedeeld |Nee |Hiermee wordt aangegeven of Hallo akoestisch alarm subsysteem in Hallo chassis functioneel. |
| Behuizing |Behuizing |Fysieke |Gedeeld |Ja |Hallo aanwezigheid van een chassis aangeeft. |
| Bijlage-instellingen |Behuizing |Fysieke |Gedeeld |Nee |Toohello OPS of Hallo voorpaneel van Hallo chassis verwijst. |
| Regel spanning sensoren |PCM |Fysieke |Gedeeld |Nee |Talrijke regel spanning sensoren hebben hun status wordt weergegeven, waarin wordt aangegeven of Hallo gemeten spanning binnen de tolerantie. |
| De huidige sensoren regel |PCM |Fysieke |Gedeeld |Nee |Talrijke regel huidige sensoren hebben hun status wordt weergegeven, waarin wordt aangegeven of hello gemeten huidige binnen de tolerantie. |
| Temperatuursensors in PCM |PCM |Fysieke |Gedeeld |Nee |Talrijke temperatuursensors zoals Inlet en Hotspot sensoren hebben hun status wordt weergegeven, waarmee wordt aangegeven of Hallo temperatuur gemeten valt binnen de tolerantie. |
| Voeding [0-1] |PCM |Fysieke |Gedeeld |Ja |Één lijn wordt weergegeven voor elke stroom wordt voorzien in Hallo Hallo twee PCMs zich in Hallo achterzijde Hallo-apparaat. |
| Koeling [0-1] |PCM |Fysieke |Gedeeld |Ja |Een regel wordt weergegeven voor elke Hallo vier ventilatoren die zich in Hallo twee PCMs. |
| Lokale opslag [HDD] |N.v.t. |Logische |Gedeeld |N.v.t. |Geeft de status van Hallo logische opslaggroep die wordt gemaakt van apparaat HDD's Hallo. |
| Controller [0-1] [state] |I/O 'S |Fysieke |Domeincontroller |Ja |Geeft de status van Hallo domeincontrollers in Hallo EBOD module Hallo. |
| Temperatuursensors in EBOD |I/O 'S |Fysieke |Domeincontroller |Nee |Talrijke temperatuursensors van elke domeincontroller hebben hun status wordt weergegeven, waarin wordt aangegeven of Hallo temperatuur aangetroffen binnen de tolerantie. |
| SAS uitbreidingsmodule |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo SAS uitbreidingsmodule, gebruikte tooconnect Hallo geïntegreerde toohello opslagcontroller is. |
| SAS-connector [0-2] |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van elke SAS-connector, gebruikte tooconnect geïntegreerd opslag toohello SAS uitbreidingsmodule. |
| SBB halverwege vlak tussen geheugenonderdelen |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft Hallo status Hallo halverwege vlak connector, gebruikte tooconnect is elke domeincontroller toohello halverwege vlak. |
| Behuizing electronics power |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo power systeem die wordt gebruikt door Hallo behuizing. |
| Behuizing electronics diagnostische gegevens |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo diagnostics subsystemen geleverd door het Hallo-controller. |
| Verbinding toodevice controller |I/O 'S |Fysieke |Domeincontroller |Nee |Geeft de status Hallo van Hallo verbinding tussen Hallo EBOD i/o-module en Hallo apparaat controller. |

## <a name="next-steps"></a>Volgende stappen
* toouse hello StorSimple Manager service tooadminister uw apparaat, ga te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).
* Als u een apparaatonderdeel met de gedegradeerde of mislukte status tootroubleshoot nodig hebt, raadpleegt u te [StorSimple indicatoren](storsimple-monitoring-indicators.md). 
* Zie voor een mislukte hardwareonderdeel tooreplace [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).
* Als u tooexperience apparaat problemen doorgaat [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).

