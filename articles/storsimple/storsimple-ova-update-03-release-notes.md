---
title: aaaStorSimple virtuele matrix Updates release-opmerkingen | Microsoft Docs
description: Kritieke open beschrijft problemen en oplossingen voor het werken met het virtuele StorSimple-matrix van Hallo Update 0.3.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>StorSimple virtuele matrix Update 0,3 release-opmerkingen
## <a name="overview"></a>Overzicht
Hallo volgende releaseopmerkingen Hallo kritieke open problemen identificeren en Hallo opgeloste problemen voor updates van Microsoft Azure StorSimple virtuele matrix.

Hallo release-opmerkingen worden voortdurend bijgewerkt en wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw virtuele StorSimple-matrix implementeert, zorgvuldig door Hallo gegevens in Hallo release-opmerkingen.

Update 0.3 overeenkomt met de softwareversie toohello **10.0.10288.0**.

> [!NOTE]
> Updates kunnen verstoren, start het apparaat. Als i/o's uitgevoerd worden, wordt het apparaat Hallo uitvaltijd systeem.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Wat is er nieuw in Update 0.3 Hallo
Update 0.3 is voornamelijk een bug fix build. In deze versie, is enkele fouten, wat leidt tot mislukte back-ups in de vorige versie Hallo behandeld.

## <a name="issues-fixed-in-hello-update-03"></a>Problemen in Hallo Update 0.3 opgelost
Hallo bevat volgende tabel een samenvatting van problemen in deze release worden opgelost.

| Nee. | Functie | Probleem |
| --- | --- | --- |
| 1 |Back-ups |Een probleem is gedetecteerd in Hallo eerdere release waar Hallo back-ups toocomplete voor een bestandsshare mislukken. Als dit probleem is opgetreden, mislukken de back-uptaak Hallo en een kritieke waarschuwing is gegenereerd op Hallo StorSimple Manager-service toonotify Hallo gebruiker. Dit probleem niet van invloed op Hallo van gegevens op Hallo shares of toegang tot toohello gegevens. Hallo hoofdoorzaak is geïdentificeerd en opgelost in deze release. <br></br> Hallo-oplossing is niet van toepassing met terugwerkende kracht tooshares die al dit probleem ziet. Klanten die dit probleem ziet moeten eerst Update 0.3 toe te passen en neem contact op met Microsoft Support tooperform een volledige back-toofix Hallo systeemprobleem. In plaats van het contact opneemt met Microsoft Support, terugzetten klanten ook nieuwe share tooa vanuit een goede back-up voor Hallo van invloed op een shares. |
| 2 |iSCSI |Een probleem is gedetecteerd in Hallo eerdere release waar Hallo volumes verdwijnen bij het kopiëren van gegevens tooa volume op Hallo virtuele StorSimple-matrix. Dit probleem is verholpen in deze release. <br></br> Hallo-oplossingen te laten treden alleen op nieuwe volumes gemaakt. Hallo-oplossingen zijn niet van toepassing met terugwerkende kracht toovolumes die al dit probleem ziet. Klanten wordt aangeraden toobring Hallo van invloed op een volumes online via Hallo klassieke Azure-portal, een back-up voor deze volumes en zet deze volumes toonew volumes. |

## <a name="known-issues-in-hello-update-03"></a>Bekende problemen in Hallo Update 0.3
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

## <a name="next-step"></a>Volgende stap
[Installeer Update 0.3](storsimple-ova-install-update-01.md) op uw virtuele StorSimple-matrix.

## <a name="references"></a>Verwijzingen
Zoekt u een oudere versie Opmerking? Ga naar: 

* [StorSimple virtuele matrix Update 0,1-0,2 Release-opmerkingen](storsimple-ova-update-01-release-notes.md)
* [StorSimple virtuele matrix algemene beschikbaarheid Release-opmerkingen](storsimple-ova-pp-release-notes.md)

