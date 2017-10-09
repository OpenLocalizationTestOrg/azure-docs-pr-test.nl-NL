---
title: aaaManage uw StorSimple-back-upbeleid | Microsoft Docs
description: Legt uit hoe Hallo StorSimple Manager-service toocreate gebruiken en beheren van handmatige back-ups, back-upschema en bewaren van back-up.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="6cef3-103">Hallo StorSimple Manager-service toomanage back-upbeleid (Update 2) gebruiken</span><span class="sxs-lookup"><span data-stu-id="6cef3-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="6cef3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6cef3-104">Overview</span></span>
<span data-ttu-id="6cef3-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager-service Hallo **back-upbeleid** pagina toocontrol back-processen en het bewaren van de back-up voor uw StorSimple-volumes.</span><span class="sxs-lookup"><span data-stu-id="6cef3-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="6cef3-106">Ook wordt beschreven hoe toocomplete een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="6cef3-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="6cef3-107">Wanneer u back-up van een volume, kunt u toocreate kiezen een momentopname van een lokale of een cloudmomentopname van de.</span><span class="sxs-lookup"><span data-stu-id="6cef3-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="6cef3-108">Als u een back-up van een lokaal vastgemaakt volume, raden wij aan dat u opgeeft dat een cloudmomentopname.</span><span class="sxs-lookup"><span data-stu-id="6cef3-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="6cef3-109">Maken van een groot aantal lokale momentopnamen van een lokaal vastgemaakt volume samen met een gegevensset die een groot aantal verloop heeft resulteert in een situatie waarin u kan snel worden uitgevoerd buiten het lokale ruimte.</span><span class="sxs-lookup"><span data-stu-id="6cef3-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="6cef3-110">Als u ervoor tootake lokale momentopnamen kiest, raden wij minder dagelijkse momentopnamen tooback duren voordat de meest recente status hello, behouden voor een dag en verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="6cef3-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="6cef3-111">Wanneer u een cloud momentopname van een lokaal vastgemaakt volume, kopieert u alleen Hallo gewijzigd gegevens toohello cloud, waar het ontdubbeld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="6cef3-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="6cef3-112">Hallo back-upbeleid pagina</span><span class="sxs-lookup"><span data-stu-id="6cef3-112">hello Backup Policies page</span></span>
<span data-ttu-id="6cef3-113">Hallo **back-upbeleid** pagina kunt u back-upbeleid toomanage en planning van lokale en cloudmomentopnamen.</span><span class="sxs-lookup"><span data-stu-id="6cef3-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="6cef3-114">(Back-upbeleid zijn gebruikte tooconfigure back-upschema's en het bewaren van de back-up voor een verzameling van volumes). Back-upbeleid kunnen u tootake een momentopname van meerdere volumes tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="6cef3-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="6cef3-115">Dit betekent dat Hallo back-ups die zijn gemaakt door een back-upbeleid crashconsistent exemplaren.</span><span class="sxs-lookup"><span data-stu-id="6cef3-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="6cef3-116">Hallo **back-upbeleid** pagina ziet u back-upbeleid hello, hun typen, volumes Hallo die zijn gekoppeld, Hallo aantal back-ups behouden en Hallo optie tooenable deze beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="6cef3-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="6cef3-117">Hallo **back-upbeleid** pagina kunt u ook toofilter Hallo bestaande back-upbeleid door een of meer van de volgende velden Hallo:</span><span class="sxs-lookup"><span data-stu-id="6cef3-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="6cef3-118">**De naam van beleid** – hello naam gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="6cef3-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="6cef3-119">verschillende soorten beleid Hallo zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="6cef3-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="6cef3-120">Geplande beleidsregels die expliciet zijn gemaakt door gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cef3-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="6cef3-121">Automatische beleidsregels die worden gemaakt wanneer Hallo standaardback-up voor deze optie volume gelijktijdig Hallo met maken van volumes is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6cef3-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="6cef3-122">Deze beleidsregels worden benoemd als *VolumeName*_Standaard waar *VolumeName* toohello-naam van het StorSimple-volume is geconfigureerd door de gebruiker in de klassieke Azure-portal Hallo HALLO hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="6cef3-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="6cef3-123">Hallo automatische beleid resulteert in dagelijkse cloudmomentopnamen beginnen bij 22.30 tijd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="6cef3-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="6cef3-124">Beleidsregels die oorspronkelijk zijn gemaakt in Hallo StorSimple Snapshot Manager geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="6cef3-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="6cef3-125">Deze hebben een code die wordt beschreven Hallo StorSimple Snapshot Manager host die Hallo beleidsregels zijn geïmporteerd uit.</span><span class="sxs-lookup"><span data-stu-id="6cef3-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="6cef3-126">**Volumes** – Hallo volumes die zijn gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="6cef3-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="6cef3-127">Alle Hallo volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6cef3-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="6cef3-128">**Laatste geslaagde back-up** – Hallo-datum en tijd van Hallo laatste geslaagde back-up die is uitgevoerd met dit beleid.</span><span class="sxs-lookup"><span data-stu-id="6cef3-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="6cef3-129">**Volgende back-up** – Hallo-datum en tijd van Hallo volgende geplande back-up die door dit beleid wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6cef3-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="6cef3-130">**Planningen** – aantal schema's die zijn gekoppeld aan de back-upbeleid Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cef3-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="6cef3-131">Hallo veelgebruikte bewerkingen die u op deze pagina uitvoeren kunt zijn:</span><span class="sxs-lookup"><span data-stu-id="6cef3-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="6cef3-132">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="6cef3-132">Add a backup policy</span></span> 
* <span data-ttu-id="6cef3-133">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="6cef3-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="6cef3-134">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="6cef3-134">Delete a backup policy</span></span> 
* <span data-ttu-id="6cef3-135">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="6cef3-135">Take a manual backup</span></span> 
* <span data-ttu-id="6cef3-136">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="6cef3-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="6cef3-137">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="6cef3-137">Add a backup policy</span></span>
<span data-ttu-id="6cef3-138">Toevoegen van een back-upbeleid tooautomatically planning uw back-ups.</span><span class="sxs-lookup"><span data-stu-id="6cef3-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="6cef3-139">Voer Hallo stappen te volgen in hello Azure classic portal tooadd een back-upbeleid voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6cef3-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="6cef3-140">Nadat u Hallo beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="6cef3-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="6cef3-141">![Video beschikbaar](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video beschikbaar**</span><span class="sxs-lookup"><span data-stu-id="6cef3-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="6cef3-142">toowatch een video die u laat zien hoe toocreate een lokaal of in de cloud back-up-beleid, klikt u op [hier](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="6cef3-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="6cef3-143">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="6cef3-143">Add or modify a schedule</span></span>
<span data-ttu-id="6cef3-144">U kunt toevoegen of wijzigen van een planning die is aangesloten tooan bestaande back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6cef3-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="6cef3-145">Hallo stappen te volgen in hello Azure classic portal tooadd uitvoeren of een schema wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6cef3-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="6cef3-146">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="6cef3-146">Delete a backup policy</span></span>
<span data-ttu-id="6cef3-147">Voer Hallo stappen te volgen in hello Azure classic portal toodelete een back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6cef3-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="6cef3-148">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="6cef3-148">Take a manual backup</span></span>
<span data-ttu-id="6cef3-149">Hallo stappen te volgen in (hello Azure classic portal toocreate op aanvraag handmatige) back-up voor één volume uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6cef3-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="6cef3-150">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="6cef3-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="6cef3-151">Hallo stappen te volgen in hello Azure classic portal toocreate een aangepaste back-upbeleid met meerdere volumes en schema's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6cef3-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="6cef3-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cef3-152">Next steps</span></span>
<span data-ttu-id="6cef3-153">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6cef3-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

