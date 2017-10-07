---
title: aaaDeactivate en verwijderen van een StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooremove StorSimple-apparaat uit de service door het eerst deactiveren en vervolgens te verwijderen.
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Deactiveren en verwijderen van een StorSimple-apparaat

## <a name="overview"></a>Overzicht

Dit artikel wordt beschreven hoe toodeactivate en verwijderen van een StorSimple-apparaat dat is verbonden tooa StorSimple-apparaat Manager-service. Hallo-instructies in dit artikel is van toepassing alleen tooStorSimple 8000 series-apparaten met inbegrip van Hallo StorSimple Cloud apparaten. Als u van een virtueel StorSimple-matrix gebruikmaakt, ga dan te[deactiveren en verwijderen van een virtueel StorSimple-matrix](storsimple-virtual-array-deactivate-and-delete-device.md).

Deactivering servers Hallo verbinding tussen Hallo-apparaat en Hallo bijbehorende Apparaatbeheer StorSimple-service. U kunt de tootake een StorSimple-apparaat buiten dienst (bijvoorbeeld, als u uw apparaat upgraden of vervangen of als u niet langer StorSimple gebruikt). Als dit het geval is, moet u toodeactivate Hallo apparaat voordat u het kunt verwijderen.

Wanneer u een apparaat deactiveert, is alle gegevens die lokaal zijn opgeslagen op Hallo-apparaat niet meer toegankelijk. Alleen Hallo gegevens die zijn gekoppeld aan het Hallo-apparaat dat is opgeslagen in de cloud Hallo kunnen worden hersteld.

> [!WARNING]
> Deactivering is een permanente bewerking en kan niet ongedaan worden gemaakt. Een gedeactiveerde apparaat kan niet worden geregistreerd met Hallo StorSimple-apparaat Manager-service, tenzij het toofactory beginwaarden.
>
> Hallo terugzetten op fabrieksinstellingen proces verwijdert alle Hallo-gegevens die lokaal zijn opgeslagen op uw apparaat. Daarom moet u een cloudmomentopname van al uw gegevens nemen voordat u een apparaat deactiveren. Deze cloudmomentopname met de kunt u toorecover alle gegevens in een later stadium Hallo.

Na het lezen van deze zelfstudie, kunt u zich kunt:

* Een apparaat deactiveren en Hallo gegevens verwijderen.
* Een apparaat deactiveren en Hallo gegevens behouden.

> [!NOTE]
> Voordat u een fysieke StorSimple-apparaat of de cloud apparaat deactiveert, stoppen of verwijderen van clients en hosts die afhankelijk van dat apparaat zijn.


## <a name="deactivate-and-delete-data"></a>Deactiveren en verwijderen van gegevens

Als u geïnteresseerd bent in het Hallo-apparaat volledig verwijderen en niet dat tooretain Hallo gegevens op Hallo-apparaat wilt, voltooit u Hallo stappen te volgen.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>gegevens uit de toodeactivate Hallo apparaat- en delete-Hallo

1. Voordat u een apparaat uitschakelt, moet u alle Hallo volume containers (en Hallo volumes) die zijn gekoppeld aan het Hallo-apparaat verwijderen. Pas nadat u de back-ups Hallo gekoppeld hebt verwijderd, kunt u volumecontainers verwijderen.

    > [!NOTE]
    > Voordat u een fysieke StorSimple-apparaat of de cloud apparaat deactiveert, zorg ervoor dat Hallo gegevens uit de volumecontainer Hallo verwijderd daadwerkelijk verwijderd uit het Hallo-apparaat. U kunt bewaken Hallo cloud verbruik grafieken en wanneer er gebruik van cloud Hallo drop vanwege Hallo back-ups die u hebt verwijderd, klikt u vervolgens kunt u doorgaan toodeactivate Hallo apparaat. Als u Hallo apparaat voordat deactiveren optreedt deze vervolgkeuzelijst, Hallo gegevens is overkomt in Hallo storage-account en kosten toenemen.

2. Deactiveren Hallo-apparaat als volgt:
   
   1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**. In Hallo **apparaten** blade, selecteer Hallo-apparaat dat u wenst toodeactivate, klik met de rechtermuisknop en klik vervolgens op **deactiveren**.

        ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. In Hallo **deactiveren** blade Hallo apparaat naam tooconfirm en klik vervolgens op **deactiveren**. Hallo deactiveren proces gestart en duurt een paar minuten toocomplete.

        ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Na de deactivering, kunt u Hallo apparaat volledig verwijderen. Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service. Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren. Gebruik Hallo stappen toodelete Hallo apparaat te volgen:
   
   1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**. In Hallo **apparaten** blade, selecteer Hallo gedeactiveerd-apparaat dat u wenst toodelete, klik met de rechtermuisknop en klik vervolgens op **verwijderen**.

        ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. In Hallo **verwijderen** blade Hallo apparaat naam tooconfirm en klik vervolgens op **verwijderen**. Hallo verwijdering duurt een paar minuten toocomplete.

        ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Nadat de verwijdering Hallo is met succes voltooid, wordt u gewaarschuwd. lijst met apparaten Hallo werkt ook tooreflect Hallo verwijderen.

## <a name="deactivate-and-retain-data"></a>Deactiveren en behoud van gegevens

Als u bent geïnteresseerd Hallo-apparaat wordt verwijderd, maar tooretain Hallo gegevens wilt, voltooit u Hallo stappen te volgen:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>een apparaat toodeactivate en Hallo gegevens bewaren
1. Hallo-apparaat deactiveren. Alle volumecontainers Hallo en Hallo momentopnamen van Hallo apparaat blijven.
   
   1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**. In Hallo **apparaten** blade, selecteer Hallo-apparaat dat u wenst toodeactivate, klik met de rechtermuisknop en klik vervolgens op **deactiveren**.

         ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. In Hallo **deactiveren** blade Hallo apparaat naam tooconfirm en klik vervolgens op **deactiveren**. Hallo deactiveren proces gestart en duurt een paar minuten toocomplete.

         ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. U kunt nu een failover Hallo volumecontainers en momentopnamen van Hallo die zijn gekoppeld. Voor procedures gaat te[Failover en herstel na noodgevallen voor uw StorSimple-apparaat](storsimple-8000-device-failover-disaster-recovery.md).
3. U kunt Hallo apparaat volledig verwijderen na deactiveren en failover. Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service. Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren. toodelete hello apparaat, volledige Hallo stappen te volgen:
   
   1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**. In Hallo **apparaten** blade, selecteer Hallo gedeactiveerd-apparaat dat u wenst toodelete, klik met de rechtermuisknop en klik vervolgens op **verwijderen**.

       ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. In Hallo **verwijderen** blade Hallo apparaat naam tooconfirm en klik vervolgens op **verwijderen**. Hallo verwijdering duurt een paar minuten toocomplete.

       ![StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Nadat de verwijdering Hallo is met succes voltooid, wordt u gewaarschuwd. lijst met apparaten Hallo werkt ook tooreflect Hallo verwijderen.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Deactiveren en verwijderen van een cloud-apparaat

Voor een StorSimple Cloud-apparaat deactiveren vanuit de portal Hallo deallocates en verwijdert Hallo virtuele machine en Hallo-resources die zijn gemaakt tijdens het inrichten. Nadat Hallo cloud toestel is gedeactiveerd, kan niet worden hersteld tooits eerdere status.

![Cloud van de StorSimple-apparaat deactiveren](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Deactivering van resultaten in Hallo van de volgende activiteiten:

* Hallo StorSimple Cloud apparaat wordt verwijderd uit het Hallo-service.
* Hallo virtuele machine voor Hallo StorSimple Cloud toestel is verwijderd.
* Hallo besturingssysteemschijf en gegevensschijven die zijn gemaakt voor Hallo StorSimple Cloud toestel worden verwijderd.
* Hallo gehoste service en virtuele netwerken die zijn gemaakt tijdens het inrichten, blijven behouden. Als u deze entiteiten niet gebruikt, moet u deze handmatig verwijderen.
* Cloudmomentopnamen die zijn gemaakt door Hallo StorSimple Cloud toestel worden bewaard.

Nadat Hallo cloud toestel is gedeactiveerd, kunt u deze verwijderen uit de lijst met apparaten Hallo. Selecteer Hallo gedeactiveerd apparaat, klik met de rechtermuisknop en klik vervolgens op **verwijderen**. StorSimple ontvangt u een melding zodra het Hallo-apparaat wordt verwijderd en Hallo lijst met apparaten updates.

## <a name="next-steps"></a>Volgende stappen

* toorestore Hallo gedeactiveerde apparaat toofactory standaardwaarden, gaat u te[Hallo apparaat toofactory standaardinstellingen herstellen](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Voor technische ondersteuning [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* toolearn informatie over hoe toouse Hallo Apparaatbeheer StorSimple-service, gaan te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

