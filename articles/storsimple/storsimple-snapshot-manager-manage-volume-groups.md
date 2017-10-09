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
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="1b225-103">Gebruik StorSimple Snapshot Manager toocreate en volume-groepen beheren</span><span class="sxs-lookup"><span data-stu-id="1b225-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="1b225-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1b225-104">Overview</span></span>
<span data-ttu-id="1b225-105">U kunt Hallo **Volume groepen** knooppunt op Hallo **bereik** deelvenster tooassign volumes toovolume groepen, informatie weergeven over een groep volume back-ups plannen en volume groepen bewerken.</span><span class="sxs-lookup"><span data-stu-id="1b225-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="1b225-106">Volume-groepen zijn groepen van gerelateerde volumes gebruikt tooensure dat back-ups toepassingsconsistente zijn.</span><span class="sxs-lookup"><span data-stu-id="1b225-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="1b225-107">Zie voor meer informatie [Volumes en volume groepen](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) en [integratie met Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1b225-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1b225-108">Alle volumes in een groep volume moeten afkomstig zijn van een serviceprovider één cloud.</span><span class="sxs-lookup"><span data-stu-id="1b225-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="1b225-109">Wanneer u een volume-groepen configureert, niet door elkaar op gedeelde clustervolumes (CSV's) en niet-CSV in Hallo dezelfde volume bevinden.</span><span class="sxs-lookup"><span data-stu-id="1b225-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="1b225-110">StorSimple Snapshot Manager biedt geen ondersteuning voor een combinatie van CSV's en niet-CSV in Hallo dezelfde momentopname.</span><span class="sxs-lookup"><span data-stu-id="1b225-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![Knooppunt voor volume-groepen](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="1b225-112">**Afbeelding 1: StorSimple Snapshot Manager Volume groepen knooppunt**</span><span class="sxs-lookup"><span data-stu-id="1b225-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="1b225-113">Deze zelfstudie wordt uitgelegd hoe u StorSimple Snapshot Manager om te kan gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1b225-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="1b225-114">Informatie over de volume-groepen weergeven</span><span class="sxs-lookup"><span data-stu-id="1b225-114">View information about your volume groups</span></span>
* <span data-ttu-id="1b225-115">De groep van een volume maken</span><span class="sxs-lookup"><span data-stu-id="1b225-115">Create a volume group</span></span>
* <span data-ttu-id="1b225-116">Back-up van een volume-groep</span><span class="sxs-lookup"><span data-stu-id="1b225-116">Back up a volume group</span></span>
* <span data-ttu-id="1b225-117">Een volume-groep bewerken</span><span class="sxs-lookup"><span data-stu-id="1b225-117">Edit a volume group</span></span>
* <span data-ttu-id="1b225-118">Een volume-groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="1b225-118">Delete a volume group</span></span>

<span data-ttu-id="1b225-119">Al deze acties zijn beschikbaar op Hallo **acties** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="1b225-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="1b225-120">Volume-groepen weergeven</span><span class="sxs-lookup"><span data-stu-id="1b225-120">View volume groups</span></span>
<span data-ttu-id="1b225-121">Als u klikt op Hallo **Volume groepen** knooppunt, Hallo **resultaten** deelvenster bevat informatie over elke groep volume na Hallo, afhankelijk van de kolomselecties Hallo u.</span><span class="sxs-lookup"><span data-stu-id="1b225-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="1b225-122">(kolommen in Hallo Hallo **resultaten** deelvenster worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1b225-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="1b225-123">Klik met de rechtermuisknop Hallo **Volumes** knooppunt **weergave**, en selecteer vervolgens **kolommen toevoegen/verwijderen**.)</span><span class="sxs-lookup"><span data-stu-id="1b225-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="1b225-124">Kolom</span><span class="sxs-lookup"><span data-stu-id="1b225-124">Results column</span></span> | <span data-ttu-id="1b225-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b225-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1b225-126">Naam</span><span class="sxs-lookup"><span data-stu-id="1b225-126">Name</span></span> |<span data-ttu-id="1b225-127">Hallo **naam** kolom Hallo-naam van Hallo volume groep bevat.</span><span class="sxs-lookup"><span data-stu-id="1b225-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="1b225-128">Toepassing</span><span class="sxs-lookup"><span data-stu-id="1b225-128">Application</span></span> |<span data-ttu-id="1b225-129">Hallo **toepassingen** kolom bevat Hallo-nummer van de VSS-schrijvers die momenteel is geïnstalleerd en uitgevoerd op Hallo van Windows-host.</span><span class="sxs-lookup"><span data-stu-id="1b225-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="1b225-130">Geselecteerd</span><span class="sxs-lookup"><span data-stu-id="1b225-130">Selected</span></span> |<span data-ttu-id="1b225-131">Hallo **geselecteerde** kolom bevat Hallo-nummer van de volumes die zijn opgenomen in Hallo volume groep.</span><span class="sxs-lookup"><span data-stu-id="1b225-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="1b225-132">Een nul (0) geeft aan dat er geen toepassing hello volumes in Hallo volume groep is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1b225-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="1b225-133">Geïmporteerd</span><span class="sxs-lookup"><span data-stu-id="1b225-133">Imported</span></span> |<span data-ttu-id="1b225-134">Hallo **geïmporteerde** kolom Hallo aantal geïmporteerde volumes bevat.</span><span class="sxs-lookup"><span data-stu-id="1b225-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="1b225-135">Als de waarde te**True**, deze kolom wordt aangegeven dat een volume-groep is geïmporteerd uit hello Azure-portal en in StorSimple Snapshot Manager niet is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1b225-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="1b225-136">StorSimple Snapshot Manager volume groepen worden ook weergegeven op Hallo **back-upbeleid** tabblad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1b225-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="1b225-137">De groep van een volume maken</span><span class="sxs-lookup"><span data-stu-id="1b225-137">Create a volume group</span></span>
<span data-ttu-id="1b225-138">Hallo te volgen procedure toocreate een volume-groep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b225-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="1b225-139">een groep volume toocreate</span><span class="sxs-lookup"><span data-stu-id="1b225-139">toocreate a volume group</span></span>
1. <span data-ttu-id="1b225-140">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1b225-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1b225-141">In Hallo **bereik** deelvenster met de rechtermuisknop op **Volume groepen**, en klik vervolgens op **Create Volume Group**.</span><span class="sxs-lookup"><span data-stu-id="1b225-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Volume-groep maken](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="1b225-143">Hallo **maakt u een groep volume** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b225-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![Het groepsdialoogvenster van een volume maken](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="1b225-145">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="1b225-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="1b225-146">In Hallo **naam** typt u een unieke naam voor het nieuwe volume groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b225-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="1b225-147">In Hallo **toepassingen** vak, bepaalde toepassingen die zijn gekoppeld aan het Hallo-volumes dat u toohello volume groep gaat toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1b225-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="1b225-148">Hallo **toepassingen** alleen die toepassingen die gebruikmaken van StorSimple-volumes en VSS-schrijvers zijn ingeschakeld voor deze in een lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b225-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="1b225-149">Een VSS-schrijver is ingeschakeld, alleen als alle volumes Hallo Hallo schrijver op de hoogte van is StorSimple-volumes.</span><span class="sxs-lookup"><span data-stu-id="1b225-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="1b225-150">Als Hallo toepassingen vak leeg is, zijn geen toepassingen die gebruikmaken van Azure StorSimple-volumes en er een ondersteunde VSS-schrijvers van geïnstalleerd zijn.</span><span class="sxs-lookup"><span data-stu-id="1b225-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="1b225-151">(Momenteel Azure StorSimple ondersteunt Microsoft Exchange en SQL Server.) Zie voor meer informatie over VSS-schrijvers [integratie met Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="1b225-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="1b225-152">Als u een toepassing selecteert, worden alle volumes die zijn gekoppeld aan deze automatisch geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1b225-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="1b225-153">Als u daarentegen als u volumes die zijn gekoppeld aan een specifieke toepassing selecteert, Hallo toepassing wordt automatisch geselecteerd in Hallo **toepassingen** vak.</span><span class="sxs-lookup"><span data-stu-id="1b225-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="1b225-154">In Hallo **Volumes** Selecteer StorSimple-volumes tooadd toohello volume groep.</span><span class="sxs-lookup"><span data-stu-id="1b225-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="1b225-155">U kunt volumes met één of meerdere partities opnemen.</span><span class="sxs-lookup"><span data-stu-id="1b225-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="1b225-156">(Meerdere volumes van de partitie kunnen worden dynamische schijven of standaardschijven met meerdere partities.) Een volume dat meerdere partities bevat wordt behandeld als één eenheid.</span><span class="sxs-lookup"><span data-stu-id="1b225-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="1b225-157">Dus als u slechts één Hallo partities tooa volume groep Hallo alle andere partities toevoegt worden automatisch toegevoegd toothat volume groeperen op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="1b225-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="1b225-158">Nadat u een groep meerdere partitie volume tooa volume toevoegt, hello meerdere partitie volume blijft toobe behandeld als één eenheid.</span><span class="sxs-lookup"><span data-stu-id="1b225-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="1b225-159">U kunt lege volume groepen maken door alle volumes toothem niet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1b225-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="1b225-160">Niet door elkaar op gedeelde clustervolumes (CSV's) en niet-CSV in Hallo dezelfde volume bevinden.</span><span class="sxs-lookup"><span data-stu-id="1b225-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="1b225-161">StorSimple Snapshot Manager biedt geen ondersteuning voor een combinatie van CSV-volumes en niet-CSV-volumes in Hallo dezelfde momentopname.</span><span class="sxs-lookup"><span data-stu-id="1b225-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="1b225-162">Klik op **OK** toosave Hallo volume groep.</span><span class="sxs-lookup"><span data-stu-id="1b225-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="1b225-163">Back-up van een volume-groep</span><span class="sxs-lookup"><span data-stu-id="1b225-163">Back up a volume group</span></span>
<span data-ttu-id="1b225-164">Hallo te volgen procedure tooback van een volume-groep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b225-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="1b225-165">tooback van een volume-groep</span><span class="sxs-lookup"><span data-stu-id="1b225-165">tooback up a volume group</span></span>
1. <span data-ttu-id="1b225-166">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1b225-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1b225-167">In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **duren back-up**.</span><span class="sxs-lookup"><span data-stu-id="1b225-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Back-up van volume-groep onmiddellijk](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="1b225-169">In Hallo **duren back-up** dialoogvenster, **lokale momentopname** of **Cloudmomentopname**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="1b225-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Back-dialoogvenster](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="1b225-171">tooconfirm die Hallo back-up wordt uitgevoerd, vouw Hallo **taken** knooppunt en klik vervolgens op **met**.</span><span class="sxs-lookup"><span data-stu-id="1b225-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="1b225-172">Hallo back-up moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b225-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="1b225-173">tooview hello voltooid Hallo momentopname, vouw **back-upcatalogus** knooppunt uitvouwen groepsnaam Hallo-volume en klik vervolgens op **lokale momentopname** of **Cloudmomentopname**.</span><span class="sxs-lookup"><span data-stu-id="1b225-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="1b225-174">Hallo back-up wordt weergegeven als deze voltooid is.</span><span class="sxs-lookup"><span data-stu-id="1b225-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="1b225-175">Een volume-groep bewerken</span><span class="sxs-lookup"><span data-stu-id="1b225-175">Edit a volume group</span></span>
<span data-ttu-id="1b225-176">Hallo te volgen procedure tooedit een volume-groep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b225-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="1b225-177">een groep volume tooedit</span><span class="sxs-lookup"><span data-stu-id="1b225-177">tooedit a volume group</span></span>
1. <span data-ttu-id="1b225-178">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1b225-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1b225-179">In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1b225-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="1b225-180">Hallo ** maakt u een groep volume ** in het dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b225-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="1b225-181">U kunt wijzigen Hallo **naam**, **toepassingen**, en **Volumes** vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="1b225-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="1b225-182">Klik op **OK** toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1b225-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="1b225-183">Een volume-groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="1b225-183">Delete a volume group</span></span>
<span data-ttu-id="1b225-184">Hallo te volgen procedure toodelete een volume-groep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b225-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="1b225-185">Hiermee verwijdert u ook alle Hallo back-ups die zijn gekoppeld aan Hallo volume groep.</span><span class="sxs-lookup"><span data-stu-id="1b225-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="1b225-186">een groep volume toodelete</span><span class="sxs-lookup"><span data-stu-id="1b225-186">toodelete a volume group</span></span>
1. <span data-ttu-id="1b225-187">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1b225-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1b225-188">In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt met de rechtermuisknop op de naam van een volume-groep en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1b225-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="1b225-189">Hallo **Volume groep verwijderen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b225-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="1b225-190">Type **bevestigen** in Hallo in het tekstvak en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b225-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="1b225-191">Hallo verwijderd volume groep uit de lijst Hallo in Hallo verdwijnt **resultaten** deelvenster en alle back-ups die gekoppeld aan die groep volume zijn zijn verwijderd uit de back-upcatalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b225-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b225-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b225-192">Next steps</span></span>
* <span data-ttu-id="1b225-193">Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="1b225-194">Meer informatie over hoe te[StorSimple Snapshot Manager toocreate gebruiken en beheren van back-upbeleid](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1b225-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

