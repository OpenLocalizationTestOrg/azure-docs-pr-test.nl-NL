---
title: aaaInstall Update 3 op uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooinstall StorSimple 8000 Series Update 3 op uw StorSimple 8000 serie-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>Update 3 op uw StorSimple 8000 series apparaat installeert

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe tooinstall Update 3 op een StorSimple-apparaat met een eerdere softwareversie via Hallo klassieke Azure portal en via Hallo hotfix-methode. Hallo hotfix methode wordt gebruikt wanneer een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van Hallo StorSimple-apparaat en u tooupdate van een versie 1 vóór het bijwerken probeert.

Update 3 omvat apparaatsoftware, LSI stuurprogramma en firmware, Storport en Spaceport updates. Als het bijwerken van de Update 2 of een eerdere versie, wordt u ook vereist tooapply iSCSI, WMI, en in bepaalde gevallen schijf firmware-updates. Hallo device-software, WMI iSCSI-, LSI stuurprogramma, Spaceport en Storport oplossingen ononderbroken updates beschikbaar zijn en kunnen worden toegepast via Hallo klassieke Azure-portal. Hallo schijf firmware-updates verstoren updates beschikbaar zijn en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo Hallo-apparaat. 

> [!IMPORTANT]
> * Een aantal handmatige en automatische eerste controles uitgevoerd voorafgaande toohello installeren toodetermine Hallo Apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u Hallo-updates van Hallo klassieke Azure-portal toepassen.
> * U wordt aangeraden dat u Hallo software installeren en updates voor stuurprogramma's via Hallo klassieke Azure-portal. Gaat toohello Windows PowerShell-interface van Hallo-apparaat (tooinstall updates) alleen als Hallo vóór het bijwerken gateway controle in Hallo-portal mislukt. Afhankelijk van het Hallo-versie die u bijwerkt, kunnen Hallo updates tooinstall 1.5 2.5 uren duren. Hallo onderhoud modus updates moeten worden geïnstalleerd via Windows PowerShell-interface Hallo Hallo-apparaat. Als onderhoud modus updates verstoren updates beschikbaar zijn, resulteert dit in een uitvaltijd voor uw apparaat.
> * Zorg ervoor dat u uw apparaat Snapshot Manager versie tooUpdate 2 voorafgaande tooupdating Hallo hebt bijgewerkt als actief hello optionele StorSimple Snapshot Manager.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Update 3 installeren via de klassieke Azure-portal Hallo
Voer Hallo tooupdate stappen te volgen uw apparaat te[Update 3](storsimple-update3-release-notes.md).

> [!NOTE]
> Als u bij het toepassen van Update 2 of hoger (inclusief Update 2.1), is Microsoft kunnen toopull aanvullende diagnostische gegevens van Hallo-apparaat. Als gevolg hiervan als onze teamleden identificeert de apparaten die problemen ondervindt, we betere uitgerust toocollect informatie van Hallo-apparaat en problemen diagnosticeren. Accepteert Update 2 of hoger, kunnen we tooprovide deze proactieve ondersteuning.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 3 (6.3.9600.17759)**. Hallo **datum laatst bijgewerkt** moet ook worden gewijzigd. 
   - Als u een eerdere tooUpdate van versie 2 bijwerkt, ook ziet u dat Hallo onderhoud modus updates beschikbaar zijn (dit bericht blijven mogelijk toobe weergegeven voor up too24 Hallo uur na de installatie van updates).
     Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo van uw apparaat. In sommige gevallen wanneer u Update 1.2 uitvoert, de firmware van de schijf is mogelijk al up-to-date, in welk geval hoeft u niet tooinstall eventuele onderhoudsmodus updates.
   - Als u bijwerken van de Update 2 of hoger, het apparaat worden nu recente. U kunt de volgende stap Hallo overslaan.

Hallo onderhoud modus updates te downloaden met behulp van Hallo stappen in [toodownload hotfixes](#to-download-hotfixes) toosearch voor en KB3121899 die wordt geïnstalleerd schijf firmware-updates te downloaden (hello andere updates al is geïnstalleerd door nu). Hallo stappen die worden vermeld in [installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Hallo onderhoud modus updates. 

## <a name="install-update-3-as-a-hotfix"></a>Update 3 installeren als een hotfix
Gebruik deze procedure als u niet Hallo gateway selectievakje bij een poging tooinstall Hallo updates via Hallo klassieke Azure-portal. Hallo controle mislukt als er een gateway tooa niet-DATA 0-netwerkinterface toegewezen en uw apparaat een eerdere tooUpdate voor software-versie 1 wordt uitgevoerd.

Hallo softwareversies die kunnen worden bijgewerkt via Hallo hotfix-methode zijn:

* Update 0.1, 0,2, 0,3
* Update 1, 1.1, 1.2
* 2, 2.1, 2.2 bijwerken 

> [!IMPORTANT]
> * Als uw apparaat kan Release (GA)-versie wordt uitgevoerd, contact op met [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist u Hello bijwerken.
> 
> 

Hallo hotfix methode omvat Hallo drie stappen te volgen:

1. Hallo hotfixes downloaden vanaf Microsoft Update-catalogus Hallo.
2. Installeren en controleer of de hotfixes voor Hallo normale modus.
3. Installeren en controleer of de Hallo onderhoud modus hotfix (alleen bij het bijwerken van 2 software vóór het bijwerken).

#### <a name="download-updates-for-your-device"></a>Updates voor uw apparaat downloaden
**Als uw apparaat wordt uitgevoerd in de Update 2.1 of 2.2**, u moet downloaden en installeren van hotfixes in Hallo voorgeschreven volgorde na Hallo:

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Software-update &#42; |Reguliere <br></br>Niet-verstoren |~ 45 minuten |
| 2. |KB3186859 |LSI stuurprogramma's en -firmware |Reguliere <br></br>Niet-verstoren |~ 20 minuten |
| 3. |KB3121261 |Storport en Spaceport oplossing </br> Windows Server 2012 R2 |Reguliere <br></br>Niet-verstoren |~ 20 minuten |

&#42;  *Opmerking die Hallo software-update bestaat uit twee binaire bestanden: apparaat software-update vooraf worden gegaan door `all-hcsmdssoftwareupdate` en Cis Hallo en vooraf worden gegaan door Mds agent `all-cismdsagentupdatebundle`. Hallo apparaat software-update moet worden geïnstalleerd voordat de Hallo configuratie-items en Mds Agent. U moet ook opnieuw starten de actieve controller Hallo via Hallo `Restart-HcsController` cmdlet na het toepassen van Hallo configuratie-items en Mds-agent bijwerken (en vóór het toepassen van updates resterende Hallo).* 

**Als uw apparaat Update 0.1, 0,2, 0,3, 1.0, 1.1, 1.2 of 2.0 wordt uitgevoerd**, u moet downloaden en installeren van hotfixes in toevoeging toohello software LSI stuurprogramma na Hallo en firmware-updates (weergegeven in Hallo voorafgaand aan de tabel), in volgorde voorgeschreven Hallo:

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |iSCSI-pakket |Reguliere <br></br>Niet-verstoren |~ 20 minuten |
| 5. |KB3103616 |WMI-pakket |Reguliere <br></br>Niet-verstoren |~ 12 minuten |

<br></br>

**Als uw apparaat wordt uitgevoerd op versies 0,2, 0,3, 1.0, 1.1 en 1.2**, moet u ook tooinstall schijf firmware-updates op alle Hallo-updates weergegeven in de voorgaande tabellen Hallo. U kunt controleren of u schijf firmware-updates door het uitvoeren van Hallo moet Hallo `Get-HcsFirmwareVersion` cmdlet. Als u deze firmwareversies: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, en u geen tooinstall deze updates hoeft.

| Volgorde | KB | Beschrijving | Updatetype | Installatietijd |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Schijf-firmware |Onderhoud <br></br>Verstoren |~ 30 minuten |

<br></br>

> [!IMPORTANT]
> * Deze procedure moet toobe uitgevoerd slechts één keer tooapply Update 3. U kunt hello Azure classic portal tooapply daaropvolgende updates.
> * Als het bijwerken van de Update 2.2, is de totale installatietijd Hallo sluiten too1.1 uur.
> * Voordat u deze procedure tooapply Hallo bijwerken, zorg ervoor dat beide apparaatcontrollers Hallo online zijn en alle Hallo hardwareonderdelen zijn in orde.
> 
> 

Uitvoeren van Hallo toodownload stappen te volgen en Hallo hotfixes installeren.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [release van Update 3](storsimple-update3-release-notes.md).

