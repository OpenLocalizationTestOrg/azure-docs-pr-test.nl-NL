---
title: een StorSimple-volume van back-up aaaRestore | Microsoft Docs
description: Legt uit hoe toouse Hallo StorSimple Manager service back-upcatalogus pagina toorestore een StorSimple-volume vanuit een back-upset.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="72b1d-103">Een StorSimple-volume herstelt vanuit een back-upset</span><span class="sxs-lookup"><span data-stu-id="72b1d-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="72b1d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="72b1d-104">Overview</span></span>
<span data-ttu-id="72b1d-105">Hallo **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72b1d-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="72b1d-106">U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.</span><span class="sxs-lookup"><span data-stu-id="72b1d-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Back-pagina van de catalogus](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="72b1d-108">Deze zelfstudie wordt uitgelegd hoe toouse hello **back-upcatalogus** pagina toorestore een volume op uw apparaat bij een back-upset.</span><span class="sxs-lookup"><span data-stu-id="72b1d-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="72b1d-109">Hoe toouse Hallo back-upcatalogus</span><span class="sxs-lookup"><span data-stu-id="72b1d-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="72b1d-110">Hallo **back-upcatalogus** pagina vindt u een query waarmee u toonarrow uw selectie back-upset.</span><span class="sxs-lookup"><span data-stu-id="72b1d-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="72b1d-111">U kunt Hallo back-upsets die worden opgehaald op basis van de volgende parameters Hallo filteren:</span><span class="sxs-lookup"><span data-stu-id="72b1d-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="72b1d-112">**Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72b1d-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="72b1d-113">**Back-up maken van beleid** of **volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.</span><span class="sxs-lookup"><span data-stu-id="72b1d-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="72b1d-114">**Van** en **naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72b1d-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="72b1d-115">Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="72b1d-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="72b1d-116">**Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.</span><span class="sxs-lookup"><span data-stu-id="72b1d-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="72b1d-117">**De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="72b1d-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="72b1d-118">**Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72b1d-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="72b1d-119">**Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="72b1d-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="72b1d-120">Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="72b1d-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="72b1d-121">Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.</span><span class="sxs-lookup"><span data-stu-id="72b1d-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="72b1d-122">**Gestart door** – Hallo back-ups worden geïnitieerd automatisch volgens tooa schema of handmatig door een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="72b1d-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="72b1d-123">(U kunt een back-upbeleid tooschedule back-ups.</span><span class="sxs-lookup"><span data-stu-id="72b1d-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="72b1d-124">U kunt ook hello gebruiken **back-up maken** optie tootake een interactieve back-up.)</span><span class="sxs-lookup"><span data-stu-id="72b1d-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="72b1d-125">Hoe toorestore uw StorSimple-volume van een back-up</span><span class="sxs-lookup"><span data-stu-id="72b1d-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="72b1d-126">U kunt Hallo **back-upcatalogus** pagina toorestore uw StorSimple-volume van een specifieke back-up.</span><span class="sxs-lookup"><span data-stu-id="72b1d-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="72b1d-127">Terugzetten vanuit een back-up wordt vervangen door bestaande volumes Hallo van Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="72b1d-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="72b1d-128">Hierdoor kunnen Hallo verlies van gegevens die is geschreven nadat Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72b1d-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="72b1d-129">Voordat u een herstelpunt op een volume hebt gestart, zorg ervoor dat de Hallo volume offline is.</span><span class="sxs-lookup"><span data-stu-id="72b1d-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="72b1d-130">U moet tootake Hallo volume offline op host Hallo eerst en vervolgens Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="72b1d-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="72b1d-131">Volg de stappen Hallo in [offline zetten van een volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="72b1d-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="72b1d-132">Volgende stappen toorestore een volume uit een back-upset Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="72b1d-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="72b1d-133">toorestore vanuit een back-upset</span><span class="sxs-lookup"><span data-stu-id="72b1d-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="72b1d-134">Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.</span><span class="sxs-lookup"><span data-stu-id="72b1d-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Back-upcatalogus](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="72b1d-136">Selecteer een back-up als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="72b1d-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="72b1d-137">Selecteer het juiste apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="72b1d-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="72b1d-138">Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.</span><span class="sxs-lookup"><span data-stu-id="72b1d-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="72b1d-139">Hallo tijdsperiode opgeven.</span><span class="sxs-lookup"><span data-stu-id="72b1d-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="72b1d-140">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="72b1d-140">Click hello check icon</span></span> ![vinkje](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="72b1d-142">tooexecute deze query.</span><span class="sxs-lookup"><span data-stu-id="72b1d-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="72b1d-143">Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.</span><span class="sxs-lookup"><span data-stu-id="72b1d-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="72b1d-144">Vouw Hallo back-upset tooview Hallo gekoppeld volumes.</span><span class="sxs-lookup"><span data-stu-id="72b1d-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="72b1d-145">Deze volumes moeten op Hallo host en het apparaat offline worden genomen voordat u ze kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="72b1d-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="72b1d-146">Volg de stappen Hallo in [offline zetten van een volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="72b1d-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="72b1d-147">Zorg ervoor dat u hebt ondernomen Hallo volumes offline op Hallo host eerst voordat u Hallo volumes offline op Hallo-apparaat nemen.</span><span class="sxs-lookup"><span data-stu-id="72b1d-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="72b1d-148">Als u niet Hallo volumes offline op Hallo host nemen, kan deze toodata beschadiging leiden.</span><span class="sxs-lookup"><span data-stu-id="72b1d-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="72b1d-149">Selecteer een back-upset.</span><span class="sxs-lookup"><span data-stu-id="72b1d-149">Select a backup set.</span></span> <span data-ttu-id="72b1d-150">Klik op **herstellen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="72b1d-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="72b1d-151">U wordt gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="72b1d-151">You will be prompted for confirmation.</span></span> 
   
    ![Bevestigingspagina](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="72b1d-153">Raadpleeg Hallo terugzetten informatie en klik op het vinkje Hallo ![vinkje](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="72b1d-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="72b1d-154">Er wordt nu een hersteltaak die u bekijken kunt door het openen van Hallo **taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="72b1d-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="72b1d-155">Nadat het Hallo herstellen is voltooid, kunt u controleren dat Hallo inhoud van uw volumes worden vervangen door de volumes van Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="72b1d-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="72b1d-156">![Video beschikbaar](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video beschikbaar**</span><span class="sxs-lookup"><span data-stu-id="72b1d-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="72b1d-157">toowatch een video die u laat zien hoe gebruikt u de Hallo klonen en herstellen van functies in StorSimple toorecover verwijderde bestanden, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="72b1d-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b1d-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72b1d-158">Next steps</span></span>
* <span data-ttu-id="72b1d-159">Meer informatie over hoe te[beheren StorSimple-volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="72b1d-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="72b1d-160">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="72b1d-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

