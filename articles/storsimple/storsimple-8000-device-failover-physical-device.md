---
title: aaaStorSimple failover disaster recovery tooa StorSimple 8000 series fysiek apparaat | Microsoft Docs
description: Meer informatie over hoe toofail via uw StorSimple 8000 series fysiek apparaat tooanother fysieke apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Failover tooa StorSimple 8000 series fysieke apparaat

## <a name="overview"></a>Overzicht

Als er een ramp, beschrijft deze zelfstudie Hallo stappen vereist toofail via een StorSimple 8000 series fysiek apparaat tooanother fysieke StorSimple-apparaat. Hallo failover-functie toomigrate apparaatgegevens vanaf een fysiek Bronapparaat StorSimple gebruikt in Hallo datacenter tooanother fysieke apparaat. Hallo richtlijnen in deze zelfstudie geldt tooStorSimple 8000 series fysieke apparaten met versies van de software Update 3 en hoger.

toolearn meer informatie over failover-apparaat en hoe deze gebruikt toorecover na een noodgeval te gaan[Failover en herstel na noodgevallen voor StorSimple 8000 series apparaten](storsimple-8000-device-failover-disaster-recovery.md).

toofail via een StorSimple fysiek apparaat tooa StorSimple Cloud toestel, gaat u te[tooa StorSimple Cloud toestel failover](storsimple-8000-device-failover-cloud-appliance.md). toofail via een tooitself fysieke apparaat te gaan[failover toohello dezelfde fysieke StorSimple-apparaat](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Vereisten

- Zorg ervoor dat u Hallo aandachtspunten voor failover-apparaat hebt bekeken. Voor meer informatie gaat te[algemene overwegingen voor het apparaat failover](storsimple-8000-device-failover-disaster-recovery.md).

- U moet een StorSimple 8000 series fysiek apparaat geïmplementeerd in Hallo datacenter hebben. Hallo-apparaat moet uitvoeren, Update 3 of hoger, software. Voor meer informatie gaat te[uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Stappen toofail via tooa fysieke apparaat

Volgende stappen toorestore Hallo uw apparaat tooa fysieke doelapparaat uitvoeren.

1. Controleer of deze Hallo volumecontainer toofail via gewenste cloudmomentopnamen is gekoppeld. Voor meer informatie gaat te[gebruik StorSimple Apparaatbeheer service toocreate back-ups](storsimple-8000-manage-backup-policies-u2.md).
2. Ga tooyour StorSimple-Apparaatbeheer en klik vervolgens op **apparaten**. In Hallo **apparaten** blade, Ga toohello lijst met apparaten die verbonden zijn met uw service.
    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Selecteer en klik op het bronapparaat. Hallo Bronapparaat heeft Hallo volumecontainers die u wilt dat toofail via. Ga te**instellingen > Volumecontainers**.
4. Selecteer een volumecontainer dat u toofail via tooanother apparaat dat wilt. Klik op Hallo volume container toodisplay Hallo lijst van volumes in deze container. Selecteer een volume, klik met de rechtermuisknop en klik op **Offline nemen** tootake Hallo volume offline. Herhaal dit proces voor alle Hallo volumes in de volumecontainer Hallo.
5. De vorige stap herhalen Hallo voor alle volumecontainers Hallo gewenst toofail via tooanother apparaat.
6. Ga terug toohello **apparaten** blade. Hallo opdrachtbalk en klik op **failover**.
    ![Klik op mislukken via](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. In Hallo **failover** blade Hallo volgende stappen uit te voeren:
   
   1. Klik op **bron**. Hallo volumecontainers met volumes die zijn gekoppeld aan cloudmomentopnamen worden weergegeven. Alleen Hallo containers weergegeven, komen in aanmerking voor failover. Selecteer in de lijst van de Hallo met volumecontainers, Hallo volumecontainers toofail via gewenst. **Alleen Hallo volumecontainers met momentopnamen van de gekoppelde cloud en offline volumes worden weergegeven.**

       ![Bron selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Klik op **doel**. Voor Hallo volumecontainers in Hallo vorige stap hebt geselecteerd, selecteert u een doelapparaat van Hallo vervolgkeuzelijst met beschikbare apparaten. Alleen Hallo-apparaten waarvoor voldoende capaciteit bron tooaccommodate volumecontainers worden in Hallo lijst weergegeven.

        ![Doel selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Controleer ten slotte alle Hallo failover-instellingen onder **samenvatting**. Nadat u de instellingen Hallo hebt doorgenomen, selecteer Hallo selectievakje die aangeeft of Hallo volumes in de geselecteerde volumecontainers offline zijn. Klik op **OK**.

       ![Failover-instellingen controleren](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple wordt een failover-taak gemaakt. Klik op Hallo taak melding toomonitor Hallo failover-taak via Hallo **taken** blade.

    Als Hallo volumecontainer waarvoor u failover lokale volumes heeft, vervolgens ziet u het herstellen van de afzonderlijke taken voor alle lokale volumes (en niet voor gelaagde volumes) in Hallo-container. Deze taken herstelpunten geruime toocomplete tijd kan duren. Is het waarschijnlijk dat Hallo failover-taak mogelijk eerder voltooid. Deze volumes hebben lokale garanties alleen nadat Hallo hersteltaken voltooid zijn.

    ![Monitor voor failover-taak](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Nadat het Hallo-failover is voltooid, gaat u toohello **apparaten** blade.
   
   1. Selecteer Hallo-apparaat dat is gebruikt voor het doelapparaat Hallo voor Hallo failover-proces.

       ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Ga toohello **Volumecontainers** blade. Alle Hallo-volumecontainers, samen met de Hallo volumes van de oude apparaat hello, moeten worden vermeld.

       ![Doel-volumecontainers weergeven](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Volgende stappen

* Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).
* Voor informatie over hoe toouse StorSimple Apparaatbeheer Hallo service, gaat u te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

