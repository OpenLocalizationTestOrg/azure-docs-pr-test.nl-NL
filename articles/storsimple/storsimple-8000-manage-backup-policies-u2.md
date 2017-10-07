---
title: aaaManage StorSimple 8000 serie back-upbeleid | Microsoft Docs
description: Legt uit hoe Hallo Apparaatbeheer StorSimple-service toocreate gebruiken en handmatige back-ups, back-upschema en bewaren van back-up op een StorSimple 8000 series apparaat beheren.
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="df2ff-103">Hallo Apparaatbeheer StorSimple-service gebruiken in Azure portal toomanage back-upbeleid</span><span class="sxs-lookup"><span data-stu-id="df2ff-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="df2ff-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="df2ff-104">Overview</span></span>

<span data-ttu-id="df2ff-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple-apparaat Manager-service Hallo **back-up maken van beleid** blade toocontrol back-processen en het bewaren van de back-up voor uw StorSimple-volumes.</span><span class="sxs-lookup"><span data-stu-id="df2ff-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="df2ff-106">Ook wordt beschreven hoe toocomplete een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="df2ff-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="df2ff-107">Wanneer u back-up van een volume, kunt u toocreate kiezen een momentopname van een lokale of een cloudmomentopname van de.</span><span class="sxs-lookup"><span data-stu-id="df2ff-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="df2ff-108">Als u een back-up van een lokaal vastgemaakt volume, raden wij aan dat u opgeeft dat een cloudmomentopname.</span><span class="sxs-lookup"><span data-stu-id="df2ff-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="df2ff-109">Maken van een groot aantal lokale momentopnamen van een lokaal vastgemaakt volume samen met een gegevensset die een groot aantal verloop heeft resulteert in een situatie waarin u kan snel worden uitgevoerd buiten het lokale ruimte.</span><span class="sxs-lookup"><span data-stu-id="df2ff-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="df2ff-110">Als u ervoor tootake lokale momentopnamen kiest, raden wij minder dagelijkse momentopnamen tooback duren voordat de meest recente status hello, behouden voor een dag en verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="df2ff-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="df2ff-111">Wanneer u een cloud momentopname van een lokaal vastgemaakt volume, kopieert u alleen Hallo gewijzigd gegevens toohello cloud, waar het ontdubbeld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="df2ff-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="df2ff-112">blade Hallo back-upbeleid</span><span class="sxs-lookup"><span data-stu-id="df2ff-112">hello Backup policy blade</span></span>

<span data-ttu-id="df2ff-113">Hallo **back-up maken van beleid** blade voor uw StorSimple-apparaat kunt u back-upbeleid toomanage en planning van lokale en cloudmomentopnamen.</span><span class="sxs-lookup"><span data-stu-id="df2ff-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="df2ff-114">Back-upbeleid zijn gebruikte tooconfigure back-upschema en de back-up van de bewaarperiode voor een verzameling van volumes.</span><span class="sxs-lookup"><span data-stu-id="df2ff-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="df2ff-115">Back-upbeleid kunnen u tootake een momentopname van meerdere volumes tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="df2ff-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="df2ff-116">Dit betekent dat Hallo back-ups die zijn gemaakt door een back-upbeleid crashconsistent exemplaren.</span><span class="sxs-lookup"><span data-stu-id="df2ff-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="df2ff-117">Hallo back-upbeleid in tabelvorm aanbieding kunt ook u toofilter Hallo bestaande back-upbeleid door een of meer van de volgende velden Hallo:</span><span class="sxs-lookup"><span data-stu-id="df2ff-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="df2ff-118">**De naam van beleid** – hello naam gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="df2ff-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="df2ff-119">verschillende soorten beleid Hallo zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="df2ff-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="df2ff-120">Geplande beleidsregels die expliciet zijn gemaakt door gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="df2ff-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="df2ff-121">Beleidsregels die oorspronkelijk zijn gemaakt in Hallo StorSimple Snapshot Manager geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="df2ff-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="df2ff-122">Deze hebben een code die wordt beschreven Hallo StorSimple Snapshot Manager host die Hallo beleidsregels zijn geïmporteerd uit.</span><span class="sxs-lookup"><span data-stu-id="df2ff-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="df2ff-123">Automatische of standaard back-upbeleid zijn niet meer ingeschakeld bij Hallo volume maken.</span><span class="sxs-lookup"><span data-stu-id="df2ff-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="df2ff-124">**Laatste geslaagde back-up** – Hallo-datum en tijd van Hallo laatste geslaagde back-up die is uitgevoerd met dit beleid.</span><span class="sxs-lookup"><span data-stu-id="df2ff-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="df2ff-125">**Volgende back-up** – Hallo-datum en tijd van Hallo volgende geplande back-up die door dit beleid wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="df2ff-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="df2ff-126">**Volumes** – Hallo volumes die zijn gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="df2ff-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="df2ff-127">Alle Hallo volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="df2ff-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="df2ff-128">**Planningen** – aantal schema's die zijn gekoppeld aan de back-upbeleid Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="df2ff-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="df2ff-129">Hallo veelgebruikte bewerkingen die u voor back-upbeleid uitvoeren kunt zijn:</span><span class="sxs-lookup"><span data-stu-id="df2ff-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="df2ff-130">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="df2ff-130">Add a backup policy</span></span>
* <span data-ttu-id="df2ff-131">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="df2ff-131">Add or modify a schedule</span></span>
* <span data-ttu-id="df2ff-132">Toevoegen of verwijderen van een volume</span><span class="sxs-lookup"><span data-stu-id="df2ff-132">Add or remove a volume</span></span>
* <span data-ttu-id="df2ff-133">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="df2ff-133">Delete a backup policy</span></span>
* <span data-ttu-id="df2ff-134">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="df2ff-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="df2ff-135">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="df2ff-135">Add a backup policy</span></span>

<span data-ttu-id="df2ff-136">Toevoegen van een back-upbeleid tooautomatically planning uw back-ups.</span><span class="sxs-lookup"><span data-stu-id="df2ff-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="df2ff-137">Wanneer u een volume maakt, is er geen back-standaardbeleid die zijn gekoppeld aan het volume.</span><span class="sxs-lookup"><span data-stu-id="df2ff-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="df2ff-138">U moet tooadd en toewijzen van een back-upbeleid tooprotect volumegegevens.</span><span class="sxs-lookup"><span data-stu-id="df2ff-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="df2ff-139">Volgende stappen uit in Azure portal tooadd een back-upbeleid voor uw StorSimple-apparaat Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="df2ff-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="df2ff-140">Nadat u Hallo beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="df2ff-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="df2ff-141">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="df2ff-141">Add or modify a schedule</span></span>

<span data-ttu-id="df2ff-142">U kunt toevoegen of wijzigen van een planning die is aangesloten tooan bestaande back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="df2ff-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="df2ff-143">Uitvoeren van de volgende stappen uit in Azure portal tooadd Hallo Hallo of te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="df2ff-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="df2ff-144">Toevoegen of verwijderen van een volume</span><span class="sxs-lookup"><span data-stu-id="df2ff-144">Add or remove a volume</span></span>

<span data-ttu-id="df2ff-145">U kunt toevoegen of verwijderen van een volume toegewezen tooa back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="df2ff-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="df2ff-146">Volgende stappen uit in Azure portal tooadd Hallo Hallo uitvoeren of verwijderen van een volume.</span><span class="sxs-lookup"><span data-stu-id="df2ff-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="df2ff-147">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="df2ff-147">Delete a backup policy</span></span>

<span data-ttu-id="df2ff-148">Voer Hallo stappen te volgen in hello Azure portal toodelete een back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="df2ff-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="df2ff-149">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="df2ff-149">Take a manual backup</span></span>

<span data-ttu-id="df2ff-150">Hallo stappen te volgen in (hello Azure portal toocreate op aanvraag handmatige) back-up voor één volume uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="df2ff-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="df2ff-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df2ff-151">Next steps</span></span>

<span data-ttu-id="df2ff-152">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="df2ff-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

