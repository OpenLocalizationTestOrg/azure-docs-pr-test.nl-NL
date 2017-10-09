---
title: aaaStorSimple Snapshot Manager back-upbeleid | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module toocreate Hallo en beheren van back-upbeleid Hallo waarmee de geplande back-ups.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>StorSimple Snapshot Manager toocreate gebruiken en beheren van back-upbeleid
## <a name="overview"></a>Overzicht
Een back-upbeleid maakt een schema voor back-ups van gegevens op volume lokaal of in de cloud Hallo. Wanneer u een back-upbeleid maakt, kunt u ook een bewaarbeleid opgeven. (U kunt maximaal 64 momentopnamen behouden). Zie voor meer informatie over back-upbeleid [typen back-up](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000-serie: een oplossing voor hybride cloud](storsimple-overview.md).

Deze zelfstudie wordt uitgelegd hoe:

* Een back-upbeleid maken
* Een back-upbeleid bewerken
* Een back-upbeleid te verwijderen

## <a name="create-a-backup-policy"></a>Een back-upbeleid maken
Gebruik Hallo toocreate procedure een nieuwe back-upbeleid te volgen.

#### <a name="toocreate-a-backup-policy"></a>een back-upbeleid toocreate
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster met de rechtermuisknop op **back-upbeleid**, en klik op **back-up-beleid maken**.

    ![Een back-upbeleid maken](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Hallo **een beleid maken** dialoogvenster wordt weergegeven.

    ![Maak een beleid - tabblad Algemeen](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Op Hallo **algemene** tabblad, volledige Hallo volgende informatie:

   1. In Hallo **naam** in het tekstvak, typ een naam voor het Hallo-beleid.
   2. In Hallo **Volume groep** tekstvak, Hallo-typenaam van Hallo volume groep die is gekoppeld aan het Hallo-beleid.
   3. Selecteer een **lokale momentopname** of **Cloud momentopname**.
   4. Selecteer het aantal momentopnamen tooretain Hallo. Als u selecteert **alle**, 64 momentopnamen behouden blijft (hello maximum).
4. Klik op Hallo **planning** tabblad.

    ![Maak een beleid - tabblad Planning](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Op Hallo **planning** tabblad, volledige Hallo volgende informatie:

   1. Klik op Hallo **inschakelen** selectievakje tooschedule Hallo volgende back-up.
   2. Onder **instellingen**, selecteer **één keer**, **dagelijkse**, **wekelijkse**, of **maandelijkse**.
   3. In Hallo **Start** tekstvak, klik op het pictogram Kalender Hallo en selecteer een begindatum.
   4. Onder **geavanceerde instellingen**, kunt u optioneel herhaaldelijk schema's en een einddatum instellen.
   5. Klik op **OK**.

Nadat u een back-upbeleid hebt gemaakt, Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:

* **Naam** – hello naam van het back-upbeleid.
* **Type** : lokale momentopname of cloudmomentopname van de.
* **Volume groep** – hello volume-groep die is gekoppeld aan het Hallo-beleid.
* **Bewaartermijn** – hello aantal momentopnamen worden bewaard; Hallo maximum 64 is.
* **Gemaakt** – Hallo datum waarop dit beleid is gemaakt.
* **Ingeschakeld** – of Hallo beleid actief is: **True** geeft aan dat deze van kracht; **False** geeft aan of dit niet van kracht is.

## <a name="edit-a-backup-policy"></a>Een back-upbeleid bewerken
Gebruik Hallo procedure tooedit een bestaande back-upbeleid te volgen.

#### <a name="tooedit-a-backup-policy"></a>een back-upbeleid tooedit
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op Hallo **back-upbeleid** knooppunt. Alle Hallo back-upbeleid worden weergegeven in Hallo **resultaten** deelvenster.
3. Met de rechtermuisknop op het Hallo-beleid dat u tooedit wilt en klik vervolgens op **bewerken**.

    ![Een back-upbeleid bewerken](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Wanneer Hallo **een beleid maken** venster wordt weergegeven, typt u de wijzigingen en klik vervolgens op **OK**.

## <a name="delete-a-backup-policy"></a>Een back-upbeleid te verwijderen
Gebruik Hallo procedure toodelete een back-upbeleid te volgen.

#### <a name="toodelete-a-backup-policy"></a>een back-upbeleid toodelete
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op Hallo **back-upbeleid** knooppunt. Alle Hallo back-upbeleid worden weergegeven in Hallo **resultaten** deelvenster.
3. Met de rechtermuisknop op de back-upbeleid Hallo toodelete wilt en klik vervolgens op **verwijderen**.
4. Wanneer het Hallo-bevestigingsbericht wordt weergegeven, klikt u op **Ja**.

    ![Bevestiging van de back-upbeleid te verwijderen](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager tooview gebruiken en beheren van back-uptaken](storsimple-snapshot-manager-manage-backup-jobs.md).
