---
title: aaaManage access control-records voor virtuele StorSimple-matrix | Microsoft Docs
description: Hierin wordt beschreven hoe toomanage toegangsbeheer (ACRs) toodetermine welke hosts verbinding van tooa volume op Hallo virtuele StorSimple-matrix maken kunnen registreert.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Gebruik StorSimple Apparaatbeheer toomanage access control-records voor virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van tooa volume op Hallo virtuele StorSimple-matrix (ook wel bekend als Hallo StorSimple on-premises virtuele apparaat maken kunnen). ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts. Wanneer een host tooconnect tooa volume probeert, Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor de naam van de IQN Hallo controleert en als er een overeenkomst, klikt u vervolgens Hallo-verbinding tot stand is gebracht. Hallo **Access control records** blade binnen Hallo **configuratie** sectie van uw service Apparaatbeheer vindt u alle Hallo access control records Hello IQN's de gebruikershandleiding Hallo hosts overeenkomt.

![Access control records beheren](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:

* Hallo IQN ophalen
* Een record voor toegangscontrole toevoegen
* Een record voor toegangscontrole bewerken
* Een record voor toegangscontrole verwijderen

> [!IMPORTANT]
> 
> * Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.
> * Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.


## <a name="get-hello-iqn"></a>Hallo IQN ophalen

Hallo te volgen stappen tooget Hallo IQN van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Een ACR toevoegen

U gebruikt **Access control records** blade binnen Hallo **configuratie** gedeelte van uw StorSimple-apparaat Manager service tooadd ACRs. Normaal gesproken koppelt u een ACR aan één volume.

Voor informatie over het koppelen van een ACR met een volume gaat te[toevoegen van een volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.


Volgende stappen tooadd een ACR Hallo uitvoeren.

#### <a name="tooadd-an-acr"></a>een ACR tooadd

1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.
2. In Hallo **Access control records** blade, klikt u op **toevoegen**.
3. In Hallo **ACR toevoegen** blade Hallo te volgen:
   
    1. Geef een **naam** voor uw ACR op.
    
    2. Onder **iSCSI-initiatornaam**, Hallo IQN naam van uw Windows-host. tooget hello IQN van Windows Server-host Hallo te volgen:
   
    3. Start Hallo Microsoft iSCSI-initiator op uw Windows-host. Hallo iSCSI-Initiator venster Eigenschappen op Hallo **configuratie** tabblad Selecteer en kopieer Hallo tekenreeks van Hallo **initiatornaam** veld.
    Plak deze tekenreeks in Hallo **IQN** veld Hallo **ACR toevoegen** blade.
   
    6. Klik op **toevoegen** tooadd hello ACR.  
   
        ![Access control records toevoegen](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. in de lijst in tabelvorm Hallo bijgewerkte tooreflect is deze aanvulling.

## <a name="edit-an-acr"></a>Een ACR bewerken

Gebruik van Hallo **Access control records** blade binnen Hallo **configuratie** gedeelte van uw service Apparaatbeheer in Azure portal tooedit ACRs Hallo.

> [!NOTE]
> U moet een ACR die momenteel in gebruik is niet wijzigen. tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.


Volgende stappen tooedit een ACR Hallo uitvoeren.

#### <a name="tooedit-an-acr"></a>een ACR tooedit

1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie **Access control records**.
2. In Hallo **Access control records** blade uit in tabelvorm aanbieding Hallo Hallo access control records, dubbelklikt u op Hallo ACR gewenste toomodify.
3. In Hallo **bewerken access control records** blade Hallo te volgen:
   
    1. Hallo IQN voor Hallo ACR op te geven.
   
    2. Klik op **opslaan** bovenaan Hallo Hallo blade toosave hello ACR gewijzigd. Hallo volgende bevestigingsbericht wordt weergegeven:
   
        ![Access control records bewerken](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Een record voor toegangscontrole verwijderen

Gebruik van Hallo **configuratie** pagina in Azure portal toodelete ACRs Hallo.

> [!NOTE]
> 
> * U moet een ACR die momenteel in gebruik is niet verwijderen. toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.
> * Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.


Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.

#### <a name="toodelete-an-access-control-record"></a>een record voor toegangscontrole toodelete

1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie **Access control records**.

2. In Hallo **Access control records** blade uit in tabelvorm aanbieding Hallo Hallo access control records, dubbelklikt u op Hallo ACR gewenste toodelete.

3. Klik op Hallo bewerken access control records blade **verwijderen**.
   
    ![ACRS verwijderen](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Wanneer u om bevestiging gevraagd, klikt u op **verwijderen** toocontinue met Hallo verwijderen. Hallo in tabelvorm aanbieding is bijgewerkte tooreflect Hallo verwijderen.
   
   ![Waarschuwingsbericht](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [volumes toevoegen en configureren van ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

