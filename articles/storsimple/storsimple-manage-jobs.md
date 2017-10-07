---
title: aaaView en beheren van taken StorSimple | Microsoft Docs
description: Hallo StorSimple Manager-servicepagina taken worden beschreven en hoe toouse het tootrack recente, huidige en geplande back-uptaken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a><span data-ttu-id="eaaf5-103">Hallo StorSimple Manager-service tooview gebruiken en beheren van StorSimple-taken</span><span class="sxs-lookup"><span data-stu-id="eaaf5-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="eaaf5-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="eaaf5-104">Overview</span></span>
<span data-ttu-id="eaaf5-105">Hallo **taken** pagina biedt één centrale portal voor weergeven en beheren van taken die zijn gestart op apparaten tooyour StorSimple Manager-service is verbonden.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="eaaf5-106">U kunt geplande, actieve voltooide en mislukte taken voor meerdere apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="eaaf5-107">Resultaten zijn in tabelvorm gepresenteerd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-107">Results are presented in a tabular format.</span></span> 

![Pagina taken](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="eaaf5-109">U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:</span><span class="sxs-lookup"><span data-stu-id="eaaf5-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="eaaf5-110">**Status** – taken kunnen worden uitgevoerd, geplande, is mislukt, voltooide, annuleren of geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="eaaf5-111">**Type** – taken kunnen worden gemaakt als gevolg van een geplande of een op aanvraag back-up (**duren back-**), klonen, een apparaat te herstellen of update-bewerking.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="eaaf5-112">**Apparaten** – taken zijn gestart op een bepaalde verbonden apparaat tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-112">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
* <span data-ttu-id="eaaf5-113">**Van en naar** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-113">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>

<span data-ttu-id="eaaf5-114">Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van de Hallo Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="eaaf5-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>

* <span data-ttu-id="eaaf5-115">**Type** : back-up, kloon, terugzetten, failover of update.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="eaaf5-116">**Status** – uitgevoerd, gepland, is mislukt, voltooid, geannuleerd of geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="eaaf5-117">**Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, een back-upbeleid of een apparaat.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="eaaf5-118">De taak van een kloon is gekoppeld aan een volume dat een geplande back-uptaak gekoppeld aan een back-upbeleid is.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="eaaf5-119">Een apparaat-taak is gemaakt als gevolg van een noodherstel (DR) of een herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="eaaf5-120">**Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-120">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="eaaf5-121">**Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-121">**Started On** – hello time when hello job was started.</span></span>
* <span data-ttu-id="eaaf5-122">**Voortgang** – Hallo percentage een actieve taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="eaaf5-123">Dit moet altijd 100% zijn voor een voltooide taak.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="eaaf5-124">Hallo-lijst met taken wordt elke 30 seconden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="eaaf5-125">U kunt Hallo op deze pagina van de volgende taak-gerelateerde activiteiten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="eaaf5-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="eaaf5-126">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="eaaf5-126">View job details</span></span>
* <span data-ttu-id="eaaf5-127">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="eaaf5-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="eaaf5-128">Details van de taak weergeven</span><span class="sxs-lookup"><span data-stu-id="eaaf5-128">View job details</span></span>
<span data-ttu-id="eaaf5-129">Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="eaaf5-130">taakdetails tooview</span><span class="sxs-lookup"><span data-stu-id="eaaf5-130">tooview job details</span></span>
1. <span data-ttu-id="eaaf5-131">Op Hallo **taken** pagina, Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="eaaf5-132">U kunt zoeken voor voltooid, uitvoeren of taken geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="eaaf5-133">Selecteer een taak.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-133">Select a job.</span></span>
3. <span data-ttu-id="eaaf5-134">Klik onder aan de pagina Hallo Hallo op **Details**.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="eaaf5-135">In Hallo **back-up taakdetails** in het dialoogvenster u Hallo status, details, tijdstatistieken en statistieken van de gegevens kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="eaaf5-136">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="eaaf5-136">Cancel a job</span></span>
<span data-ttu-id="eaaf5-137">Hallo te volgen stappen toocancel een actieve taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-137">Perform hello following steps toocancel a running job.</span></span>

### <a name="toocancel-a-job"></a><span data-ttu-id="eaaf5-138">een taak toocancel</span><span class="sxs-lookup"><span data-stu-id="eaaf5-138">toocancel a job</span></span>
1. <span data-ttu-id="eaaf5-139">Op Hallo **taken** pagina, Hallo actieve taken die u door het uitvoeren van een query met de juiste filters toocancel wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-139">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="eaaf5-140">Hallo taak selecteren.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-140">Select hello job.</span></span>
3. <span data-ttu-id="eaaf5-141">Klik onder aan de pagina Hallo Hallo op **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-141">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="eaaf5-142">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="eaaf5-143">Deze taak is nu geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="eaaf5-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaaf5-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eaaf5-144">Next steps</span></span>
* <span data-ttu-id="eaaf5-145">Meer informatie over hoe te[beheren van uw StorSimple-back-upbeleid](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="eaaf5-145">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="eaaf5-146">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="eaaf5-146">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

