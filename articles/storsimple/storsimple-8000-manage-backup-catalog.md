---
title: aaaManage uw StorSimple-back-upcatalogus | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple Apparaatbeheer service back-upcatalogus pagina toolist selecteren en back-upsets verwijderen.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="5d65a-103">Hallo Apparaatbeheer StorSimple-service toomanage uw back-upcatalogus gebruiken</span><span class="sxs-lookup"><span data-stu-id="5d65a-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="5d65a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5d65a-104">Overview</span></span>
<span data-ttu-id="5d65a-105">Hallo StorSimple-apparaat Manager-service **back-upcatalogus** blade geeft alle Hallo back-upsets die worden gemaakt wanneer de handmatige of geplande back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d65a-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="5d65a-106">U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.</span><span class="sxs-lookup"><span data-stu-id="5d65a-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="5d65a-107">Deze zelfstudie wordt uitgelegd hoe toolist, selecteer en delete een back-upset.</span><span class="sxs-lookup"><span data-stu-id="5d65a-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="5d65a-108">toolearn hoe toorestore uw apparaat bij back-up, gaat u te[uw apparaat terugzetten vanaf een back-upset](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5d65a-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="5d65a-109">hoe tooclone een volume te gaan toolearn[klonen van een StorSimple-volume](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5d65a-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Back-upcatalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="5d65a-111">Hallo **back-upcatalogus** blade biedt een query toonarrow uw selectie back-upset.</span><span class="sxs-lookup"><span data-stu-id="5d65a-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="5d65a-112">U kunt back-upsets Hallo die zijn opgehaald, op basis van de volgende parameters Hallo filteren:</span><span class="sxs-lookup"><span data-stu-id="5d65a-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="5d65a-113">**Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d65a-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="5d65a-114">**Back-upbeleid of Volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.</span><span class="sxs-lookup"><span data-stu-id="5d65a-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="5d65a-115">**Van en naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d65a-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="5d65a-116">Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="5d65a-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="5d65a-117">**Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="5d65a-118">**De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="5d65a-119">**Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d65a-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="5d65a-120">**Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5d65a-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="5d65a-121">Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="5d65a-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="5d65a-122">Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="5d65a-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="5d65a-123">**Gestart door** – Hallo back-ups automatisch kunnen worden gestart door een schema of handmatig door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5d65a-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="5d65a-124">U kunt een back-upbeleid tooschedule back-ups.</span><span class="sxs-lookup"><span data-stu-id="5d65a-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="5d65a-125">U kunt ook hello gebruiken **back-up maken** optie tootake een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="5d65a-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="5d65a-126">Lijst met back-up wordt ingesteld voor een back-upbeleid</span><span class="sxs-lookup"><span data-stu-id="5d65a-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="5d65a-127">Volgende stappen toolist Hallo alle Hallo back-ups voor een back-upbeleid voltooien.</span><span class="sxs-lookup"><span data-stu-id="5d65a-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="5d65a-128">back-upsets toolist</span><span class="sxs-lookup"><span data-stu-id="5d65a-128">toolist backup sets</span></span>
1. <span data-ttu-id="5d65a-129">Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="5d65a-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="5d65a-130">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="5d65a-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5d65a-131">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="5d65a-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="5d65a-132">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="5d65a-133">Filteren op **back-up maken van beleid** tooview Hallo bijbehorende Hallo back-ups.</span><span class="sxs-lookup"><span data-stu-id="5d65a-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="5d65a-134">Kies in de back-upbeleid vervolgkeuzelijst Hallo **alle** tooview alle back-ups op Hallo geselecteerd Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="5d65a-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="5d65a-135">Klik op **toepassen** tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="5d65a-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="5d65a-136">Hallo back-ups die zijn gekoppeld aan de back-upbeleid Hallo geselecteerd moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="5d65a-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="5d65a-138">Selecteer een back-upset</span><span class="sxs-lookup"><span data-stu-id="5d65a-138">Select a backup set</span></span>
<span data-ttu-id="5d65a-139">Volledige Hallo tooselect stappen na een back-up instellen voor een volume of back-up-beleid.</span><span class="sxs-lookup"><span data-stu-id="5d65a-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="5d65a-140">een back-upset tooselect</span><span class="sxs-lookup"><span data-stu-id="5d65a-140">tooselect a backup set</span></span>
1. <span data-ttu-id="5d65a-141">Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="5d65a-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="5d65a-142">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="5d65a-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5d65a-143">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="5d65a-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="5d65a-144">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="5d65a-145">Filteren op een volume of back-up beleid voor back-up Hallo gewenste tooselect.</span><span class="sxs-lookup"><span data-stu-id="5d65a-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="5d65a-146">Klik op **toepassen** tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="5d65a-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="5d65a-147">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="5d65a-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="5d65a-149">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="5d65a-149">Select and expand a backup set.</span></span> <span data-ttu-id="5d65a-150">U ziet nu de back-upsets Hallo uitgesplitst Hallo volumes die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="5d65a-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="5d65a-151">Hallo **herstellen** en **verwijderen** opties zijn beschikbaar via Hallo contextmenu (Klik met de rechtermuisknop) voor back-upset Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="5d65a-152">U kunt een van deze acties uitvoeren op Hallo back-upset die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="5d65a-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="5d65a-154">Een back-upset verwijderen</span><span class="sxs-lookup"><span data-stu-id="5d65a-154">Delete a backup set</span></span>
<span data-ttu-id="5d65a-155">Een back-up verwijderen als u niet langer wenst dat tooretain Hallo-gegevens gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5d65a-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="5d65a-156">Volgende stappen toodelete een back-upset Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5d65a-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="5d65a-157">een back-upset toodelete</span><span class="sxs-lookup"><span data-stu-id="5d65a-157">toodelete a backup set</span></span>
 <span data-ttu-id="5d65a-158">Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="5d65a-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="5d65a-159">Filter Hallo selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="5d65a-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5d65a-160">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="5d65a-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="5d65a-161">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="5d65a-162">Filteren op een volume of back-up beleid voor back-up Hallo gewenste tooselect.</span><span class="sxs-lookup"><span data-stu-id="5d65a-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="5d65a-163">Klik op **toepassen** tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="5d65a-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="5d65a-164">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="5d65a-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="5d65a-166">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="5d65a-166">Select and expand a backup set.</span></span> <span data-ttu-id="5d65a-167">U ziet nu de back-upsets Hallo uitgesplitst Hallo volumes die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="5d65a-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="5d65a-168">Hallo **herstellen** en **verwijderen** opties zijn beschikbaar via Hallo contextmenu (Klik met de rechtermuisknop) voor back-upset Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d65a-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="5d65a-169">Met de rechtermuisknop op de back-upset Hallo geselecteerd en selecteer in het contextmenu hello, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5d65a-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="5d65a-171">Wanneer u wordt gevraagd om bevestiging, Raadpleeg Hallo weergegeven informatie en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5d65a-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="5d65a-172">de geselecteerde back-up Hello wordt permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5d65a-172">hello selected backup is deleted permanently.</span></span>

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="5d65a-174">U wordt gewaarschuwd wanneer Hallo verwijdering uitgevoerd wordt en wanneer is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d65a-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="5d65a-175">Nadat de Hallo verwijdering is voltooid, kunt u Hallo query op deze pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="5d65a-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="5d65a-176">back-upset Hallo verwijderd weergegeven niet meer in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="5d65a-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="5d65a-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d65a-178">Next steps</span></span>
* <span data-ttu-id="5d65a-179">Meer informatie over hoe te[gebruik Hallo back-upcatalogus toorestore uw apparaat bij een back-upset](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5d65a-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="5d65a-180">Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5d65a-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

