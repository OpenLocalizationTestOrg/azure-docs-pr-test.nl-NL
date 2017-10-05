---
title: Beheren van uw StorSimple-back-upcatalogus | Microsoft Docs
description: Wordt uitgelegd hoe u met de StorSimple Manager-servicepagina back-upcatalogus lijst, selecteert en back-upsets voor een volume verwijderen.
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
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="011f7-103">De StorSimple Manager-service gebruiken voor het beheren van uw back-upcatalogus</span><span class="sxs-lookup"><span data-stu-id="011f7-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="011f7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="011f7-104">Overview</span></span>
<span data-ttu-id="011f7-105">De StorSimple Manager-service **back-upcatalogus** pagina wordt weergegeven voor de back-upsets die worden gemaakt wanneer de handmatige of geplande back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="011f7-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="011f7-106">U kunt deze pagina gebruiken alle-ups voor een back-upbeleid of een volume, selecteer weergeven of verwijderen van back-ups, of een back-up gebruiken om te zetten of te klonen van een volume.</span><span class="sxs-lookup"><span data-stu-id="011f7-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="011f7-107">Deze zelfstudie wordt uitgelegd hoe u de optie en verwijderen van een back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="011f7-108">Als u wilt weten hoe u uw apparaat van de back-up herstellen, gaat u naar [uw apparaat terugzetten vanaf een back-upset](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="011f7-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="011f7-109">Voor informatie over het klonen van een volume, gaat u naar [klonen van een StorSimple-volume](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="011f7-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Back-upcatalogus](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="011f7-111">De **back-upcatalogus** pagina vindt u een query voor het verfijnen van uw back-up selectie instellen.</span><span class="sxs-lookup"><span data-stu-id="011f7-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="011f7-112">U kunt de back-upsets die zijn opgehaald, op basis van de volgende parameters op te filteren:</span><span class="sxs-lookup"><span data-stu-id="011f7-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="011f7-113">**Apparaat** : het apparaat waarop de back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="011f7-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="011f7-114">**Back-up maken van beleid of Volume** – de back-upbeleid of het volume dat is gekoppeld aan deze back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="011f7-115">**Van en naar** – het bereik datum en tijd wanneer de back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="011f7-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="011f7-116">De gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="011f7-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="011f7-117">**Naam** : de naam van de back-upbeleid of het volume dat is gekoppeld aan de back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="011f7-118">**De grootte van** : de werkelijke grootte van de back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="011f7-119">**Gemaakt op** – de datum en tijd waarop de back-ups zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="011f7-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="011f7-120">**Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="011f7-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="011f7-121">Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op het apparaat dat een cloudmomentopname verwijst naar de back-up van de volumegegevens die zich in de cloud.</span><span class="sxs-lookup"><span data-stu-id="011f7-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="011f7-122">Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="011f7-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="011f7-123">**Gestart door** – de back-ups automatisch kunnen worden geïnitieerd door een schema of handmatig door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="011f7-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="011f7-124">U kunt een back-upbeleid back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="011f7-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="011f7-125">U kunt ook de **back-up maken** optie voor het uitvoeren van een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="011f7-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="011f7-126">Lijst met back-up wordt ingesteld voor een volume</span><span class="sxs-lookup"><span data-stu-id="011f7-126">List backup sets for a volume</span></span>
<span data-ttu-id="011f7-127">De volgende stappen als u alle de back-ups voor een volume wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="011f7-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="011f7-128">Aan de lijst met back-upsets</span><span class="sxs-lookup"><span data-stu-id="011f7-128">To list backup sets</span></span>
1. <span data-ttu-id="011f7-129">Klik op de pagina StorSimple Manager-service op de **back-upcatalogus** tabblad.</span><span class="sxs-lookup"><span data-stu-id="011f7-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="011f7-130">Filter de selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="011f7-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="011f7-131">Selecteer het juiste apparaat.</span><span class="sxs-lookup"><span data-stu-id="011f7-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="011f7-132">Kies een volume om de bijbehorende de back-ups weer te geven in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="011f7-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="011f7-133">Geef het tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="011f7-133">Specify the time range.</span></span>
   4. <span data-ttu-id="011f7-134">Klik op het vinkje</span><span class="sxs-lookup"><span data-stu-id="011f7-134">Click the check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="011f7-136">Deze query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="011f7-136">to execute this query.</span></span>
      
      <span data-ttu-id="011f7-137">De back-ups die zijn gekoppeld aan het geselecteerde volume worden weergegeven in de lijst met back-upsets.</span><span class="sxs-lookup"><span data-stu-id="011f7-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="011f7-138">Selecteer een back-upset</span><span class="sxs-lookup"><span data-stu-id="011f7-138">Select a backup set</span></span>
<span data-ttu-id="011f7-139">De volgende stappen om te selecteren van een back-upset voor een volume of de back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="011f7-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="011f7-140">Een back-upset selecteren</span><span class="sxs-lookup"><span data-stu-id="011f7-140">To select a backup set</span></span>
1. <span data-ttu-id="011f7-141">Klik op de pagina StorSimple Manager-service op de **back-upcatalogus** tabblad.</span><span class="sxs-lookup"><span data-stu-id="011f7-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="011f7-142">Filter de selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="011f7-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="011f7-143">Selecteer het juiste apparaat.</span><span class="sxs-lookup"><span data-stu-id="011f7-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="011f7-144">Kies in de vervolgkeuzelijst het volume of back-up-beleid voor de back-up die u wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="011f7-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="011f7-145">Geef het tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="011f7-145">Specify the time range.</span></span>
   4. <span data-ttu-id="011f7-146">Klik op het vinkje</span><span class="sxs-lookup"><span data-stu-id="011f7-146">Click the check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="011f7-148">Deze query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="011f7-148">to execute this query.</span></span>
      
      <span data-ttu-id="011f7-149">De back-ups die zijn gekoppeld aan het geselecteerde volume of back-upbeleid moet worden weergegeven in de lijst met back-upsets.</span><span class="sxs-lookup"><span data-stu-id="011f7-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="011f7-150">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-150">Select and expand a backup set.</span></span> <span data-ttu-id="011f7-151">De **herstellen** en **verwijderen** opties worden weergegeven onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="011f7-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="011f7-152">U kunt een van deze acties uitvoeren op de back-upset die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="011f7-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="011f7-153">Een back-upset verwijderen</span><span class="sxs-lookup"><span data-stu-id="011f7-153">Delete a backup set</span></span>
<span data-ttu-id="011f7-154">Een back-up verwijderen als u niet langer wilt bewaren van de gegevens die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="011f7-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="011f7-155">Voer de volgende stappen uit als u wilt verwijderen van een back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="011f7-156">Een back-upset verwijderen</span><span class="sxs-lookup"><span data-stu-id="011f7-156">To delete a backup set</span></span>
1. <span data-ttu-id="011f7-157">Klik op de pagina StorSimple Manager-service op de **back-upcatalogus tabblad**.</span><span class="sxs-lookup"><span data-stu-id="011f7-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="011f7-158">Filter de selecties als volgt:</span><span class="sxs-lookup"><span data-stu-id="011f7-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="011f7-159">Selecteer het juiste apparaat.</span><span class="sxs-lookup"><span data-stu-id="011f7-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="011f7-160">Kies in de vervolgkeuzelijst het volume of back-up-beleid voor de back-up die u wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="011f7-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="011f7-161">Geef het tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="011f7-161">Specify the time range.</span></span>
   4. <span data-ttu-id="011f7-162">Klik op het vinkje</span><span class="sxs-lookup"><span data-stu-id="011f7-162">Click the check icon</span></span> ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="011f7-164">Deze query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="011f7-164">to execute this query.</span></span>
      
      <span data-ttu-id="011f7-165">De back-ups die zijn gekoppeld aan het geselecteerde volume of back-upbeleid moet worden weergegeven in de lijst met back-upsets.</span><span class="sxs-lookup"><span data-stu-id="011f7-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="011f7-166">Selecteer en breid uit een back-upset.</span><span class="sxs-lookup"><span data-stu-id="011f7-166">Select and expand a backup set.</span></span> <span data-ttu-id="011f7-167">De **herstellen** en **verwijderen** opties worden weergegeven onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="011f7-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="011f7-168">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="011f7-168">Click **Delete**.</span></span>
4. <span data-ttu-id="011f7-169">U wordt gewaarschuwd wanneer het verwijderen is uitgevoerd en wanneer het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="011f7-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="011f7-170">Nadat de verwijdering is voltooid, kunt u de query op deze pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="011f7-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="011f7-171">De verwijderde back-upset wordt niet meer weergegeven in de lijst met back-upsets.</span><span class="sxs-lookup"><span data-stu-id="011f7-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="011f7-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="011f7-172">Next steps</span></span>
* <span data-ttu-id="011f7-173">Meer informatie over hoe [gebruik van de back-upcatalogus uw apparaat terugzetten vanaf een back-upset](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="011f7-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="011f7-174">Meer informatie over hoe [de StorSimple Manager-service gebruiken voor het beheren van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="011f7-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

