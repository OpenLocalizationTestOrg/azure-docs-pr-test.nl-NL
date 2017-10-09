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
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="d00fb-103">StorSimple Snapshot Manager toocreate gebruiken en beheren van back-upbeleid</span><span class="sxs-lookup"><span data-stu-id="d00fb-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="d00fb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d00fb-104">Overview</span></span>
<span data-ttu-id="d00fb-105">Een back-upbeleid maakt een schema voor back-ups van gegevens op volume lokaal of in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="d00fb-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="d00fb-106">Wanneer u een back-upbeleid maakt, kunt u ook een bewaarbeleid opgeven.</span><span class="sxs-lookup"><span data-stu-id="d00fb-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="d00fb-107">(U kunt maximaal 64 momentopnamen behouden). Zie voor meer informatie over back-upbeleid [typen back-up](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000-serie: een oplossing voor hybride cloud](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d00fb-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="d00fb-108">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="d00fb-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="d00fb-109">Een back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="d00fb-109">Create a backup policy</span></span>
* <span data-ttu-id="d00fb-110">Een back-upbeleid bewerken</span><span class="sxs-lookup"><span data-stu-id="d00fb-110">Edit a backup policy</span></span>
* <span data-ttu-id="d00fb-111">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="d00fb-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="d00fb-112">Een back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="d00fb-112">Create a backup policy</span></span>
<span data-ttu-id="d00fb-113">Gebruik Hallo toocreate procedure een nieuwe back-upbeleid te volgen.</span><span class="sxs-lookup"><span data-stu-id="d00fb-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="d00fb-114">een back-upbeleid toocreate</span><span class="sxs-lookup"><span data-stu-id="d00fb-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="d00fb-115">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="d00fb-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d00fb-116">In Hallo **bereik** deelvenster met de rechtermuisknop op **back-upbeleid**, en klik op **back-up-beleid maken**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Een back-upbeleid maken](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="d00fb-118">Hallo **een beleid maken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d00fb-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Maak een beleid - tabblad Algemeen](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="d00fb-120">Op Hallo **algemene** tabblad, volledige Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="d00fb-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="d00fb-121">In Hallo **naam** in het tekstvak, typ een naam voor het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="d00fb-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="d00fb-122">In Hallo **Volume groep** tekstvak, Hallo-typenaam van Hallo volume groep die is gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="d00fb-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="d00fb-123">Selecteer een **lokale momentopname** of **Cloud momentopname**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="d00fb-124">Selecteer het aantal momentopnamen tooretain Hallo.</span><span class="sxs-lookup"><span data-stu-id="d00fb-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="d00fb-125">Als u selecteert **alle**, 64 momentopnamen behouden blijft (hello maximum).</span><span class="sxs-lookup"><span data-stu-id="d00fb-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="d00fb-126">Klik op Hallo **planning** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d00fb-126">Click hello **Schedule** tab.</span></span>

    ![Maak een beleid - tabblad Planning](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="d00fb-128">Op Hallo **planning** tabblad, volledige Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="d00fb-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="d00fb-129">Klik op Hallo **inschakelen** selectievakje tooschedule Hallo volgende back-up.</span><span class="sxs-lookup"><span data-stu-id="d00fb-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="d00fb-130">Onder **instellingen**, selecteer **één keer**, **dagelijkse**, **wekelijkse**, of **maandelijkse**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="d00fb-131">In Hallo **Start** tekstvak, klik op het pictogram Kalender Hallo en selecteer een begindatum.</span><span class="sxs-lookup"><span data-stu-id="d00fb-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="d00fb-132">Onder **geavanceerde instellingen**, kunt u optioneel herhaaldelijk schema's en een einddatum instellen.</span><span class="sxs-lookup"><span data-stu-id="d00fb-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="d00fb-133">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-133">Click **OK**.</span></span>

<span data-ttu-id="d00fb-134">Nadat u een back-upbeleid hebt gemaakt, Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:</span><span class="sxs-lookup"><span data-stu-id="d00fb-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="d00fb-135">**Naam** – hello naam van het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="d00fb-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="d00fb-136">**Type** : lokale momentopname of cloudmomentopname van de.</span><span class="sxs-lookup"><span data-stu-id="d00fb-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="d00fb-137">**Volume groep** – hello volume-groep die is gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="d00fb-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="d00fb-138">**Bewaartermijn** – hello aantal momentopnamen worden bewaard; Hallo maximum 64 is.</span><span class="sxs-lookup"><span data-stu-id="d00fb-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="d00fb-139">**Gemaakt** – Hallo datum waarop dit beleid is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d00fb-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="d00fb-140">**Ingeschakeld** – of Hallo beleid actief is: **True** geeft aan dat deze van kracht; **False** geeft aan of dit niet van kracht is.</span><span class="sxs-lookup"><span data-stu-id="d00fb-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="d00fb-141">Een back-upbeleid bewerken</span><span class="sxs-lookup"><span data-stu-id="d00fb-141">Edit a backup policy</span></span>
<span data-ttu-id="d00fb-142">Gebruik Hallo procedure tooedit een bestaande back-upbeleid te volgen.</span><span class="sxs-lookup"><span data-stu-id="d00fb-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="d00fb-143">een back-upbeleid tooedit</span><span class="sxs-lookup"><span data-stu-id="d00fb-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="d00fb-144">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="d00fb-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d00fb-145">In Hallo **bereik** deelvenster, klikt u op Hallo **back-upbeleid** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d00fb-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="d00fb-146">Alle Hallo back-upbeleid worden weergegeven in Hallo **resultaten** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d00fb-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="d00fb-147">Met de rechtermuisknop op het Hallo-beleid dat u tooedit wilt en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Een back-upbeleid bewerken](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="d00fb-149">Wanneer Hallo **een beleid maken** venster wordt weergegeven, typt u de wijzigingen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="d00fb-150">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="d00fb-150">Delete a backup policy</span></span>
<span data-ttu-id="d00fb-151">Gebruik Hallo procedure toodelete een back-upbeleid te volgen.</span><span class="sxs-lookup"><span data-stu-id="d00fb-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="d00fb-152">een back-upbeleid toodelete</span><span class="sxs-lookup"><span data-stu-id="d00fb-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="d00fb-153">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="d00fb-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="d00fb-154">In Hallo **bereik** deelvenster, klikt u op Hallo **back-upbeleid** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d00fb-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="d00fb-155">Alle Hallo back-upbeleid worden weergegeven in Hallo **resultaten** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d00fb-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="d00fb-156">Met de rechtermuisknop op de back-upbeleid Hallo toodelete wilt en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="d00fb-157">Wanneer het Hallo-bevestigingsbericht wordt weergegeven, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="d00fb-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Bevestiging van de back-upbeleid te verwijderen](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="d00fb-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d00fb-159">Next steps</span></span>
* <span data-ttu-id="d00fb-160">Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="d00fb-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="d00fb-161">Meer informatie over hoe te[StorSimple Snapshot Manager tooview gebruiken en beheren van back-uptaken](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="d00fb-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
