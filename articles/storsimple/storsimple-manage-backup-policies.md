---
title: aaaManage uw StorSimple-back-upbeleid | Microsoft Docs
description: Legt uit hoe Hallo StorSimple Manager-service toocreate gebruiken en beheren van handmatige back-ups, back-upschema en bewaren van back-up.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="85637-103">Hallo StorSimple Manager-service toomanage back-upbeleid gebruiken</span><span class="sxs-lookup"><span data-stu-id="85637-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="85637-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="85637-104">Overview</span></span>
<span data-ttu-id="85637-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager-service Hallo **back-upbeleid** pagina toocontrol back-processen en het bewaren van de back-up voor uw StorSimple-volumes.</span><span class="sxs-lookup"><span data-stu-id="85637-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="85637-106">Ook wordt beschreven hoe toocomplete een handmatige back-up.</span><span class="sxs-lookup"><span data-stu-id="85637-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="85637-107">Hallo **back-upbeleid** pagina kunt u back-upbeleid toomanage en planning van lokale en cloudmomentopnamen.</span><span class="sxs-lookup"><span data-stu-id="85637-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="85637-108">(Back-upbeleid zijn gebruikte tooconfigure back-upschema's en het bewaren van de back-up voor een verzameling van volumes). Back-upbeleid kunnen u tootake een momentopname van meerdere volumes tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="85637-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="85637-109">Dit betekent dat Hallo back-ups die zijn gemaakt door een back-upbeleid crashconsistent exemplaren.</span><span class="sxs-lookup"><span data-stu-id="85637-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="85637-110">Deze pagina bevat Hallo back-upbeleid, hun typen, volumes Hallo die zijn gekoppeld, Hallo aantal back-ups behouden en Hallo optie tooenable deze beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="85637-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="85637-111">Hallo **back-upbeleid** pagina kunt u ook toofilter Hallo bestaande back-upbeleid door een of meer van de volgende velden Hallo:</span><span class="sxs-lookup"><span data-stu-id="85637-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="85637-112">**De naam van beleid** – hello naam gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="85637-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="85637-113">verschillende soorten beleid Hallo zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="85637-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="85637-114">Geplande beleidsregels die expliciet zijn gemaakt door gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="85637-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="85637-115">Automatische beleidsregels die worden gemaakt wanneer Hallo standaardback-up voor deze optie volume gelijktijdig Hallo met maken van volumes is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="85637-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="85637-116">Deze beleidsregels zijn benoemde als VolumeName_Default waarbij volumenaam toohello-naam van het StorSimple-volume is geconfigureerd door de gebruiker in de klassieke Azure-portal Hallo HALLO hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="85637-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="85637-117">Hallo automatische beleid resulteert in dagelijkse cloudmomentopnamen beginnen bij 22.30 tijd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="85637-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="85637-118">Beleidsregels die oorspronkelijk zijn gemaakt in Hallo StorSimple Snapshot Manager geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="85637-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="85637-119">Deze hebben een code die wordt beschreven Hallo StorSimple Snapshot Manager host die Hallo beleidsregels zijn geïmporteerd uit.</span><span class="sxs-lookup"><span data-stu-id="85637-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="85637-120">**Volumes** – Hallo volumes die zijn gekoppeld aan het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="85637-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="85637-121">Alle Hallo volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="85637-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="85637-122">**Laatste geslaagde back-up** – Hallo-datum en tijd van Hallo laatste geslaagde back-up die is uitgevoerd met dit beleid.</span><span class="sxs-lookup"><span data-stu-id="85637-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="85637-123">**Volgende back-up** – Hallo-datum en tijd van Hallo volgende geplande back-up die door dit beleid wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="85637-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="85637-124">**Planningen** – aantal schema's die zijn gekoppeld aan de back-upbeleid Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="85637-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="85637-125">Hallo veelgebruikte bewerkingen die u op deze pagina uitvoeren kunt zijn:</span><span class="sxs-lookup"><span data-stu-id="85637-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="85637-126">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="85637-126">Add a backup policy</span></span> 
* <span data-ttu-id="85637-127">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="85637-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="85637-128">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="85637-128">Delete a backup policy</span></span> 
* <span data-ttu-id="85637-129">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="85637-129">Take a manual backup</span></span> 
* <span data-ttu-id="85637-130">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="85637-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="85637-131">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="85637-131">Add a backup policy</span></span>
<span data-ttu-id="85637-132">Toevoegen van een back-upbeleid tooautomatically planning uw back-ups.</span><span class="sxs-lookup"><span data-stu-id="85637-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="85637-133">Voer Hallo stappen te volgen in hello Azure classic portal tooadd een back-upbeleid voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85637-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="85637-134">Nadat u Hallo beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="85637-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="85637-135">![Video beschikbaar](./media/storsimple-manage-backup-policies/Video_icon.png) **Video beschikbaar**</span><span class="sxs-lookup"><span data-stu-id="85637-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="85637-136">toowatch een video die u laat zien hoe toocreate een lokaal of in de cloud back-up-beleid, klikt u op [hier](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="85637-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="85637-137">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="85637-137">Add or modify a schedule</span></span>
<span data-ttu-id="85637-138">U kunt toevoegen of wijzigen van een planning die is aangesloten tooan bestaande back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85637-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="85637-139">Hallo stappen te volgen in hello Azure classic portal tooadd uitvoeren of een schema wijzigen.</span><span class="sxs-lookup"><span data-stu-id="85637-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="85637-140">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="85637-140">Delete a backup policy</span></span>
<span data-ttu-id="85637-141">Voer Hallo stappen te volgen in hello Azure classic portal toodelete een back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="85637-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="85637-142">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="85637-142">Take a manual backup</span></span>
<span data-ttu-id="85637-143">Hallo stappen te volgen in (hello Azure classic portal toocreate op aanvraag handmatige) back-up voor één volume uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="85637-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="85637-144">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="85637-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="85637-145">Hallo stappen te volgen in hello Azure classic portal toocreate een aangepaste back-upbeleid met meerdere volumes en schema's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="85637-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="85637-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85637-146">Next steps</span></span>
<span data-ttu-id="85637-147">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="85637-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

