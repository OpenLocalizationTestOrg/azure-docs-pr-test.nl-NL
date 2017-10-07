---
title: aaaUpdate uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple functie tooinstall reguliere en onderhoud modus updates en hotfixes bijwerken.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Uw StorSimple 8000-serie-apparaat bijwerken
## <a name="overview"></a>Overzicht
Hallo StorSimple updates functies kunt u de tooeasily uw StorSimple-apparaat up-to-date houden. Afhankelijk van het type update hello, kunt u updates toohello apparaat via Hallo klassieke Azure-portal of via Windows PowerShell-interface Hallo toepassen. Deze zelfstudie wordt de update-typen Hallo beschreven en hoe tooinstall hiervan.

U kunt twee soorten apparaatupdates toepassen: 

* Reguliere (of de normale modus) updates
* Onderhoud modus updates

U kunt ook regelmatige updates via de klassieke Azure-portal Hallo of Windows PowerShell; installeren echter, moet u Windows PowerShell tooinstall onderhoud modus updates. 

Elk updatetype wordt afzonderlijk hieronder beschreven.

### <a name="regular-updates"></a>Regelmatig updates
Regelmatig updates zijn ononderbroken updates die kunnen worden geïnstalleerd wanneer het Hallo-apparaat is in de normale modus. Deze updates worden toegepast via Hallo Microsoft Update-website tooeach apparaat controller. 

> [!IMPORTANT]
> Een failover van de domeincontroller kan optreden tijdens het updateproces Hallo. Dit wordt echter niet gewijzigd beschikbaarheid van het systeem of de bewerking.
> 
> 

* Zie voor informatie over hoe tooinstall regelmatige updates via Hallo klassieke Azure-portal, [installeren regelmatig updates via de klassieke Azure-portal Hallo](#install-regular-updates-via-the-azure-classic-portal).
* U kunt ook regelmatige updates via Windows PowerShell voor StorSimple installeren. Zie voor meer informatie [regelmatig updates via Windows PowerShell voor StorSimple installeren](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Onderhoud modus updates
Onderhoud modus updates zijn verstoren updates zoals upgrades van de schijf. Deze updates vereisen Hallo apparaat toobe in onderhoudsmodus geplaatst. Zie voor meer informatie [stap 2: Voer onderhoudsmodus](#step2). U kunt hello Azure classic portal tooinstall onderhoud modus updates niet gebruiken. In plaats daarvan moet u Windows PowerShell voor StorSimple. 

Zie voor informatie over de manier waarop de onderhoudsmodus tooinstall wordt bijgewerkt, [installeren onderhoud modus updates via Windows PowerShell voor StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Onderhoudsmodus updates moet afzonderlijk tooeach domeincontroller toegepast. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Regelmatig updates via Hallo klassieke Azure-portal installeren
U kunt hello Azure classic portal tooapply updates tooyour StorSimple-apparaat gebruiken.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Installeer regelmatig updates via Windows PowerShell voor StorSimple
U kunt ook Windows PowerShell voor StorSimple tooapply regular (normale modus)-updates.

> [!IMPORTANT]
> Hoewel u regelmatig updates met Windows PowerShell voor StorSimple installeren kunt, wordt aangeraden dat u regelmatig updates via Hallo klassieke Azure-portal installeert. Vanaf Update 1, zijn eerste controles uitgevoerd voorafgaande tooinstalling updates van Hallo-portal. Deze controles vooraf wordt hebben voorrang op fouten en zorg ervoor dat een soepeler ervaring. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Onderhoud modus updates via Windows PowerShell voor StorSimple installeren
U Windows PowerShell voor StorSimple tooapply onderhoud modus updates tooyour StorSimple-apparaat gebruiken. Alle i/o-aanvragen zijn in deze modus onderbroken. Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice Hallo zijn ook gestopt. Beide domeincontrollers worden opgestart wanneer u in of uit deze modus. Wanneer u deze modus afsluit, worden alle Hallo-services wordt hervat en moeten in orde. (Dit kan enkele minuten duren.)

Als u tooapply onderhoud modus updates nodig hebt, ontvangt u een waarschuwing via Hallo klassieke Azure-portal of er updates die moeten worden geïnstalleerd. Deze waarschuwing bevat instructies voor het gebruik van Windows PowerShell voor StorSimple tooinstall Hallo-updates. Nadat u uw apparaat bijwerkt, Hallo gebruik dezelfde procedure toochange Hallo apparaat tooRegular modus. Zie voor stapsgewijze instructies [stap 4: afsluiten onderhoudsmodus](#step4).

> [!IMPORTANT]
> * Controleer of beide apparaatcontrollers zijn in orde door Hallo controleren voordat u de onderhoudsmodus invoert, **hardwarestatus** op Hallo **onderhoud** pagina in Hallo klassieke Azure-portal. Hallo-controller is niet in orde, contact op met Microsoft Support voor de volgende stappen Hallo. Ga voor meer informatie tooContact Microsoft Support. 
> * Wanneer u in de onderhoudsmodus bevindt bent, moet u tooapply Hallo update eerst op een domeincontroller en klik vervolgens op Hallo andere domeincontroller.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Stap 1: Verbinding maken met de seriële console toohello<a name="step1">
Eerst gebruik van een toepassing, zoals PuTTY tooaccess Hallo seriële console. Hallo volgende procedure wordt uitgelegd hoe toouse PuTTY tooconnect toohello seriële console.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Stap 2: Geef de onderhoudsmodus<a name="step2">
Nadat u toohello console verbinding maakt, bepalen of er updates tooinstall en onderhoud modus tooinstall Voer ze.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Stap 3: Uw updates installeren<a name="step3">
Vervolgens installeert u de updates.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Stap 4: Afsluiten onderhoudsmodus<a name="step4">
Onderhoudsmodus ten slotte af te sluiten.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Installeren van hotfixes via Windows PowerShell voor StorSimple
In tegenstelling tot de updates voor Microsoft Azure StorSimple zijn-hotfixes geïnstalleerd vanuit een gedeelde map. Net als bij updates, zijn er twee soorten hotfixes: 

* Reguliere hotfixes 
* Onderhoud modus hotfixes  

Hallo volgende procedures wordt uitgelegd hoe toouse Windows PowerShell voor StorSimple tooinstall reguliere en hotfixes voor onderhoud-modus.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Wat gebeurt er tooupdates als u een fabriek voeren opnieuw instellen van Hallo apparaat?
Als een apparaat opnieuw instellen van toofactory instellingen, zijn alle Hallo updates gaan verloren. Nadat de Hallo fabrieksinstellingen apparaat is geregistreerd en geconfigureerd, moet u updates van de toomanually installeren via de klassieke Azure-portal Hallo en/of Windows PowerShell voor StorSimple. Zie voor meer informatie over de fabrieksinstellingen [Hallo apparaat toofactory standaardinstellingen herstellen](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [met Windows PowerShell voor StorSimple tooadminister uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

