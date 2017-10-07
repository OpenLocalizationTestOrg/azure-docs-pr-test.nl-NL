---
title: aaaStorSimple virtuele matrix Update 0,4 release-opmerkingen | Microsoft Docs
description: Kritieke open beschrijft problemen en oplossingen voor het werken met het virtuele StorSimple-matrix van Hallo 0,4 bijwerken.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>StorSimple virtuele matrix Update 0,4 release-opmerkingen

## <a name="overview"></a>Overzicht

Hallo volgende releaseopmerkingen Hallo kritieke open problemen identificeren en Hallo opgeloste problemen voor updates van Microsoft Azure StorSimple virtuele matrix.

Hallo release-opmerkingen worden voortdurend bijgewerkt en wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw virtuele StorSimple-matrix implementeert, zorgvuldig door Hallo gegevens in Hallo release-opmerkingen.

Update 0,4 overeenkomt met de softwareversie toohello **10.0.10289.0**.

> [!NOTE]
> Updates kunnen verstoren, start het apparaat. Als i/o's uitgevoerd worden, wordt het apparaat Hallo uitvaltijd systeem.


## <a name="whats-new-in-hello-update-04"></a>Wat is er nieuw in Update 0,4 Hallo
Update 0,4 is voornamelijk een bug fix build samen met enkele verbeteringen. In deze versie, is enkele fouten, wat leidt tot mislukte back-ups in de vorige versie Hallo behandeld. de belangrijkste verbeteringen Hallo en oplossingen voor problemen zijn als volgt:

- **Back-up prestatieverbeteringen** -deze release heeft gemaakt, worden verschillende belangrijke verbeteringen tooimprove Hallo back-upprestaties. Als gevolg hiervan Zie Hallo back-ups waarbij een groot aantal bestanden een significante vermindering van Hallo tijd toocomplete voor volledige en incrementele back-ups.

- **Verbeterde prestaties terugzetten** -deze release bevat verbeteringen in de Hallo terugzetten prestaties aanzienlijk verbeteren wanneer u veel bestanden. Als 2-4 miljoen bestanden gebruikt, raden wij aan dat u een virtuele-matrix met 16 GB RAM-geheugen toosee Hallo verbeteringen inrichten. Wanneer met behulp van minder dan 2 miljoen bestanden, Hallo minimumvereiste voor Hallo virtuele machine blijft toobe wordt 8 GB RAM-geheugen.

- **Verbeteringen tooSupport pakket** -Hallo verbeteringen bestaan onder andere statistieken voor de schijf, CPU, geheugen, netwerk- en cloud in Hallo ondersteuningspakket waardoor verbetering Hallo proces van het apparaat problemen diagnosticeren/foutopsporing Hallo aanmelden.

- **Limiet lokaal vastgemaakt iSCSI-volumes too200 GB** -voor lokaal vastgemaakte volumes is het raadzaam dat u tooa 200 GB iSCSI-volume op uw virtuele StorSimple-matrix beperkt. Hallo lokale reservering voor gelaagde volumes blijft toobe 10% Hallo volumegrootte ingericht, maar is beperkt tot 200 GB. 

- **Back-up-gerelateerde oplossingen voor problemen** -In eerdere versies van software gerelateerde toobackups problemen waardoor mislukte back-ups zijn. Deze fouten zijn gericht in deze release.


## <a name="issues-fixed-in-hello-update-04"></a>Problemen in Hallo Update 0,4 opgelost

Hallo bevat volgende tabel een samenvatting van problemen in deze release worden opgelost.

| Nee. | Functie | Probleem |
| --- | --- | --- |
| 1 |Back-upprestaties|In eerdere versies Hallo, Hallo back-ups met betrekking tot groot aantal bestanden een toocomplete lang zou duren (in volgorde van de Hallo van dagen). Zie een significante vermindering van Hallo tijd toocompletion in deze release, zowel Hallo volledige en incrementele back-ups. |
| 2 |Ondersteuningspakket|Schijf, CPU, geheugen, netwerk- en cloud-statistieken worden nu vastgelegd in Logboeken toohello Hallo ondersteuningspakketten zeer effectief zijn bij het oplossen van problemen apparaat maken.|
| 3 |Back-up |In eerdere versies kan langlopende back-ups leiden tot een crisis ruimte op Hallo apparaat, wat leidt tot mislukte back-ups. Deze fout wordt beschreven in deze release in één keer doordat tooqueue niet meer dan 5 back-ups.|
| 4 |iSCSI | In eerdere versies was Hallo lokale reservering voor gelaagde of lokaal vastgemaakte volumes 10% van de volumegrootte Hallo ingericht. In deze release is Hallo lokale reservering voor alle iSCSI-volumes (lokaal vastgemaakt of gelaagde) beperkt too10% met een maximum van maximaal 200 GB (voor gelaagde volumes die groter is dan 2 TB) zodat u meer ruimte op de lokale schijf Hallo vrijmaken. U wordt aangeraden dat Hallo lokaal vastgemaakte volumes in deze release beperkt too200 GB zijn.|


## <a name="known-issues-in-hello-update-04"></a>Bekende problemen in Hallo Update 0,4

Hallo volgende tabel bevat een samenvatting van bekende problemen voor het virtuele StorSimple-matrix Hallo en omvat Hallo problemen release genoteerd uit Hallo vorige versies. 

| Nee. | Functie | Probleem | Tijdelijke oplossing/opmerkingen |
| --- | --- | --- | --- |
| **1.** |Updates |Hallo virtuele apparaten gemaakt in de preview-versie Hallo niet bijgewerkte tooa ondersteund algemene beschikbaarheid versie. |Deze virtuele apparaten, moeten voor algemene beschikbaarheid release met een disaster recovery (DR) werkstroom Hallo failover worden uitgevoerd. |
| **2.** |Ingerichte gegevensschijf |Eenmaal hebt u een gegevensschijf van een bepaalde opgegeven omvang ingericht en Hallo bijbehorende virtuele StorSimple-apparaat hebt gemaakt, moet u niet uitbreiden of verkleinen Hallo gegevensschijf. Er wordt geprobeerd toodo resulteert in een verlies van alle Hallo gegevens in de lokale lagen Hallo Hallo-apparaat. | |
| **3.** |Groepsbeleid |Wanneer een apparaat lid van een domein is, kan een Groepsbeleid toepassen nadelig beïnvloeden Hallo apparaat bewerking. |Zorg ervoor dat uw virtuele matrix in de eigen organisatie-eenheid (OE) voor Active Directory en geen groepsbeleidsobjecten (GPO) toegepaste tooit zijn. |
| **4.** |Lokale webgebruikersinterface |Als verbeterde beveiligingsfuncties zijn ingeschakeld in Internet Explorer (IE ESC), is het mogelijk dat sommige gebruikersinterface lokale webpagina's zoals probleemoplossing of onderhoud niet correct werkt. Knoppen op deze pagina's ook werkt mogelijk niet. |Verbeterde beveiligingsfuncties in Internet Explorer uitschakelen. |
| **5.** |Lokale webgebruikersinterface |In een Hyper-V virtuele machine, Hallo netwerkinterfaces in Hallo web-gebruikersinterface worden weergegeven als 10 Gbps-interfaces. |Dit gedrag is een weerspiegeling van Hyper-V. 10 Gbps voor virtuele netwerkadapters worden altijd weergegeven in Hyper-V. |
| **6.** |Gelaagde volumes of shares |Vergrendeling voor toepassingen die met Hallo StorSimple gelaagde volumes werken bereik in bytes wordt niet ondersteund. Als byte bereik vergrendeling is ingeschakeld, werkt StorSimple lagen niet. |Aanbevolen maatregelen zijn onder andere: <br></br>Bereik aan bytes is vergrendeld in uw toepassingslogica uitschakelen.<br></br>Kies tooput gegevens voor deze toepassing in lokaal vastgemaakte volumes tegenstelling tot tootiered volumes.<br></br>*Hoewel*: wanneer met behulp van lokaal volumes vastgemaakte en byte bereik vergrendeling is ingeschakeld, Hallo lokaal vastgemaakt volume online kan worden voordat Hallo herstellen voltooid is. In dergelijke gevallen als een herstelbewerking uitgevoerd wordt, moet klikt u wachten Hallo terugzetten toocomplete. |
| **7.** |Gelaagde shares |Werken met grote bestanden kan leiden tot een trage laag. |Als u werkt met grote bestanden, wordt u aangeraden dat Hallo grootste bestand kleiner is dan 3% van de grootte van de bestandsshare Hallo. |
| **8.** |Capaciteit voor shares gebruikt |Mogelijk ziet u verbruik delen wanneer er geen gegevens op Hallo-share zijn. Dit is omdat Hallo gebruikt capaciteit voor shares metagegevens bevat. | |
| **9.** |Herstel na noodgevallen |U kunt alleen noodherstel Hallo van een bestand server toohello uitvoeren hetzelfde domein als die van het bronvolume Hallo. Disaster recovery tooa doelapparaat in een ander domein wordt niet ondersteund in deze release. |Dit is geïmplementeerd in een latere release. |
| **10.** |Azure PowerShell |Hallo virtuele StorSimple-apparaten kunnen niet worden beheerd via hello Azure PowerShell in deze release. |Alle Hallo beheer van virtuele apparaten Hallo moet worden gedaan door middel van Hallo klassieke Azure-portal en Hallo lokale webgebruikersinterface. |
| **11.** |Wachtwoord wijzigen |Hallo virtuele matrix apparaat console accepteert alleen invoer in de indeling en-US. | |
| **12.** |CHAP |CHAP-referenties eenmaal is gemaakt, kunnen niet worden verwijderd. Bovendien als u CHAP-referenties Hallo wijzigt, u moet tootake Hallo volumes offline en breng vervolgens on line voor Hallo wijziging tootake effect. |Dit probleem is verholpen in een latere versie. |
| **13.** |iSCSI-server |Hallo 'Opslagruimte hebt gebruikt' voor een iSCSI-volume weergegeven kan niet verschillen in Hallo StorSimple Manager-service en Hallo iSCSI-host. |Hallo iSCSI-host heeft Hallo bestandssysteem weergave.<br></br>Hallo apparaat ziet toegewezen wanneer Hallo volume op de maximale grootte Hallo is Hallo-blokken. |
| **14.** |Bestandsserver |Als een bestand in een map een alternatieve gegevens stroom (ADS heeft) gekoppeld, is niet Hallo ADVERTENTIES back-up gemaakt of hersteld via herstel na noodgevallen, klonen en herstel Item. | |
| **15.** |Bestandsserver |Symbolische koppelingen worden niet ondersteund. | |
| **16.** |Bestandsserver |Bestanden beveiligd door Windows Encrypting File System (EFS) wanneer gekopieerd of opgeslagen op Hallo virtuele StorSimple-matrix bestand server resultaat in een niet-ondersteunde configuratie.  | |

## <a name="next-step"></a>Volgende stap
[Installeer Update 0,4](storsimple-virtual-array-install-update-04.md) op uw virtuele StorSimple-matrix.

## <a name="references"></a>Verwijzingen
Zoekt u een oudere versie Opmerking? Ga naar: 

* [StorSimple virtuele matrix Update 0,3 Release-opmerkingen](storsimple-ova-update-03-release-notes.md)
* [StorSimple virtuele matrix Update 0,1-0,2 Release-opmerkingen](storsimple-ova-update-01-release-notes.md)
* [StorSimple virtuele matrix algemene beschikbaarheid Release-opmerkingen](storsimple-ova-pp-release-notes.md)

