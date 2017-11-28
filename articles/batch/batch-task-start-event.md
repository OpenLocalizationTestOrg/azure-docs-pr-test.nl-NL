---
title: aaa "Azure Batch-taakgebeurtenis start | Microsoft Docs'
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="f7f6e-103">Gebeurtenissen voor het starten van taak</span><span class="sxs-lookup"><span data-stu-id="f7f6e-103">Task start event</span></span>

 <span data-ttu-id="f7f6e-104">Deze gebeurtenis wordt verzonden als een taak is gepland toostart op een rekenknooppunt door Hallo scheduler.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="f7f6e-105">Houd er rekening mee dat als Hallo-taak wordt later opnieuw of opnieuw deze gebeurtenis wordt worden verzonden opnieuw voor hello dezelfde taak, maar Hallo aantal nieuwe pogingen en besturingssysteemversie van de taak wordt dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="f7f6e-106">Hallo ziet volgende voorbeeld Hallo-hoofdtekst van een taak start-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="f7f6e-107">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="f7f6e-107">Element name</span></span>|<span data-ttu-id="f7f6e-108">Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-108">Type</span></span>|<span data-ttu-id="f7f6e-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7f6e-110">JobId</span><span class="sxs-lookup"><span data-stu-id="f7f6e-110">jobId</span></span>|<span data-ttu-id="f7f6e-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f7f6e-111">String</span></span>|<span data-ttu-id="f7f6e-112">Hallo-id van Hallo-taak met taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="f7f6e-113">id</span><span class="sxs-lookup"><span data-stu-id="f7f6e-113">id</span></span>|<span data-ttu-id="f7f6e-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f7f6e-114">String</span></span>|<span data-ttu-id="f7f6e-115">Hallo-id van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-115">hello id of hello task.</span></span>|
|<span data-ttu-id="f7f6e-116">taskType</span><span class="sxs-lookup"><span data-stu-id="f7f6e-116">taskType</span></span>|<span data-ttu-id="f7f6e-117">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f7f6e-117">String</span></span>|<span data-ttu-id="f7f6e-118">Hallo type Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-118">hello type of hello task.</span></span> <span data-ttu-id="f7f6e-119">Dit kan worden 'Taakbeheer heeft, die aangeeft dat het een jobbeheertaak of gebruiker is niet een jobbeheertaak aangeeft.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="f7f6e-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="f7f6e-120">systemTaskVersion</span></span>|<span data-ttu-id="f7f6e-121">Int32</span><span class="sxs-lookup"><span data-stu-id="f7f6e-121">Int32</span></span>|<span data-ttu-id="f7f6e-122">Dit is interne Hallo nieuwe pogingen voor een taak.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="f7f6e-123">Intern Hallo Batch-service kan opnieuw proberen van een taak tooaccount voor tijdelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="f7f6e-124">Deze problemen kunnen interne planning fouten of pogingen toorecover uit rekenknooppunten opnemen in een verkeerde status.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="f7f6e-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="f7f6e-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="f7f6e-126">Complex Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-126">Complex Type</span></span>|<span data-ttu-id="f7f6e-127">Bevat informatie over het Hallo-rekenknooppunt op welke Hallo taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="f7f6e-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="f7f6e-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="f7f6e-129">Complex Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-129">Complex Type</span></span>|<span data-ttu-id="f7f6e-130">Hiermee geeft u dat die taak Hallo taak met meerdere instanties vereisen van meerdere rekenknooppunten is.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="f7f6e-131">Zie [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="f7f6e-132">beperkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-132">constraints</span></span>](#constraints)|<span data-ttu-id="f7f6e-133">Complex Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-133">Complex Type</span></span>|<span data-ttu-id="f7f6e-134">Hallo uitvoering beperkingen toothis taak.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="f7f6e-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="f7f6e-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="f7f6e-136">Complex Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-136">Complex Type</span></span>|<span data-ttu-id="f7f6e-137">Bevat informatie over Hallo uitvoering van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="f7f6e-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="f7f6e-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="f7f6e-139">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="f7f6e-139">Element name</span></span>|<span data-ttu-id="f7f6e-140">Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-140">Type</span></span>|<span data-ttu-id="f7f6e-141">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7f6e-142">poolId</span><span class="sxs-lookup"><span data-stu-id="f7f6e-142">poolId</span></span>|<span data-ttu-id="f7f6e-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f7f6e-143">String</span></span>|<span data-ttu-id="f7f6e-144">Hallo-id van Hallo-pool op welke Hallo taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="f7f6e-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="f7f6e-145">nodeId</span></span>|<span data-ttu-id="f7f6e-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f7f6e-146">String</span></span>|<span data-ttu-id="f7f6e-147">Hallo-id van Hallo-knooppunt op welke Hallo taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="f7f6e-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="f7f6e-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="f7f6e-149">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="f7f6e-149">Element name</span></span>|<span data-ttu-id="f7f6e-150">Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-150">Type</span></span>|<span data-ttu-id="f7f6e-151">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7f6e-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="f7f6e-152">numberOfInstances</span></span>|<span data-ttu-id="f7f6e-153">int</span><span class="sxs-lookup"><span data-stu-id="f7f6e-153">Int</span></span>|<span data-ttu-id="f7f6e-154">Hallo aantal rekenknooppunten door Hallo taak vereist.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="f7f6e-155"><a name="constraints"></a>beperkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="f7f6e-156">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="f7f6e-156">Element name</span></span>|<span data-ttu-id="f7f6e-157">Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-157">Type</span></span>|<span data-ttu-id="f7f6e-158">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7f6e-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="f7f6e-159">maxTaskRetryCount</span></span>|<span data-ttu-id="f7f6e-160">Int32</span><span class="sxs-lookup"><span data-stu-id="f7f6e-160">Int32</span></span>|<span data-ttu-id="f7f6e-161">Hallo maximum aantal keren Hallo taak kan opnieuw worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="f7f6e-162">Hallo Batch-service probeert een taak opnieuw als de afsluitcode gelijk aan nul is.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="f7f6e-163">Houd er rekening mee dat deze waarde specifiek het aantal nieuwe pogingen Hallo bepaalt.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="f7f6e-164">Hallo Batch-service eenmaal probeert Hallo taak en probeer vervolgens up toothis limiet.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="f7f6e-165">Bijvoorbeeld, als Hallo maximale aantal pogingen 3 is, Batch wordt geprobeerd een taak too4 tijden (een initiële probeer en 3 nieuwe pogingen).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="f7f6e-166">Als Hallo maximale aantal nieuwe pogingen 0 is, probeert Hallo Batch-service niet taken opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="f7f6e-167">Als Hallo maximale aantal pogingen -1 is, probeert Hallo Batch-service opnieuw taken zonder limiet.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="f7f6e-168">Hallo-standaardwaarde is 0 (geen herhaalde pogingen).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="f7f6e-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="f7f6e-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="f7f6e-170">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="f7f6e-170">Element name</span></span>|<span data-ttu-id="f7f6e-171">Type</span><span class="sxs-lookup"><span data-stu-id="f7f6e-171">Type</span></span>|<span data-ttu-id="f7f6e-172">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7f6e-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7f6e-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="f7f6e-173">retryCount</span></span>|<span data-ttu-id="f7f6e-174">Int32</span><span class="sxs-lookup"><span data-stu-id="f7f6e-174">Int32</span></span>|<span data-ttu-id="f7f6e-175">Hallo aantal keren Hallo taak door Hallo Batch-service opnieuw is geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="f7f6e-176">Hallo-taak wordt herhaald als deze wordt afgesloten met een andere waarde dan nul afsluitcode up toohello opgegeven MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="f7f6e-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
