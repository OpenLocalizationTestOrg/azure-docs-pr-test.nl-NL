---
title: aaaView en beheren van taken StorSimple | Microsoft Docs
description: Hallo StorSimple Manager-servicepagina taken worden beschreven en hoe toouse het tootrack recente, huidige en geplande back-uptaken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="062de-103">Hallo StorSimple Manager-service tooview gebruiken en beheren van StorSimple-taken (Update 2)</span><span class="sxs-lookup"><span data-stu-id="062de-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="062de-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="062de-104">Overview</span></span>
<span data-ttu-id="062de-105">Hallo **taken** pagina biedt één centrale portal voor weergeven en beheren van taken die zijn gestart op apparaten tooyour StorSimple Manager-service is verbonden.</span><span class="sxs-lookup"><span data-stu-id="062de-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="062de-106">U kunt geplande, actieve, voltooide, geannuleerde en mislukte taken voor meerdere apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="062de-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="062de-107">Resultaten zijn in tabelvorm gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="062de-107">Results are presented in a tabular format.</span></span> 

![Pagina taken](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="062de-109">U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:</span><span class="sxs-lookup"><span data-stu-id="062de-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="062de-110">**Status** – taken kunnen worden uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.</span><span class="sxs-lookup"><span data-stu-id="062de-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="062de-111">**Van en naar** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.</span><span class="sxs-lookup"><span data-stu-id="062de-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="062de-112">**Type** – Hallo taaktype kan worden back-up, handmatige back-up, herstel, kloon, apparaat-failover, lokaal vastgemaakt volume maakt, volume wijzigen, bijwerken en ondersteuning voor pakket- of virtuele apparaten inrichten.</span><span class="sxs-lookup"><span data-stu-id="062de-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="062de-113">**Apparaten** – taken zijn gestart op een bepaalde verbonden apparaat tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="062de-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="062de-114">Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van de Hallo Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="062de-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="062de-115">**Type** : back-up, handmatige back-up, herstel, kloon, apparaat-failover, lokaal vastgemaakt volume maakt, volume wijzigen, bijwerken en ondersteuning voor pakket- of virtuele apparaten inrichten.</span><span class="sxs-lookup"><span data-stu-id="062de-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="062de-116">**Status** – uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.</span><span class="sxs-lookup"><span data-stu-id="062de-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="062de-117">**Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, een back-upbeleid of een apparaat.</span><span class="sxs-lookup"><span data-stu-id="062de-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="062de-118">De taak van een kloon is bijvoorbeeld gekoppeld aan een volume dat een geplande back-uptaak gekoppeld aan een back-upbeleid is.</span><span class="sxs-lookup"><span data-stu-id="062de-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="062de-119">Een apparaat-taak is gemaakt als gevolg van een noodherstel (DR) of een herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="062de-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="062de-120">**Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="062de-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="062de-121">**Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="062de-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="062de-122">**Voortgang** – Hallo percentage een actieve taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="062de-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="062de-123">Dit moet altijd 100% zijn voor een voltooide taak.</span><span class="sxs-lookup"><span data-stu-id="062de-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="062de-124">Hallo-lijst met taken wordt elke 30 seconden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="062de-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="062de-125">U kunt Hallo op deze pagina van de volgende taak-gerelateerde activiteiten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="062de-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="062de-126">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="062de-126">View job details</span></span>
* <span data-ttu-id="062de-127">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="062de-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="062de-128">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="062de-128">View job details</span></span>
<span data-ttu-id="062de-129">Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="062de-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="062de-130">taakdetails tooview</span><span class="sxs-lookup"><span data-stu-id="062de-130">tooview job details</span></span>
1. <span data-ttu-id="062de-131">Op Hallo **taken** pagina, Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters weergegeven.</span><span class="sxs-lookup"><span data-stu-id="062de-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="062de-132">U kunt zoeken voor voltooid, uitvoeren of taken geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="062de-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="062de-133">Selecteer een taak.</span><span class="sxs-lookup"><span data-stu-id="062de-133">Select a job.</span></span>
3. <span data-ttu-id="062de-134">Klik onder aan de pagina Hallo Hallo op **Details**.</span><span class="sxs-lookup"><span data-stu-id="062de-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="062de-135">In Hallo **back-up taakdetails** in het dialoogvenster u Hallo status, details, tijdstatistieken en statistieken van de gegevens kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="062de-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![De pagina details taak](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="062de-137">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="062de-137">Cancel a job</span></span>
<span data-ttu-id="062de-138">Hallo te volgen stappen toocancel een actieve taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="062de-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="062de-139">Sommige taken, zoals een volumetype toochange Hallo volume te wijzigen of het uitbreiden van een volume kunnen niet worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="062de-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="062de-140">een taak toocancel</span><span class="sxs-lookup"><span data-stu-id="062de-140">toocancel a job</span></span>
1. <span data-ttu-id="062de-141">Op Hallo **taken** pagina, Hallo actieve taken die u door het uitvoeren van een query met de juiste filters toocancel wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="062de-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="062de-142">Hallo taak selecteren.</span><span class="sxs-lookup"><span data-stu-id="062de-142">Select hello job.</span></span>
3. <span data-ttu-id="062de-143">Klik onder aan de pagina Hallo Hallo op **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="062de-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="062de-144">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="062de-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="062de-145">Deze taak is nu geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="062de-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="062de-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="062de-146">Next steps</span></span>
* <span data-ttu-id="062de-147">Meer informatie over hoe te[beheren van uw StorSimple-back-upbeleid](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="062de-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="062de-148">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="062de-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

