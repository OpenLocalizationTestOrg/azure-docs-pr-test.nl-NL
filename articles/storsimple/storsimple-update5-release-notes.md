---
title: Opmerkingen bij de release van de aaaStorSimple 8000 Series Update 5 | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 5.
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Opmerkingen bij de release van de StorSimple 8000 Series Update 5

## <a name="overview"></a>Overzicht

Hallo volgende releaseopmerkingen beschrijven Hallo nieuwe functies en StorSimple 8000 Series Update 5 Hallo kritieke open problemen identificeren. Ze bevatten ook een lijst met software-updates voor Hallo StorSimple is opgenomen in deze release.

Update 5 kan worden toegepast tooany StorSimple-apparaat met Update 0.1 tot en met 4 van de Update. Hallo apparaatversie die is gekoppeld met Update 5 is 6.3.9600.17845.

Bekijk Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.

> [!IMPORTANT]
> * Update 5 heeft device-software, firmware van de schijf, OS-beveiliging en andere updates voor het besturingssysteem. Het duurt ongeveer 4 uur tooinstall deze update. Schijf firmware-update is een update verstoren en resulteert in een uitvaltijd voor uw apparaat. Het is raadzaam om toe te passen Update 5 tookeep uw apparaat up-to-date.
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Wacht een paar dagen, en vervolgens zoeken naar updates opnieuw als deze updates worden binnenkort beschikbaar.

## <a name="whats-new-in-update-5"></a>Wat is er nieuw in Update 5

Hallo zijn volgende belangrijke verbeteringen en correcties aangebracht in Update 5.

* **Gebruik van Azure Active Directory (AAD) tooauthenticate met Apparaatbeheer StorSimple-service** – van Update 5 en hoger, Azure Active Directory is gebruikte tooauthenticate met Hallo Apparaatbeheer StorSimple-service. Hallo oude verificatiemechanisme wordt afgeschaft per December 2017. Alle gebruikers van Hallo moeten Hallo nieuwe verificatie URL's opnemen in hun firewallregels. Voor meer informatie gaat te[verificatie URL's die worden vermeld in de netwerkvereisten voor uw StorSimple-apparaat Hallo](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Als het Hallo-URL voor webverificatie niet is opgenomen in de firewallregels hello, zien gebruikers Hallo een kritieke waarschuwing voor die hun StorSimple-apparaat kan niet worden geverifieerd met Hallo-service. Als gebruikers Hallo deze waarschuwing wordt weergegeven, moeten ze tooinclude Hallo nieuwe URL voor webverificatie. Voor meer informatie gaat te[StorSimple networking waarschuwingen](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nieuwe versie van StorSimple Snapshot Manager** -een nieuwe versie van StorSimple Snapshot Manager met Update 5 is uitgebracht. U wordt aangeraden dat u toothis versie bijwerken. Deze versie is compatibel met alle Hallo StorSimple-apparaten met Update 3 of hoger. Voor meer informatie gaat te[StorSimple Snapshot Manager implementeren](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problemen opgelost met Update 5

Hallo bevat volgende tabel een samenvatting van problemen die in Update 5 zijn opgelost.

| Nee | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Windows PowerShell op afstand |In de vorige release hello, zou een gebruiker een foutbericht ontvangt bij tooestablish probeert een verbinding met extern toohello StorSimple Cloud toestel via Windows PowerShell. Dit probleem is veroorzaakt met een hoofdmap en opgelost in deze release. |Nee |Ja |
| 2 |Bandbreedte-sjablonen |In eerdere versie is er een probleem met de bandbreedte-sjablonen dat heeft geresulteerd in lagere bandbreedte dan welk apparaat Hallo is geconfigureerd voor. Dit probleem wordt opgelost in deze release. |Ja |Ja |
| 3 |Failover |In de vorige release wanneer een apparaat met een groot aantal volumes is mislukt via tooanother apparaat met Update 4 mislukken Hallo proces wanneer u probeert tooapply Hallo access control-records. Dit probleem is opgelost in deze release. |Ja |Ja |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Bekende problemen in Update 5 uit eerdere versies

Er zijn geen nieuwe bekende problemen in Update 5. Voor een lijst met problemen die zijn overgedragen tooUpdate 5 uit vorige versies, gaat u te[opmerkingen bij de release van Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Serial attached SCSI (SAS)-controller en firmware-updates in Update 5

Deze release heeft SAS-controller en LSI stuurprogramma en firmware-updates. Voor meer informatie over hoe tooinstall deze updates, Zie [installeren Update 5](storsimple-8000-install-update-5.md) op uw StorSimple-apparaat.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>StorSimple Cloud toestel-updates in de Update 5

Deze update kan niet worden toegepast toohello StorSimple Cloud toestel (ook wel bekend als Hallo virtueel apparaat). Nieuwe cloud toestellen moeten toobe gemaakt met behulp van Hallo Update 5-installatiekopie. Voor meer informatie over een apparaat van de Cloud StorSimple toocreate te gaan[implementeren en beheren van een StorSimple-apparaat met Cloud](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Volgende stap

Meer informatie over hoe te[installeren Update 5](storsimple-8000-install-update-5.md) op uw StorSimple-apparaat.

