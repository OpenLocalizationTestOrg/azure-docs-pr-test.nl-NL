---
title: aaaInstall Update 1.2 op uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooinstall StorSimple 8000 Series Update 1.2 op uw StorSimple 8000 serie-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>1.2 Update installeren op uw StorSimple 8000 series apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe tooinstall 1.2 op een StorSimple-apparaat waarop een eerdere tooUpdate voor software-versie 1 wordt bijgewerkt. Hallo-zelfstudie vallen ook Hallo extra stappen vereist voor de update hello, wanneer een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van Hallo StorSimple-apparaat.

Update 1.2 bevat de software-apparaatupdates, LSI-updates voor stuurprogramma's en schijf firmware-updates. Hallo-software en updates voor stuurprogramma's LSI ononderbroken updates beschikbaar zijn en kunnen worden toegepast via Hallo klassieke Azure-portal. Hallo schijf firmware-updates verstoren updates beschikbaar zijn en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo Hallo-apparaat.

Afhankelijk van welke versie van het apparaat wordt uitgevoerd, kunt u bepalen als Update 1.2 wordt toegepast. U kunt de softwareversie Hallo van uw apparaat controleren door te navigeren toohello **snelle weergave** gedeelte van uw apparaat **Dashboard**.

</br>

| Als softwareversie... | Wat gebeurt er in Hallo-portal? |
| --- | --- |
| Versie - GA |Als u een releaseversie (GA) uitvoert, zijn deze update niet van toepassing. Neem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate uw apparaat. |
| Update 0.1 |Portal geldt Update 1.2. |
| Update 0.2 |Portal geldt Update 1.2. |
| Update 0.3 |Portal geldt Update 1.2. |
| Update 1 |Deze update is niet beschikbaar. |
| 1.1 bijwerken |Deze update is niet beschikbaar. |

</br>

> [!IMPORTANT]
> * Er kan geen Update 1.2 onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Zoeken naar updates in een paar dagen opnieuw als deze Update is binnenkort beschikbaar.
> * Deze update bevat een set van de eerste controles van handmatige en automatische toodetermine Hallo Apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u Hallo-updates van Hallo klassieke Azure-portal toepassen.
> * U wordt aangeraden dat u Hallo software installeren en updates voor stuurprogramma's via Hallo klassieke Azure-portal. Gaat toohello Windows PowerShell-interface van Hallo-apparaat (tooinstall updates) alleen als Hallo vóór het bijwerken gateway controle in Hallo-portal mislukt. Hallo updates duurt 5 tot 10 uur tooinstall (inclusief Updates voor Windows hello). Hallo onderhoud modus updates moeten worden geïnstalleerd via Windows PowerShell-interface Hallo Hallo-apparaat. Als onderhoud modus updates verstoren updates beschikbaar zijn, resulteert dit in een uitvaltijd voor uw apparaat.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>1.2 Update installeren via de klassieke Azure-portal Hallo
Voer Hallo tooupdate stappen te volgen uw apparaat te[Update 1.2](storsimple-update1-release-notes.md). Gebruik deze procedure alleen als u een gateway is ingesteld op DATA 0-netwerkinterface op uw apparaat hebt.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**. Hallo **datum laatst bijgewerkt** moet ook worden gewijzigd. U ziet ook dat onderhoud modus updates beschikbaar zijn (dit bericht blijven mogelijk toobe weergegeven voor up too24 Hallo uur na de installatie van updates).
   
   Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via Windows PowerShell-interface Hallo van uw apparaat.
   
   ![Onderhoudspagina](./media/storsimple-install-update-1/InstallUpdate12_10M.png "pagina onderhoud")
2. Hallo onderhoud modus updates te downloaden met behulp van Hallo stappen in [toodownload hotfixes](#to-download-hotfixes) toosearch voor en KB3063416 die wordt geïnstalleerd schijf firmware-updates te downloaden (hello andere updates al is geïnstalleerd door nu).
3. Hallo stappen die worden vermeld in [installeren en controleer of de onderhoudsmodus modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall Hallo onderhoud modus updates.
4. In Hallo klassieke Azure-portal, gaat u toohello **onderhoud** pagina en klik onder aan de pagina Hallo Hallo op **Updates zoeken** toocheck voor alle Windows-Updates en klik vervolgens op **Updates installeren** . U bent klaar nadat alle Hallo updates worden geïnstalleerd.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>1.2 Update installeren op een apparaat waarop een gateway is geconfigureerd voor een niet-DATA 0-netwerkinterface
U moet deze procedure alleen gebruiken als u niet Hallo gateway selectievakje bij een poging tooinstall Hallo updates via Hallo klassieke Azure-portal. Hallo controle mislukt als er een gateway tooa niet-DATA 0-netwerkinterface toegewezen en uw apparaat een eerdere tooUpdate voor software-versie 1 wordt uitgevoerd. Als uw apparaat geen een gateway voor een niet-DATA 0-netwerkinterface heeft, kunt u uw apparaat rechtstreeks vanuit de klassieke Azure-portal Hallo bijwerken. Zie [installeert u update 1.2 via de klassieke Azure-portal Hallo](#install-update-1.2-via-the-azure-classic-portal).

Hallo softwareversies die kunnen worden bijgewerkt met deze methode zijn Update 0.1, Update 0.2 en Update 0.3.

> [!IMPORTANT]
> * Als uw apparaat kan Release (GA)-versie wordt uitgevoerd, contact op met [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist u Hello bijwerken.
> * Deze procedure moet toobe uitgevoerd slechts één keer tooapply Update 1.2. U kunt hello Azure classic portal tooapply daaropvolgende updates.
> 
> 

Als uw apparaat 1 software vóór het bijwerken wordt uitgevoerd en er een gateway instellen voor een netwerkinterface dan DATA 0, kunt u Update 1.2 toepassen in de volgende twee manieren Hallo:

* **Optie 1**: Hallo update downloaden en deze toe te passen met behulp van Hallo `Start-HcsHotfix` cmdlet in Windows PowerShell-interface Hallo Hallo-apparaat. Dit is de aanbevolen methode Hallo. **Gebruik deze methode tooapply Update 1.2 niet als uw apparaat Update 1.0 of 1.1 van de Update wordt uitgevoerd.**
* **Optie 2**: Verwijder Hallo gatewayconfiguratie en installatie Hallo update rechtstreeks vanuit de klassieke Azure-portal Hallo.

Voor elk van deze gedetailleerde instructies vindt u in Hallo uit te voeren.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Optie 1: Gebruik Windows PowerShell voor StorSimple tooapply Update 1.2 als een hotfix
U moet deze procedure alleen gebruiken als u Update 0.1, 0,2, 0,3 en als uw gateway-controle is mislukt bij het tooinstall updates van Hallo klassieke Azure-portal uitvoert. Als u versie (GA) software uitvoert, neemt u [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate uw apparaat.

tooinstall Update 1.2 als een hotfix, moet u downloaden en installeren van Hallo hotfixes te volgen:

| Volgorde | KB | Beschrijving | Updatetype |
| --- | --- | --- | --- |
| 1 |KB3063418 |Software-update |Reguliere |
| 2 |KB3043005 |LSI SAS-controller update |Reguliere |
| 3 |KB3063416 |Schijf-firmware |Onderhoud |

Voordat u deze procedure tooapply Hallo-updates, zorg ervoor dat:

* Beide apparaatcontrollers zijn online.

Volgende stappen tooapply Update 1.2 Hallo uitvoeren. **Hallo-updates kunnen enige tijd duren ongeveer 2 uur toocomplete (ongeveer 30 minuten voor software, 30 minuten voor stuurprogramma, 45 minuten voor schijf-firmware).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Optie 2: Hello Azure classic portal tooapply Update 1.2 gebruiken na het verwijderen van de configuratie van de gateway Hallo
Deze procedure geldt alleen tooStorSimple-apparaten met een eerdere tooUpdate voor software-versie 1 en een gateway die is ingesteld op een netwerkinterface dan DATA 0 hebben. U moet tooclear Hallo gateway instelling voorafgaande tooapplying Hallo update.

Hallo update duurt enkele uren toocomplete. Als uw hosts zich in verschillende subnetten, kan verwijderen van de gatewayconfiguratie Hallo op Hallo iSCSI-interfaces leiden tot uitvaltijd. Het is raadzaam dat u DATA 0 voor iSCSI-verkeer tooreduce Hallo uitvaltijd configureren.

Hallo te volgen stappen toodisable Hallo netwerkinterface met Hallo gateway uitvoeren en vervolgens Hallo update toepassen.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Update 1.2 release](storsimple-update1-release-notes.md).

