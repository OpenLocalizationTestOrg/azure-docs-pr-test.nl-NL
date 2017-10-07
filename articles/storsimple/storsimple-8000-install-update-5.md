---
title: aaaInstall Update 5 op StorSimple 8000 series apparaat | Microsoft Docs
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Update 5 installeren op uw StorSimple-apparaat

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe tooinstall Update 5 op een StorSimple-apparaat met een eerdere softwareversie via Azure portal en via de hotfix-methode Hallo Hallo. Hallo hotfix methode wordt gebruikt wanneer een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van Hallo StorSimple-apparaat en u tooupdate van een versie 1 vóór het bijwerken probeert.

Update 5 omvat software van apparaten, Storport en Spaceport, OS beveiligingsupdates en updates voor het besturingssysteem en schijf firmware-updates.  Hallo-device-software, Spaceport Storport, beveiliging en andere updates OS ononderbroken updates beschikbaar zijn. Hallo ononderbroken of regelmatig updates kunnen worden toegepast via hello Azure-portal of een Hallo hotfix methode. Hallo schijf firmware-updates verstoren updates beschikbaar zijn en worden toegepast wanneer Hallo-apparaat in de onderhoudsmodus via Hallo hotfix methode met behulp van Windows PowerShell-interface Hallo Hallo-apparaat.

> [!IMPORTANT]
> * Een aantal handmatige en automatische eerste controles uitgevoerd voorafgaande toohello installeren toodetermine Hallo Apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u Hallo-updates van hello Azure-portal toepassen.
> * Het is raadzaam dat u Hallo software en andere regelmatig updates via hello Azure-portal installeert. Gaat toohello Windows PowerShell-interface van Hallo-apparaat (tooinstall updates) alleen als Hallo vóór het bijwerken gateway controle in Hallo-portal mislukt. Afhankelijk van het Hallo-versie die u bijwerkt, Hallo updates kunnen 4 uur duren (of hoger) tooinstall. Hallo onderhoud modus updates moeten worden geïnstalleerd via Windows PowerShell-interface Hallo Hallo-apparaat. Als u onderhoud modus updates verstoren updates beschikbaar zijn, wordt deze leiden tot een uitvaltijd voor uw apparaat.
> * Zorg ervoor dat u uw apparaat Snapshot Manager versie 5 tooUpdate voorafgaande tooupdating Hallo hebt bijgewerkt als actief hello optionele StorSimple Snapshot Manager.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Update 5 via hello Azure-portal installeren
Voer Hallo tooupdate stappen te volgen uw apparaat te[Update 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft haalt aanvullende diagnostische gegevens van het Hallo-apparaat. Als gevolg hiervan als onze teamleden identificeert de apparaten die problemen ondervindt, we betere uitgerust toocollect informatie van Hallo-apparaat en problemen diagnosticeren.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 5 (6.3.9600.17845)**. Hallo **datum laatst bijgewerkt** moet worden gewijzigd.

* U ziet nu dat Hallo onderhoud modus updates beschikbaar zijn (dit bericht blijven mogelijk toobe weergegeven voor up too24 Hallo uur na de installatie van updates). Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo van uw apparaat.

* Hallo onderhoud modus updates te downloaden met behulp van Hallo stappen in [toodownload hotfixes](#to-download-hotfixes) toosearch voor en KB4011837 die wordt geïnstalleerd schijf firmware-updates te downloaden (hello andere updates al is geïnstalleerd door nu). Hallo stappen die worden vermeld in [installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Hallo onderhoud modus updates.

## <a name="install-update-5-as-a-hotfix"></a>Update 5 als een hotfix installeren


Hallo softwareversies die kunnen worden bijgewerkt via Hallo hotfix-methode zijn:

* Update 0.1, 0,2, 0,3
* Update 1, 1.1, 1.2
* 2, 2.1, 2.2 bijwerken
* Update 3, 3.1
* Update 4

> [!NOTE] 
> Hallo aanbevolen methode tooinstall die update 5 via hello Azure-portal is. Gebruik deze procedure als u niet Hallo gateway selectievakje bij een poging tooinstall Hallo updates via hello Azure-portal. Hallo controle mislukt wanneer u een gateway tooa niet-DATA 0-netwerkinterface toegewezen en uw apparaat een softwareversie ouder is dan Update 1 wordt uitgevoerd.

Hallo hotfix methode omvat Hallo drie stappen te volgen:

1. Hallo hotfixes downloaden vanaf Microsoft Update-catalogus Hallo.
2. Installeren en controleer of de hotfixes voor Hallo normale modus.
3. Installeren en controleer of Hallo onderhoud modus hotfix.

#### <a name="download-updates-for-your-device"></a>Updates voor uw apparaat downloaden

U moet downloaden en installeren van de volgende Hallo hotfixes in Hallo voorgeschreven volgorde en Hallo voorgestelde mappen:

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Software-update<br> Download beide _HcsSfotwareUpdate.exe_ en _CisMSDAgent.exe_ |Reguliere <br></br>Niet-verstoren |~ 25 minuten |FirstOrderUpdate|

Als u bijwerkt vanaf een apparaat met Update 4, hoeft u alleen tooinstall Hallo OS cumulatieve updates als tweede volgorde updates.

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |OS cumulatieve updates pakket <br> Versie van Windows Server 2012 R2 downloaden |Reguliere <br></br>Niet-verstoren |- |SecondOrderUpdate|

Als installeren vanaf een apparaat met Update 3 of ouder, installeert u Hallo volgen bovendien toohello cumulatieve updates.

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |LSI stuurprogramma's en firmware-updates <br> USM firmware-update (versie 3.38) |Reguliere <br></br>Niet-verstoren |~ 3 uur <br> (inclusief 2A. + 2B. (+ 2 C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |OS-beveiligingspakket updates <br> Versie van Windows Server 2012 R2 downloaden |Reguliere <br></br>Niet-verstoren |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |OS-updates-pakket <br> Versie van Windows Server 2012 R2 downloaden |Reguliere <br></br>Niet-verstoren |- |SecondOrderUpdate|


U moet mogelijk ook tooinstall schijf firmware-updates op alle Hallo-updates weergegeven in de voorgaande tabellen Hallo. U kunt controleren of u schijf firmware-updates door het uitvoeren van Hallo moet Hallo `Get-HcsFirmwareVersion` cmdlet. Als u deze firmwareversies: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, en u geen tooinstall deze updates hoeft.

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd | Installeren in map|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Schijf-firmware |Onderhoud <br></br>Verstoren |~ 30 minuten | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Als het bijwerken van de Update 4, is de totale installatietijd Hallo sluiten too4 uur.
> * Voordat u deze procedure tooapply Hallo bijwerken, zorg ervoor dat beide apparaatcontrollers Hallo online zijn en alle Hallo hardwareonderdelen zijn in orde.

Uitvoeren van Hallo toodownload stappen te volgen en Hallo hotfixes installeren.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Update 5 release](storsimple-update5-release-notes.md).

