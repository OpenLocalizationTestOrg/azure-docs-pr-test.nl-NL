---
title: aaaInstall Update 4 op StorSimple 8000 series apparaat | Microsoft Docs
description: Legt uit hoe tooinstall StorSimple 8000 Series Update 4 op uw StorSimple 8000 serie-apparaat.
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 3507edbde5e6e43b6c450bfea19494d47b5a5ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Update 4 installeren op uw StorSimple-apparaat

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe tooinstall Update 4 op een StorSimple-apparaat met een eerdere softwareversie via Azure portal en via de hotfix-methode Hallo Hallo. Hallo hotfix methode wordt gebruikt wanneer een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van Hallo StorSimple-apparaat en u tooupdate van een versie 1 vóór het bijwerken probeert.

Update 4 bevat device-software, USM firmware LSI stuurprogramma en firmware, Storport en Spaceport, OS beveiligingsupdates en tal van andere updates voor het besturingssysteem.  Hallo-device-software, USM firmware Spaceport, Storport en andere updates OS ononderbroken updates beschikbaar zijn. Hallo ononderbroken of regelmatig updates kunnen worden toegepast via hello Azure-portal of een Hallo hotfix methode. Hallo schijf firmware-updates verstoren updates beschikbaar zijn en kunnen alleen worden toegepast via Hallo hotfix methode met behulp van Windows PowerShell-interface Hallo Hallo-apparaat.

> [!IMPORTANT]
> * Een aantal handmatige en automatische eerste controles uitgevoerd voorafgaande toohello installeren toodetermine Hallo Apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u Hallo-updates van hello Azure-portal toepassen.
> * Het is raadzaam dat u Hallo software en andere regelmatig updates via hello Azure-portal installeert. Gaat toohello Windows PowerShell-interface van Hallo-apparaat (tooinstall updates) alleen als Hallo vóór het bijwerken gateway controle in Hallo-portal mislukt. Afhankelijk van het Hallo-versie die u bijwerkt, Hallo updates kunnen 4 uur duren (of hoger) tooinstall. Hallo onderhoud modus updates moeten ook worden geïnstalleerd via Windows PowerShell-interface Hallo Hallo-apparaat. Als onderhoud modus updates verstoren updates beschikbaar zijn, resulteert dit in een uitvaltijd voor uw apparaat.
> * Zorg ervoor dat u uw apparaat Snapshot Manager versie 4 tooUpdate voorafgaande tooupdating Hallo hebt bijgewerkt als actief hello optionele StorSimple Snapshot Manager.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-portal"></a>Update 4 installeren via hello Azure-portal
Voer Hallo tooupdate stappen te volgen uw apparaat te[Update 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Microsoft haalt aanvullende diagnostische gegevens van het Hallo-apparaat. Als gevolg hiervan als onze teamleden identificeert de apparaten die problemen ondervindt, we betere uitgerust toocollect informatie van Hallo-apparaat en problemen diagnosticeren. 

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update4-via-portal.md)]

Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 4 (6.3.9600.17820)**. Hallo **datum laatst bijgewerkt** moet ook worden gewijzigd.

* U ziet nu dat Hallo onderhoud modus updates beschikbaar zijn (dit bericht blijven mogelijk toobe weergegeven voor up too24 Hallo uur na de installatie van updates). Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo van uw apparaat.

* Hallo onderhoud modus updates te downloaden met behulp van Hallo stappen in [toodownload hotfixes](#to-download-hotfixes) toosearch voor en KB4011837 die wordt geïnstalleerd schijf firmware-updates te downloaden (hello andere updates al is geïnstalleerd door nu). Hallo stappen die worden vermeld in [installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Hallo onderhoud modus updates.

## <a name="install-update-4-as-a-hotfix"></a>Update 4 installeren als een hotfix
Hallo aanbevolen methode tooinstall die update 4, via hello Azure-portal is.

Gebruik deze procedure als u niet Hallo gateway selectievakje bij een poging tooinstall Hallo updates via hello Azure-portal. Hallo controle mislukt als er een gateway tooa niet-DATA 0-netwerkinterface toegewezen en uw apparaat een eerdere tooUpdate voor software-versie 1 wordt uitgevoerd.

Hallo softwareversies die kunnen worden bijgewerkt via Hallo hotfix-methode zijn:

* Update 0.1, 0,2, 0,3
* Update 1, 1.1, 1.2
* 2, 2.1, 2.2 bijwerken
* Update 3, 3.1


Hallo hotfix methode omvat Hallo drie stappen te volgen:

1. Hallo hotfixes downloaden vanaf Microsoft Update-catalogus Hallo.
2. Installeren en controleer of de hotfixes voor Hallo normale modus.
3. Installeren en controleer of Hallo onderhoud modus hotfix.

#### <a name="download-updates-for-your-device"></a>Updates voor uw apparaat downloaden

U moet downloaden en installeren van de volgende Hallo hotfixes in Hallo voorgeschreven volgorde en Hallo voorgestelde mappen:

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 |Software-update |Reguliere <br></br>Niet-verstoren |~ 25 minuten |FirstOrderUpdate|
| 2A. |KB4011841 <br> KB4011842 |LSI stuurprogramma's en firmware-updates <br> USM firmware-update (versie 3.38) |Reguliere <br></br>Niet-verstoren |~ 3 uur <br> (inclusief 2A. + 2B. (+ 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3197873 <br> KB3192392, KB3153704 <br> KB3174644, KB3139914  |OS-beveiligingspakket updates <br> Windows Server 2012 R2 downloaden |Reguliere <br></br>Niet-verstoren |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |OS-updates-pakket <br> Windows Server 2012 R2 downloaden |Reguliere <br></br>Niet-verstoren |- |SecondOrderUpdate|

U moet mogelijk ook tooinstall schijf firmware-updates op alle Hallo-updates weergegeven in de voorgaande tabellen Hallo. U kunt controleren of u schijf firmware-updates door het uitvoeren van Hallo moet Hallo `Get-HcsFirmwareVersion` cmdlet. Als u deze firmwareversies: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, en u geen tooinstall deze updates hoeft.

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd | Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 3. |KB3121899 |Schijf-firmware |Onderhoud <br></br>Verstoren |~ 30 minuten | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Deze procedure moet toobe uitgevoerd slechts één keer tooapply Update 4. U kunt hello Azure portal tooapply daaropvolgende updates.
> * Als het bijwerken van de Update 3 of 3.1, is de totale installatietijd Hallo sluiten too4 uur.
> * Voordat u deze procedure tooapply Hallo bijwerken, zorg ervoor dat beide apparaatcontrollers Hallo online zijn en alle Hallo hardwareonderdelen zijn in orde.

Uitvoeren van Hallo toodownload stappen te volgen en Hallo hotfixes installeren.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Update 4 release](storsimple-update4-release-notes.md).

