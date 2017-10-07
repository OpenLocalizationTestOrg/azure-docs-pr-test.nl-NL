---
title: aaaManage access control-records in StorSimple | Microsoft Docs
description: Hierin wordt beschreven hoe toouse toegangsbeheer (ACRs) toodetermine welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen registreert.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Hallo StorSimple Manager-service toomanage access control records gebruiken
## <a name="overview"></a>Overzicht
Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen. ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts. Wanneer een host tooconnect tooa volume probeert, controleert Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor Hallo IQN naam en als er een overeenkomst is, wordt hello verbinding tot stand is gebracht. Hallo-toegangsbeheer registreert sectie op Hallo **configureren** pagina alle Hallo access control records wordt weergegeven met Hallo IQN's de gebruikershandleiding Hallo hosts overeenkomt.

Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:

* Een record voor toegangscontrole toevoegen 
* Een record voor toegangscontrole bewerken 
* Een record voor toegangscontrole verwijderen 

> [!IMPORTANT]
> * Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd. 
> * Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.
> 
> 

## <a name="add-an-access-control-record"></a>Een record voor toegangscontrole toevoegen
Gebruik van de StorSimple Manager-service Hallo **configureren** tooadd ACRs pagina. U koppelt doorgaans één ACR met één volume.

Volgende stappen tooadd een ACR Hallo uitvoeren.

#### <a name="tooadd-an-access-control-record"></a>een record voor toegangscontrole tooadd
1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.
2. In Hallo in tabelvorm aanbieding onder **Access control records**, supply een **naam** voor uw ACR.
3. Hallo IQN naam van uw Windows-host onder **iSCSI-initiatornaam**. tooget hello IQN van Windows Server-host Hallo te volgen:
   
   * Start Hallo Microsoft iSCSI-initiator op uw Windows-host.
   * In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **configuratie** tabblad Selecteer en kopieer Hallo tekenreeks van Hallo **initiatornaam** veld.
   * Plak deze tekenreeks in Hallo **iSCSI-initiatornaam** op Hallo ACRs tabel in Hallo klassieke Azure-portal.
4. Klik op **opslaan** toosave hello ACR van een nieuw gemaakt. Hallo in tabelvorm aanbieding zal worden bijgewerkte tooreflect deze toevoeging.

## <a name="edit-an-access-control-record"></a>Een record voor toegangscontrole bewerken
Gebruik van Hallo **configureren** pagina in hello Azure classic portal tooedit ACRs. 

> [!NOTE]
> U kunt alleen deze ACRs die zich momenteel niet in gebruik wijzigen. tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.
> 
> 

Volgende stappen tooedit een ACR Hallo uitvoeren.

#### <a name="tooedit-an-access-control-record"></a>een record voor toegangscontrole tooedit
1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.
2. In tabelvorm aanbieding Hallo Hallo access control records, de muisaanwijzer op Hallo ACR gewenste toomodify.
3. Geef een nieuwe naam en/of IQN voor Hallo ACR.
4. Klik op **opslaan** toosave hello ACR gewijzigd. Hallo in tabelvorm aanbieding zal worden bijgewerkte tooreflect deze wijziging.

## <a name="delete-an-access-control-record"></a>Een record voor toegangscontrole verwijderen
Gebruik van Hallo **configureren** pagina in hello Azure classic portal toodelete ACRs. 

> [!NOTE]
> U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen. toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.
> 
> 

Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.

#### <a name="toodelete-an-access-control-record"></a>een record voor toegangscontrole toodelete
1. Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.
2. In tabelvorm aanbieding Hallo van Hallo access control-records (ACRs), de muisaanwijzer op Hallo ACR gewenste toodelete.
3. Een verwijderpictogram (**x**) wordt weergegeven in Hallo extreme rechterkolom voor Hallo ACR die u selecteert. Klik op Hallo **x** pictogram toodelete hello ACR.
4. Wanneer u om bevestiging gevraagd, klikt u op **Ja** toocontinue met Hallo verwijderen. in de lijst in tabelvorm Hallo worden bijgewerkte tooreflect Hallo verwijderen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple-volumes beheren](storsimple-manage-volumes.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

