---
title: aaaInstall Update 2 op uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooinstall StorSimple 8000 Series Update 2 op uw StorSimple 8000 serie-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Installeer Update 2 op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe tooinstall Update 2 op een StorSimple-apparaat met een eerdere softwareversie via Hallo klassieke Azure-portal. Hallo-zelfstudie vallen ook Hallo stappen Hallo update vereist wanneer een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van Hallo StorSimple-apparaat en u tooupdate van een versie 1 vóór het bijwerken probeert.

Update 2 bevat apparaat software-updates en updates voor stuurprogramma's LSI schijf firmware-updates. Hallo-device-software en updates van LSI ononderbroken updates beschikbaar zijn en kunnen worden toegepast via Hallo klassieke Azure-portal. Hallo schijf firmware-updates verstoren updates beschikbaar zijn en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo Hallo-apparaat.

> [!IMPORTANT]
> * Er kan geen Update 2 onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Zoeken naar updates in een paar dagen opnieuw als deze Update is binnenkort beschikbaar.
> * Een aantal handmatige en automatische eerste controles uitgevoerd voorafgaande toohello installeren toodetermine Hallo Apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u Hallo-updates van Hallo klassieke Azure-portal toepassen.
> * U wordt aangeraden dat u Hallo software installeren en updates voor stuurprogramma's via Hallo klassieke Azure-portal. Gaat toohello Windows PowerShell-interface van Hallo-apparaat (tooinstall updates) alleen als Hallo vóór het bijwerken gateway controle in Hallo-portal mislukt. Hallo updates duurt 4 tot en met 7 uur tooinstall (inclusief Updates voor Windows hello). Hallo onderhoud modus updates moeten worden geïnstalleerd via Windows PowerShell-interface Hallo Hallo-apparaat. Als onderhoud modus updates verstoren updates beschikbaar zijn, resulteert dit in een uitvaltijd voor uw apparaat.
> * Zorg ervoor dat u uw apparaat Snapshot Manager versie tooUpdate 2 voorafgaande tooupdating Hallo hebt bijgewerkt als actief hello optionele StorSimple Snapshot Manager.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Update 2 installeren via de klassieke Azure-portal Hallo
Voer Hallo tooupdate stappen te volgen uw apparaat te[Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Update 2 zorgt ervoor dat Microsoft toopull aanvullende diagnostische gegevens van het Hallo-apparaat. Als gevolg hiervan als onze teamleden identificeert de apparaten die problemen ondervindt, we betere uitgerust toocollect informatie van Hallo-apparaat en problemen diagnosticeren. Update 2 accepteert, kunnen we tooprovide deze proactieve ondersteuning.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 2 (6.3.9600.17673)**. Hallo **datum laatst bijgewerkt** moet ook worden gewijzigd. U ziet ook dat onderhoud modus updates beschikbaar zijn (dit bericht blijven mogelijk toobe weergegeven voor up too24 Hallo uur na de installatie van updates).
   
   Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo van uw apparaat. In sommige gevallen wanneer u Update 1.2 uitvoert, de firmware van de schijf is mogelijk al up-to-date, in welk geval hoeft u niet tooinstall eventuele onderhoudsmodus updates.
2. Hallo onderhoud modus updates te downloaden met behulp van Hallo stappen in [toodownload hotfixes](#to-download-hotfixes) toosearch voor en KB3121899 die wordt geïnstalleerd schijf firmware-updates te downloaden (hello andere updates al is geïnstalleerd door nu).
3. Hallo stappen die worden vermeld in [installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Hallo onderhoud modus updates.

## <a name="install-update-2-as-a-hotfix"></a>Update 2 installeren als een hotfix
Gebruik deze procedure als u niet Hallo gateway selectievakje bij een poging tooinstall Hallo updates via Hallo klassieke Azure-portal. Hallo controle mislukt als er een gateway tooa niet-DATA 0-netwerkinterface toegewezen en uw apparaat een eerdere tooUpdate voor software-versie 1 wordt uitgevoerd.

Hallo softwareversies die kunnen worden bijgewerkt via Hallo hotfix-methode zijn Update 0.1 Update 0.2, en Update 0.3, Update 1, Update 1.1 en 1.2 van de Update. Hallo hotfix methode omvat Hallo drie stappen te volgen:

* Hallo hotfixes downloaden vanaf Microsoft Update-catalogus Hallo.
* Installeren en controleer of de hotfixes voor Hallo normale modus.
* Installeren en controleer of Hallo onderhoud modus hotfix.

Update 2 als een hotfix tooinstall, moet u downloaden en installeren van Hallo hotfixes te volgen:

| Volgorde | KB | Beschrijving | Updatetype |
| --- | --- | --- | --- |
| 1 |KB3121901 |Software-update |Reguliere |
| 2 |KB3121900 |LSI stuurprogramma |Reguliere |
| 3 |KB3080728 |Storport-oplossing </br> Windows Server 2012 R2 |Reguliere |
| 4 |KB3090322 |Spaceport oplossing </br> Windows Server 2012 R2 |Reguliere |
| 5 |KB3121899 |Schijf-firmware |Onderhoud |

> [!IMPORTANT]
> * Als uw apparaat kan Release (GA)-versie wordt uitgevoerd, contact op met [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist u Hello bijwerken.
> * Deze procedure moet toobe uitgevoerd slechts één keer tooapply Update 2. U kunt hello Azure classic portal tooapply daaropvolgende updates.
> * De installatie van elke hotfix kan toocomplete ongeveer 20 minuten duren. Totale installatietijd is sluiten too2 uur.
> * Voordat u deze procedure tooapply Hallo bijwerken, zorg ervoor dat beide apparaatcontrollers online zijn en alle Hallo hardwareonderdelen zijn in orde.
> 
> 

Hallo stappen tooapply na deze update hebt uitgevoerd als een hotfix.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [release van Update 2](storsimple-update2-release-notes.md).

