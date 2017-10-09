---
title: aaaManage access control-records in StorSimple | Microsoft Docs
description: Hierin wordt beschreven hoe toouse toegangsbeheer (ACRs) toodetermine welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen registreert.
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Hallo StorSimple Manager-service toomanage access control records gebruiken

## <a name="overview"></a>Overzicht
Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen. ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts. Wanneer een host tooconnect tooa volume probeert, controleert Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor Hallo IQN naam en als er een overeenkomst is, wordt hello verbinding tot stand is gebracht. access control-records in Hallo Hallo **configuratie** sectie van de blade van uw StorSimple Device Manager-service alle Hallo access control records weergeven met Hallo IQN's de gebruikershandleiding Hallo hosts overeenkomt.

Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:

* Een record voor toegangscontrole toevoegen
* Een record voor toegangscontrole bewerken
* Een record voor toegangscontrole verwijderen

> [!IMPORTANT]
> * Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.
> * Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.

## <a name="get-hello-iqn"></a>Hallo IQN ophalen

Hallo te volgen stappen tooget Hallo IQN van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Een record voor toegangscontrole toevoegen
Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade tooadd ACRs. U koppelt doorgaans één ACR met één volume.

Volgende stappen tooadd een ACR Hallo uitvoeren.

#### <a name="tooadd-an-acr"></a>een ACR tooadd

1. Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.
2. In Hallo **Access control records** blade, klikt u op **+ toevoegen ACR**.

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. In Hallo **ACR toevoegen** blade Hallo volgende stappen:

    1. Geef een naam voor uw ACR.
    
    2. Hallo IQN naam van uw Windows Server-host onder **iSCSI-Initiator Name (IQN)**.

    3. Klik op **toevoegen** toocreate hello ACR.

        ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Hallo toegevoegde dat ACR in tabelvorm aanbieding Hallo van ACRs wordt weergegeven.

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Een record voor toegangscontrole bewerken
Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade tooedit ACRs.

> [!NOTE]
> Het is raadzaam dat u alleen deze ACRs die zich momenteel niet in gebruik. tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.

Volgende stappen tooedit een ACR Hallo uitvoeren.

#### <a name="tooedit-an-access-control-record"></a>een record voor toegangscontrole tooedit
1.  Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/createacr1.png)

2. In tabelvorm aanbieding Hallo Hallo access control records, op en selecteer Hallo ACR gewenste toomodify.

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr1.png)

3. In Hallo **record voor toegangscontrole bewerken** blade, Geef een andere IQN bijbehorende tooanother host.

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Klik op **Opslaan**. Klik op **Ja** als u om bevestiging wordt gevraagd. 

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr3.png)

5. U wordt gewaarschuwd wanneer Hallo ACR wordt bijgewerkt. in de lijst in tabelvorm Hallo werkt ook tooreflect Hallo wijzigen.

   
## <a name="delete-an-access-control-record"></a>Een record voor toegangscontrole verwijderen
Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade toodelete ACRs.

> [!NOTE]
> U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen. toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.

Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.

#### <a name="toodelete-an-access-control-record"></a>een record voor toegangscontrole toodelete
1.  Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/createacr1.png)

2. In tabelvorm aanbieding Hallo Hallo access control records, op en selecteer Hallo ACR gewenste toodelete.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Met de rechtermuisknop op tooinvoke Hallo contextmenu en selecteer **verwijderen**.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Als u wordt gevraagd om bevestiging, Hallo informatie bekijken en klik vervolgens op **verwijderen**.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. U wordt gewaarschuwd wanneer Hallo verwijdering is voltooid. Hallo in tabelvorm aanbieding is bijgewerkte tooreflect Hallo verwijderen.

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple-volumes beheren](storsimple-8000-manage-volumes-u2.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

