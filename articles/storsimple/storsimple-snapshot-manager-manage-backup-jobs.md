---
title: aaaStorSimple Snapshot Manager back-uptaken | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module tooview Hallo en beheren van back-uptaken voor geplande, voltooide en die momenteel worden uitgevoerd.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="3778e-103">StorSimple Snapshot Manager tooview gebruiken en beheren van back-uptaken</span><span class="sxs-lookup"><span data-stu-id="3778e-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="3778e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3778e-104">Overview</span></span>
<span data-ttu-id="3778e-105">Hallo **taken** knooppunt in Hallo **bereik** deelvenster bevat Hallo **geplande**, **afgelopen 24 uur**, en **met**back-up van taken die u hebt gestart, interactief of door een geconfigureerde beleid.</span><span class="sxs-lookup"><span data-stu-id="3778e-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="3778e-106">Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **taken** knooppunt toodisplay informatie over back-uptaken voor geplande, recente en die momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3778e-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="3778e-107">(Hallo lijst met taken en de bijbehorende informatie wordt weergegeven in Hallo **resultaten** deelvenster.) Bovendien kunt u met de rechtermuisknop op een vermelde taak en contextmenu met een lijst met beschikbare acties weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3778e-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="3778e-108">Geplande taken weergeven</span><span class="sxs-lookup"><span data-stu-id="3778e-108">View scheduled jobs</span></span>
<span data-ttu-id="3778e-109">Gebruik hello te volgen procedure tooview geplande back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="3778e-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="3778e-110">tooview geplande taken</span><span class="sxs-lookup"><span data-stu-id="3778e-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="3778e-111">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3778e-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="3778e-112">In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **geplande**.</span><span class="sxs-lookup"><span data-stu-id="3778e-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="3778e-113">Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:</span><span class="sxs-lookup"><span data-stu-id="3778e-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="3778e-114">**Naam** – hello naam van het Hallo geplande momentopname</span><span class="sxs-lookup"><span data-stu-id="3778e-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="3778e-115">**Voer vervolgens** : Hallo datum en tijd van de volgende geplande momentopname Hallo</span><span class="sxs-lookup"><span data-stu-id="3778e-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="3778e-116">**Laatste uitvoering** : Hallo datum en tijd van de meest recente geplande momentopname Hallo</span><span class="sxs-lookup"><span data-stu-id="3778e-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="3778e-117">Hallo voor eenmalige alleen momentopnamen, **volgende uitvoeren** en **laatste start** Hallo identiek zijn.</span><span class="sxs-lookup"><span data-stu-id="3778e-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Geplande back-uptaken](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="3778e-119">tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3778e-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="3778e-120">Recente taken weergeven</span><span class="sxs-lookup"><span data-stu-id="3778e-120">View recent jobs</span></span>
<span data-ttu-id="3778e-121">Gebruik hello te volgen procedure tooview back-up- en hersteltaken die zijn voltooid in Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="3778e-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="3778e-122">tooview recente taken</span><span class="sxs-lookup"><span data-stu-id="3778e-122">tooview recent jobs</span></span>
1. <span data-ttu-id="3778e-123">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3778e-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3778e-124">In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **afgelopen 24 uur**.</span><span class="sxs-lookup"><span data-stu-id="3778e-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="3778e-125">Hallo **resultaten** deelvenster ziet u back-uptaken voor Hallo afgelopen 24 uur (tooa maximaal 64 taken).</span><span class="sxs-lookup"><span data-stu-id="3778e-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="3778e-126">Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster, afhankelijk van Hallo **weergave** opties die u opgeeft:</span><span class="sxs-lookup"><span data-stu-id="3778e-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="3778e-127">**Naam** – hello naam van het Hallo geplande momentopname.</span><span class="sxs-lookup"><span data-stu-id="3778e-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="3778e-128">**Gestart** : Hallo datum en tijd wanneer Hallo momentopname is begonnen.</span><span class="sxs-lookup"><span data-stu-id="3778e-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="3778e-129">**Gestopt** : Hallo datum en tijd wanneer Hallo momentopname is voltooid of is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="3778e-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="3778e-130">**Verstreken** – Hallo hoeveelheid tijd tussen Hallo **gestart** en **gestopt** tijden.</span><span class="sxs-lookup"><span data-stu-id="3778e-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="3778e-131">**Status** – Hallo status van taak Hallo onlangs voltooid.</span><span class="sxs-lookup"><span data-stu-id="3778e-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="3778e-132">**Geslaagde** geeft aan dat Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3778e-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="3778e-133">**Kan geen** geeft aan dat Hallo-taak niet kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3778e-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="3778e-134">**Informatie** – Hallo reden voor Hallo mislukken.</span><span class="sxs-lookup"><span data-stu-id="3778e-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="3778e-135">**Bytes verwerkt (MB)** – hello en de hoeveelheid gegevens uit Hallo volume groep die is verwerkt (in MB).</span><span class="sxs-lookup"><span data-stu-id="3778e-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Taken die zijn uitgevoerd in Hallo afgelopen 24 uur](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="3778e-137">tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3778e-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Een taak verwijderen](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="3778e-139">Actieve taken weergeven</span><span class="sxs-lookup"><span data-stu-id="3778e-139">View currently running jobs</span></span>
<span data-ttu-id="3778e-140">Gebruik hello te volgen procedure tooview taken die momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3778e-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="3778e-141">tooview momenteel actieve taken</span><span class="sxs-lookup"><span data-stu-id="3778e-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="3778e-142">Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="3778e-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3778e-143">In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **met**.</span><span class="sxs-lookup"><span data-stu-id="3778e-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="3778e-144">Afhankelijk van Hallo **weergave** opties die u opgeeft, Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:</span><span class="sxs-lookup"><span data-stu-id="3778e-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="3778e-145">**Naam** – hello naam van het Hallo geplande momentopname.</span><span class="sxs-lookup"><span data-stu-id="3778e-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="3778e-146">**Gestart** : Hallo datum en tijd wanneer Hallo momentopname is begonnen.</span><span class="sxs-lookup"><span data-stu-id="3778e-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="3778e-147">**Controlepunt** – Hallo van de huidige actie Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="3778e-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="3778e-148">**Status** – Hallo percentage voltooid.</span><span class="sxs-lookup"><span data-stu-id="3778e-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="3778e-149">**Verstreken** – Hallo hoeveelheid tijd is verstreken sinds het begin van Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="3778e-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="3778e-150">**Gemiddelde doorvoer (MB)** – verhouding van totaal aantal bytes van toothat verwerkte gegevens van de totale tijd voor het verwerken van (MB).</span><span class="sxs-lookup"><span data-stu-id="3778e-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="3778e-151">**Bytes verwerkt (MB)** : totaal aantal bytes van gegevens die zijn verwerkt (in MB).</span><span class="sxs-lookup"><span data-stu-id="3778e-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="3778e-152">**Bytes geschreven (MB)** : totaal aantal bytes van gegevens die zijn geschreven (in MB).</span><span class="sxs-lookup"><span data-stu-id="3778e-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="3778e-153">Het bevat Hallo gegevens, evenals Hallo metagegevens en is daarom meestal groter is dan Hallo Bytes verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3778e-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Taken worden uitgevoerd](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="3778e-155">tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3778e-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3778e-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3778e-156">Next steps</span></span>
* <span data-ttu-id="3778e-157">Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="3778e-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="3778e-158">Meer informatie over hoe te[StorSimple Snapshot Manager toomanage Hallo back-upcatalogus gebruiken](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3778e-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

