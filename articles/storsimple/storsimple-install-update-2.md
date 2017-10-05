---
title: Update 2 op uw StorSimple-apparaat installeert | Microsoft Docs
description: Legt uit hoe StorSimple 8000 Series Update 2 op uw StorSimple 8000 series apparaat installeert.
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
ms.openlocfilehash: e788439608b7122f2bca6b99b832baa5258e472d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Installeer Update 2 op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe u Update 2 installeren op een StorSimple-apparaat waarop een eerdere softwareversie wordt uitgevoerd via de klassieke Azure portal. De zelfstudie bevat ook informatie over de stappen die nodig zijn voor de update als een gateway is geconfigureerd op een andere netwerkinterface dan DATA 0 van de StorSimple-apparaat en u probeert bij te werken vanaf een versie 1 vóór het bijwerken.

Update 2 bevat apparaat software-updates en updates voor stuurprogramma's LSI schijf firmware-updates. De apparaatsoftware en updates LSI ononderbroken updates beschikbaar zijn en kunnen worden toegepast via de klassieke Azure portal. De schijf firmware-updates verstoren updates beschikbaar zijn en kunnen alleen worden toegepast via de Windows PowerShell-interface van het apparaat.

> [!IMPORTANT]
> * Er kan geen Update 2 onmiddellijk omdat we een gefaseerde implementatie van de updates. Zoeken naar updates in een paar dagen opnieuw als deze Update is binnenkort beschikbaar.
> * Een aantal handmatige en automatische eerste controles worden uitgevoerd voordat de installatie om te bepalen van de apparaatstatus in termen van hardware-staat en de netwerkverbinding. Deze controles vooraf worden alleen uitgevoerd als u de updates via de klassieke Azure portal toepassen.
> * Het is raadzaam dat u de software en stuurprogramma's via de klassieke Azure portal installeert. U moet alleen gaat u naar de Windows PowerShell-interface van het apparaat (om updates te installeren) als de controle van de gateway vóór het bijwerken is mislukt in de portal. De updates kunnen 4-7 uur duren te installeren (met inbegrip van de Windows-Updates). De updates van de modus onderhoud moeten worden geïnstalleerd via de Windows PowerShell-interface van het apparaat. Als onderhoud modus updates verstoren updates beschikbaar zijn, resulteert dit in een uitvaltijd voor uw apparaat.
> * Als de optionele StorSimple Snapshot Manager wordt uitgevoerd, zorg ervoor dat u uw Snapshot Manager-versie hebt bijgewerkt naar Update 2 vóór het bijwerken van het apparaat.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-the-azure-classic-portal"></a>Update 2 installeren via de klassieke Azure portal
Voer de volgende stappen uit voor het bijwerken van uw apparaat om te [Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Update 2 kan Microsoft voor het ophalen van aanvullende diagnostische gegevens van het apparaat. Als gevolg hiervan als onze teamleden identificeert de apparaten die problemen ondervindt, zijn wij beter ingericht voor het verzamelen van informatie van het apparaat en problemen diagnosticeren. Update 2 accepteren, kunnen wij deze proactieve ondersteuning.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Controleren of uw apparaat wordt uitgevoerd **StorSimple 8000 Series Update 2 (6.3.9600.17673)**. De **datum laatst bijgewerkt** moet ook worden gewijzigd. U ziet ook dat onderhoud modus updates beschikbaar zijn (dit bericht kan nog wel weergegeven tot 24 uur nadat u de updates hebt geïnstalleerd).
   
   Onderhoud modus updates zijn verstoren updates die leiden tot uitvaltijd apparaat en kunnen alleen worden toegepast via de Windows PowerShell-interface van uw apparaat. In sommige gevallen wanneer u Update 1.2 uitvoert uw schijf firmware mogelijk al up-to-date zijn, in dat geval moet u geen onderhoud modus updates installeren.
2. De modus onderhoud updates downloaden met behulp van de stappen in [downloaden hotfixes](#to-download-hotfixes) zoeken naar en downloaden van KB3121899, welke schijf firmware-updates zijn geïnstalleerd (de andere updates al is geïnstalleerd door nu).
3. Volg de stappen die worden vermeld in [installeren en testen van onderhoud modus hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) updates voor het installeren van de onderhoudsmodus.

## <a name="install-update-2-as-a-hotfix"></a>Update 2 installeren als een hotfix
Gebruik deze procedure als u de controle van de gateway niet bij het installeren van de updates via de klassieke Azure portal. De controle mislukt als er een gateway die is toegewezen aan een niet-DATA 0-netwerkinterface en uw apparaat een softwareversie dan Update 1 wordt uitgevoerd.

De softwareversies die kunnen worden bijgewerkt met de hotfix-methode zijn Update 0.1 Update 0.2, en Update 0.3, Update 1, Update 1.1 en 1.2 van de Update. De hotfix-methode omvat de volgende drie stappen:

* De hotfixes downloaden vanaf Microsoft Update-catalogus.
* Installeren en controleer of de hotfixes normale modus.
* Installeren en controleer of de hotfix onderhoud-modus.

U moet voor het installeren van Update 2 als een hotfix, downloaden en installeren van de volgende hotfixes:

| Volgorde | KB | Beschrijving | Updatetype |
| --- | --- | --- | --- |
| 1 |KB3121901 |Software-update |Reguliere |
| 2 |KB3121900 |LSI stuurprogramma |Reguliere |
| 3 |KB3080728 |Storport-oplossing </br> Windows Server 2012 R2 |Reguliere |
| 4 |KB3090322 |Spaceport oplossing </br> Windows Server 2012 R2 |Reguliere |
| 5 |KB3121899 |Schijf-firmware |Onderhoud |

> [!IMPORTANT]
> * Als uw apparaat kan Release (GA)-versie wordt uitgevoerd, contact op met [Microsoft Support](storsimple-contact-microsoft-support.md) om u te helpen met de update.
> * Deze procedure moet slechts één keer worden uitgevoerd om de Update 2 toepassen. U kunt de klassieke Azure portal gebruiken daaropvolgende updates toe te passen.
> * Elke hotfix-installatie kan ongeveer 20 minuten duren om te voltooien. Totale installatietijd is bijna 2 uur.
> * Voordat u deze procedure de update toe te passen, zorg ervoor dat beide apparaatcontrollers online zijn en alle hardwareonderdelen zijn in orde.
> 
> 

Voer de volgende stappen voor deze update als een hotfix toepast.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over de [release van Update 2](storsimple-update2-release-notes.md).

