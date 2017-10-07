---
title: aaaDeactivate en verwijderen van een Microsoft Azure StorSimple virtuele matrix | Microsoft Docs
description: Hierin wordt beschreven hoe tooremove StorSimple-apparaat uit de service door het eerst deactiveren en vervolgens te verwijderen.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Deactiveren en verwijderen van een virtueel StorSimple-matrix

## <a name="overview"></a>Overzicht

Wanneer u een virtueel StorSimple-matrix deactiveert, verbreekt Hallo verbinding tussen Hallo-apparaat en Hallo bijbehorende Apparaatbeheer StorSimple-service. Deze zelfstudie wordt uitgelegd hoe:

* Een apparaat deactiveren 
* Een gedeactiveerde apparaat verwijderen

Hallo-informatie in dit artikel is van toepassing alleen tooStorSimple virtuele matrices. Ga voor informatie over 8000-serie, toohow te[deactiveren of verwijderen van een apparaat](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Wanneer toodeactivate?

Deactivering is een permanente bewerking en kan niet ongedaan worden gemaakt. U kunt een gedeactiveerde apparaat niet opnieuw registreren met Hallo StorSimple-apparaat Manager-service. U kunt toodeactivate moet en verwijderen van een virtueel StorSimple-matrix in Hallo volgen scenario's:

* **De geplande failover** : het apparaat online is en u toofail van plan bent op uw apparaat. Als u van plan bent tooupgrade tooa groter apparaat, moet u mogelijk toofail via uw apparaat. Nadat Hallo Gegevenseigendom wordt overgedragen en Hallo failover voltooid is, wordt het bronvolume Hallo automatisch verwijderd.
* **Niet-geplande failover** : het apparaat offline is en u toofail dan Hallo-apparaat nodig. Dit scenario optreden tijdens een noodgeval wanneer er een storing in Hallo datacenter en het primaire apparaat niet beschikbaar is. U van plan bent toofail via Hallo apparaat tooa secundair apparaat. Nadat Hallo Gegevenseigendom wordt overgedragen en Hallo failover voltooid is, wordt het bronvolume Hallo automatisch verwijderd.
* **Buiten gebruik stellen** : U wilt dat toodecommission Hallo apparaat. Hiervoor moet u toofirst Hallo-apparaat deactiveren en vervolgens te verwijderen. Wanneer u een apparaat deactiveert, u niet langer toegang tot alle gegevens die lokaal wordt opgeslagen. U kunt alleen toegang herstellen Hallo gegevens en opgeslagen in de cloud Hallo. Als u tookeep Hallo apparaatgegevens na deactivering plant, moet u een cloudmomentopname van al uw gegevens nemen voordat u een apparaat deactiveren. Deze cloudmomentopname met de kunt u toorecover alle gegevens in een later stadium Hallo.

## <a name="deactivate-a-device"></a>Een apparaat deactiveren

toodeactivate uw apparaat Hallo volgende stappen uit te voeren.

#### <a name="toodeactivate-hello-device"></a>toodeactivate hello apparaat

1. Ga te in uw service**Management > apparaten**. In Hallo **apparaten** blade, klikt u op en selecteer Hallo-apparaat dat u wenst dat toodeactivate.
   
    ![Selecteer welk apparaat toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. In uw **apparaat dashboard** blade, klikt u op **... Meer** en selecteer in de lijst Hallo **deactiveren**.
   
    ![Klikt u op deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. In Hallo **deactiveren** blade, type Hallo apparaatnaam en klik vervolgens op **deactiveren**. 
   
    ![Bevestig deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Hallo deactiveren proces gestart en duurt een paar minuten toocomplete.
   
    ![Deactiveren wordt uitgevoerd](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Na de deactivering, Hallo lijst met apparaten wordt vernieuwd.
   
    ![Volledige deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Nu kunt u dit apparaat verwijderen.

## <a name="delete-hello-device"></a>Hallo-apparaat verwijderen

Een apparaat heeft de eerste gedeactiveerde toodelete toobe deze. Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service. Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren. Hallo-gegevens die zijn gekoppeld met Hallo apparaat blijft echter in Hallo cloud. Deze gegevens worden vervolgens kosten toenemen.

toodelete hello apparaat Hallo volgende stappen uit te voeren.

#### <a name="toodelete-hello-device"></a>toodelete hello apparaat

1. Gaat u in uw StorSimple-Apparaatbeheer te**Management > apparaten**. In Hallo **apparaten** blade een gedeactiveerde apparaat dat u wenst dat toodelete selecteert.
2. In Hallo **apparaat dashboard** blade, klikt u op **... Meer** en klik vervolgens op **verwijderen**.
   
   ![Selecteer welk apparaat toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. In Hallo **verwijderen** blade, type Hallo-naam van uw apparaat tooconfirm Hallo verwijderen en klik vervolgens op **verwijderen**. Verwijderen Hallo-apparaat verwijdert geen Hallo cloudgegevens die zijn gekoppeld aan het Hallo-apparaat. 
   
   ![De verwijdering bevestigen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. Hallo verwijdering wordt gestart en duurt een paar minuten toocomplete.
   
   ![Bezig met verwijderen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Nadat het Hallo-apparaat wordt verwijderd, kunt u Hallo bijgewerkt lijst met apparaten weergeven.

## <a name="next-steps"></a>Volgende stappen

* Voor meer informatie over toofail over te gaan[Failover en herstel na noodgevallen van uw virtuele StorSimple-matrix](storsimple-virtual-array-failover-dr.md).

* toolearn informatie over hoe toouse Hallo Apparaatbeheer StorSimple-service, gaan te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw virtuele StorSimple-matrix](storsimple-virtual-array-manager-service-administration.md). 

