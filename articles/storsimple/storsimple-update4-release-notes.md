---
title: Opmerkingen bij de release van de aaaStorSimple 8000 Series Update 4 | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 4.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Opmerkingen bij de release van de StorSimple 8000 Series Update 4

## <a name="overview"></a>Overzicht

Hallo volgende releaseopmerkingen beschrijven Hallo nieuwe functies en StorSimple 8000 Series Update 4 Hallo kritieke open problemen identificeren. Ze bevatten ook een lijst met software-updates voor Hallo StorSimple is opgenomen in deze release. 

Update 4 kan worden toegepast tooany StorSimple-apparaat met Release (GA) of Update 0.1 via Update 3.1. Hallo apparaatversie die is gekoppeld met Update 4 is 6.3.9600.17820.

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.

> [!IMPORTANT]
> * Update 4 heeft device-software, USM firmware, stuurprogramma LSI en firmware, schijf-firmware, Storport en Spaceport, beveiligingsupdates en andere updates OS. Het duurt ongeveer 4 uur tooinstall deze update. Schijf firmware-update is een update verstoren en resulteert in een uitvaltijd voor uw apparaat. Het is raadzaam om toe te passen Update 4 tookeep uw apparaat up-to-date. 
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Wacht een paar dagen en vervolgens zoeken naar updates opnieuw als deze is binnenkort beschikbaar.

## <a name="whats-new-in-update-4"></a>Wat is er nieuw in Update 4

Hallo zijn volgende belangrijke verbeteringen en correcties aangebracht in Update 4.

* **Slimmer geautomatiseerde ruimte vrijmaken algoritmen** – In Update 4 hello geautomatiseerde ruimte vrijmaken algoritmen zijn verbeterde tooadjust Hallo ruimte wordt vrijgemaakt op basis van verwacht Hallo cycli ruimte beschikbaar in de cloud Hallo vrijgemaakt. 

* **Prestatieverbeteringen voor lokaal vastgemaakte volumes** – Update 4 Hallo prestaties van lokaal vastgemaakte volumes in scenario's waarvoor hoge gegevensopname (gegevensgrootte vergelijkbare toovolume) is verbeterd.

* **Heatmap-herstelfuncties** - In Hallo eerdere versies van een noodherstel (DR) Hallo gegevens na is teruggezet vanaf een Hallo-cloud op basis van toegangspatronen Hallo leiden tot een trage prestaties. 

    Een nieuwe functie is geïmplementeerd in Update 4 dat nummers gegevens toocreate een heatmap veelgebruikte wanneer Hallo-apparaat in de voorafgaande tooDR gebruik (meestgebruikte gegevenssegmenten hoge hitte hebben dat kleiner segmenten gebruikt lage hitte hebt). Na DR, StorSimple gebruikt Hallo heatmap tooautomatically terugzetten en rehydrate Hallo gegevens uit Hallo cloud. 

    Alle Hallo Herstelacties zijn nu gebaseerd heatmap herstelt. Voor meer informatie over hoe heatmap tooquery en annuleren op basis van terugzetten en rehydratering taken, gaat u te[Windows PowerShell voor StorSimple cmdlet-verwijzing](https://technet.microsoft.com/library/dn688168.aspx).

* **Diagnostische StorSimple** : Update 4 een StorSimple-diagnostische hulpprogramma wordt uitgebracht tooallow voor het oplossen van eenvoudige en status van toosystem, netwerk, prestaties en hardware-onderdeel oplossen van problemen met betrekking. Dit hulpprogramma wordt uitgevoerd via Hallo Windows PowerShell voor StorSimple. Voor meer informatie gaat te[oplossen met behulp van StorSimple diagnostische hulpprogramma](storsimple-8000-diagnostics.md).

* **Hulpprogramma voor migratie van de StorSimple van gebruikersinterface gebaseerde** -voorafgaande toothis release, migratie van gegevens van de 5000-en 7000-serie vereist Hallo gebruikers tooexecute deel uit van Hallo Migratiewerkstroom met hello Azure PowerShell-interface. In deze release Hallo een eenvoudig te gebruiken StorSimple migratie gebruikersinterface gebaseerde hulpprogramma wordt beschikbaar gesteld voor ondersteuning toofacilitate dezelfde Migratiewerkstroom. Dit hulpprogramma wordt ook de mogelijkheid voor Hallo consolidatie van herstel buckets. 

* **FIPS-gerelateerde wijzigingen** - deze release en hoger, FIPS is standaard ingeschakeld op alle apparaten uit Hallo StorSimple 8000 serie voor beide Hallo Microsoft Azure Government en openbare Azure-cloud-accounts.

* **Wijzigingen doorvoeren** - In deze release bugs gerelateerde tooupdate fouten zijn gecorrigeerd.

* **Waarschuwing voor schijffouten** -een nieuwe waarschuwing voor die gebruiker Hallo van aanstaande schijffouten waarschuwt in deze release is toegevoegd. Als u deze waarschuwing tegenkomt, neem dan contact op met Microsoft Support tooship een vervangende schijf. Voor meer informatie gaat te[hardware waarschuwingen op het StorSimple-apparaat](storsimple-manage-alerts.md#hardware-alerts).

* **Controller vervanging wijzigingen** -een cmdlet waarmee Hallo tooquery Hallo Gebruikersstatus van het proces voor het Hallo-controller vervangen in deze release is toegevoegd. Ga voor meer informatie, toohello [cmdlet tooquery controller Vervangingsstatus](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemen opgelost in Update 4

Hallo bevat volgende tabel een samenvatting van problemen die in Update 4 zijn opgelost.    

| Nee | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Failover |In Hallo oudere versie, na een failover hello, er is een probleem gerelateerd toocleanup waargenomen op de locatie van de klant Hallo. Dit probleem is opgelost in deze release. |Ja |Ja |
| 2 |Lokaal vastgemaakte volumes |In de vorige release hello is er een probleem toorelated volume maken voor lokaal vastgemaakte volumes die tot fouten bij het maken van volume leiden zou. Dit probleem is veroorzaakt met een hoofdmap en opgelost in deze release. |Ja |Nee |
| 3 |Ondersteuningspakket |In de vorige release zijn er problemen gerelateerde tooSupport pakket dat zou leiden tot een uitzondering System.OutOfMemory of andere fouten waardoor een ondersteuning pakket maken is mislukt. Deze fouten worden opgelost in deze release. |Ja |Ja |
| 4 |Bewaking |In de vorige release er een probleem gerelateerd toomonitoring grafieken voor lokaal vastgemaakte volumes waar verbruik is weergegeven in EB. Deze fout is opgelost in deze release. |Ja |Ja |
| 5 |Migratie |In eerdere versie gebruikt zijn er verschillende problemen gerelateerde toohello betrouwbaarheid van de migratie van 5000 7000-serie too8000 reeks apparaten. Deze problemen zijn gericht in deze release. |Ja |Ja |
| 6 |Update |In eerdere versies, als er een update-fout is opgetreden, Hallo domeincontrollers in de herstelmodus vallen zou en daarom Hallo-gebruiker kan niet doorgaan met Hallo update en moet toocontact Microsoft Support. <br> Dit gedrag is gewijzigd in deze release. Als gebruiker Hallo heeft een update mislukt nadat beide domeincontrollers Hallo zijn Hallo uitgevoerd dezelfde versie (Update 4), Hallo domeincontrollers gaan niet in de herstelmodus overgaat. Als Hallo gebruiker deze fout wordt aangetroffen, raden wij aan dat ze een bits wacht en probeer vervolgens Hallo-update. Hallo opnieuw kan slagen. Als Hallo opnieuw mislukt, moeten ze contact met Microsoft Support. |Ja |Ja |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Bekende problemen in Update 4 uit eerdere versies

Er zijn geen nieuwe bekende problemen in Update 4. Voor een lijst met problemen die zijn overgedragen tooUpdate 4 uit vorige versies, gaat u te[opmerkingen bij de release van Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Serial attached SCSI (SAS)-controller en firmware-updates in Update 4

Deze release heeft SAS-controller en LSI stuurprogramma en firmware-updates. Voor meer informatie over hoe tooinstall deze updates, Zie [Update 4 installeren](storsimple-install-update-4.md) op uw StorSimple-apparaat.

## <a name="virtual-device-updates-in-update-4"></a>Virtueel apparaat-updates in Update 4

Deze update kan niet worden toegepast toohello StorSimple Cloud toestel (ook wel bekend als Hallo virtueel apparaat). Nieuwe virtuele apparaten moet toobe gemaakt. 

## <a name="next-step"></a>Volgende stap

Meer informatie over hoe te[Update 4 installeren](storsimple-install-update-4.md) op uw StorSimple-apparaat.

