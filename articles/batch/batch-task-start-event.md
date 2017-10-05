---
title: Azure Batch-taak startgebeurtenis | Microsoft Docs
description: Naslaginformatie voor Batch-taak start gebeurtenis.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="e98a0-103">Gebeurtenissen voor het starten van taak</span><span class="sxs-lookup"><span data-stu-id="e98a0-103">Task start event</span></span>

 <span data-ttu-id="e98a0-104">Deze gebeurtenis wordt verzonden wanneer een taak is gepland om te starten op een rekenknooppunt door de planner.</span><span class="sxs-lookup"><span data-stu-id="e98a0-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="e98a0-105">Houd er rekening mee dat als de taak wordt later opnieuw of opnieuw wordt deze gebeurtenis weer voor dezelfde taak, maar het aantal nieuwe pogingen worden verzonden en besturingssysteemversie van de taak wordt dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e98a0-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="e98a0-106">Het volgende voorbeeld ziet de instantie van een taak start gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="e98a0-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="e98a0-107">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e98a0-107">Element name</span></span>|<span data-ttu-id="e98a0-108">Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-108">Type</span></span>|<span data-ttu-id="e98a0-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="e98a0-110">JobId</span><span class="sxs-lookup"><span data-stu-id="e98a0-110">jobId</span></span>|<span data-ttu-id="e98a0-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e98a0-111">String</span></span>|<span data-ttu-id="e98a0-112">De id van de taak met de taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="e98a0-113">id</span><span class="sxs-lookup"><span data-stu-id="e98a0-113">id</span></span>|<span data-ttu-id="e98a0-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e98a0-114">String</span></span>|<span data-ttu-id="e98a0-115">De id van de taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-115">The id of the task.</span></span>|
|<span data-ttu-id="e98a0-116">taskType</span><span class="sxs-lookup"><span data-stu-id="e98a0-116">taskType</span></span>|<span data-ttu-id="e98a0-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e98a0-117">String</span></span>|<span data-ttu-id="e98a0-118">Het type van de taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-118">The type of the task.</span></span> <span data-ttu-id="e98a0-119">Dit kan worden 'Taakbeheer heeft, die aangeeft dat het een jobbeheertaak of gebruiker is niet een jobbeheertaak aangeeft.</span><span class="sxs-lookup"><span data-stu-id="e98a0-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="e98a0-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="e98a0-120">systemTaskVersion</span></span>|<span data-ttu-id="e98a0-121">Int32</span><span class="sxs-lookup"><span data-stu-id="e98a0-121">Int32</span></span>|<span data-ttu-id="e98a0-122">Dit is de interne nieuwe pogingen voor een taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="e98a0-123">Intern kan de Batch-service opnieuw proberen een taak voor het account voor tijdelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="e98a0-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="e98a0-124">Deze problemen kunnen interne planning fouten of pogingen tot het herstellen van de rekenknooppunten in een verkeerde status.</span><span class="sxs-lookup"><span data-stu-id="e98a0-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="e98a0-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="e98a0-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="e98a0-126">Complex Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-126">Complex Type</span></span>|<span data-ttu-id="e98a0-127">Bevat informatie over het rekenknooppunt waarop de taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e98a0-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="e98a0-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="e98a0-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="e98a0-129">Complex Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-129">Complex Type</span></span>|<span data-ttu-id="e98a0-130">Geeft aan dat de taak taak met meerdere instanties vereisen van meerdere rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e98a0-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="e98a0-131">Zie [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e98a0-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="e98a0-132">beperkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-132">constraints</span></span>](#constraints)|<span data-ttu-id="e98a0-133">Complex Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-133">Complex Type</span></span>|<span data-ttu-id="e98a0-134">De uitvoering van beperkingen voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="e98a0-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="e98a0-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="e98a0-136">Complex Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-136">Complex Type</span></span>|<span data-ttu-id="e98a0-137">Bevat informatie over de uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="e98a0-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="e98a0-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="e98a0-139">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e98a0-139">Element name</span></span>|<span data-ttu-id="e98a0-140">Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-140">Type</span></span>|<span data-ttu-id="e98a0-141">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="e98a0-142">poolId</span><span class="sxs-lookup"><span data-stu-id="e98a0-142">poolId</span></span>|<span data-ttu-id="e98a0-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e98a0-143">String</span></span>|<span data-ttu-id="e98a0-144">De id van de groep waarop de taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e98a0-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="e98a0-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="e98a0-145">nodeId</span></span>|<span data-ttu-id="e98a0-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e98a0-146">String</span></span>|<span data-ttu-id="e98a0-147">De id van het knooppunt waarop de taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e98a0-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="e98a0-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="e98a0-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="e98a0-149">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e98a0-149">Element name</span></span>|<span data-ttu-id="e98a0-150">Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-150">Type</span></span>|<span data-ttu-id="e98a0-151">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="e98a0-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="e98a0-152">numberOfInstances</span></span>|<span data-ttu-id="e98a0-153">int</span><span class="sxs-lookup"><span data-stu-id="e98a0-153">Int</span></span>|<span data-ttu-id="e98a0-154">Het aantal rekenknooppunten dat is vereist voor de taak.</span><span class="sxs-lookup"><span data-stu-id="e98a0-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="e98a0-155"><a name="constraints"></a>beperkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="e98a0-156">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e98a0-156">Element name</span></span>|<span data-ttu-id="e98a0-157">Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-157">Type</span></span>|<span data-ttu-id="e98a0-158">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="e98a0-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="e98a0-159">maxTaskRetryCount</span></span>|<span data-ttu-id="e98a0-160">Int32</span><span class="sxs-lookup"><span data-stu-id="e98a0-160">Int32</span></span>|<span data-ttu-id="e98a0-161">Het maximum aantal keren dat de taak kan opnieuw worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e98a0-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="e98a0-162">De Batch-service probeert een taak opnieuw als de afsluitcode gelijk aan nul is.</span><span class="sxs-lookup"><span data-stu-id="e98a0-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="e98a0-163">Houd er rekening mee dat deze waarde specifiek het aantal nieuwe pogingen bepaalt.</span><span class="sxs-lookup"><span data-stu-id="e98a0-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="e98a0-164">De Batch-service probeert de taak één keer en probeer vervolgens tot deze limiet.</span><span class="sxs-lookup"><span data-stu-id="e98a0-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="e98a0-165">Bijvoorbeeld, als het maximale aantal pogingen maximaal 3, Batch probeert een taak is 4 een time-out (een initiële probeer en 3 nieuwe pogingen).</span><span class="sxs-lookup"><span data-stu-id="e98a0-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="e98a0-166">Als het maximale aantal pogingen 0 is, probeert taken niet in de Batch-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e98a0-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="e98a0-167">Als het maximale aantal pogingen -1 is, probeert de Batch-service opnieuw taken zonder limiet.</span><span class="sxs-lookup"><span data-stu-id="e98a0-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="e98a0-168">De standaardwaarde is 0 (geen herhaalde pogingen).</span><span class="sxs-lookup"><span data-stu-id="e98a0-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="e98a0-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="e98a0-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="e98a0-170">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e98a0-170">Element name</span></span>|<span data-ttu-id="e98a0-171">Type</span><span class="sxs-lookup"><span data-stu-id="e98a0-171">Type</span></span>|<span data-ttu-id="e98a0-172">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e98a0-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="e98a0-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="e98a0-173">retryCount</span></span>|<span data-ttu-id="e98a0-174">Int32</span><span class="sxs-lookup"><span data-stu-id="e98a0-174">Int32</span></span>|<span data-ttu-id="e98a0-175">Het aantal keren dat de taak door de Batch-service opnieuw is geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="e98a0-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="e98a0-176">De taak opnieuw wordt gestart als deze wordt afgesloten met een andere waarde dan nul afsluitcode tot maximaal de opgegeven MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="e98a0-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
