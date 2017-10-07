---
title: aaaCreate taken tooprepare taken en volledige taken op rekenknooppunten - Azure Batch | Microsoft Docs
description: Gebruik op jobniveau voorbereiding taken toominimize gegevens overbrengen tooAzure Batch-rekenknooppunten en release van taken voor het opruimen van knooppunt bij Taakvoltooiing.
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
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="2736a-103">Taak uitvoeren voorbereidings- en jobvrijgevingstaken voor Batch-rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="2736a-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="2736a-104">Een Azure Batch-taak is een vorm van setup vaak vereist voordat de bijbehorende taken worden uitgevoerd en onderhoud na taak wanneer de taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="2736a-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="2736a-105">U mogelijk nodig toodownload algemene taak invoergegevens tooyour rekenknooppunten of taak uitvoer gegevens tooAzure opslag uploaden nadat het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2736a-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="2736a-106">U kunt **taak voorbereiding** en **taak release** taken tooperform deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2736a-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="2736a-107">Wat zijn taakvoorbereidingstaak en release van taken?</span><span class="sxs-lookup"><span data-stu-id="2736a-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="2736a-108">Voordat een job taken worden uitgevoerd, Hallo jobvoorbereidingstaak wordt uitgevoerd op alle compute knooppunten geplande toorun ten minste één taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="2736a-109">Zodra het Hallo-taak is voltooid, wordt Hallo jobvrijgevingstaak uitgevoerd op elk knooppunt in Hallo pool dat ten minste één taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="2736a-110">Net als bij normale Batch-taken, kunt u een opdrachtregel toobe aangeroepen wanneer een taakvoorbereidingstaak of release-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="2736a-111">Jobvoorbereidingstaken en jobvrijgevingstaken taken bieden vertrouwde Batch taakfuncties zoals bestand downloaden ([bronbestanden][net_job_prep_resourcefiles]), verhoogde uitvoering, aangepaste omgevingsvariabelen, maximale uitvoering duur, probeer het opnieuw aantal en bewaartijd voor bestanden.</span><span class="sxs-lookup"><span data-stu-id="2736a-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="2736a-112">In de Hallo uit te voeren, leert u hoe toouse hello [JobPreparationTask] [ net_job_prep] en [JobReleaseTask] [ net_job_release] in Hallo klassen gevonden [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2736a-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="2736a-113">Jobvoorbereidingstaken en jobvrijgevingstaken taken zijn vooral handig in omgevingen 'van toepassingen wordt gedeeld', waarop een pool van rekenknooppunten zich blijft voordoen tussen de taak wordt uitgevoerd en wordt gebruikt door veel taken.</span><span class="sxs-lookup"><span data-stu-id="2736a-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="2736a-114">Wanneer toouse taak voorbereiding en release van taken</span><span class="sxs-lookup"><span data-stu-id="2736a-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="2736a-115">Taakvoorbereidings- en jobvrijgevingstaken zijn geschikt voor Hallo volgende situaties:</span><span class="sxs-lookup"><span data-stu-id="2736a-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="2736a-116">**Algemene taakgegevens downloaden**</span><span class="sxs-lookup"><span data-stu-id="2736a-116">**Download common task data**</span></span>

<span data-ttu-id="2736a-117">Batchtaken is vaak een gemeenschappelijke set gegevens als invoer voor Hallo projecttaken vereist.</span><span class="sxs-lookup"><span data-stu-id="2736a-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="2736a-118">In de dagelijkse risico analysis berekeningen is marktgegevens bijvoorbeeld specifieke nog algemene tooall taken in Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="2736a-119">Deze marktgegevens, grootte, vaak enkele gigabytes moet gedownloade tooeach rekenknooppunt slechts één keer zodat elke taak die wordt uitgevoerd op Hallo knooppunt kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2736a-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="2736a-120">Gebruik een **jobvoorbereidingstaak** toodownload dit gegevens tooeach knooppunt voordat de uitvoering van Hallo taak Hallo's andere taken.</span><span class="sxs-lookup"><span data-stu-id="2736a-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="2736a-121">**Verwijderen van de taak en uitvoer**</span><span class="sxs-lookup"><span data-stu-id="2736a-121">**Delete job and task output**</span></span>

<span data-ttu-id="2736a-122">In een omgeving 'van toepassingen wordt gedeeld', waarbij een groep rekenknooppunten zich niet buiten gebruik gestelde tussen taken, moet u de taakgegevens toodelete tussen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="2736a-123">Mogelijk moet u tooconserve vrije schijfruimte op Hallo knooppunten of voldoen aan het beveiligingsbeleid van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="2736a-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="2736a-124">Gebruik een **jobvrijgevingstaak** toodelete gegevens die zijn gedownload door een jobvoorbereidingstaak of gegenereerd tijdens de uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="2736a-125">**Logboek bewaren**</span><span class="sxs-lookup"><span data-stu-id="2736a-125">**Log retention**</span></span>

<span data-ttu-id="2736a-126">U kunt een kopie van de logboekbestanden die uw taken wordt gegenereerd of misschien crashdumpbestanden dat kunnen worden gegenereerd door de mislukte toepassingen tookeep.</span><span class="sxs-lookup"><span data-stu-id="2736a-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="2736a-127">Gebruik een **jobvrijgevingstaak** in dergelijke gevallen toocompress en upload dit tooan gegevens [Azure Storage] [ azure_storage] account.</span><span class="sxs-lookup"><span data-stu-id="2736a-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="2736a-128">Een andere manier toopersist logboeken en andere taak en uitvoer gegevens zijn toouse hello [Azure Batch-bestand conventies](batch-task-output.md) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2736a-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="2736a-129">Jobvoorbereidingstaak</span><span class="sxs-lookup"><span data-stu-id="2736a-129">Job preparation task</span></span>
<span data-ttu-id="2736a-130">Batch: Hallo jobvoorbereidingstaak voordat de uitvoering van een job taken uitvoeren op elk rekenknooppunt die geplande toorun een taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="2736a-131">Standaard wacht Hallo Batch-service op Hallo taak voorbereiding taak toobe voltooid voordat de geplande taken-tooexecute Hallo op Hallo knooppunt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="2736a-132">U kunt echter Hallo-service niet toowait configureren.</span><span class="sxs-lookup"><span data-stu-id="2736a-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="2736a-133">Als Hallo knooppunt opnieuw wordt opgestart, Hallo jobvoorbereidingstaak opnieuw wordt uitgevoerd, maar u kunt dit gedrag ook uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="2736a-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="2736a-134">Hallo jobvoorbereidingstaak wordt alleen uitgevoerd op knooppunten die geplande toorun een taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="2736a-135">Dit voorkomt dat Hallo onnodige uitvoering van een jobvoorbereidingstaak als een knooppunt niet aan een taak toegewezen is.</span><span class="sxs-lookup"><span data-stu-id="2736a-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="2736a-136">Dit kan gebeuren wanneer Hallo aantal taken voor een job minder dan het aantal knooppunten in een pool Hallo is.</span><span class="sxs-lookup"><span data-stu-id="2736a-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="2736a-137">Dit geldt ook wanneer [uitvoering van gelijktijdige taken](batch-parallel-node-tasks.md) is ingeschakeld, waardoor sommige knooppunten inactief als het aantal van de taak Hallo is lager dan Hallo totale mogelijke gelijktijdige taken.</span><span class="sxs-lookup"><span data-stu-id="2736a-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="2736a-138">Door de jobvoorbereidingstaak Hallo niet wordt uitgevoerd op niet-actieve knooppunten, kunt u minder geld besteden aan gegevensbelasting overdracht.</span><span class="sxs-lookup"><span data-stu-id="2736a-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="2736a-139">[JobPreparationTask] [ net_job_prep_cloudjob] verschilt van [CloudPool.StartTask] [ pool_starttask] in dat JobPreparationTask aan Hallo begin van elke taak wordt uitgevoerd terwijl StartTask voert alleen wanneer een rekenknooppunt eerst lid wordt van een groep of opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="2736a-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="2736a-140">Jobvrijgevingstaak</span><span class="sxs-lookup"><span data-stu-id="2736a-140">Job release task</span></span>
<span data-ttu-id="2736a-141">Zodra een taak is gemarkeerd als voltooid, wordt Hallo jobvrijgevingstaak uitgevoerd op elk knooppunt in Hallo pool dat ten minste één taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="2736a-142">U kunt een taak markeren als voltooid door uitgifte van een aanvraag beëindigen.</span><span class="sxs-lookup"><span data-stu-id="2736a-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="2736a-143">Hallo Batch-service en vervolgens stelt Hallo taakstatus te*beëindigd*, die is gekoppeld aan taak Hallo actief of actieve taken beëindigd en Hallo jobvrijgevingstaak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="2736a-144">Hallo taak gaat vervolgens toohello *voltooid* status.</span><span class="sxs-lookup"><span data-stu-id="2736a-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="2736a-145">Verwijderen van een taak worden ook Hallo jobvrijgevingstaak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="2736a-146">Echter als al een taak is beëindigd, is Hallo release taak niet uitgevoerd een tweede keer als Hallo-taak wordt later verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2736a-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="2736a-147">Taak prep en de vrijgave van taken met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="2736a-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="2736a-148">toewijzen van een jobvoorbereidingstaak toouse een [JobPreparationTask] [ net_job_prep] object tooyour taak [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] eigenschap .</span><span class="sxs-lookup"><span data-stu-id="2736a-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="2736a-149">Op deze manier initialiseren een [JobReleaseTask] [ net_job_release] en toewijzen van de taak tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] eigenschap tooset Hallo jobvrijgevingstaak.</span><span class="sxs-lookup"><span data-stu-id="2736a-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="2736a-150">In dit codefragment `myBatchClient` is een exemplaar van [BatchClient][net_batch_client], en `myPool` is een bestaande pool binnen Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="2736a-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="2736a-151">Zoals eerder vermeld, worden de Hallo release taak wordt uitgevoerd wanneer een taak is beëindigd of is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2736a-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="2736a-152">Beëindigen van een taak met [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="2736a-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="2736a-153">Verwijderen van een taak met [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="2736a-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="2736a-154">U doorgaans beëindigen of verwijderen van een taak wanneer de taken zijn voltooid of wanneer een time-out die u hebt gedefinieerd is bereikt.</span><span class="sxs-lookup"><span data-stu-id="2736a-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="2736a-155">Voorbeeld van code op GitHub</span><span class="sxs-lookup"><span data-stu-id="2736a-155">Code sample on GitHub</span></span>
<span data-ttu-id="2736a-156">toosee jobvoorbereidingstaken en jobvrijgevingstaken taken in actie, bekijk Hallo [JobPrepRelease] [ job_prep_release_sample] voorbeeldproject op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2736a-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="2736a-157">Deze consoletoepassing Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2736a-157">This console application does hello following:</span></span>

1. <span data-ttu-id="2736a-158">Maakt een groep met twee knooppunten voor 'kleine'.</span><span class="sxs-lookup"><span data-stu-id="2736a-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="2736a-159">Maakt een taak met taak voorbereidings-, release- en standaardtaken.</span><span class="sxs-lookup"><span data-stu-id="2736a-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="2736a-160">Wordt uitgevoerd Hallo jobvoorbereidingstaak schrijft eerst tooa tekstbestand voor Hallo knooppunt-ID in van een knooppunt 'gedeeld' directory.</span><span class="sxs-lookup"><span data-stu-id="2736a-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="2736a-161">Een taak wordt uitgevoerd op elk knooppunt dat de taak-ID toohello schrijft dezelfde tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="2736a-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="2736a-162">Hallo-inhoud van elk knooppunt tekst bestand toohello console afdrukken zodra alle taken zijn voltooid (of Hallo time-out is bereikt)</span><span class="sxs-lookup"><span data-stu-id="2736a-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="2736a-163">Wanneer Hallo-taak is voltooid, voert u Hallo taak release toodelete Hallo-bestand van het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="2736a-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="2736a-164">Afdrukken bestellen Hallo afsluitcodes van Hallo taakvoorbereidingstaak en release van taken voor elk knooppunt waarop ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="2736a-165">Onderbroken uitvoering tooallow bevestiging van de taak en/of de groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2736a-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="2736a-166">De uitvoer van de voorbeeldtoepassing Hallo is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="2736a-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
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

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="2736a-167">Vervaldatum toohello variabele maken en start het tijdstip knooppunten in een nieuwe pool (sommige knooppunten zijn gereed voor taken vóór andere), ziet u andere uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2736a-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="2736a-168">In het bijzonder omdat Hallo taken snel kunnen worden uitgevoerd, mogen een van de knooppunten van de pool Hallo uitvoeren alle taken van Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="2736a-169">Als dit gebeurt, ziet u dat Hallo prep taak en de vrijgave van taken bestaan niet voor Hallo-knooppunt dat geen taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2736a-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="2736a-170">Inspecteer de taakvoorbereidingstaak en release-taken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2736a-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="2736a-171">Wanneer u de voorbeeldtoepassing Hallo uitvoert, kunt u Hallo [Azure-portal] [ portal] tooview Hallo eigenschappen van het Hallo-taak en de bijbehorende taken of zelfs Hallo gedeelde tekstbestand dat door Hallo projecttaken wordt gewijzigd te downloaden.</span><span class="sxs-lookup"><span data-stu-id="2736a-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="2736a-172">Hallo schermafbeelding hieronder ziet u Hallo **voorbereiding taken blade** in Hallo na een uitvoering van de voorbeeldtoepassing hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2736a-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="2736a-173">Navigeer toohello *JobPrepReleaseSampleJob* eigenschappen nadat uw taken hebt voltooid (maar voordat de job en de pool wordt verwijderd) en klik op **systeemvoorbereidingstaken** of **takenRelease** tooview hun eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2736a-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Voorbereiding taakeigenschappen in Azure-portal][1]

## <a name="next-steps"></a><span data-ttu-id="2736a-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2736a-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="2736a-176">Toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="2736a-176">Application packages</span></span>
<span data-ttu-id="2736a-177">In aanvulling toohello jobvoorbereidingstaak, kunt u ook hello gebruiken [toepassingspakketten](batch-application-packages.md) functie van Batch tooprepare rekenknooppunten voor uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="2736a-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="2736a-178">Deze functie is vooral handig voor het implementeren van toepassingen die niet met een installatieprogramma, toepassingen die veel (100 en hoger) bestanden bevatten of toepassingen waarvoor strikte versiebeheer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="2736a-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="2736a-179">Installeren van toepassingen en gegevens voor fasering</span><span class="sxs-lookup"><span data-stu-id="2736a-179">Installing applications and staging data</span></span>
<span data-ttu-id="2736a-180">Dit bericht MSDN-forum biedt een overzicht van de verschillende methoden voor het voorbereiden van uw knooppunten om taken uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2736a-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="2736a-181">[Installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten][forum_post]</span><span class="sxs-lookup"><span data-stu-id="2736a-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="2736a-182">Geschreven door een van de Azure Batch-teamleden hello, besproken verschillende technieken waarmee u toodeploy toepassingen en gegevens toocompute knooppunten kunt.</span><span class="sxs-lookup"><span data-stu-id="2736a-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

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
