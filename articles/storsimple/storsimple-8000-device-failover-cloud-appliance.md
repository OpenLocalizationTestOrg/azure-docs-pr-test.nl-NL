---
title: aaaStorSimple failover disaster recovery tooa StorSimple Cloud toestel | Microsoft Docs
description: Meer informatie over hoe toofail via uw fysieke apparaat tooa van StorSimple 8000 series toestel cloud.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Tooyour StorSimple Cloud toestel failover

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt Hallo stappen vereist toofail via een fysiek apparaat tooa voor StorSimple 8000 serie StorSimple Cloud toestel beschreven als er een noodgeval. StorSimple gebruikt Hallo apparaat failover-functie toomigrate gegevens vanaf een fysiek Bronapparaat in Hallo datacenter tooa cloud toestel in Azure wordt uitgevoerd. Hallo richtlijnen in deze zelfstudie geldt tooStorSimple 8000 series fysieke apparaten en apparaten van cloud met versies van de software Update 3 en hoger.

toolearn meer informatie over failover-apparaat en hoe deze gebruikt toorecover na een noodgeval te gaan[Failover en herstel na noodgevallen voor StorSimple 8000 series apparaten](storsimple-8000-device-failover-disaster-recovery.md).

toofail via een fysiek apparaat tooanother fysieke StorSimple-apparaat, gaat u te[failover fysieke StorSimple-apparaat tooa](storsimple-8000-device-failover-physical-device.md). toofail via een tooitself apparaat gaat te[failover toohello dezelfde fysieke StorSimple-apparaat](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Vereisten

- Zorg ervoor dat u Hallo aandachtspunten voor failover-apparaat hebt bekeken. Voor meer informatie gaat te[algemene overwegingen voor het apparaat failover](storsimple-8000-device-failover-disaster-recovery.md).

- Een StorSimple Cloud toestel gemaakt en geconfigureerd voordat u deze procedure uitvoert, moet u hebben. Als uitgevoerd bijwerken van versie 3 of hoger, kunt u overwegen een toestel 8020 cloud voor Hallo Noodherstel. Hallo 8020 model heeft van 64 TB en Premium-opslag gebruikt. Voor meer informatie gaat te[implementeren en beheren van een StorSimple-apparaat met Cloud](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Stappen toofail via tooa cloud toestel

Volgende stappen toorestore Hallo apparaat tooa doel StorSimple Cloud toestel Hallo uitvoeren.

1.  Controleer of deze Hallo volumecontainer toofail via gewenste cloudmomentopnamen is gekoppeld. Voor meer informatie gaat te[gebruik StorSimple Apparaatbeheer service toocreate back-ups](storsimple-8000-manage-backup-policies-u2.md).
2. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**. In Hallo **apparaten** blade, Ga toohello lijst met apparaten die verbonden zijn met uw service.
    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Selecteer en klik op het bronapparaat. Hallo Bronapparaat heeft Hallo volumecontainers die u wilt dat toofail via. Ga te**instellingen > Volumecontainers**.

    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Selecteer een volumecontainer dat u toofail via tooanother apparaat dat wilt. Klik op Hallo volume container toodisplay Hallo lijst van volumes in deze container. Selecteer een volume, klik met de rechtermuisknop en klik op **Offline nemen** tootake Hallo volume offline.

    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Herhaal dit proces voor alle Hallo volumes in de volumecontainer Hallo.

     ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. De vorige stap herhalen Hallo voor alle volumecontainers Hallo gewenst toofail via tooanother apparaat.

7. Ga terug toohello **apparaten** blade. Hallo opdrachtbalk en klik op **failover**.

    ![Klik op mislukken via](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. In Hallo **failover** blade Hallo volgende stappen uit te voeren:
   
    1. Klik op **bron**. Hallo volume containers toofail via selecteren. **Alleen Hallo volumecontainers met momentopnamen van de gekoppelde cloud en offline volumes worden weergegeven.**
        ![Bron selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Klik op **doel**. Selecteer een doel-cloud-toestel Hallo vervolgkeuzelijst met beschikbare apparaten. **Alleen Hallo-apparaten waarvoor voldoende capaciteit bron tooaccommodate volumecontainers worden in Hallo lijst weergegeven.**

        ![Doel selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Controleer Hallo failover-instellingen onder **samenvatting** en selecteer Hallo selectievakje die aangeeft of Hallo volumes in de geselecteerde volumecontainers offline zijn. 

        ![Failover-instellingen controleren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Er wordt een failover-taak gemaakt. toomonitor hello failover taak, klikt u op Hallo taakmeldingen.

    ![Monitor voor failover-taak](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Nadat het Hallo-failover is voltooid, gaat u terug toohello **apparaten** blade.

    1. Selecteer Hallo-apparaat dat is gebruikt als doel Hallo voor Hallo failover.

       ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Klik op **Volumecontainers**. Alle Hallo-volumecontainers, samen met de Hallo volumes van de oude apparaat hello, moeten worden vermeld.

       Als het Hallo-volumecontainer waarvoor u failover is lokaal vastgemaakt volumes, zijn deze volumes als gelaagde volumes kan niet via. Lokaal vastgemaakte volumes worden niet ondersteund op een StorSimple-apparaat met Cloud.

       ![Doel-volumecontainers weergeven](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Volgende stappen

* Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).

* Voor informatie over hoe toouse StorSimple Apparaatbeheer Hallo service, gaat u te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

