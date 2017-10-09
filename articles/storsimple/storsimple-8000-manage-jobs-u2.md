---
title: aaaView en beheren van taken voor StorSimple 8000 serie | Microsoft Docs
description: Beschrijving van de blade taken Hallo Apparaatbeheer StorSimple-service en hoe toouse het tootrack recente, huidige en geplande back-uptaken.
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="a352e-103">Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van taken (Update 3 en hoger)</span><span class="sxs-lookup"><span data-stu-id="a352e-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="a352e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a352e-104">Overview</span></span>
<span data-ttu-id="a352e-105">Hallo **taken** blade biedt één centrale portal voor het weergeven en beheren van taken die zijn gestart op apparaten tooyour StorSimple-apparaat Manager-service is verbonden.</span><span class="sxs-lookup"><span data-stu-id="a352e-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a352e-106">U kunt geplande, actieve, voltooide, geannuleerde en mislukte taken voor meerdere apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="a352e-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="a352e-107">Resultaten zijn in tabelvorm gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="a352e-107">Results are presented in a tabular format.</span></span>

![Blade taken](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="a352e-109">U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:</span><span class="sxs-lookup"><span data-stu-id="a352e-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a352e-110">**Status** – taken kunnen worden uitgevoerd, is voltooid, geannuleerd, is mislukt, annuleren of voltooid met fouten.</span><span class="sxs-lookup"><span data-stu-id="a352e-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="a352e-111">**Tijdsbereik** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.</span><span class="sxs-lookup"><span data-stu-id="a352e-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="a352e-112">Hallo-bereik is 1 uur, afgelopen 24 uur, afgelopen 7 dagen, afgelopen 30 dagen, afgelopen jaar of aangepaste datum uit het verleden.</span><span class="sxs-lookup"><span data-stu-id="a352e-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="a352e-113">**Type** – Hallo taaktype mag geplande back-up, handmatige back-up, herstel back-up, volume klonen, failover volumecontainers, lokaal vastgemaakt volume maakt, volume wijzigen, updates installeren, verzamelen van Ondersteuningslogboeken en cloud toestel maken.</span><span class="sxs-lookup"><span data-stu-id="a352e-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="a352e-114">**Apparaten** – taken zijn gestart op een bepaalde verbonden apparaat tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="a352e-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="a352e-115">Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van de Hallo Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="a352e-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="a352e-116">**Naam** – geplande back-up, handmatige back-up en terugzetten van back-up, kloon volume, failover volumecontainers, lokaal vastgemaakt volume maakt, volume wijzigen, updates installeren, verzamelen van Ondersteuningslogboeken of cloud toestel maken.</span><span class="sxs-lookup"><span data-stu-id="a352e-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="a352e-117">**Status** – uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.</span><span class="sxs-lookup"><span data-stu-id="a352e-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="a352e-118">**Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, een back-upbeleid of een apparaat.</span><span class="sxs-lookup"><span data-stu-id="a352e-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="a352e-119">De taak van een kloon is bijvoorbeeld gekoppeld aan een volume dat een geplande back-uptaak gekoppeld aan een back-upbeleid is.</span><span class="sxs-lookup"><span data-stu-id="a352e-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="a352e-120">Een apparaat-taak is gemaakt als gevolg van een noodherstel (DR) of een herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="a352e-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="a352e-121">**Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="a352e-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="a352e-122">**Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="a352e-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="a352e-123">**Duur** – Hallo tijd vereist toocomplete Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="a352e-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="a352e-124">Hallo-lijst met taken wordt elke 30 seconden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="a352e-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="a352e-125">U kunt Hallo op deze pagina van de volgende taak-gerelateerde activiteiten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a352e-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="a352e-126">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="a352e-126">View job details</span></span>
* <span data-ttu-id="a352e-127">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="a352e-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a352e-128">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="a352e-128">View job details</span></span>
<span data-ttu-id="a352e-129">Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a352e-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="a352e-130">taakdetails tooview</span><span class="sxs-lookup"><span data-stu-id="a352e-130">tooview job details</span></span>
1. <span data-ttu-id="a352e-131">Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **taken**.</span><span class="sxs-lookup"><span data-stu-id="a352e-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="a352e-132">In Hallo **taken** blade, weergave Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters.</span><span class="sxs-lookup"><span data-stu-id="a352e-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a352e-133">U kunt zoeken voor voltooid, uitvoeren of taken geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="a352e-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Blade taak](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="a352e-135">Selecteer en klik op een taak.</span><span class="sxs-lookup"><span data-stu-id="a352e-135">Select and click a job.</span></span>

    ![Blade taak](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="a352e-137">U kunt Hallo job details blade Hallo status, details, tijdstatistieken en statistieken van de gegevens weergeven.</span><span class="sxs-lookup"><span data-stu-id="a352e-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Taakdetails](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="a352e-139">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="a352e-139">Cancel a job</span></span>
<span data-ttu-id="a352e-140">Hallo te volgen stappen toocancel een actieve taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a352e-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="a352e-141">Sommige taken, zoals een volumetype toochange Hallo volume te wijzigen of het uitbreiden van een volume kunnen niet worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="a352e-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="a352e-142">een taak toocancel</span><span class="sxs-lookup"><span data-stu-id="a352e-142">toocancel a job</span></span>
1. <span data-ttu-id="a352e-143">Op Hallo **taken** pagina, Hallo actieve taken die u door het uitvoeren van een query met de juiste filters toocancel wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="a352e-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="a352e-144">Hallo taak selecteren.</span><span class="sxs-lookup"><span data-stu-id="a352e-144">Select hello job.</span></span>

2. <span data-ttu-id="a352e-145">Met de rechtermuisknop op Hallo geselecteerde taak tooinvoke Hallo-contextmenu en klik op **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="a352e-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Taakdetails](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="a352e-147">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a352e-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="a352e-148">Deze taak is nu geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="a352e-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a352e-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a352e-149">Next steps</span></span>
* <span data-ttu-id="a352e-150">Meer informatie over hoe te[beheren van uw StorSimple-back-upbeleid](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="a352e-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="a352e-151">Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a352e-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

