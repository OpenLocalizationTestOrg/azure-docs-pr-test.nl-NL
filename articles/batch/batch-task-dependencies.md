---
title: aaaUse taak afhankelijkheden toorun taken op basis van Hallo voltooiing van andere taken - Azure Batch | Microsoft Docs
description: Taken maken die afhankelijk van Hallo voltooiing van andere taken zijn voor het verwerken van MapReduce-stijl en vergelijkbare big data werkbelastingen in Azure Batch.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="e264c-103">Taakafhankelijkheden toorun-taken die afhankelijk van andere taken zijn maken</span><span class="sxs-lookup"><span data-stu-id="e264c-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="e264c-104">U kunt toorun van taak afhankelijkheden definiëren een taak of taken alleen als een bovenliggende-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="e264c-105">Sommige scenario's waarbij taakafhankelijkheden nuttig zijn omvatten:</span><span class="sxs-lookup"><span data-stu-id="e264c-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="e264c-106">MapReduce-stijl werkbelastingen in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="e264c-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="e264c-107">Taken waarvan gegevensverwerkingstaken kunnen worden uitgedrukt als een gerichte acyclische grafiek (DAG).</span><span class="sxs-lookup"><span data-stu-id="e264c-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="e264c-108">Voorweergave en na rendering processen, waarbij elke taak uitvoeren moet voordat de volgende taak Hallo kan beginnen.</span><span class="sxs-lookup"><span data-stu-id="e264c-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="e264c-109">Een andere taak waarbij downstream taken afhankelijk van het Hallo-uitvoer van de upstream-taken zijn.</span><span class="sxs-lookup"><span data-stu-id="e264c-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="e264c-110">Bij taakafhankelijkheden Batch kunt kunt u taken die zijn gepland voor uitvoering op rekenknooppunten na voltooiing van een of meer taken van de bovenliggende Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="e264c-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="e264c-111">U kunt bijvoorbeeld een taak die elk frame van een 3D-film met afzonderlijke, parallelle taken renders maken.</span><span class="sxs-lookup"><span data-stu-id="e264c-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="e264c-112">de laatste taak Hallo--Hallo 'merge taak'--samenvoegingen Hallo frames in Hallo alleen volledige film weergegeven nadat alle frames zijn correct weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e264c-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="e264c-113">Standaard worden afhankelijke taken gepland voor uitvoering pas nadat Hallo bovenliggende taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="e264c-114">U kunt een afhankelijkheid actie toooverride Hallo standaardgedrag opgeven en taken uitvoeren als Hallo bovenliggende taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e264c-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="e264c-115">Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e264c-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="e264c-116">U kunt taken die afhankelijk van andere taken in een-op-een- of een-op-veel-relatie zijn maken.</span><span class="sxs-lookup"><span data-stu-id="e264c-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="e264c-117">U kunt ook een bereik afhankelijkheid waar een taak van Hallo voltooiing van een groep taken binnen een opgegeven bereik van taak-id's afhangt maken.</span><span class="sxs-lookup"><span data-stu-id="e264c-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="e264c-118">U kunt deze drie basisscenario's toocreate veel-op-veel-relaties combineren.</span><span class="sxs-lookup"><span data-stu-id="e264c-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="e264c-119">Afhankelijkheden van de taak met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="e264c-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="e264c-120">In dit artikel bespreken we hoe tooconfigure taakafhankelijkheden met behulp van Hallo [Batch .NET] [ net_msdn] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="e264c-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="e264c-121">Laten we eerst zien u hoe te[afhankelijkheid inschakelen](#enable-task-dependencies) op uw taken, en vervolgens te laten zien hoe te[configureert u een taak met afhankelijkheden](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="e264c-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="e264c-122">Ook wordt beschreven hoe toospecify afhankelijkheid actie toorun afhankelijke taken als bovenliggende Hallo mislukt.</span><span class="sxs-lookup"><span data-stu-id="e264c-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="e264c-123">Ten slotte bespreken we Hallo [afhankelijkheid scenario's](#dependency-scenarios) die ondersteuning biedt voor Batch.</span><span class="sxs-lookup"><span data-stu-id="e264c-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="e264c-124">Taakafhankelijkheden inschakelen</span><span class="sxs-lookup"><span data-stu-id="e264c-124">Enable task dependencies</span></span>
<span data-ttu-id="e264c-125">taakafhankelijkheden toouse in uw Batch-toepassing, moet u eerst taakafhankelijkheden van Hallo taak toouse configureren.</span><span class="sxs-lookup"><span data-stu-id="e264c-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="e264c-126">In de Batch .NET inschakelen op uw [CloudJob] [ net_cloudjob] door in te stellen de [UsesTaskDependencies] [ net_usestaskdependencies] eigenschap te`true`:</span><span class="sxs-lookup"><span data-stu-id="e264c-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="e264c-127">In Hallo voorgaande codefragment, 'batchClient' is een exemplaar van Hallo [BatchClient] [ net_batchclient] klasse.</span><span class="sxs-lookup"><span data-stu-id="e264c-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="e264c-128">Afhankelijke taken maken</span><span class="sxs-lookup"><span data-stu-id="e264c-128">Create dependent tasks</span></span>
<span data-ttu-id="e264c-129">een taak die afhankelijk zijn van Hallo voltooiing van een of meer taken van de bovenliggende toocreate, kunt u die taak 'afhankelijk is van' Hallo Hallo andere taken.</span><span class="sxs-lookup"><span data-stu-id="e264c-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="e264c-130">Configureer in Batch .NET Hallo [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] eigenschap met een exemplaar van Hallo [taakafhankelijkheden] [ net_taskdependencies] klasse:</span><span class="sxs-lookup"><span data-stu-id="e264c-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="e264c-131">Dit codefragment maakt een afhankelijke taak met taak-ID 'Bloemen'.</span><span class="sxs-lookup"><span data-stu-id="e264c-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="e264c-132">Hallo 'Bloemen' taak afhankelijk is van taken 'Regen' en 'Sun'.</span><span class="sxs-lookup"><span data-stu-id="e264c-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="e264c-133">Taak 'Bloemen' worden geplande toorun op een rekenknooppunt alleen geldig na taken 'Regen' en 'Sun' zijn met succes voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="e264c-134">Een taak wordt beschouwd als toobe voltooid wanneer het zich in Hallo **voltooid** status en de bijbehorende **afsluitcode** is `0`.</span><span class="sxs-lookup"><span data-stu-id="e264c-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="e264c-135">In de Batch .NET, betekent dit een [CloudTask][net_cloudtask].[ Status] [ net_taskstate] waarde van de eigenschap `Completed` en Hallo van CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] waarde voor eigenschap `0`.</span><span class="sxs-lookup"><span data-stu-id="e264c-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="e264c-136">Afhankelijkheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="e264c-136">Dependency scenarios</span></span>
<span data-ttu-id="e264c-137">Er zijn drie algemene taak afhankelijkheid scenario's die u in Azure Batch gebruiken kunt:-op-een, een-op-veel en taak-ID bereik afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="e264c-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="e264c-138">Deze kunnen worden gecombineerd tooprovide een vierde scenario veel-op-veel.</span><span class="sxs-lookup"><span data-stu-id="e264c-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="e264c-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="e264c-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="e264c-140">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e264c-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="e264c-141">-Op-een</span><span class="sxs-lookup"><span data-stu-id="e264c-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="e264c-142">*Taakb* is afhankelijk van *Taaka*</span><span class="sxs-lookup"><span data-stu-id="e264c-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="e264c-143">*Taakb* zal niet worden gepland voor uitvoering tot *Taaka* is voltooid</span><span class="sxs-lookup"><span data-stu-id="e264c-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="e264c-144">![Diagram:-op-een afhankelijkheid][1]</span><span class="sxs-lookup"><span data-stu-id="e264c-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="e264c-145">Een-op-veel</span><span class="sxs-lookup"><span data-stu-id="e264c-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="e264c-146">*taakC* is afhankelijk van *taakA* én *taakB*</span><span class="sxs-lookup"><span data-stu-id="e264c-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="e264c-147">*Taakc* zal niet worden gepland voor uitvoering totdat beide *Taaka* en *Taakb* zijn met succes voltooid</span><span class="sxs-lookup"><span data-stu-id="e264c-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="e264c-148">![Diagram: een-op-veel-afhankelijkheid][2]</span><span class="sxs-lookup"><span data-stu-id="e264c-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="e264c-149">Taak-ID-bereik</span><span class="sxs-lookup"><span data-stu-id="e264c-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="e264c-150">*Taakd* afhankelijk is van een bereik van taken</span><span class="sxs-lookup"><span data-stu-id="e264c-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="e264c-151">*Taakd* zal niet worden gepland voor uitvoering tot Hallo taken met de id's *1* via *10* zijn met succes voltooid</span><span class="sxs-lookup"><span data-stu-id="e264c-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="e264c-152">![Diagram: Taak-id bereik afhankelijkheid][3]</span><span class="sxs-lookup"><span data-stu-id="e264c-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="e264c-153">U kunt maken **veel-op-veel** relaties, zoals waar taken C, D, E en F elke afhankelijk van taken A en B. zijn Dit is handig zijn, bijvoorbeeld in geparallelliseerde voorverwerking scenario's waar uw downstream taken afhankelijk van Hallo-uitvoer van meerdere upstream-taken zijn.</span><span class="sxs-lookup"><span data-stu-id="e264c-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="e264c-154">In Hallo voorbeelden in deze sectie wordt een afhankelijke taak alleen wordt uitgevoerd nadat Hallo bovenliggende taken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="e264c-155">Dit gedrag is Hallo standaardgedrag voor een afhankelijke taak.</span><span class="sxs-lookup"><span data-stu-id="e264c-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="e264c-156">Nadat een bovenliggende-taak is mislukt door te geven van een afhankelijkheid actie toooverride Hallo standaardgedrag, kunt u een afhankelijke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e264c-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="e264c-157">Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e264c-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="e264c-158">-Op-een</span><span class="sxs-lookup"><span data-stu-id="e264c-158">One-to-one</span></span>
<span data-ttu-id="e264c-159">Een taak afhankelijk is in een-op-een-relatie op Hallo van één bovenliggend taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="e264c-160">toocreate Hallo afhankelijkheid, Geef een enkele taak-ID toohello [taakafhankelijkheden][net_taskdependencies].[ OnId] [ net_onid] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e264c-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="e264c-161">Een-op-veel</span><span class="sxs-lookup"><span data-stu-id="e264c-161">One-to-many</span></span>
<span data-ttu-id="e264c-162">Een taak afhankelijk Hallo voltooiing van meerdere bovenliggende taken in een een-op-veel-relatie.</span><span class="sxs-lookup"><span data-stu-id="e264c-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="e264c-163">toocreate Hallo afhankelijkheid, een verzameling van taak-id's toohello bieden [taakafhankelijkheden][net_taskdependencies].[ OnIds] [ net_onids] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e264c-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="e264c-164">Taak-ID-bereik</span><span class="sxs-lookup"><span data-stu-id="e264c-164">Task ID range</span></span>
<span data-ttu-id="e264c-165">Een afhankelijkheid op een bereik van bovenliggende taken, wordt een taak afhangt van Hallo Hallo voltooiing van taken waarvoor id's binnen een bereik liggen.</span><span class="sxs-lookup"><span data-stu-id="e264c-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="e264c-166">toocreate hello afhankelijkheid, bieden Hallo eerste en laatste taak-id's in Hallo bereik toohello [taakafhankelijkheden][net_taskdependencies].[ OnIdRange] [ net_onidrange] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e264c-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e264c-167">Wanneer u bereiken voor taak-ID voor de afhankelijkheden, taak-id's in bereik Hallo Hallo *moet* tekenreeksrepresentaties van gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="e264c-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="e264c-168">Elke taak in Hallo bereik moet voldoen aan Hallo afhankelijkheid, door het voltooid of door te voeren met een fout die is toegewezen tooa afhankelijkheid actie instellen te**Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="e264c-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="e264c-169">Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e264c-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="e264c-170">Afhankelijkheid acties</span><span class="sxs-lookup"><span data-stu-id="e264c-170">Dependency actions</span></span>

<span data-ttu-id="e264c-171">Standaard wordt een afhankelijke taak of taken uitgevoerd nadat een bovenliggende-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="e264c-172">In sommige gevallen kunt u de afhankelijke taken toorun zelfs als Hallo bovenliggende taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e264c-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="e264c-173">U kunt standaardgedrag Hallo overschrijven door te geven van een afhankelijkheid in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="e264c-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="e264c-174">Een afhankelijkheid actie geeft aan of een afhankelijke taak in aanmerking komende toorun, op basis van Hallo slagen of mislukken van Hallo bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="e264c-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="e264c-175">Stel dat een afhankelijke taak wacht op gegevens van Hallo Hallo upstream-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e264c-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="e264c-176">Als Hallo upstream taak mislukt, Hallo afhankelijke taak nog steeds is mogelijk kunnen toorun met oudere gegevens.</span><span class="sxs-lookup"><span data-stu-id="e264c-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="e264c-177">In dit geval wordt kunt een afhankelijkheid actie opgeven dat afhankelijke taak Hallo in aanmerking komende toorun ondanks Hallo mislukken van Hallo bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="e264c-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="e264c-178">Een actie afhankelijkheid is gebaseerd op een voorwaarde voor het afsluiten voor Hallo bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="e264c-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="e264c-179">U kunt een afhankelijkheid actie voor een van de volgende afsluitvoorwaarden; Hallo opgeven Zie voor .NET, Hallo [ExitConditions] [ net_exitconditions] klasse voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="e264c-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="e264c-180">Als een vooraf verwerken fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="e264c-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="e264c-181">Fout treedt op wanneer een bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="e264c-181">When a file upload error occurs.</span></span> <span data-ttu-id="e264c-182">Als de taak Hallo met een afsluitcode die is opgegeven afgesloten via **exitCodes** of **exitCodeRanges**, en vervolgens dat een fout bij het uploaden, Hallo actie die is opgegeven door Hallo afsluiten code heeft een hogere prioriteit.</span><span class="sxs-lookup"><span data-stu-id="e264c-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="e264c-183">Wanneer de Hallo taak met de afsluitcode gedefinieerd door Hallo verlaat **ExitCodes** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e264c-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="e264c-184">Wanneer de taak Hallo verlaat met een afsluitcode die binnen een bereik dat is opgegeven door Hallo valt **ExitCodeRanges** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e264c-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="e264c-185">standaard-case Hallo als Hallo-taak wordt afgesloten met een afsluitcode die niet zijn gedefinieerd door **ExitCodes** of **ExitCodeRanges**, of als het Hallo-taak wordt afgesloten met een vooraf verwerken fout en Hallo **PreProcessingError**  eigenschap is niet ingesteld of als hello taak mislukt met een bestand uploadt u fout- en Hallo **FileUploadError** eigenschap is niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e264c-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="e264c-186">een actie afhankelijkheid in .NET set Hallo toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] eigenschap voor de voorwaarde voor het afsluiten van Hallo.</span><span class="sxs-lookup"><span data-stu-id="e264c-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="e264c-187">Hallo **DependencyAction** voor deze eigenschap is een van twee waarden:</span><span class="sxs-lookup"><span data-stu-id="e264c-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="e264c-188">Instelling Hallo **DependencyAction** eigenschap te**Satisfy** geeft aan dat de afhankelijke taken in aanmerking komende toorun zijn als Hallo bovenliggende taak wordt afgesloten met een opgegeven fout.</span><span class="sxs-lookup"><span data-stu-id="e264c-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="e264c-189">Instelling Hallo **DependencyAction** eigenschap te**blok** geeft aan dat afhankelijke taken niet in aanmerking komende toorun.</span><span class="sxs-lookup"><span data-stu-id="e264c-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="e264c-190">standaardinstelling voor Hallo Hallo **DependencyAction** eigenschap is **Satisfy** voor afsluitcode 0, en **blok** voor alle andere afsluitvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="e264c-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="e264c-191">Hallo volgende codefragment ingesteld Hallo **DependencyAction** eigenschap voor een bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="e264c-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="e264c-192">Als Hallo bovenliggende taak wordt afgesloten met een vooraf verwerken fout of Hello opgegeven foutcodes Hallo afhankelijke is taak geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e264c-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="e264c-193">Als Hallo bovenliggende taak met een andere niet-nul-fout afgesloten, is de afhankelijke taak Hallo in aanmerking komende toorun.</span><span class="sxs-lookup"><span data-stu-id="e264c-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="e264c-194">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="e264c-194">Code sample</span></span>
<span data-ttu-id="e264c-195">Hallo [taakafhankelijkheden] [ github_taskdependencies] voorbeeldproject is een van de Hallo [Azure Batch-codevoorbeelden] [ github_samples] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="e264c-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="e264c-196">Deze Visual Studio-oplossing wordt gedemonstreerd:</span><span class="sxs-lookup"><span data-stu-id="e264c-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="e264c-197">Hoe tooenable afhankelijkheid van een taak taak</span><span class="sxs-lookup"><span data-stu-id="e264c-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="e264c-198">Hoe toocreate taken die afhankelijk zijn van andere taken</span><span class="sxs-lookup"><span data-stu-id="e264c-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="e264c-199">Hoe tooexecute die taken op een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e264c-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e264c-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e264c-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="e264c-201">Toepassingsimplementatie</span><span class="sxs-lookup"><span data-stu-id="e264c-201">Application deployment</span></span>
<span data-ttu-id="e264c-202">Hallo [toepassingspakketten](batch-application-packages.md) functie van Batch biedt een eenvoudige manier tooboth implementeren en versie Hallo-toepassingen die uw taken uitvoeren op rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e264c-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="e264c-203">Installeren van toepassingen en gegevens voor fasering</span><span class="sxs-lookup"><span data-stu-id="e264c-203">Installing applications and staging data</span></span>
<span data-ttu-id="e264c-204">Zie [installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten] [ forum_post] in hello Azure Batch-forum voor een overzicht van de methoden voor het voorbereiden van uw knooppunten toorun taken.</span><span class="sxs-lookup"><span data-stu-id="e264c-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="e264c-205">Geschreven door een van de Azure Batch teamleden Hallo dat dit bericht is een goede primer op Hallo verschillende manieren toocopy toepassingen, rekenknooppunten invoergegevens van de taak en andere bestanden tooyour.</span><span class="sxs-lookup"><span data-stu-id="e264c-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram:-op-een afhankelijkheid"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: een-op-veel-afhankelijkheid"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: taak-id bereik afhankelijkheid"
