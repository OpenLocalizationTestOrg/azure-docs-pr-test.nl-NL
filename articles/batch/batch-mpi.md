---
title: Taken met meerdere instanties gebruiken voor het uitvoeren van MPI-toepassingen - Azure Batch | Microsoft Docs
description: Informatie over het gebruik van het type van de taak meerdere exemplaren in Azure Batch Message Passing Interface (MPI)-toepassingen uitvoeren.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="9ea46-103">Taken met meerdere instanties gebruiken Message Passing Interface (MPI)-toepassingen uitvoeren in Batch</span><span class="sxs-lookup"><span data-stu-id="9ea46-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="9ea46-104">Taken met meerdere instanties kunnen u een Azure Batch-taak tegelijkertijd op meerdere rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="9ea46-105">Deze taken kunnen high performance computing-scenario's zoals Message Passing Interface (MPI) applications in Batch.</span><span class="sxs-lookup"><span data-stu-id="9ea46-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="9ea46-106">In dit artikel leert u hoe uit te voeren taken met meerdere instanties met behulp van de [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="9ea46-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="9ea46-107">De voorbeelden in dit artikel ligt de nadruk op Batch .NET, MS-MPI en rekenknooppunten voor Windows, zijn die hier worden besproken concepten voor meerdere exemplaren taak van toepassing op andere platforms en -technologieën (Python en Intel MPI op Linux-knooppunten, bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="9ea46-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="9ea46-108">Overzicht van de taak meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="9ea46-108">Multi-instance task overview</span></span>
<span data-ttu-id="9ea46-109">In een Batch elke taak normaal wordt uitgevoerd op één rekenknooppunt--verzenden van meerdere taken aan een job en de Batch-service plant u elke taak voor uitvoering op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="9ea46-110">Echter, door het configureren van een taak **instellingen voor meerdere exemplaren van**, zien van Batch in plaats daarvan één primaire taak en verschillende subtaken die vervolgens worden uitgevoerd op meerdere knooppunten te maken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="9ea46-111">![Overzicht van de taak meerdere exemplaren][1]</span><span class="sxs-lookup"><span data-stu-id="9ea46-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="9ea46-112">Wanneer u een taak met meerdere exemplaren instellingen voor een taak indient, voert Batch in de verschillende stappen die uniek zijn voor taken met meerdere instanties:</span><span class="sxs-lookup"><span data-stu-id="9ea46-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="9ea46-113">De Batch-service maakt een **primaire** en verschillende **subtaken** op basis van de instellingen van meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="9ea46-114">Het totale aantal taken (primaire plus alle subtaken) overeenkomt met het aantal **exemplaren** (rekenknooppunten) u opgeeft in de instellingen van meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="9ea46-115">Batch wijst een van de rekenknooppunten als de **master**, en de belangrijkste taak moet worden uitgevoerd op de master plant.</span><span class="sxs-lookup"><span data-stu-id="9ea46-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="9ea46-116">Hiermee plant u de subtaken moet worden uitgevoerd op de rest van de rekenknooppunten die zijn toegewezen aan de taak met meerdere instanties, één subtaak per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="9ea46-117">De primaire server en alle subtaken downloaden **algemene bronbestanden** u opgeeft in de instellingen van meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="9ea46-118">Na de algemene resource bestanden zijn gedownload, de primaire en subtaken uit te voeren de **coördinatie opdracht** u opgeeft in de instellingen van meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="9ea46-119">De opdracht coördinatie wordt meestal gebruikt voor het voorbereiden van de knooppunten voor het uitvoeren van de taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="9ea46-120">Het kan hierbij gaan Achtergrondservices wordt gestart (zoals [Microsoft MPI][msmpi_msdn]van `smpd.exe`) en verifiëren dat de knooppunten gereed zijn voor verwerking van berichten tussen knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9ea46-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="9ea46-121">De belangrijkste taak wordt uitgevoerd de **toepassingsopdracht** op het hoofdknooppunt *nadat* de coördinatie-opdracht is voltooid door de primaire server en alle subtaken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="9ea46-122">De toepassingsopdracht wordt de opdrachtregel van de taak met meerdere instanties zelf en alleen door de belangrijkste taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="9ea46-123">In een [MS MPI][msmpi_msdn]-gebaseerde oplossing, dit is waar u uw MPI-toepassingen met uitvoeren `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="9ea46-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="9ea46-124">Hoewel functioneel distinct, de 'meerdere exemplaren-taak' is niet een unieke taaktype zoals de [StartTask] [ net_starttask] of [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="9ea46-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="9ea46-125">De taak meerdere exemplaren is gewoon een Batch standaardtaak ([CloudTask] [ net_task] in Batch .NET) waarvan u meerdere exemplaren de instellingen zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="9ea46-126">In dit artikel is als de **taak met meerdere instanties**.</span><span class="sxs-lookup"><span data-stu-id="9ea46-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="9ea46-127">Vereisten voor taken met meerdere instanties</span><span class="sxs-lookup"><span data-stu-id="9ea46-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="9ea46-128">Taken met meerdere instanties vereisen een pool met **communicatie tussen knooppunten ingeschakeld**, en met **uitvoering van gelijktijdige taken uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="9ea46-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="9ea46-129">Schakel de uitvoering van gelijktijdige taken instellen de [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) eigenschap in op 1.</span><span class="sxs-lookup"><span data-stu-id="9ea46-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="9ea46-130">Dit codefragment laat zien hoe een groep maken voor taken met meerdere instanties met behulp van de Batch .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="9ea46-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="9ea46-131">Als u probeert uit te voeren van een taak met meerdere instanties in een pool communicatie tussen knooppunten is uitgeschakeld of met een *maxTasksPerNode* waarde groter dan 1: de taak wordt nooit gepland--voor onbepaalde tijd blijft in de status 'active'.</span><span class="sxs-lookup"><span data-stu-id="9ea46-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="9ea46-132">Taken met meerdere instanties kunnen alleen op knooppunten in groepen die zijn gemaakt na 14 December 2015 uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="9ea46-133">StartTask gebruiken voor het installeren van MPI</span><span class="sxs-lookup"><span data-stu-id="9ea46-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="9ea46-134">Als u wilt uitvoeren van MPI-toepassingen met een taak meerdere exemplaren, moet u eerst een MPI-implementatie (MS-MPI of Intel MPI, bijvoorbeeld) installeren op de rekenknooppunten in de groep.</span><span class="sxs-lookup"><span data-stu-id="9ea46-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="9ea46-135">Dit is een goed moment om het gebruik van een [StartTask][net_starttask], die wordt uitgevoerd zodra er een knooppunt aan een pool wordt toegevoegd of opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="9ea46-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="9ea46-136">Dit codefragment maakt u een StartTask waarmee het MS MPI-installatiepakket als een [bronbestand][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="9ea46-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="9ea46-137">De begintaak vanaf de opdrachtregel wordt uitgevoerd nadat het bronbestand is gedownload naar het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="9ea46-138">In dit geval wordt voert de opdrachtregel een installatie zonder toezicht van MS MPI.</span><span class="sxs-lookup"><span data-stu-id="9ea46-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="9ea46-139">Remote direct memory access (RDMA)</span><span class="sxs-lookup"><span data-stu-id="9ea46-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="9ea46-140">Als u kiest een [RDMA-compatibele grootte](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) zoals A9 voor de rekenknooppunten in uw Batch-pool uw MPI-toepassingen kan profiteren van Azure hoge prestaties, lage latentie remote direct memory access (RDMA) netwerk.</span><span class="sxs-lookup"><span data-stu-id="9ea46-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="9ea46-141">Zoek naar de grootte die is opgegeven als 'RDMA-compatibele' in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="9ea46-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="9ea46-142">**CloudServiceConfiguration** pools</span><span class="sxs-lookup"><span data-stu-id="9ea46-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="9ea46-143">[Grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md) (alleen Windows)</span><span class="sxs-lookup"><span data-stu-id="9ea46-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="9ea46-144">**VirtualMachineConfiguration** pools</span><span class="sxs-lookup"><span data-stu-id="9ea46-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="9ea46-145">[Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="9ea46-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="9ea46-146">[Grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="9ea46-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="9ea46-147">Om te profiteren van RDMA op [Linux-rekenknooppunten](batch-linux-nodes.md), moet u **Intel MPI** op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9ea46-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="9ea46-148">Zie voor meer informatie over CloudServiceConfiguration en VirtualMachineConfiguration groepen de Pool-sectie van de [overzicht Batch-functies](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="9ea46-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="9ea46-149">Een taak meerdere exemplaren maken met de Batch .NET</span><span class="sxs-lookup"><span data-stu-id="9ea46-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="9ea46-150">Nu dat we de pool-vereisten en installatie van MPI-pakket besproken hebben, gaan we de taak meerdere exemplaren te maken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="9ea46-151">In dit fragment maken we een standaard [CloudTask][net_task], configureert u de [MultiInstanceSettings] [ net_multiinstance_prop] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9ea46-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="9ea46-152">Zoals eerder vermeld, wordt de taak meerdere exemplaren niet is een afzonderlijke taaktype, maar een Batch standaardtaak geconfigureerd met instellingen voor meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="9ea46-153">Primaire taken en subtaken</span><span class="sxs-lookup"><span data-stu-id="9ea46-153">Primary task and subtasks</span></span>
<span data-ttu-id="9ea46-154">Wanneer u de instellingen voor meerdere exemplaren van een taak maakt, geeft u het aantal rekenknooppunten die de taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="9ea46-155">Wanneer u de taak aan een job indient, maakt de Batch-service een **primaire** taak en er voldoende **subtaken** die samen overeenkomen met het aantal knooppunten dat u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9ea46-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="9ea46-156">Deze taken zijn toegewezen een integer-id in het bereik van 0 tot en met *numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="9ea46-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="9ea46-157">De taak met id 0 is de belangrijkste taak en andere id's subtaken zijn.</span><span class="sxs-lookup"><span data-stu-id="9ea46-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="9ea46-158">Als u de volgende instellingen voor meerdere instanties voor een taak maakt, de belangrijkste taak moet een id van 0 en subtaken ids 1 t/m 9 zou hebben.</span><span class="sxs-lookup"><span data-stu-id="9ea46-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="9ea46-159">Hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="9ea46-159">Master node</span></span>
<span data-ttu-id="9ea46-160">Wanneer u een taak met meerdere instanties verzendt, wordt de Batch-service wijst een van de rekenknooppunten als de 'master'-knooppunt en plant u de belangrijkste taak moet worden uitgevoerd op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="9ea46-161">De subtaken zijn gepland om uit te voeren op de rest van de knooppunten die zijn toegewezen aan de taak meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="9ea46-162">Coördinatie opdracht</span><span class="sxs-lookup"><span data-stu-id="9ea46-162">Coordination command</span></span>
<span data-ttu-id="9ea46-163">De **coördinatie opdracht** wordt uitgevoerd door de primaire en subtaken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="9ea46-164">Het aanroepen van de opdracht coördinatie blokkeert--Batch niet de toepassingsopdracht wordt uitgevoerd totdat de opdracht coördinatie met succes voor alle subtaken heeft geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="9ea46-165">De opdracht coördinatie moet daarom start alle vereiste Achtergrondservices, Ga na of deze klaar voor gebruik en sluit vervolgens af.</span><span class="sxs-lookup"><span data-stu-id="9ea46-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="9ea46-166">Bijvoorbeeld: met deze opdracht coördinatie voor een oplossing met behulp van MS MPI-versie 7 start de service SMPD op het knooppunt vervolgens afgesloten:</span><span class="sxs-lookup"><span data-stu-id="9ea46-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="9ea46-167">Let op het gebruik van `start` in deze opdracht coördinatie.</span><span class="sxs-lookup"><span data-stu-id="9ea46-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="9ea46-168">Dit is nodig omdat de `smpd.exe` toepassing geen retourneert onmiddellijk na de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="9ea46-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="9ea46-169">Zonder het gebruik van de [start] [ cmd_start] opdracht met deze opdracht coördinatie niet geretourneerd, en daarom aangeraden de toepassingsopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="9ea46-170">Toepassingsopdracht</span><span class="sxs-lookup"><span data-stu-id="9ea46-170">Application command</span></span>
<span data-ttu-id="9ea46-171">Zodra de belangrijkste taak en alle subtaken hebt uitvoeren van de opdracht coördinatie, opdrachtregel voor de meerdere exemplaren van de taak wordt uitgevoerd door de belangrijkste taak *alleen*.</span><span class="sxs-lookup"><span data-stu-id="9ea46-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="9ea46-172">We noemen dit de **toepassingsopdracht** te onderscheiden van de opdracht coördinatie.</span><span class="sxs-lookup"><span data-stu-id="9ea46-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="9ea46-173">Gebruik de toepassingsopdracht voor MS-MPI-toepassingen uitvoeren van MPI-toepassingen met `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="9ea46-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="9ea46-174">Dit is bijvoorbeeld een toepassingsopdracht voor een oplossing met behulp van MS-MPI versie 7:</span><span class="sxs-lookup"><span data-stu-id="9ea46-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="9ea46-175">Omdat MS-MPI `mpiexec.exe` maakt gebruik van de `CCP_NODES` variabele standaard (Zie [omgevingsvariabelen](#environment-variables)) het voorbeeld van de toepassing vanaf de opdrachtregel bovenstaande sluit het.</span><span class="sxs-lookup"><span data-stu-id="9ea46-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="9ea46-176">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="9ea46-176">Environment variables</span></span>
<span data-ttu-id="9ea46-177">Batch maakt verschillende [omgevingsvariabelen] [ msdn_env_var] specifiek voor taken met meerdere instanties op de rekenknooppunten die zijn toegewezen aan een taak meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="9ea46-178">Uw opdrachtregels coördinatie en toepassing kunt verwijzen naar van deze omgevingsvariabelen zoals u kunnen de scripts en programma's die ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="9ea46-179">De volgende omgevingsvariabelen zijn gemaakt door de Batch-service voor gebruik door meerdere exemplaren taken:</span><span class="sxs-lookup"><span data-stu-id="9ea46-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="9ea46-180">Zie voor meer details over deze en de andere Batch knooppunt omgevingsvariabelen COMPUTE, waaronder de inhoud en zichtbaarheid, [Compute knooppunt omgevingsvariabelen][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="9ea46-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="9ea46-181">Voorbeeld van de Batch Linux MPI-code bevat een voorbeeld van hoe diverse van deze omgevingsvariabelen kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="9ea46-182">De [coördinatie cmd] [ coord_cmd_example] Bash script downloadt algemene toepassing en invoer van Azure-opslag-bestanden, kunt u een share Network File System (NFS) op het hoofdknooppunt en configureert u de andere knooppunten toegewezen aan de taak met meerdere instanties als NFS-clients.</span><span class="sxs-lookup"><span data-stu-id="9ea46-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="9ea46-183">Bronbestanden</span><span class="sxs-lookup"><span data-stu-id="9ea46-183">Resource files</span></span>
<span data-ttu-id="9ea46-184">Er zijn twee sets van bronbestanden voor taken met meerdere instanties: **algemene bronbestanden** die *alle* taken downloaden (zowel de primaire en subtaken), en de **bronbestanden** opgegeven voor meerdere exemplaren van de taak zelf, die *alleen de primaire* downloads van de taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="9ea46-185">U kunt een of meer opgeven **algemene bronbestanden** in de instellingen voor meerdere instanties voor een taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="9ea46-186">Deze algemene resource-bestanden worden gedownload van [Azure Storage](../storage/common/storage-introduction.md) in elk knooppunt **taak gedeelde map** door de primaire server en alle subtaken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="9ea46-187">U kunt de gedeelde taakmap openen vanaf de toepassing en coördinatie opdrachtregels met behulp van de `AZ_BATCH_TASK_SHARED_DIR` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="9ea46-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="9ea46-188">De `AZ_BATCH_TASK_SHARED_DIR` pad is identiek zijn op elk knooppunt dat is toegewezen aan de taak met meerdere instanties, dus kunt u een opdracht één coördinatie tussen de primaire en alle subtaken delen.</span><span class="sxs-lookup"><span data-stu-id="9ea46-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="9ea46-189">Batch geen 'gedeeld' de map in een zin externe toegang, maar u kunt gebruiken als een koppeling of punt zoals eerder beschreven in de tip op omgevingsvariabelen delen.</span><span class="sxs-lookup"><span data-stu-id="9ea46-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="9ea46-190">Bronbestanden die u opgeeft voor de taak met meerdere instanties zelf worden gedownload naar de werkmap van de taak, `AZ_BATCH_TASK_WORKING_DIR`, standaard.</span><span class="sxs-lookup"><span data-stu-id="9ea46-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="9ea46-191">Zoals gezegd, in tegenstelling tot de bronbestanden voor algemene, downloadt alleen de belangrijkste taak resource-bestanden opgegeven voor de taak met meerdere instanties zelf.</span><span class="sxs-lookup"><span data-stu-id="9ea46-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ea46-192">Gebruik altijd de omgevingsvariabelen `AZ_BATCH_TASK_SHARED_DIR` en `AZ_BATCH_TASK_WORKING_DIR` om te verwijzen naar deze mappen in uw opdrachtregels.</span><span class="sxs-lookup"><span data-stu-id="9ea46-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="9ea46-193">Probeer niet de paden handmatig maken.</span><span class="sxs-lookup"><span data-stu-id="9ea46-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="9ea46-194">Taak levensduur</span><span class="sxs-lookup"><span data-stu-id="9ea46-194">Task lifetime</span></span>
<span data-ttu-id="9ea46-195">De levensduur van de belangrijkste taak bepaalt de levensduur van de taak voor volledige meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9ea46-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="9ea46-196">Wanneer de primaire wordt afgesloten, worden alle subtaken beëindigd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="9ea46-197">De afsluitcode van de primaire is de afsluitcode van de taak en wordt daarom gebruikt om te bepalen het slagen of mislukken van de taak voor opnieuw proberen doeleinden.</span><span class="sxs-lookup"><span data-stu-id="9ea46-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="9ea46-198">Als een van de subtaken mislukt, afgesloten met een niet-nul-retourcode, bijvoorbeeld de volledige meerdere exemplaren taak mislukt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="9ea46-199">De taak met meerdere instanties vervolgens wordt beëindigd en opnieuw worden geprobeerd tot de limiet voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="9ea46-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="9ea46-200">Wanneer u een taak met meerdere instanties verwijdert, worden ook de primaire server en alle subtaken verwijderd door de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="9ea46-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="9ea46-201">Alle mappen een subtaak en hun bestanden worden verwijderd uit de rekenknooppunten, net als voor een taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="9ea46-202">[TaskConstraints] [ net_taskconstraints] voor een taak met meerdere instanties, zoals de [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], en [RetentionTime] [ net_taskconstraint_retention] -eigenschappen, zoals ze zijn voor een standaardtaak en gelden voor de primaire server en alle subtaken worden gehonoreerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="9ea46-203">Echter, als u wijzigt de [RetentionTime] [ net_taskconstraint_retention] eigenschap na het toevoegen van de taak met meerdere instanties voor de job deze wijziging wordt alleen toegepast op de belangrijkste taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="9ea46-204">Alle subtaken blijven gebruiken van de oorspronkelijke [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="9ea46-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="9ea46-205">Een rekenknooppunt lijst met recente taken komt overeen met de id van een subtaak als de recente taak deel van een taak meerdere exemplaren uitmaakte.</span><span class="sxs-lookup"><span data-stu-id="9ea46-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="9ea46-206">Verzamel informatie over subtaken</span><span class="sxs-lookup"><span data-stu-id="9ea46-206">Obtain information about subtasks</span></span>
<span data-ttu-id="9ea46-207">Aanroepen om informatie te verkrijgen op subtaken met behulp van de Batch .NET-bibliotheek, de [CloudTask.ListSubtasks] [ net_task_listsubtasks] methode.</span><span class="sxs-lookup"><span data-stu-id="9ea46-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="9ea46-208">Deze methode retourneert informatie over alle subtaken en informatie over het rekenknooppunt die de taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="9ea46-209">Met deze informatie kunt u bepalen de hoofdmap van elke subtaak, de pool-id, de huidige status, afsluitcode en meer.</span><span class="sxs-lookup"><span data-stu-id="9ea46-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="9ea46-210">U kunt deze informatie gebruiken in combinatie met de [PoolOperations.GetNodeFile] [ poolops_getnodefile] methode van de subtaak-bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="9ea46-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="9ea46-211">Houd er rekening mee dat deze methode heeft geen informatie geretourneerd voor de belangrijkste taak (id 0).</span><span class="sxs-lookup"><span data-stu-id="9ea46-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="9ea46-212">Tenzij anders vermeld, Batch .NET-methoden die worden uitgevoerd voor meerdere exemplaren [CloudTask] [ net_task] zelf toepassen *alleen* voor de primaire taak.</span><span class="sxs-lookup"><span data-stu-id="9ea46-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="9ea46-213">Bijvoorbeeld, als u aanroept de [CloudTask.ListNodeFiles] [ net_task_listnodefiles] methode op een taak met meerdere instanties, alleen de belangrijkste taak bestanden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="9ea46-214">Het volgende codefragment laat zien hoe subtaak informatie verkrijgen, evenals bestandsinhoud aanvragen bij de knooppunten waarop ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="9ea46-215">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="9ea46-215">Code sample</span></span>
<span data-ttu-id="9ea46-216">De [MultiInstanceTasks] [ github_mpi] codevoorbeeld op GitHub laat zien hoe een taak met meerdere instanties gebruiken om uit te voeren een [MS MPI] [ msmpi_msdn] toepassing op Batch-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="9ea46-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="9ea46-217">Volg de stappen in [voorbereiding](#preparation) en [uitvoering](#execution) om uit te voeren van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9ea46-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="9ea46-218">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="9ea46-218">Preparation</span></span>
1. <span data-ttu-id="9ea46-219">De eerste twee stappen in [compileren en uitvoeren van een eenvoudig MS MPI-programma][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="9ea46-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="9ea46-220">Dit voldoet aan de prerequesites voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="9ea46-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="9ea46-221">Bouwen een *Release* versie van de [MPIHelloWorld] [ helloworld_proj] MPI voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="9ea46-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="9ea46-222">Dit is het programma dat door de taak met meerdere instanties op rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ea46-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="9ea46-223">Maak een zip-bestand met `MPIHelloWorld.exe` (die u hebt gebouwd stap 2) en `MSMpiSetup.exe` (die u hebt gedownload stap 1).</span><span class="sxs-lookup"><span data-stu-id="9ea46-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="9ea46-224">U hebt dit zipbestand uploaden als een toepassingspakket in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="9ea46-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="9ea46-225">Gebruik de [Azure-portal] [ portal] voor het maken van een Batch [toepassing](batch-application-packages.md) 'MPIHelloWorld' genoemd en geef het zip-bestand dat u in de vorige stap hebt gemaakt als "1.0" versie van de toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="9ea46-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="9ea46-226">Zie [uploaden en beheren van toepassingen](batch-application-packages.md#upload-and-manage-applications) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9ea46-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="9ea46-227">Bouwen een *Release* versie van `MPIHelloWorld.exe` zodat u hoeft extra afhankelijkheden zijn (bijvoorbeeld `msvcp140d.dll` of `vcruntime140d.dll`) in het toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="9ea46-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="9ea46-228">Uitvoering</span><span class="sxs-lookup"><span data-stu-id="9ea46-228">Execution</span></span>
1. <span data-ttu-id="9ea46-229">Download de [azure-batch-samples] [ github_samples_zip] vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ea46-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="9ea46-230">Open de MultiInstanceTasks **oplossing** in Visual Studio 2015 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9ea46-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="9ea46-231">De `MultiInstanceTasks.sln` oplossingsbestand bevindt zich in:</span><span class="sxs-lookup"><span data-stu-id="9ea46-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="9ea46-232">Voer uw referenties in Batch- en Storage-account in `AccountSettings.settings` in de **Microsoft.Azure.Batch.Samples.Common** project.</span><span class="sxs-lookup"><span data-stu-id="9ea46-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="9ea46-233">**Bouwen en uitvoeren van** de MultiInstanceTasks oplossing voor het uitvoeren van de MPI-voorbeeldtoepassing op rekenknooppunten in een Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="9ea46-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="9ea46-234">*Optionele*: Gebruik de [Azure-portal] [ portal] of de [Batch Explorer] [ batch_explorer] om te onderzoeken van de voorbeeld-pool, Jobs en taak (' MultiInstanceSamplePool', 'MultiInstanceSampleJob', "MultiInstanceSampleTask") voordat u de resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9ea46-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="9ea46-235">U kunt downloaden [Visual Studio Community] [ visual_studio] gratis als u Visual Studio niet hebt.</span><span class="sxs-lookup"><span data-stu-id="9ea46-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="9ea46-236">De uitvoer van `MultiInstanceTasks.exe` is vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="9ea46-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="9ea46-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ea46-237">Next steps</span></span>
* <span data-ttu-id="9ea46-238">De Microsoft HPC & Azure Batch-Team blog besproken [MPI-ondersteuning voor Linux op Azure Batch][blog_mpi_linux], en bevat informatie over het gebruik van [OpenFOAM] [ openfoam] met Batch.</span><span class="sxs-lookup"><span data-stu-id="9ea46-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="9ea46-239">Vindt u voorbeelden van Python-code voor de [OpenFOAM voorbeeld op GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="9ea46-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="9ea46-240">Meer informatie over hoe [maken van groepen van Linux-rekenknooppunten](batch-linux-nodes.md) voor gebruik in uw Azure Batch MPI-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="9ea46-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Overzicht van meerdere exemplaren"
