---
title: Beheren van uw StorSimple-back-upbeleid | Microsoft Docs
description: Legt uit hoe u kunt de StorSimple Manager-service maken en beheren van handmatige back-ups en back-upschema's bewaren van back-up.
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
ms.openlocfilehash: 5448247428ab96887470c6b53f7a9b3dcd9238f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="59bc9-103">De StorSimple Manager-service gebruiken voor het beheren van back-upbeleid (Update 2)</span><span class="sxs-lookup"><span data-stu-id="59bc9-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="59bc9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="59bc9-104">Overview</span></span>
<span data-ttu-id="59bc9-105">Deze zelfstudie wordt uitgelegd hoe u de StorSimple Manager-service **back-upbeleid** pagina om back-processen en bewaren van back-up voor uw StorSimple-volumes te beheren.</span><span class="sxs-lookup"><span data-stu-id="59bc9-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="59bc9-106">Ook wordt beschreven hoe u een handmatige back-up uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="59bc9-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="59bc9-107">Wanneer u back-up van een volume, kunt u kiezen voor het maken van een momentopname van een lokale of een cloudmomentopname van de.</span><span class="sxs-lookup"><span data-stu-id="59bc9-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="59bc9-108">Als u een back-up van een lokaal vastgemaakt volume, raden wij aan dat u opgeeft dat een cloudmomentopname.</span><span class="sxs-lookup"><span data-stu-id="59bc9-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="59bc9-109">Maken van een groot aantal lokale momentopnamen van een lokaal vastgemaakt volume samen met een gegevensset die een groot aantal verloop heeft resulteert in een situatie waarin u kan snel worden uitgevoerd buiten het lokale ruimte.</span><span class="sxs-lookup"><span data-stu-id="59bc9-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="59bc9-110">Als u kiest voor het lokale momentopnamen, raden wij u momentopnamen minder dagelijkse back-up van de meest recente status behouden voor een dag en verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="59bc9-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="59bc9-111">Wanneer u een cloudmomentopname van een lokaal vastgemaakt volume maakt, kunt u alleen de gewijzigde gegevens kopiëren naar de cloud, waar het ontdubbeld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="59bc9-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="59bc9-112">De pagina back-upbeleid</span><span class="sxs-lookup"><span data-stu-id="59bc9-112">The Backup Policies page</span></span>
<span data-ttu-id="59bc9-113">De **back-upbeleid** op de pagina kunt u back-upbeleid beheren en plannen van lokale en cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="59bc9-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="59bc9-114">(Back-upbeleid worden gebruikt om back-upschema en de back-up van de bewaarperiode voor een verzameling van volumes te configureren.) Back-upbeleid kunnen u een momentopname van meerdere volumes tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="59bc9-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="59bc9-115">Dit betekent dat de back-ups gemaakt door een back-upbeleid crashconsistent exemplaren.</span><span class="sxs-lookup"><span data-stu-id="59bc9-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="59bc9-116">De **back-upbeleid** pagina geeft een lijst van de back-upbeleid, de typen, de gekoppelde volumes, het aantal back-ups behouden en de optie voor het inschakelen van deze beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="59bc9-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="59bc9-117">De **back-upbeleid** op de pagina kunt u het bestaande back-upbeleid door een of meer van de volgende velden te filteren:</span><span class="sxs-lookup"><span data-stu-id="59bc9-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="59bc9-118">**De naam van beleid** : de naam gekoppeld aan het beleid.</span><span class="sxs-lookup"><span data-stu-id="59bc9-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="59bc9-119">De verschillende soorten beleid zijn:</span><span class="sxs-lookup"><span data-stu-id="59bc9-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="59bc9-120">Geplande beleidsregels die expliciet zijn gemaakt door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="59bc9-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="59bc9-121">Automatische beleidsregels die worden gemaakt wanneer de standaardback-up voor deze optie volume is ingeschakeld op het moment van volume maken.</span><span class="sxs-lookup"><span data-stu-id="59bc9-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="59bc9-122">Deze beleidsregels worden benoemd als *VolumeName*_Standaard waar *VolumeName* verwijst naar de naam van het StorSimple-volume dat is geconfigureerd door de gebruiker in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59bc9-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="59bc9-123">De automatische beleid resulteert in dagelijkse cloudmomentopnamen beginnen bij 22.30 tijd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="59bc9-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="59bc9-124">Geïmporteerde beleid, StorSimple Snapshot Manager oorspronkelijk zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59bc9-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="59bc9-125">Deze hebben een code die de StorSimple Snapshot Manager-host die de beleidsregels zijn geïmporteerd beschrijft uit.</span><span class="sxs-lookup"><span data-stu-id="59bc9-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="59bc9-126">**Volumes** – de volumes die zijn gekoppeld aan het beleid.</span><span class="sxs-lookup"><span data-stu-id="59bc9-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="59bc9-127">Alle volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59bc9-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="59bc9-128">**Laatste geslaagde back-up** – de datum en tijd van de laatste goede back-up die is uitgevoerd met dit beleid.</span><span class="sxs-lookup"><span data-stu-id="59bc9-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="59bc9-129">**Volgende back-up** – de datum en tijd van de volgende geplande back-up die door dit beleid wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="59bc9-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="59bc9-130">**Planningen** – het nummer van schema's die zijn gekoppeld aan de back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="59bc9-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="59bc9-131">De veelgebruikte bewerkingen die u op deze pagina uitvoeren kunt zijn:</span><span class="sxs-lookup"><span data-stu-id="59bc9-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="59bc9-132">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="59bc9-132">Add a backup policy</span></span> 
* <span data-ttu-id="59bc9-133">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="59bc9-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="59bc9-134">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="59bc9-134">Delete a backup policy</span></span> 
* <span data-ttu-id="59bc9-135">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="59bc9-135">Take a manual backup</span></span> 
* <span data-ttu-id="59bc9-136">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="59bc9-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="59bc9-137">Een back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="59bc9-137">Add a backup policy</span></span>
<span data-ttu-id="59bc9-138">Toevoegen van een back-upbeleid automatisch uw back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="59bc9-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="59bc9-139">Voer de volgende stappen uit in de klassieke Azure portal een back-upbeleid voor uw StorSimple-apparaat toevoegen.</span><span class="sxs-lookup"><span data-stu-id="59bc9-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="59bc9-140">Nadat u het beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="59bc9-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="59bc9-141">![Video beschikbaar](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video beschikbaar**</span><span class="sxs-lookup"><span data-stu-id="59bc9-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="59bc9-142">Als u wilt een video over het maken van een lokale of back-upbeleid cloud bekijken, klikt u op [hier](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="59bc9-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="59bc9-143">Toevoegen of wijzigen van een planning</span><span class="sxs-lookup"><span data-stu-id="59bc9-143">Add or modify a schedule</span></span>
<span data-ttu-id="59bc9-144">U kunt toevoegen of wijzigen van een schema dat is gekoppeld aan een bestaande back-upbeleid op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="59bc9-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="59bc9-145">Voer de volgende stappen uit in de klassieke Azure portal toevoegen of wijzigen van een planning.</span><span class="sxs-lookup"><span data-stu-id="59bc9-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="59bc9-146">Een back-upbeleid te verwijderen</span><span class="sxs-lookup"><span data-stu-id="59bc9-146">Delete a backup policy</span></span>
<span data-ttu-id="59bc9-147">Voer de volgende stappen uit in de klassieke Azure portal een back-upbeleid op uw StorSimple-apparaat verwijderen.</span><span class="sxs-lookup"><span data-stu-id="59bc9-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="59bc9-148">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="59bc9-148">Take a manual backup</span></span>
<span data-ttu-id="59bc9-149">Voer de volgende stappen uit in de klassieke Azure portal voor het maken van een op aanvraag back-up (handmatige) voor één volume.</span><span class="sxs-lookup"><span data-stu-id="59bc9-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="59bc9-150">Een aangepaste back-upbeleid maken met meerdere volumes en schema 's</span><span class="sxs-lookup"><span data-stu-id="59bc9-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="59bc9-151">De volgende stappen uitvoeren in de klassieke Azure portal voor het maken van een aangepaste back-upbeleid met meerdere volumes en schema's.</span><span class="sxs-lookup"><span data-stu-id="59bc9-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="59bc9-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59bc9-152">Next steps</span></span>
<span data-ttu-id="59bc9-153">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="59bc9-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

