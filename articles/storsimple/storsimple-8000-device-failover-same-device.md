---
title: aaaStorSimple failover, herstel na noodgevallen voor apparaten 8000 serie | Microsoft Docs
description: Meer informatie over hoe toofail via uw StorSimple-apparaat toohello hetzelfde apparaat.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Uw StorSimple-apparaat fysiek apparaat toosame failover

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt Hallo stappen vereist toofail via een StorSimple 8000 series fysiek apparaat tooitself beschreven als er een noodgeval. Hallo failover-functie toomigrate apparaatgegevens vanaf een fysiek Bronapparaat StorSimple gebruikt in Hallo datacenter tooanother fysieke apparaat. Hallo richtlijnen in deze zelfstudie geldt tooStorSimple 8000 series fysieke apparaten met versies van de software Update 3 en hoger.

toolearn meer informatie over failover-apparaat en hoe deze gebruikt toorecover na een noodgeval te gaan[Failover en herstel na noodgevallen voor StorSimple 8000 series apparaten](storsimple-8000-device-failover-disaster-recovery.md).

toofail via een fysiek apparaat tooanother fysiek apparaat, gaat u te[failover toohello dezelfde fysieke StorSimple-apparaat](storsimple-8000-device-failover-physical-device.md). toofail via een StorSimple fysiek apparaat tooa StorSimple Cloud toestel, gaat u te[tooa StorSimple Cloud toestel failover](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Vereisten

- Zorg ervoor dat u Hallo aandachtspunten voor failover-apparaat hebt bekeken. Voor meer informatie gaat te[algemene overwegingen voor het apparaat failover](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Stappen toofail via toohello hetzelfde apparaat

Uitvoeren van de volgende stappen uit als u toofail via toohello moet Hallo hetzelfde apparaat.

1. Momentopnamen cloud van alle Hallo volumes in uw apparaat. Voor meer informatie gaat te[gebruik StorSimple Apparaatbeheer service toocreate back-ups](storsimple-8000-manage-backup-policies-u2.md).
2. De standaardinstellingen van uw apparaat toofactory opnieuw. Ga als volgt Hallo gedetailleerde instructies in [hoe de standaardinstellingen voor een StorSimple-apparaat toofactory tooreset](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Ga toohello Apparaatbeheer StorSimple-service en selecteer vervolgens **apparaten**. In Hallo **apparaten** blade Hallo oude apparaat moet worden weergegeven als **Offline**.

    ![Offline Bronapparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Uw apparaat configureren en het opnieuw registreren met uw StorSimple-apparaat Manager-service. Hallo nieuw ingeschreven apparaat moet worden weergegeven als **tooset gereed**. Hallo apparaatnaam voor het nieuwe apparaat Hallo is Hallo hetzelfde als het oude apparaat Hallo maar toegevoegd met een cijfer tooindicate dat Hallo-apparaat opnieuw instellen van toofactory standaard was en opnieuw geregistreerd.

    ![Nieuw ingeschreven apparaat gereed tooset up](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Voor het nieuwe apparaat hello, Apparaatinstelling Hallo. Voor meer informatie gaat te[stap 4: minimale apparaatconfiguratie voltooien](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). Op Hallo **apparaten** blade Hallo Hallo apparaat statuswijzigingen te**Online**.

   > [!IMPORTANT]
   > **Minimale configuratie Hallo eerst te voltooien of uw DR mislukken.**

    ![Nieuw ingeschreven apparaat online is](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Selecteer Hallo oude apparaat (offline status) en uit de opdrachtbalk hello, klikt u op **failover**. In Hallo **failover** blade oude apparaat selecteren als bron Hallo en geef Hallo doelapparaat zoals Hallo apparaat opnieuw is geregistreerd.

    ![Overzicht van failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Voor gedetailleerde instructies te verwijzen[tooanother fysiek apparaat failover](#fail-over-to-another-physical-device).

7. Een hersteltaak van het apparaat wordt gemaakt dat u vanaf Hallo bewaken kunt **taken** blade.

8. Nadat het Hallo-taak is voltooid, toegang tot Hallo nieuwe apparaat en navigeer toohello **volumecontainers** blade. Controleren of alle Hallo volumecontainers van het oude apparaat Hallo toohello nieuw apparaat zijn gemigreerd.

   ![Volumecontainers gemigreerd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Nadat het Hallo failover is voltooid, kunt u deactiveren en Hallo oude apparaat verwijderen uit Hallo-portal. Selecteer Hallo oude apparaat (offline), klik met de rechtermuisknop en selecteer vervolgens **deactiveren**. Nadat het Hallo-apparaat wordt gedeactiveerd, wordt Hallo status van Hallo-apparaat bijgewerkt.

     ![Het bronvolume is gedeactiveerd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Selecteer Hallo gedeactiveerd apparaat, klik met de rechtermuisknop en selecteer vervolgens **verwijderen**. Hierdoor Hallo-apparaat wordt verwijderd uit het Hallo-lijst met apparaten.

    ![Het bronvolume is verwijderd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Volgende stappen

* Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).
* Voor informatie over hoe toouse StorSimple Apparaatbeheer Hallo service, gaat u te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

