---
title: aaaStorSimple virtuele matrix Update 0,5 release-opmerkingen | Microsoft Docs
description: Kritieke open beschrijft problemen en oplossingen voor het werken met het virtuele StorSimple-matrix van Hallo 0,5 bijwerken.
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
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>StorSimple virtuele matrix Update 0,5 release-opmerkingen

## <a name="overview"></a>Overzicht

Hallo volgende releaseopmerkingen Hallo kritieke open problemen identificeren en Hallo opgeloste problemen voor updates van Microsoft Azure StorSimple virtuele matrix.

Hallo release-opmerkingen worden voortdurend bijgewerkt en wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw virtuele StorSimple-matrix implementeert, zorgvuldig door Hallo gegevens in Hallo release-opmerkingen.

Update 0,5 overeenkomt met de softwareversie toohello **10.0.10290.0**.

> [!NOTE]
> Updates kunnen verstoren, start het apparaat. Als i/o's uitgevoerd worden, wordt het apparaat Hallo uitvaltijd systeem. Voor gedetailleerde instructies voor het hoe tooapply Hallo update gaat te[installeert u Update 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Wat is er nieuw in Update 0,5 Hallo
Update 0,5 is voornamelijk een bug fix build. de belangrijkste verbeteringen Hallo en oplossingen voor problemen zijn als volgt:

- **Back-up tolerantie verbeteringen** -deze release is oplossingen die Hallo back-tolerantie te verbeteren. In Hallo back-ups van eerdere versies werden opnieuw alleen voor bepaalde uitzonderingen. Deze release opnieuw probeert alle Hallo back-uitzonderingen en zorgt ervoor dat de back-ups toleranter Hallo.

- **Updates voor het gebruik van opslagbewaking** -30 juni 2017 wordt gestart, Hallo gebruik opslagbewaking voor het virtuele apparaat serie StorSimple wordt ingetrokken. Dit geldt toohello bewaking grafieken op alle Hallo virtuele matrices met Update 0,4 of lager. Deze update bevat Hallo wijzigingen vereist zijn voor u toocontinue Hallo gebruik van opslaggebruik bewaken in hello Azure-portal. Deze essentiële update vóór 30 juni 2017 installeren met behulp van de bewaking van de functie Hallo toocontinue.


## <a name="issues-fixed-in-hello-update-05"></a>Problemen in Hallo Update 0,5 opgelost

Hallo bevat volgende tabel een samenvatting van problemen in deze release worden opgelost.

| Nee. | Functie | Probleem |
| --- | --- | --- |
| 1 |Back-tolerantie| In Hallo back-ups van eerdere versies werden opnieuw alleen voor bepaalde uitzonderingen. Deze release bevat een fix toomake back-ups toleranter door alle uitzonderingen voor Hallo-back-up opnieuw proberen.|
| 2 |Bewaking| Hallo gebruik opslagbewaking voor het virtuele apparaat serie StorSimple zullen worden afgeschaft vanaf 30 juni 2017. Deze actie heeft impact op Hallo grafieken op Hallo StorSimple Apparaatbeheer service wordt uitgevoerd op virtuele StorSimple-matrices monitoring (1200 model). Deze release bevat updates die Hallo gebruiker toocontinue Hallo gebruik van het gebruik van opslagbewaking op Hallo virtuele matrices na 30 juni 2017 toestaan.|
| 3 |Bestandsserver| In Hallo eerdere releases van een gebruiker kunnen de versleutelde bestanden toohello virtuele matrix per ongeluk kopiëren. Deze release bevat een oplossing waarmee niet kopiëren van versleutelde bestanden toovirtual matrix. Als het apparaat heeft een bestaande versleutelde bestanden voorafgaande toohello bijwerken, blijven back-ups toofail totdat alle Hallo versleutelde bestanden worden verwijderd uit Hallo-systeem. |


## <a name="known-issues-in-hello-update-05"></a>Bekende problemen in Hallo Update 0,5

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
| **8.** |Capaciteit voor shares gebruikt |Mogelijk ziet u verbruik delen wanneer er geen gegevens op Hallo-share zijn. Dit verbruik is omdat de capaciteit voor shares Hallo gebruikt metagegevens bevat. | |
| **9.** |Herstel na noodgevallen |U kunt alleen noodherstel Hallo van een bestand server toohello uitvoeren hetzelfde domein als die van het bronvolume Hallo. Disaster recovery tooa doelapparaat in een ander domein wordt niet ondersteund in deze release. |Dit is geïmplementeerd in een latere release. Voor meer informatie gaat te[Failover en herstel na noodgevallen voor uw virtuele StorSimple-matrix](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |Hallo virtuele StorSimple-apparaten kunnen niet worden beheerd via hello Azure PowerShell in deze release. |Alle Hallo beheer van virtuele apparaten Hallo moet worden uitgevoerd via hello Azure portal en Hallo lokale webgebruikersinterface. |
| **11.** |Wachtwoord wijzigen |Hallo virtuele matrix apparaat console accepteert alleen invoer in de norm en-us indeling toetsenbord. | |
| **12.** |CHAP |CHAP-referenties eenmaal is gemaakt, kunnen niet worden verwijderd. Bovendien als u CHAP-referenties Hallo wijzigt, u moet tootake Hallo volumes offline en breng vervolgens on line voor Hallo wijziging tootake effect. |Dit probleem is verholpen in een latere versie. |
| **13.** |iSCSI-server |Hallo 'Opslagruimte hebt gebruikt' voor een iSCSI-volume weergegeven kan niet verschillen in Hallo Apparaatbeheer StorSimple-service en Hallo iSCSI-host. |Hallo iSCSI-host heeft Hallo bestandssysteem weergave.<br></br>Hallo apparaat ziet toegewezen wanneer Hallo volume op de maximale grootte Hallo is Hallo-blokken. |
| **14.** |Bestandsserver |Als een bestand in een map een alternatieve gegevens stroom (ADS heeft) gekoppeld, is niet Hallo ADVERTENTIES back-up gemaakt of hersteld via herstel na noodgevallen, klonen en herstel Item. | |
| **15.** |Bestandsserver |Symbolische koppelingen worden niet ondersteund. | |
| **16.** |Bestandsserver |Bestanden beveiligd door Windows Encrypting File System (EFS) wanneer gekopieerd of opgeslagen op Hallo virtuele StorSimple-matrix bestand server resultaat in een niet-ondersteunde configuratie.  | |

## <a name="next-step"></a>Volgende stap
[Installeer Update 0,5](storsimple-virtual-array-install-update-05.md) op uw virtuele StorSimple-matrix.

## <a name="references"></a>Verwijzingen
Zoekt u een oudere versie Opmerking? Ga naar:

* [StorSimple virtuele matrix Update 0,4 Release-opmerkingen](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple virtuele matrix Update 0,3 Release-opmerkingen](storsimple-ova-update-03-release-notes.md)
* [StorSimple virtuele matrix Update 0,1-0,2 Release-opmerkingen](storsimple-ova-update-01-release-notes.md)
* [StorSimple virtuele matrix algemene beschikbaarheid Release-opmerkingen](storsimple-ova-pp-release-notes.md)

