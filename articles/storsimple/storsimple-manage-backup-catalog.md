---
title: aaaManage uw StorSimple-back-upcatalogus | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple Manager service back-upcatalogus pagina toolist selecteren en back-upsets voor een volume verwijderen.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="83601-103">Hallo StorSimple Manager-service toomanage uw back-upcatalogus gebruiken</span><span class="sxs-lookup"><span data-stu-id="83601-103">Use hello StorSimple Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="83601-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="83601-104">Overview</span></span>
<span data-ttu-id="83601-105">Hallo StorSimple Manager-service **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of geplande back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83601-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="83601-106">U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.</span><span class="sxs-lookup"><span data-stu-id="83601-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="83601-107">Deze zelfstudie wordt uitgelegd hoe toolist, selecteer en delete een back-upset.</span><span class="sxs-lookup"><span data-stu-id="83601-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="83601-108">toolearn hoe toorestore uw apparaat bij back-up, gaat u te[uw apparaat terugzetten vanaf een back-upset](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="83601-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="83601-109">hoe tooclone een volume te gaan toolearn[klonen van een StorSimple-volume](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="83601-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Back-upcatalogus](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="83601-111">Hallo **back-upcatalogus** pagina vindt u een query toonarrow uw selectie back-upset.</span><span class="sxs-lookup"><span data-stu-id="83601-111">hello **Backup Catalog** page provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="83601-112">U kunt back-upsets Hallo die zijn opgehaald, op basis van de volgende parameters Hallo filteren:</span><span class="sxs-lookup"><span data-stu-id="83601-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="83601-113">**Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83601-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="83601-114">**Back-up maken van beleid of Volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.</span><span class="sxs-lookup"><span data-stu-id="83601-114">**Backup Policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="83601-115">**Van en naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83601-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="83601-116">Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="83601-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="83601-117">**Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.</span><span class="sxs-lookup"><span data-stu-id="83601-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="83601-118">**De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="83601-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="83601-119">**Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83601-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="83601-120">**Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="83601-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="83601-121">Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="83601-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="83601-122">Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="83601-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="83601-123">**Gestart door** – Hallo back-ups automatisch kunnen worden gestart door een schema of handmatig door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="83601-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="83601-124">U kunt een back-upbeleid tooschedule back-ups.</span><span class="sxs-lookup"><span data-stu-id="83601-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="83601-125">U kunt ook hello gebruiken **back-up maken** optie tootake een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="83601-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="83601-126">Lijst met back-up wordt ingesteld voor een volume</span><span class="sxs-lookup"><span data-stu-id="83601-126">List backup sets for a volume</span></span>
<span data-ttu-id="83601-127">De volgende volledige Hallo stappen toolist alle Hallo back-ups voor een volume.</span><span class="sxs-lookup"><span data-stu-id="83601-127">Complete hello following steps toolist all hello backups for a volume.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="83601-128">back-upsets toolist</span><span class="sxs-lookup"><span data-stu-id="83601-128">toolist backup sets</span></span>
1. <span data-ttu-id="83601-129">Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.</span><span class="sxs-lookup"><span data-stu-id="83601-129">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="83601-130">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="83601-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="83601-131">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="83601-131">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="83601-132">In de vervolgkeuzelijst hello, kiest u een volume tooview Hallo bijbehorende Hallo back-ups.</span><span class="sxs-lookup"><span data-stu-id="83601-132">In hello drop-down list, choose a volume tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="83601-133">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="83601-133">Specify hello time range.</span></span>
   4. <span data-ttu-id="83601-134">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="83601-134">Click hello check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="83601-136">tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="83601-136">tooexecute this query.</span></span>
      
      <span data-ttu-id="83601-137">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="83601-137">hello backups associated with hello selected volume should appear in hello list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="83601-138">Selecteer een back-upset</span><span class="sxs-lookup"><span data-stu-id="83601-138">Select a backup set</span></span>
<span data-ttu-id="83601-139">Volledige Hallo tooselect stappen na een back-up instellen voor een volume of back-up-beleid.</span><span class="sxs-lookup"><span data-stu-id="83601-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="83601-140">een back-upset tooselect</span><span class="sxs-lookup"><span data-stu-id="83601-140">tooselect a backup set</span></span>
1. <span data-ttu-id="83601-141">Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.</span><span class="sxs-lookup"><span data-stu-id="83601-141">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="83601-142">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="83601-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="83601-143">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="83601-143">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="83601-144">Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.</span><span class="sxs-lookup"><span data-stu-id="83601-144">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="83601-145">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="83601-145">Specify hello time range.</span></span>
   4. <span data-ttu-id="83601-146">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="83601-146">Click hello check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="83601-148">tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="83601-148">tooexecute this query.</span></span>
      
      <span data-ttu-id="83601-149">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="83601-149">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="83601-150">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="83601-150">Select and expand a backup set.</span></span> <span data-ttu-id="83601-151">Hallo **herstellen** en **verwijderen** opties onder Hallo van Hallo pagina worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83601-151">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="83601-152">U kunt een van deze acties uitvoeren op Hallo back-upset die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="83601-152">You can perform either of these actions on hello backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="83601-153">Een back-upset verwijderen</span><span class="sxs-lookup"><span data-stu-id="83601-153">Delete a backup set</span></span>
<span data-ttu-id="83601-154">Een back-up verwijderen als u niet langer wenst dat tooretain Hallo-gegevens gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="83601-154">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="83601-155">Volgende stappen toodelete een back-upset Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83601-155">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="83601-156">een back-upset toodelete</span><span class="sxs-lookup"><span data-stu-id="83601-156">toodelete a backup set</span></span>
1. <span data-ttu-id="83601-157">Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus tabblad**.</span><span class="sxs-lookup"><span data-stu-id="83601-157">On hello StorSimple Manager service page, click hello **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="83601-158">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="83601-158">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="83601-159">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="83601-159">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="83601-160">Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.</span><span class="sxs-lookup"><span data-stu-id="83601-160">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="83601-161">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="83601-161">Specify hello time range.</span></span>
   4. <span data-ttu-id="83601-162">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="83601-162">Click hello check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="83601-164">tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="83601-164">tooexecute this query.</span></span>
      
      <span data-ttu-id="83601-165">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="83601-165">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="83601-166">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="83601-166">Select and expand a backup set.</span></span> <span data-ttu-id="83601-167">Hallo **herstellen** en **verwijderen** opties onder Hallo van Hallo pagina worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83601-167">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="83601-168">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="83601-168">Click **Delete**.</span></span>
4. <span data-ttu-id="83601-169">U wordt gewaarschuwd wanneer Hallo verwijdering uitgevoerd wordt en wanneer is voltooid.</span><span class="sxs-lookup"><span data-stu-id="83601-169">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="83601-170">Nadat de Hallo verwijdering is voltooid, kunt u Hallo query op deze pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="83601-170">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="83601-171">back-upset Hallo verwijderd weergegeven niet meer in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="83601-171">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83601-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83601-172">Next steps</span></span>
* <span data-ttu-id="83601-173">Meer informatie over hoe te[gebruik Hallo back-upcatalogus toorestore uw apparaat bij een back-upset](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="83601-173">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="83601-174">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="83601-174">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

