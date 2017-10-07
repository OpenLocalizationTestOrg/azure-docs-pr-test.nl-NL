---
title: aaaStorSimple virtuele matrix Update 0,6 release-opmerkingen | Microsoft Docs
description: Kritieke open beschrijft problemen en oplossingen voor het werken met het virtuele StorSimple-matrix van Hallo 0,6 bijwerken.
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
ms.date: 05/24/2017
ms.author: alkohli
ms.openlocfilehash: 7b573457dc07ce41e95d49d66ccc174045f31a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-06-release-notes"></a>StorSimple virtuele matrix Update 0,6 release-opmerkingen

## <a name="overview"></a>Overzicht

Hallo volgende releaseopmerkingen Hallo kritieke open problemen identificeren en Hallo opgeloste problemen voor updates van Microsoft Azure StorSimple virtuele matrix.

Hallo release-opmerkingen worden voortdurend bijgewerkt en wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw virtuele StorSimple-matrix implementeert, zorgvuldig door Hallo gegevens in Hallo release-opmerkingen.

Update 0,6 overeenkomt met de softwareversie toohello **10.0.10293.0**.

> [!IMPORTANT]
> - Updates kunnen verstoren, start het apparaat. Als i/o's uitgevoerd worden, wordt het apparaat Hallo uitvaltijd systeem. Voor gedetailleerde instructies voor het hoe tooapply Hallo update gaat te[installeert u Update 0,6](storsimple-virtual-array-install-update-06.md).
>
> - Het is raadzaam dat u 0,6 installeert onmiddellijk omdat het bevat kritieke beveiligingsproblemen.


## <a name="whats-new-in-hello-update-06"></a>Wat is er nieuw in Update 0,6 Hallo
Update 0,6 is een essentiële update en onmiddellijk moet worden geïmplementeerd. Deze update bevat Hallo oplossingen te volgen: 

- **Windows-beveiliging corrigeert** -deze release is **kritieke beveiligingsproblemen Windows**. Bekijk Hallo beveiligingsupdates voor meer informatie over beveiligingsproblemen hello te volgen en bijbehorende oplossingen Hallo:
    - [December 2016 beveiliging alleen kwaliteit Update voor Windows 8.1 en WindowsServer 2012 R2](https://support.microsoft.com/help/3205400/december-2016-security-only-quality-update-for-windows-8.1-and-windows-server-2012-r2)
    - [Maart 2017 beveiliging alleen kwaliteit Update voor Windows 8.1 en WindowsServer 2012 R2](https://support.microsoft.com/help/4012213/march-2017-security-only-quality-update-for-windows-8-1-and-windows-server-2012-r23)
    - [9 mei 2017: KB4019213 (beveiliging alleen-lezen-update)](https://support.microsoft.com/help/4019213/windows-8-update-kb4019213)

- **Herstellen van de oplossing** -In eerdere versies is een fout die voorkomen Hallo herstel worden voltooid dat. Deze fout is verholpen in deze release.


## <a name="issues-fixed-in-hello-update-06"></a>Problemen in Hallo Update 0,6 opgelost

Hallo bevat volgende tabel een samenvatting van problemen in deze release worden opgelost.

| Nee. | Functie | Probleem |
| --- | --- | --- |
| 1 |Beveiliging| Deze release bevat essentiële updates voor Windows-beveiliging. Het is raadzaam dat u deze update onmiddellijk te installeren.|
| 2 |Herstellen| Tijdens een terugzetbewerking is er een zeldzame situatie die voorkomen de hersteltaak Hallo voltooien dat. Hallo bug fix lost deze race condition.|


## <a name="known-issues-in-hello-update-06"></a>Bekende problemen in Hallo Update 0,6

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
| **17.** |Updates |Als u fout ziet code: 2359302 (hex 0x240006) bij het tooinstall een hotfix door middel van lokale UI Hallo en dit betekent dat deze hotfix Hallo is al geïnstalleerd op uw apparaat.   | |

## <a name="next-step"></a>Volgende stap
[Installeer Update 0,6](storsimple-virtual-array-install-update-06.md) op uw virtuele StorSimple-matrix.

## <a name="references"></a>Verwijzingen
Zoekt u een oudere versie Opmerking? Ga naar:

* [StorSimple virtuele matrix Update 0,5 Release-opmerkingen](storsimple-virtual-array-update-05-release-notes.md)
* [StorSimple virtuele matrix Update 0,4 Release-opmerkingen](storsimple-virtual-array-update-04-release-notes.md)
* [StorSimple virtuele matrix Update 0,3 Release-opmerkingen](storsimple-ova-update-03-release-notes.md)
* [StorSimple virtuele matrix Update 0,1-0,2 Release-opmerkingen](storsimple-ova-update-01-release-notes.md)
* [StorSimple virtuele matrix algemene beschikbaarheid Release-opmerkingen](storsimple-ova-pp-release-notes.md)

