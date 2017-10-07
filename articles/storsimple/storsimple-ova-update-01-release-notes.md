---
title: aaaStorSimple virtuele matrix Updates release-opmerkingen | Microsoft Docs
description: Beschrijft kritieke open problemen en oplossingen voor Hallo virtuele StorSimple-matrix met Update 0.2 en 0,1.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Opmerkingen bij de release van de StorSimple virtuele matrix Update 0.2 en 0,1
## <a name="overview"></a>Overzicht
Hallo volgende releaseopmerkingen Hallo kritieke open problemen identificeren en Hallo opgeloste problemen voor updates van Microsoft Azure StorSimple virtuele matrix. (Microsoft Azure StorSimple virtuele matrix is ook bekend als Hallo lokale virtueel StorSimple-apparaat of Hallo virtuele StorSimple-apparaat.) 

Hallo release-opmerkingen worden voortdurend bijgewerkt en wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw virtuele StorSimple-apparaat implementeert, zorgvuldig door Hallo gegevens in Hallo release-opmerkingen.

Update 0.2 overeenkomt met de softwareversie toohello **10.0.10280.0**; Update 0.1 is versie **10.0.10279.0**. de volgende secties voor Hallo Hallo wijzigingen voor elke update vermeld. 

> [!NOTE]
> Updates kunnen verstoren, wordt uw apparaat opnieuw opstarten. Als i/o's uitgevoerd worden, wordt Hallo apparaat uitvaltijd in rekening gebracht.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemen in Hallo Update 0.2 opgelost
Update 0.2 bevat alle wijzigingen van de Update 0.1 in toevoeging toohello oplossing wordt beschreven in de volgende tabel Hallo:

| Functie | Probleem |
| --- | --- |
| Updates |In de laatste versie Hallo zijn niet updates automatisch gedetecteerd in de klassieke Azure-portal Hallo zodat u toouse Hallo lokale Webgebruikersinterface tooinstall updates had. Dit probleem is opgelost in deze release. U kunt na de installatie van Update 0.2 toekomstige updates met behulp van Hallo klassieke Azure-portal installeren. |

## <a name="whats-new-in-hello-update-01"></a>Wat is er nieuw in Update 0.1 Hallo
Update 0.1 Hallo volgende bevat oplossingen voor problemen en verbeteringen. 

* **Verbeterde tolerantie voor cloud uitval**: deze release heeft verschillende oplossingen voor problemen rond herstel na noodgevallen, back-up, herstel en lagen in Hallo-gebeurtenis van een onderbreking van de cloud-connectiviteit. 
* **Verbeterde prestaties terugzetten**: deze versie bevat oplossingen voor problemen die hebben Hallo voltooiingstijd van hersteltaken Hallo aanzienlijk verminderen.
* **Ruimte vrijmaken optimalisatie geautomatiseerde**: wanneer gegevens worden verwijderd op dun ingerichte volumes, hello ongebruikte opslagruimte blokken moeten toobe vrijgemaakt. Deze release heeft verbeterde Hallo ruimte vrijmaken proces uit Hallo cloud waardoor Hallo ongebruikte ruimte worden beschikbare sneller als vergeleken toohello vorige versies.
* **Installatiekopieën van het nieuwe virtuele schijf**: nieuwe VHD en VHDX VMDK zijn nu beschikbaar via Hallo klassieke Azure-portal. U kunt deze installatiekopieën tooprovision nieuwe Update 0.1 apparaten downloaden.
* **Hallo nauwkeurigheid van de status van de taken in het Hallo-portal verbeteren**: In Hallo eerdere versie van software, rapportage in de portal Hallo taakstatus is niet gedetailleerde. Dit probleem wordt opgelost in deze release.
* **Domain join-ervaring**: bugfixes verwante toodomain toevoegen en het hernoemen van Hallo-apparaat.

## <a name="issues-fixed-in-hello-update-01"></a>Problemen in Hallo Update 0.1 opgelost
Hallo bevat volgende tabel een samenvatting van problemen in deze release worden opgelost.

| Nee. | Functie | Probleem |
| --- | --- | --- |
| 1 |VMDK |In sommige versies van VMware is Hallo besturingssysteemschijf gezien als sparse die waarschuwingen veroorzaken en normale bewerkingen verstoren. Dit is opgelost in deze release. |
| 2 |iSCSI-server |Hallo-gebruiker is in de laatste versie Hallo vereist toospecify een gateway voor elke ingeschakelde netwerkinterface van uw virtuele StorSimple-apparaat. Dit gedrag is gewijzigd in deze release zodat hello gebruiker tooconfigure ten minste één gateway voor alle netwerkinterfaces van Hallo ingeschakeld. |
| 3 |Ondersteuningspakket |In eerdere versie van software Hallo, ondersteuning voor verzameling van pakket mislukt bij het Hallo pakket grootten zijn groter dan 1 GB. Dit probleem is opgelost in deze release. |
| 4 |Toegang tot de cloud |In de laatste versie Hallo als hello virtuele StorSimple-matrix is geen verbinding met het netwerk- en opnieuw is opgestart, heeft hello lokale UI problemen met de netwerkverbinding. Dit probleem is opgelost in deze release. |
| 5 |Bewaking van grafieken |Hallo cloud capaciteit gebruik grafieken weergegeven in de vorige release hello, na een failover apparaat onjuiste waarden in de klassieke Azure-portal Hallo. Dit probleem wordt opgelost in de huidige release Hallo. |

## <a name="known-issues-in-hello-update-01"></a>Bekende problemen in Hallo Update 0.1
Hallo volgende tabel bevat een samenvatting van bekende problemen voor het virtuele StorSimple-matrix Hallo en omvat Hallo problemen release genoteerd uit Hallo vorige versies. **Hallo problemen release vermeld in deze release zijn gemarkeerd met een sterretje. Bijna alle Hallo problemen in deze lijst hebt overgedragen Hallo GA-release van het virtuele StorSimple-matrix.**

| Nee. | Functie | Probleem | Tijdelijke oplossing/opmerkingen |
| --- | --- | --- | --- |
| **1.** |Updates |Hallo virtuele apparaten gemaakt in de preview-versie Hallo niet bijgewerkte tooa ondersteund algemene beschikbaarheid versie. |Deze virtuele apparaten, moeten voor algemene beschikbaarheid release met een disaster recovery (DR) werkstroom Hallo failover worden uitgevoerd. |
| **2.** |Ingerichte gegevensschijf |Eenmaal hebt u een gegevensschijf van een bepaalde opgegeven omvang ingericht en Hallo bijbehorende virtuele StorSimple-apparaat hebt gemaakt, moet u niet uitbreiden of verkleinen Hallo gegevensschijf. Poging toodo dus leidt tot verlies van alle Hallo-gegevens in de lokale lagen Hallo Hallo-apparaat. | |
| **3.** |Groepsbeleid |Wanneer een apparaat lid van een domein is, kan een Groepsbeleid toepassen nadelig beïnvloeden Hallo apparaat bewerking. |Zorg ervoor dat uw virtuele matrix in de eigen organisatie-eenheid (OE) voor Active Directory en geen groepsbeleidsobjecten (GPO) toegepaste tooit zijn. |
| **4.** |Lokale webgebruikersinterface |Als verbeterde beveiligingsfuncties zijn ingeschakeld in Internet Explorer (IE ESC), is het mogelijk dat sommige gebruikersinterface lokale webpagina's zoals probleemoplossing of onderhoud niet correct werkt. Knoppen op deze pagina's ook werkt mogelijk niet. |Verbeterde beveiligingsfuncties in Internet Explorer uitschakelen. |
| **5.** |Lokale webgebruikersinterface |In een Hyper-V virtuele machine, Hallo netwerkinterfaces in Hallo web-gebruikersinterface worden weergegeven als 10 Gbps-interfaces. |Dit gedrag is een weerspiegeling van Hyper-V. 10 Gbps voor virtuele netwerkadapters worden altijd weergegeven in Hyper-V. |
| **6.** |Gelaagde volumes of shares |Vergrendeling voor toepassingen die met Hallo StorSimple gelaagde volumes werken bereik in bytes wordt niet ondersteund. Als byte bereik vergrendeling is ingeschakeld, werkt StorSimple lagen niet. |Aanbevolen maatregelen zijn onder andere: <br></br>Bereik aan bytes is vergrendeld in uw toepassingslogica uitschakelen.<br></br>Kies tooput gegevens voor deze toepassing in lokaal vastgemaakte volumes tegenstelling tot tootiered volumes.<br></br>*Hoewel*: als met behulp van lokaal volumes vastgemaakte en byte bereik vergrendeling is ingeschakeld, u zich Hallo lokaal vastgemaakt volume kunt online voordat Hallo herstellen voltooid is. In dergelijke gevallen als een herstelbewerking uitgevoerd wordt, moet klikt u wachten Hallo terugzetten toocomplete. |
| **7.** |Gelaagde shares |Werken met grote bestanden kan leiden tot een trage laag. |Als u werkt met grote bestanden, wordt u aangeraden dat Hallo grootste bestand kleiner is dan 3% van de grootte van de bestandsshare Hallo. |
| **8.** |Capaciteit voor shares gebruikt |Mogelijk ziet u verbruik op Hallo afwezigheid van alle gegevens op Hallo share delen. Dit is omdat Hallo gebruikt capaciteit voor shares metagegevens bevat. | |
| **9.** |Herstel na noodgevallen |U kunt alleen noodherstel Hallo van een bestand server toohello uitvoeren hetzelfde domein als die van het bronvolume Hallo. Disaster recovery tooa doelapparaat in een ander domein wordt niet ondersteund in deze release. |Dit wordt geïmplementeerd in een latere versie. |
| **10.** |Azure PowerShell |Hallo virtuele StorSimple-apparaten kunnen niet worden beheerd via hello Azure PowerShell in deze release. |Alle Hallo beheer van virtuele apparaten Hallo moet worden gedaan door middel van Hallo klassieke Azure-portal en Hallo lokale webgebruikersinterface. |
| **11.** |Wachtwoord wijzigen |Hallo virtuele matrix apparaat console accepteert alleen invoer in de indeling en-US. | |
| **12.** |CHAP |CHAP-referenties eenmaal is gemaakt, kunnen niet worden verwijderd. Bovendien als u CHAP-referenties Hallo wijzigt, u moet tootake Hallo volumes offline en brengt ze online voor Hallo wijziging tootake effect. |Deze wordt opgelost in een latere versie. |
| **13.** |iSCSI-server |Hallo 'Opslagruimte hebt gebruikt' voor een iSCSI-volume weergegeven kan niet verschillen in Hallo StorSimple Manager-service en Hallo iSCSI-host. |Hallo iSCSI-host heeft Hallo bestandssysteem weergave.<br></br>Hallo apparaat ziet toegewezen wanneer Hallo volume op de maximale grootte Hallo is Hallo-blokken. |
| **14.** |File server * |Als een bestand in een map een alternatieve gegevens stroom (ADS heeft) gekoppeld, is niet Hallo ADVERTENTIES back-up gemaakt of hersteld via herstel na noodgevallen, klonen en herstel Item. | |

## <a name="next-step"></a>Volgende stap
[Updates installeren](storsimple-ova-install-update-01.md) op uw virtuele StorSimple-matrix.

