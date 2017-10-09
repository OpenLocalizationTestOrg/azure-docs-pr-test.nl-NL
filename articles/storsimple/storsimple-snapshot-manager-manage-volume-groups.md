---
title: aaaStorSimple Snapshot Manager volume groepen | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module toocreate Hallo en volume-groepen beheren.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Gebruik StorSimple Snapshot Manager toocreate en volume-groepen beheren
## <a name="overview"></a>Overzicht
U kunt Hallo **Volume groepen** knooppunt op Hallo **bereik** deelvenster tooassign volumes toovolume groepen, informatie weergeven over een groep volume back-ups plannen en volume groepen bewerken.

Volume-groepen zijn groepen van gerelateerde volumes gebruikt tooensure dat back-ups toepassingsconsistente zijn. Zie voor meer informatie [Volumes en volume groepen](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) en [integratie met Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Alle volumes in een groep volume moeten afkomstig zijn van een serviceprovider één cloud.
> * Wanneer u een volume-groepen configureert, niet door elkaar op gedeelde clustervolumes (CSV's) en niet-CSV in Hallo dezelfde volume bevinden. StorSimple Snapshot Manager biedt geen ondersteuning voor een combinatie van CSV's en niet-CSV in Hallo dezelfde momentopname.

![Knooppunt voor volume-groepen](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Afbeelding 1: StorSimple Snapshot Manager Volume groepen knooppunt** 

Deze zelfstudie wordt uitgelegd hoe u StorSimple Snapshot Manager om te kan gebruiken:

* Informatie over de volume-groepen weergeven
* De groep van een volume maken
* Back-up van een volume-groep
* Een volume-groep bewerken
* Een volume-groep verwijderen

Al deze acties zijn beschikbaar op Hallo **acties** deelvenster.

## <a name="view-volume-groups"></a>Volume-groepen weergeven
Als u klikt op Hallo **Volume groepen** knooppunt, Hallo **resultaten** deelvenster bevat informatie over elke groep volume na Hallo, afhankelijk van de kolomselecties Hallo u. (kolommen in Hallo Hallo **resultaten** deelvenster worden geconfigureerd. Klik met de rechtermuisknop Hallo **Volumes** knooppunt **weergave**, en selecteer vervolgens **kolommen toevoegen/verwijderen**.)

| Kolom | Beschrijving |
|:--- |:--- |
| Naam |Hallo **naam** kolom Hallo-naam van Hallo volume groep bevat. |
| Toepassing |Hallo **toepassingen** kolom bevat Hallo-nummer van de VSS-schrijvers die momenteel is geïnstalleerd en uitgevoerd op Hallo van Windows-host. |
| Geselecteerd |Hallo **geselecteerde** kolom bevat Hallo-nummer van de volumes die zijn opgenomen in Hallo volume groep. Een nul (0) geeft aan dat er geen toepassing hello volumes in Hallo volume groep is gekoppeld. |
| Geïmporteerd |Hallo **geïmporteerde** kolom Hallo aantal geïmporteerde volumes bevat. Als de waarde te**True**, deze kolom wordt aangegeven dat een volume-groep is geïmporteerd uit hello Azure-portal en in StorSimple Snapshot Manager niet is gemaakt. |

> [!NOTE]
> StorSimple Snapshot Manager volume groepen worden ook weergegeven op Hallo **back-upbeleid** tabblad in hello Azure-portal.
> 
> 

## <a name="create-a-volume-group"></a>De groep van een volume maken
Hallo te volgen procedure toocreate een volume-groep gebruiken.

#### <a name="toocreate-a-volume-group"></a>een groep volume toocreate
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster met de rechtermuisknop op **Volume groepen**, en klik vervolgens op **Create Volume Group**.
   
    ![Volume-groep maken](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Hallo **maakt u een groep volume** dialoogvenster wordt weergegeven.
   
    ![Het groepsdialoogvenster van een volume maken](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Voer Hallo volgende informatie:
   
   1. In Hallo **naam** typt u een unieke naam voor het nieuwe volume groep Hallo.
   2. In Hallo **toepassingen** vak, bepaalde toepassingen die zijn gekoppeld aan het Hallo-volumes dat u toohello volume groep gaat toevoegen.
      
       Hallo **toepassingen** alleen die toepassingen die gebruikmaken van StorSimple-volumes en VSS-schrijvers zijn ingeschakeld voor deze in een lijst weergegeven. Een VSS-schrijver is ingeschakeld, alleen als alle volumes Hallo Hallo schrijver op de hoogte van is StorSimple-volumes. Als Hallo toepassingen vak leeg is, zijn geen toepassingen die gebruikmaken van Azure StorSimple-volumes en er een ondersteunde VSS-schrijvers van geïnstalleerd zijn. (Momenteel Azure StorSimple ondersteunt Microsoft Exchange en SQL Server.) Zie voor meer informatie over VSS-schrijvers [integratie met Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Als u een toepassing selecteert, worden alle volumes die zijn gekoppeld aan deze automatisch geselecteerd. Als u daarentegen als u volumes die zijn gekoppeld aan een specifieke toepassing selecteert, Hallo toepassing wordt automatisch geselecteerd in Hallo **toepassingen** vak. 
   3. In Hallo **Volumes** Selecteer StorSimple-volumes tooadd toohello volume groep. 
      
      * U kunt volumes met één of meerdere partities opnemen. (Meerdere volumes van de partitie kunnen worden dynamische schijven of standaardschijven met meerdere partities.) Een volume dat meerdere partities bevat wordt behandeld als één eenheid. Dus als u slechts één Hallo partities tooa volume groep Hallo alle andere partities toevoegt worden automatisch toegevoegd toothat volume groeperen op Hallo dezelfde tijd. Nadat u een groep meerdere partitie volume tooa volume toevoegt, hello meerdere partitie volume blijft toobe behandeld als één eenheid.
      * U kunt lege volume groepen maken door alle volumes toothem niet toewijzen. 
      * Niet door elkaar op gedeelde clustervolumes (CSV's) en niet-CSV in Hallo dezelfde volume bevinden. StorSimple Snapshot Manager biedt geen ondersteuning voor een combinatie van CSV-volumes en niet-CSV-volumes in Hallo dezelfde momentopname.
4. Klik op **OK** toosave Hallo volume groep.

## <a name="back-up-a-volume-group"></a>Back-up van een volume-groep
Hallo te volgen procedure tooback van een volume-groep gebruiken.

#### <a name="tooback-up-a-volume-group"></a>tooback van een volume-groep
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **duren back-up**.
   
    ![Back-up van volume-groep onmiddellijk](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. In Hallo **duren back-up** dialoogvenster, **lokale momentopname** of **Cloudmomentopname**, en klik vervolgens op **maken**.
   
    ![Back-dialoogvenster](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. tooconfirm die Hallo back-up wordt uitgevoerd, vouw Hallo **taken** knooppunt en klik vervolgens op **met**. Hallo back-up moet worden weergegeven.
5. tooview hello voltooid Hallo momentopname, vouw **back-upcatalogus** knooppunt uitvouwen groepsnaam Hallo-volume en klik vervolgens op **lokale momentopname** of **Cloudmomentopname**. Hallo back-up wordt weergegeven als deze voltooid is.

## <a name="edit-a-volume-group"></a>Een volume-groep bewerken
Hallo te volgen procedure tooedit een volume-groep gebruiken.

#### <a name="tooedit-a-volume-group"></a>een groep volume tooedit
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **bewerken**.
3. Hallo ** maakt u een groep volume ** in het dialoogvenster wordt weergegeven. U kunt wijzigen Hallo **naam**, **toepassingen**, en **Volumes** vermeldingen.
4. Klik op **OK** toosave uw wijzigingen.

## <a name="delete-a-volume-group"></a>Een volume-groep verwijderen
Hallo te volgen procedure toodelete een volume-groep gebruiken. 

> [!WARNING]
> Hiermee verwijdert u ook alle Hallo back-ups die zijn gekoppeld aan Hallo volume groep.
> 
> 

#### <a name="toodelete-a-volume-group"></a>een groep volume toodelete
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **verwijderen**.
3. Hallo **Volume groep verwijderen** dialoogvenster wordt weergegeven. Type **bevestigen** in Hallo in het tekstvak en klik vervolgens op **OK**.
   
    Hallo verwijderd volume groep uit de lijst Hallo in Hallo verdwijnt **resultaten** deelvenster en alle back-ups die gekoppeld aan die groep volume zijn zijn verwijderd uit de back-upcatalogus Hallo.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager toocreate gebruiken en beheren van back-upbeleid](storsimple-snapshot-manager-manage-backup-policies.md).

