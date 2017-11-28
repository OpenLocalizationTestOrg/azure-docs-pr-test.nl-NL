---
title: Taakafhankelijkheden gebruiken voor het uitvoeren van taken op basis van de voltooiing van andere taken - Azure Batch | Microsoft Docs
description: Taken maken die afhankelijk van de voltooiing van andere taken zijn voor het verwerken van MapReduce-stijl en vergelijkbare big data werkbelastingen in Azure Batch.
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
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="eeefd-103">Maak taakafhankelijkheden taken die afhankelijk van andere taken zijn uitvoeren</span><span class="sxs-lookup"><span data-stu-id="eeefd-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="eeefd-104">Taakafhankelijkheden om een taak of taken worden uitgevoerd nadat een bovenliggende-taak is voltooid, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="eeefd-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="eeefd-105">Sommige scenario's waarbij taakafhankelijkheden nuttig zijn omvatten:</span><span class="sxs-lookup"><span data-stu-id="eeefd-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="eeefd-106">MapReduce-stijl-workloads in de cloud.</span><span class="sxs-lookup"><span data-stu-id="eeefd-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="eeefd-107">Taken waarvan gegevensverwerkingstaken kunnen worden uitgedrukt als een gerichte acyclische grafiek (DAG).</span><span class="sxs-lookup"><span data-stu-id="eeefd-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="eeefd-108">Rendering van vóór en na het opbouwen van processen, waarbij elke taak voordat u de volgende taak uitvoeren moet kunnen beginnen.</span><span class="sxs-lookup"><span data-stu-id="eeefd-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="eeefd-109">Een andere taak waarbij downstream taken afhankelijk van de uitvoer van de upstream-taken zijn.</span><span class="sxs-lookup"><span data-stu-id="eeefd-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="eeefd-110">Bij taakafhankelijkheden Batch kunt kunt u taken die zijn gepland voor uitvoering op rekenknooppunten na de voltooiing van een of meer bovenliggende taken maken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="eeefd-111">U kunt bijvoorbeeld een taak die elk frame van een 3D-film met afzonderlijke, parallelle taken renders maken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="eeefd-112">De laatste taak--de 'merge taak'--samenvoegingen de gerenderde frames in de volledige film pas nadat alle frames hebt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="eeefd-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="eeefd-113">Standaard worden afhankelijke taken gepland voor uitvoering pas nadat de bovenliggende taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="eeefd-114">U kunt opgeven dat een afhankelijkheid actie voor het standaardgedrag negeren en taken uitvoeren als de bovenliggende taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="eeefd-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="eeefd-115">Zie de [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eeefd-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="eeefd-116">U kunt taken die afhankelijk van andere taken in een-op-een- of een-op-veel-relatie zijn maken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="eeefd-117">U kunt ook een bereik afhankelijkheid waar een taak afhankelijk van de voltooiing van een groep taken binnen een opgegeven bereik van taak-id's is maken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="eeefd-118">U kunt deze drie basisscenario's voor het maken van veel-op-veel-relaties combineren.</span><span class="sxs-lookup"><span data-stu-id="eeefd-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="eeefd-119">Afhankelijkheden van de taak met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="eeefd-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="eeefd-120">In dit artikel wordt besproken hoe we taakafhankelijkheden configureren met behulp van de [Batch .NET] [ net_msdn] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="eeefd-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="eeefd-121">Laten we eerst zien u hoe aan [afhankelijkheid inschakelen](#enable-task-dependencies) op uw taken, en vervolgens te demonstreren hoe [configureert u een taak met afhankelijkheden](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="eeefd-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="eeefd-122">We beschrijven ook het opgeven van een afhankelijkheid actie om uit te voeren van afhankelijke taken als het bovenliggende item is mislukt.</span><span class="sxs-lookup"><span data-stu-id="eeefd-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="eeefd-123">Ten slotte bespreken we de [afhankelijkheid scenario's](#dependency-scenarios) die ondersteuning biedt voor Batch.</span><span class="sxs-lookup"><span data-stu-id="eeefd-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="eeefd-124">Taakafhankelijkheden inschakelen</span><span class="sxs-lookup"><span data-stu-id="eeefd-124">Enable task dependencies</span></span>
<span data-ttu-id="eeefd-125">Als u taakafhankelijkheden in uw Batch-toepassing, moet u eerst de taak voor het gebruik van taakafhankelijkheden configureren.</span><span class="sxs-lookup"><span data-stu-id="eeefd-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="eeefd-126">In de Batch .NET inschakelen op uw [CloudJob] [ net_cloudjob] door in te stellen de [UsesTaskDependencies] [ net_usestaskdependencies] eigenschap `true`:</span><span class="sxs-lookup"><span data-stu-id="eeefd-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="eeefd-127">In het bovenstaande codefragment 'batchClient' is een exemplaar van de [BatchClient] [ net_batchclient] klasse.</span><span class="sxs-lookup"><span data-stu-id="eeefd-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="eeefd-128">Afhankelijke taken maken</span><span class="sxs-lookup"><span data-stu-id="eeefd-128">Create dependent tasks</span></span>
<span data-ttu-id="eeefd-129">U kunt opgeven dat de taak 'afhankelijk van' de andere taken is voor het maken van een taak die afhankelijk zijn van de voltooiing van een of meer bovenliggende taken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="eeefd-130">In de Batch .NET, configureert u de [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] eigenschap met een exemplaar van de [taakafhankelijkheden] [ net_taskdependencies] klasse:</span><span class="sxs-lookup"><span data-stu-id="eeefd-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="eeefd-131">Dit codefragment maakt een afhankelijke taak met taak-ID 'Bloemen'.</span><span class="sxs-lookup"><span data-stu-id="eeefd-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="eeefd-132">De taak 'Bloemen', is afhankelijk van taken 'Regen' en 'Sun'.</span><span class="sxs-lookup"><span data-stu-id="eeefd-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="eeefd-133">Taak 'bloemen' gepland moet worden uitgevoerd op een rekenknooppunt alleen na taken 'Regen' en 'Sun' zijn met succes voltooid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="eeefd-134">Een taak wordt beschouwd als is voltooid als het in de **voltooid** status en de bijbehorende **afsluitcode** is `0`.</span><span class="sxs-lookup"><span data-stu-id="eeefd-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="eeefd-135">In de Batch .NET, betekent dit een [CloudTask][net_cloudtask].[ Status] [ net_taskstate] waarde van de eigenschap `Completed` en de CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] waarde voor eigenschap `0`.</span><span class="sxs-lookup"><span data-stu-id="eeefd-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="eeefd-136">Afhankelijkheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="eeefd-136">Dependency scenarios</span></span>
<span data-ttu-id="eeefd-137">Er zijn drie algemene taak afhankelijkheid scenario's die u in Azure Batch gebruiken kunt:-op-een, een-op-veel en taak-ID bereik afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="eeefd-138">Deze kunnen worden gecombineerd om een vierde veel-op-veel-scenario.</span><span class="sxs-lookup"><span data-stu-id="eeefd-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="eeefd-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="eeefd-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="eeefd-140">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="eeefd-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="eeefd-141">-Op-een</span><span class="sxs-lookup"><span data-stu-id="eeefd-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="eeefd-142">*Taakb* is afhankelijk van *Taaka*</span><span class="sxs-lookup"><span data-stu-id="eeefd-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="eeefd-143">*Taakb* zal niet worden gepland voor uitvoering tot *Taaka* is voltooid</span><span class="sxs-lookup"><span data-stu-id="eeefd-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="eeefd-144">![Diagram:-op-een afhankelijkheid][1]</span><span class="sxs-lookup"><span data-stu-id="eeefd-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="eeefd-145">Een-op-veel</span><span class="sxs-lookup"><span data-stu-id="eeefd-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="eeefd-146">*taakC* is afhankelijk van *taakA* én *taakB*</span><span class="sxs-lookup"><span data-stu-id="eeefd-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="eeefd-147">*Taakc* zal niet worden gepland voor uitvoering totdat beide *Taaka* en *Taakb* zijn met succes voltooid</span><span class="sxs-lookup"><span data-stu-id="eeefd-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="eeefd-148">![Diagram: een-op-veel-afhankelijkheid][2]</span><span class="sxs-lookup"><span data-stu-id="eeefd-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="eeefd-149">Taak-ID-bereik</span><span class="sxs-lookup"><span data-stu-id="eeefd-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="eeefd-150">*Taakd* afhankelijk is van een bereik van taken</span><span class="sxs-lookup"><span data-stu-id="eeefd-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="eeefd-151">*Taakd* zal niet worden gepland voor uitvoering totdat de taken met de id's *1* via *10* zijn met succes voltooid</span><span class="sxs-lookup"><span data-stu-id="eeefd-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="eeefd-152">![Diagram: Taak-id bereik afhankelijkheid][3]</span><span class="sxs-lookup"><span data-stu-id="eeefd-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="eeefd-153">U kunt maken **veel-op-veel** relaties, zoals waar taken C, D, E en F elke afhankelijk van taken A en B. zijn Dit is handig zijn, bijvoorbeeld in geparallelliseerde voorverwerking scenario's waar uw downstream taken afhankelijk van de uitvoer van meerdere upstream-taken zijn.</span><span class="sxs-lookup"><span data-stu-id="eeefd-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="eeefd-154">In de voorbeelden in deze sectie wordt een afhankelijke taak alleen wordt uitgevoerd nadat de bovenliggende taken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="eeefd-155">Dit gedrag is het standaardgedrag voor een afhankelijke taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="eeefd-156">Nadat een bovenliggende-taak is mislukt door te geven van een afhankelijkheid-actie voor het standaardgedrag negeren, kunt u een afhankelijke taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eeefd-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="eeefd-157">Zie de [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eeefd-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="eeefd-158">-Op-een</span><span class="sxs-lookup"><span data-stu-id="eeefd-158">One-to-one</span></span>
<span data-ttu-id="eeefd-159">In een-op-een-relatie is een taak afhankelijk is van een bovenliggende taak voltooid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="eeefd-160">Voor het maken van de afhankelijkheid bieden een enkele taak-ID toe aan de [taakafhankelijkheden][net_taskdependencies].[ OnId] [ net_onid] statische methode wanneer u de waarden voor de [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="eeefd-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="eeefd-161">Een-op-veel</span><span class="sxs-lookup"><span data-stu-id="eeefd-161">One-to-many</span></span>
<span data-ttu-id="eeefd-162">In een een-op-veel-relatie is een taak afhankelijk van de voltooiing van taken met meerdere bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="eeefd-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="eeefd-163">Geef een verzameling van taak-id's voor het maken van de afhankelijkheid de [taakafhankelijkheden][net_taskdependencies].[ OnIds] [ net_onids] statische methode wanneer u de waarden voor de [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="eeefd-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="eeefd-164">Taak-ID-bereik</span><span class="sxs-lookup"><span data-stu-id="eeefd-164">Task ID range</span></span>
<span data-ttu-id="eeefd-165">Een afhankelijkheid op een bereik van bovenliggende taken een taak afhankelijk is van de de voltooiing van taken waarvoor id's binnen een bereik liggen.</span><span class="sxs-lookup"><span data-stu-id="eeefd-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="eeefd-166">De afhankelijkheid maken, geef de eerste en laatste taak-id's in het bereik tot de [taakafhankelijkheden][net_taskdependencies].[ OnIdRange] [ net_onidrange] statische methode wanneer u de waarden voor de [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="eeefd-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eeefd-167">Als u een taak-ID adresbereiken gebruikt voor uw afhankelijkheden, taak-id's in het bereik *moet* tekenreeksrepresentaties van gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="eeefd-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="eeefd-168">Elke taak in het bereik moet voldoen aan de afhankelijkheid door voltooid, of door te voeren met een fout die toegewezen aan een afhankelijkheid-actie ingesteld op **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="eeefd-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="eeefd-169">Zie de [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eeefd-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="eeefd-170">Afhankelijkheid acties</span><span class="sxs-lookup"><span data-stu-id="eeefd-170">Dependency actions</span></span>

<span data-ttu-id="eeefd-171">Standaard wordt een afhankelijke taak of taken uitgevoerd nadat een bovenliggende-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eeefd-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="eeefd-172">In sommige gevallen wilt u mogelijk afhankelijke taken uitvoeren, zelfs als de bovenliggende taak mislukt.</span><span class="sxs-lookup"><span data-stu-id="eeefd-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="eeefd-173">U kunt het standaardgedrag negeren door op te geven van een afhankelijkheid in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="eeefd-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="eeefd-174">Een afhankelijkheid actie geeft aan of een afhankelijke taak kunnen worden uitgevoerd, op basis van het slagen of mislukken van de bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="eeefd-175">Stel dat een afhankelijke taak wacht op gegevens van de voltooiing van de upstream-taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="eeefd-176">Als de upstream-taak is mislukt, de afhankelijke taak nog steeds mogelijk uitgevoerd met behulp van oudere gegevens.</span><span class="sxs-lookup"><span data-stu-id="eeefd-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="eeefd-177">In dit geval kunt een afhankelijkheid actie opgeven dat de afhankelijke taak in aanmerking komt ondanks het mislukken van de bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="eeefd-178">Een actie afhankelijkheid is gebaseerd op een voorwaarde voor het afsluiten van de bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="eeefd-179">U kunt opgeven dat de actie van een afhankelijkheid voor een van de volgende afsluitvoorwaarden; Zie voor .NET, de [ExitConditions] [ net_exitconditions] klasse voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="eeefd-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="eeefd-180">Als een vooraf verwerken fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="eeefd-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="eeefd-181">Fout treedt op wanneer een bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="eeefd-181">When a file upload error occurs.</span></span> <span data-ttu-id="eeefd-182">Als de taak moet worden afgesloten met een afsluitcode die is opgegeven via **exitCodes** of **exitCodeRanges**, en vervolgens een bestand geüpload fout, de actie die is opgegeven door de afsluitcode tegenkomt voorrang heeft.</span><span class="sxs-lookup"><span data-stu-id="eeefd-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="eeefd-183">Wanneer de taak wordt afgesloten met een afsluitcode die zijn gedefinieerd door de **ExitCodes** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="eeefd-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="eeefd-184">Wanneer de taak wordt afgesloten met een afsluitcode die binnen een bereik dat is opgegeven valt door de **ExitCodeRanges** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="eeefd-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="eeefd-185">De standaard-case, als de taak wordt afgesloten met een afsluitcode die niet zijn gedefinieerd door **ExitCodes** of **ExitCodeRanges**, of als de taak wordt afgesloten met een vooraf verwerken fout en de **PreProcessingError** eigenschap niet is ingesteld, of als de taak met een bestand mislukt fout bij het uploaden en de **FileUploadError** eigenschap is niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="eeefd-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="eeefd-186">Als een afhankelijkheid actie in .NET opgeven, stelt u de [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] eigenschap voor de voorwaarde voor het afsluiten.</span><span class="sxs-lookup"><span data-stu-id="eeefd-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="eeefd-187">De **DependencyAction** voor deze eigenschap is een van twee waarden:</span><span class="sxs-lookup"><span data-stu-id="eeefd-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="eeefd-188">Instellen van de **DependencyAction** eigenschap **Satisfy** geeft aan dat afhankelijke taken kunnen worden uitgevoerd als de bovenliggende taak wordt afgesloten met een opgegeven fout.</span><span class="sxs-lookup"><span data-stu-id="eeefd-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="eeefd-189">Instellen van de **DependencyAction** eigenschap **blok** geeft aan dat afhankelijke taken niet kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eeefd-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="eeefd-190">De standaardinstelling voor de **DependencyAction** eigenschap is **Satisfy** voor afsluitcode 0, en **blok** voor alle andere afsluitvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="eeefd-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="eeefd-191">De volgende code codefragment stelt de **DependencyAction** eigenschap voor een bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="eeefd-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="eeefd-192">Als de bovenliggende taak met een vooraf verwerken fout of met de opgegeven foutcodes afgesloten, wordt de afhankelijke taak geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="eeefd-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="eeefd-193">Als de bovenliggende taak met een andere niet-nul-fout afgesloten, komt de afhankelijke taak in aanmerking om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="eeefd-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
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
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="eeefd-194">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="eeefd-194">Code sample</span></span>
<span data-ttu-id="eeefd-195">De [taakafhankelijkheden] [ github_taskdependencies] voorbeeldproject is een van de [Azure Batch-codevoorbeelden] [ github_samples] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="eeefd-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="eeefd-196">Deze Visual Studio-oplossing wordt gedemonstreerd:</span><span class="sxs-lookup"><span data-stu-id="eeefd-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="eeefd-197">Het inschakelen van taakafhankelijkheid op een andere taak</span><span class="sxs-lookup"><span data-stu-id="eeefd-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="eeefd-198">Taken die afhankelijk van andere taken zijn maken</span><span class="sxs-lookup"><span data-stu-id="eeefd-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="eeefd-199">Klik hier voor meer informatie over het uitvoeren van deze taken op een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="eeefd-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeefd-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eeefd-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="eeefd-201">Toepassingsimplementatie</span><span class="sxs-lookup"><span data-stu-id="eeefd-201">Application deployment</span></span>
<span data-ttu-id="eeefd-202">De [toepassingspakketten](batch-application-packages.md) functie van Batch biedt een eenvoudige manier om beide te implementeren en de rekenknooppunten van de toepassingen die uw taken uitvoeren op versie.</span><span class="sxs-lookup"><span data-stu-id="eeefd-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="eeefd-203">Installeren van toepassingen en gegevens voor fasering</span><span class="sxs-lookup"><span data-stu-id="eeefd-203">Installing applications and staging data</span></span>
<span data-ttu-id="eeefd-204">Zie [installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten] [ forum_post] in het Azure Batch-forum voor een overzicht van de methoden voor het voorbereiden van uw knooppunten om uit te voeren taken.</span><span class="sxs-lookup"><span data-stu-id="eeefd-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="eeefd-205">Dit bericht is geschreven door een van de Azure Batch-teamleden, is een goede primer op de verschillende manieren toepassingen, invoergegevens van de taak en andere bestanden kopiëren naar uw rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="eeefd-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

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

<span data-ttu-id="eeefd-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram:-op-een afhankelijkheid"</span><span class="sxs-lookup"><span data-stu-id="eeefd-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="eeefd-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: een-op-veel-afhankelijkheid"</span><span class="sxs-lookup"><span data-stu-id="eeefd-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="eeefd-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: taak-id bereik afhankelijkheid"</span><span class="sxs-lookup"><span data-stu-id="eeefd-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
