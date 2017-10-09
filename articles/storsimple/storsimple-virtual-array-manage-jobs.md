---
title: aaaView en beheren van virtuele StorSimple-matrix taken | Microsoft Docs
description: Hallo StorSimple Apparaatbeheer servicepagina taken worden beschreven en hoe toouse het tootrack recente en de huidige taken voor Hallo virtuele StorSimple-matrix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="4f0ce-103">Hallo Apparaatbeheer StorSimple-service tooview taken gebruiken voor Hallo virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="4f0ce-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="4f0ce-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4f0ce-104">Overview</span></span>
<span data-ttu-id="4f0ce-105">Hallo **taken** blade biedt één centrale portal voor het weergeven en beheren van taken die zijn gestart op de virtuele matrices die verbonden tooyour StorSimple-apparaat Manager-service zijn.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4f0ce-106">U kunt actieve voltooide en mislukte taken voor meerdere virtuele apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="4f0ce-107">Resultaten zijn in tabelvorm gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-107">Results are presented in a tabular format.</span></span>

![Blade taken](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="4f0ce-109">U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:</span><span class="sxs-lookup"><span data-stu-id="4f0ce-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="4f0ce-110">**Tijdsbereik** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="4f0ce-111">**Apparaten** – taken zijn gestart op een specifiek apparaat verbonden tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="4f0ce-112">Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="4f0ce-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="4f0ce-113">**Naam** – Hallo taaknaam mag **alle**, **back-up**, **kloon**, **failover**, **updates downloaden** , of **updates installeren**.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="4f0ce-114">**Status** – taken kunnen worden **alle**, **Bezig**, **geslaagd**, of **mislukt**, of **geannuleerd**.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="4f0ce-115">**Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, share of apparaat.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="4f0ce-116">**Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="4f0ce-117">**Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="4f0ce-118">**Duur** – hello duur voor op welke Hallo-taak werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="4f0ce-119">**Status** – u kunt zoeken naar alle, uitgevoerd, is voltooid of mislukte taken.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="4f0ce-120">**Taaktype** – Hallo taaktype worden all, back-up, herstel, failover, downloaden van updates of updates installeren.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="4f0ce-121">Hallo-lijst met taken wordt elke 30 seconden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="4f0ce-122">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="4f0ce-122">View job details</span></span>
<span data-ttu-id="4f0ce-123">Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="4f0ce-124">taakdetails tooview</span><span class="sxs-lookup"><span data-stu-id="4f0ce-124">tooview job details</span></span>
1. <span data-ttu-id="4f0ce-125">Op Hallo **taken** blade, weergave Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="4f0ce-126">U kunt zoeken naar is voltooid of actieve taken.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="4f0ce-127">Selecteer een taak uit Hallo in tabelvorm lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Blade taak](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="4f0ce-129">Klik onder aan de pagina Hallo Hallo op **Details**.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="4f0ce-130">In Hallo **Details** in het dialoogvenster vindt u de status, details en statistieken.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="4f0ce-131">Hallo volgende afbeelding toont een voorbeeld van Hallo **back-up taakdetails** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Taakdetails](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="4f0ce-133">Taakfouten wanneer Hallo virtuele machine in Hallo hypervisor is onderbroken</span><span class="sxs-lookup"><span data-stu-id="4f0ce-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="4f0ce-134">Wanneer een taak wordt uitgevoerd op uw virtuele StorSimple-matrix en het Hallo-apparaat (virtuele machine is ingericht in de hypervisor) voor meer dan 15 minuten is onderbroken, Hallo taak mislukt.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="4f0ce-135">Dit is vanwege tooyour virtuele StorSimple-matrix tijd wordt niet gesynchroniseerd met de Hallo Microsoft Azure-tijd.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="4f0ce-136">U ziet Hallo volgende fout: "de tijd op het apparaat is niet gesynchroniseerd met Microsoft Azure-tijd Hallo door meer dan 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="4f0ce-137">Zorg ervoor dat Hallo hypervisor en Hallo apparaat tijden zijn gesynchroniseerd met een clientverzoeken NTP.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="4f0ce-138">Controleer of er geen verbindingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="4f0ce-139">problemen met de netwerkverbinding van tootroubleshoot diagnostische tests uitvoeren van Hallo lokale webgebruikersinterface van uw virtuele apparaat."</span><span class="sxs-lookup"><span data-stu-id="4f0ce-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="4f0ce-140">Deze fouten van toepassing toobackup, herstellen, bijwerken en failover-taken.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="4f0ce-141">Als uw virtuele machine is ingericht in Hyper-V, synchroniseert Hallo machine tijd uiteindelijk met de hypervisor.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="4f0ce-142">Wanneer dit gebeurt, kunt u de taak opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="4f0ce-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f0ce-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f0ce-143">Next steps</span></span>
<span data-ttu-id="4f0ce-144">[Meer informatie over hoe toouse Hallo lokale web UI tooadminister uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="4f0ce-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

