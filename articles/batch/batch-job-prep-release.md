---
title: Maak taken om voor te bereiden, taken en volledige taken op rekenknooppunten - Azure Batch | Microsoft Docs
description: Gebruik op jobniveau systeemvoorbereidingstaken om te beperken van overdracht van gegevens naar Azure Batch-rekenknooppunten en release van taken voor het opruimen van knooppunt bij Taakvoltooiing.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="3781a-103">Taak uitvoeren voorbereidings- en jobvrijgevingstaken voor Batch-rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="3781a-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="3781a-104">Een Azure Batch-taak is een vorm van setup vaak vereist voordat de bijbehorende taken worden uitgevoerd en onderhoud na taak wanneer de taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="3781a-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="3781a-105">Mogelijk moet u algemene taak invoergegevens downloaden naar uw rekenknooppunten, of de taak uitvoergegevens uploaden naar Azure Storage nadat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3781a-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="3781a-106">U kunt **taak voorbereiding** en **taak release** taken voor het uitvoeren van deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="3781a-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="3781a-107">Wat zijn taakvoorbereidingstaak en release van taken?</span><span class="sxs-lookup"><span data-stu-id="3781a-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="3781a-108">Voordat een job taken worden uitgevoerd, is de jobvoorbereidingstaak wordt uitgevoerd op alle rekenknooppunten die ten minste één taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="3781a-109">Zodra de taak is voltooid, wordt de jobvrijgevingstaak uitgevoerd op elk knooppunt in de pool dat ten minste één taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="3781a-110">Net als bij normale Batch-taken, kunt u een opdrachtregel moet worden aangeroepen wanneer een taak voorbereidings- of release-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="3781a-111">Jobvoorbereidingstaken en jobvrijgevingstaken taken bieden vertrouwde Batch taakfuncties zoals bestand downloaden ([bronbestanden][net_job_prep_resourcefiles]), verhoogde uitvoering, aangepaste omgevingsvariabelen, maximale uitvoering duur, probeer het opnieuw aantal en bewaartijd voor bestanden.</span><span class="sxs-lookup"><span data-stu-id="3781a-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="3781a-112">In de volgende gedeelten leert u hoe u de [JobPreparationTask] [ net_job_prep] en [JobReleaseTask] [ net_job_release] klassen gevonden in de [ Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="3781a-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="3781a-113">Jobvoorbereidingstaken en jobvrijgevingstaken taken zijn vooral handig in omgevingen 'van toepassingen wordt gedeeld', waarop een pool van rekenknooppunten zich blijft voordoen tussen de taak wordt uitgevoerd en wordt gebruikt door veel taken.</span><span class="sxs-lookup"><span data-stu-id="3781a-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="3781a-114">Bij het gebruik van de taakvoorbereidingstaak en de vrijgave van taken</span><span class="sxs-lookup"><span data-stu-id="3781a-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="3781a-115">Taakvoorbereidings- en jobvrijgevingstaken zijn geschikt voor de volgende situaties:</span><span class="sxs-lookup"><span data-stu-id="3781a-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="3781a-116">**Algemene taakgegevens downloaden**</span><span class="sxs-lookup"><span data-stu-id="3781a-116">**Download common task data**</span></span>

<span data-ttu-id="3781a-117">Batchtaken vereisen vaak een gemeenschappelijke set gegevens als invoer voor de taken van de taak.</span><span class="sxs-lookup"><span data-stu-id="3781a-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="3781a-118">In de dagelijkse risico analysis berekeningen is marktgegevens bijvoorbeeld specifieke, nog gemeenschappelijk zijn voor alle taken in de taak.</span><span class="sxs-lookup"><span data-stu-id="3781a-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="3781a-119">Deze marktgegevens, vaak verscheidene gigabytes groot, moet worden gedownload naar elk rekenknooppunt slechts één keer zodat elke taak die wordt uitgevoerd op het knooppunt kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3781a-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="3781a-120">Gebruik een **jobvoorbereidingstaak** te downloaden van deze gegevens voor elk knooppunt voordat de uitvoering van de taak's andere taken.</span><span class="sxs-lookup"><span data-stu-id="3781a-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="3781a-121">**Verwijderen van de taak en uitvoer**</span><span class="sxs-lookup"><span data-stu-id="3781a-121">**Delete job and task output**</span></span>

<span data-ttu-id="3781a-122">In een omgeving 'van toepassingen wordt gedeeld', waarbij een groep rekenknooppunten zich niet buiten gebruik gestelde tussen taken, moet u wellicht verwijderen taakgegevens tussen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="3781a-123">Mogelijk moet u beschikbare schijfruimte op de knooppunten of voldoen aan het beveiligingsbeleid van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3781a-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="3781a-124">Gebruik een **jobvrijgevingstaak** om gegevens die zijn gedownload door een jobvoorbereidingstaak of gegenereerd tijdens de uitvoering van de taak te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3781a-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="3781a-125">**Logboek bewaren**</span><span class="sxs-lookup"><span data-stu-id="3781a-125">**Log retention**</span></span>

<span data-ttu-id="3781a-126">Mogelijk wilt een kopie van de logboekbestanden die uw taken wordt gegenereerd of mogelijk crashdumpbestanden dat kan worden gegenereerd door de mislukte toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3781a-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="3781a-127">Gebruik een **jobvrijgevingstaak** in dergelijke gevallen comprimeren en het uploaden van deze gegevens naar een [Azure Storage] [ azure_storage] account.</span><span class="sxs-lookup"><span data-stu-id="3781a-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="3781a-128">Een andere manier om vast te leggen logboeken en andere taak en uitvoer gegevens is het gebruik van de [Azure Batch-bestand conventies](batch-task-output.md) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="3781a-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="3781a-129">Jobvoorbereidingstaak</span><span class="sxs-lookup"><span data-stu-id="3781a-129">Job preparation task</span></span>
<span data-ttu-id="3781a-130">Batch: de jobvoorbereidingstaak voordat de uitvoering van een job taken uitvoeren op elk rekenknooppunt die is gepland voor een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3781a-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="3781a-131">Standaard wacht de Batch-service voor de jobvoorbereidingstaak om te worden voltooid voordat de taken die moeten worden uitgevoerd op het knooppunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="3781a-132">U kunt echter de service niet te wachten.</span><span class="sxs-lookup"><span data-stu-id="3781a-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="3781a-133">Als het knooppunt opnieuw wordt opgestart, wordt de jobvoorbereidingstaak wordt opnieuw uitgevoerd, maar u kunt dit gedrag ook uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="3781a-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="3781a-134">De jobvoorbereidingstaak wordt alleen uitgevoerd op knooppunten die zijn gepland voor een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3781a-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="3781a-135">Dit voorkomt dat de onnodige uitvoering van een jobvoorbereidingstaak als een knooppunt niet aan een taak toegewezen is.</span><span class="sxs-lookup"><span data-stu-id="3781a-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="3781a-136">Dit kan gebeuren als het aantal taken voor een job kleiner dan het aantal knooppunten in een pool is.</span><span class="sxs-lookup"><span data-stu-id="3781a-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="3781a-137">Dit geldt ook wanneer [uitvoering van gelijktijdige taken](batch-parallel-node-tasks.md) is ingeschakeld, waardoor sommige knooppunten inactief als het aantal taken lager is dan de totale mogelijke gelijktijdige taken.</span><span class="sxs-lookup"><span data-stu-id="3781a-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="3781a-138">Door de jobvoorbereidingstaak niet wordt uitgevoerd op niet-actieve knooppunten, kunt u minder geld besteden aan gegevensoverdracht kosten.</span><span class="sxs-lookup"><span data-stu-id="3781a-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="3781a-139">[JobPreparationTask] [ net_job_prep_cloudjob] verschilt van [CloudPool.StartTask] [ pool_starttask] in dat JobPreparationTask aan het begin van elke taak wordt uitgevoerd terwijl StartTask voert alleen wanneer een rekenknooppunt eerst lid wordt van een groep of opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="3781a-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="3781a-140">Jobvrijgevingstaak</span><span class="sxs-lookup"><span data-stu-id="3781a-140">Job release task</span></span>
<span data-ttu-id="3781a-141">Zodra een taak is gemarkeerd als voltooid, wordt de jobvrijgevingstaak uitgevoerd op elk knooppunt in de pool dat ten minste één taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="3781a-142">U kunt een taak markeren als voltooid door uitgifte van een aanvraag beëindigen.</span><span class="sxs-lookup"><span data-stu-id="3781a-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="3781a-143">De Batch-service wordt de taakstatus van de vervolgens ingesteld op *beëindigd*, alle actieve of actieve taken die zijn gekoppeld aan de taak wordt beëindigd en wordt de jobvrijgevingstaak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="3781a-144">De taak wordt verplaatst naar de *voltooid* status.</span><span class="sxs-lookup"><span data-stu-id="3781a-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="3781a-145">Verwijderen van een taak worden ook de jobvrijgevingstaak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="3781a-146">Echter, als er al een taak is beëindigd, de release-taak wordt niet uitgevoerd een tweede keer als de taak wordt later verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3781a-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="3781a-147">Taak prep en de vrijgave van taken met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="3781a-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="3781a-148">Voor het gebruik van een jobvoorbereidingstaak toewijzen een [JobPreparationTask] [ net_job_prep] object aan uw project [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3781a-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="3781a-149">Op deze manier initialiseren een [JobReleaseTask] [ net_job_release] en toe te wijzen aan uw project [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] eigenschap van de taak ingesteld Release-taak.</span><span class="sxs-lookup"><span data-stu-id="3781a-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="3781a-150">In dit codefragment `myBatchClient` is een exemplaar van [BatchClient][net_batch_client], en `myPool` is een bestaande pool in de Batch-account.</span><span class="sxs-lookup"><span data-stu-id="3781a-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="3781a-151">Zoals eerder vermeld, wordt de release-taak wordt uitgevoerd wanneer een taak is beëindigd of is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3781a-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="3781a-152">Beëindigen van een taak met [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="3781a-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="3781a-153">Verwijderen van een taak met [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="3781a-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="3781a-154">U doorgaans beëindigen of verwijderen van een taak wanneer de taken zijn voltooid of wanneer een time-out die u hebt gedefinieerd is bereikt.</span><span class="sxs-lookup"><span data-stu-id="3781a-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="3781a-155">Voorbeeld van code op GitHub</span><span class="sxs-lookup"><span data-stu-id="3781a-155">Code sample on GitHub</span></span>
<span data-ttu-id="3781a-156">Als u wilt zien taakvoorbereidingstaak en taken in actie release, bekijk de [JobPrepRelease] [ job_prep_release_sample] voorbeeldproject op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3781a-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="3781a-157">Deze consoletoepassing doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="3781a-157">This console application does the following:</span></span>

1. <span data-ttu-id="3781a-158">Maakt een groep met twee knooppunten voor 'kleine'.</span><span class="sxs-lookup"><span data-stu-id="3781a-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="3781a-159">Maakt een taak met taak voorbereidings-, release- en standaardtaken.</span><span class="sxs-lookup"><span data-stu-id="3781a-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="3781a-160">De jobvoorbereidingstaak schrijft eerst de knooppunt-ID naar een tekstbestand in een knooppunt 'gedeeld' directory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="3781a-161">Voert een taak op elk knooppunt dat de taak-ID naar hetzelfde tekstbestand schrijft.</span><span class="sxs-lookup"><span data-stu-id="3781a-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="3781a-162">Zodra alle taken zijn voltooid (of de time-out is bereikt), wordt de inhoud van elk knooppunt tekstbestand dat aan de console.</span><span class="sxs-lookup"><span data-stu-id="3781a-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="3781a-163">Wanneer de taak is voltooid, voert u de jobvrijgevingstaak om het bestand verwijderen uit het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3781a-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="3781a-164">Afdrukken van de afsluitcodes van de taak jobvoorbereidingstaken en jobvrijgevingstaken taken voor elk knooppunt waarop ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="3781a-165">De uitvoering van de onderbroken waarmee de bevestiging van de taak en/of de groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3781a-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="3781a-166">De uitvoer van de voorbeeldtoepassing is vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="3781a-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob to reach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="3781a-167">Als gevolg van de variabele maken en start tijd van de knooppunten in een nieuwe pool (sommige knooppunten zijn gereed voor taken vóór andere), ziet u andere uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3781a-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="3781a-168">In het bijzonder omdat de taken snel kunnen worden uitgevoerd, kan een van de groep knooppunten uitvoeren alle taken van de taak.</span><span class="sxs-lookup"><span data-stu-id="3781a-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="3781a-169">Als dit gebeurt, ziet u dat de taak voorbereiden en release taken bestaan niet voor het knooppunt dat geen taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3781a-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="3781a-170">Inspecteer de taakvoorbereidingstaak en release-taken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="3781a-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="3781a-171">Wanneer u de voorbeeldtoepassing uitvoert, kunt u de [Azure-portal] [ portal] voor het weergeven van de eigenschappen van de taak en de bijbehorende taken of zelfs het gedeelde tekstbestand dat door de taken van de taak wordt gewijzigd te downloaden.</span><span class="sxs-lookup"><span data-stu-id="3781a-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="3781a-172">De schermafbeelding hieronder bevat de **voorbereiding taken blade** in de Azure portal na een uitvoering van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3781a-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="3781a-173">Navigeer naar de *JobPrepReleaseSampleJob* eigenschappen nadat uw taken hebt voltooid (maar voordat de job en de pool wordt verwijderd) en klik op **systeemvoorbereidingstaken** of **takenRelease**eigenschappen weergeven.</span><span class="sxs-lookup"><span data-stu-id="3781a-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Voorbereiding taakeigenschappen in Azure-portal][1]

## <a name="next-steps"></a><span data-ttu-id="3781a-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3781a-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="3781a-176">Toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="3781a-176">Application packages</span></span>
<span data-ttu-id="3781a-177">Naast de jobvoorbereidingstaak ook kunt u de [toepassingspakketten](batch-application-packages.md) functie van Batch rekenknooppunten voorbereiden voor uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="3781a-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="3781a-178">Deze functie is vooral handig voor het implementeren van toepassingen die niet met een installatieprogramma, toepassingen die veel (100 en hoger) bestanden bevatten of toepassingen waarvoor strikte versiebeheer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="3781a-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="3781a-179">Installeren van toepassingen en gegevens voor fasering</span><span class="sxs-lookup"><span data-stu-id="3781a-179">Installing applications and staging data</span></span>
<span data-ttu-id="3781a-180">Dit bericht MSDN-forum biedt een overzicht van de verschillende methoden voor het voorbereiden van uw knooppunten om taken uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3781a-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="3781a-181">[Installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten][forum_post]</span><span class="sxs-lookup"><span data-stu-id="3781a-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="3781a-182">Geschreven door een van de Azure Batch-teamleden, besproken verschillende technieken die u gebruiken kunt voor het implementeren van toepassingen en gegevens rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3781a-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
