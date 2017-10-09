---
title: meerdere exemplaren van aaaUse taken toorun MPI-toepassingen - Azure Batch | Microsoft Docs
description: Meer informatie over hoe tooexecute Message Passing Interface (MPI)-toepassingen met behulp van de taak met meerdere instanties Hallo typt u in Azure Batch.
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="39e44-103">Gebruik van meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Batch</span><span class="sxs-lookup"><span data-stu-id="39e44-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="39e44-104">Taken met meerdere instanties kunnen u een Azure Batch-taak toorun op meerdere rekenknooppunten tegelijk.</span><span class="sxs-lookup"><span data-stu-id="39e44-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="39e44-105">Deze taken kunnen high performance computing-scenario's zoals Message Passing Interface (MPI) applications in Batch.</span><span class="sxs-lookup"><span data-stu-id="39e44-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="39e44-106">In dit artikel leert u hoe taken met meerdere instanties tooexecute met Hallo [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="39e44-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="39e44-107">Terwijl de rekenknooppunten van Windows hello voorbeelden in dit artikel ligt de nadruk op Batch .NET, MS-MPI zijn Hallo meerdere exemplaren taak concepten die hier worden besproken tooother toepasselijke platforms en -technologieën (Python en Intel MPI op Linux-knooppunten, bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="39e44-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="39e44-108">Overzicht van de taak meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="39e44-108">Multi-instance task overview</span></span>
<span data-ttu-id="39e44-109">In een Batch elke taak normaal wordt uitgevoerd op één rekenknooppunt--u bij het verzenden van meerdere taken tooa taak en plant u elke taak voor uitvoering op een knooppunt dat Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="39e44-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="39e44-110">Echter, door het configureren van een taak **meerdere exemplaren instellingen**, zien van Batch tooinstead één primaire taak en verschillende subtaken die vervolgens worden uitgevoerd op meerdere knooppunten maken.</span><span class="sxs-lookup"><span data-stu-id="39e44-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="39e44-111">![Overzicht van de taak meerdere exemplaren][1]</span><span class="sxs-lookup"><span data-stu-id="39e44-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="39e44-112">Wanneer u een taak met meerdere exemplaren instellingen tooa taak indient, Batch verschillende stappen unieke toomulti-exemplaar taken worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="39e44-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="39e44-113">Hallo Batch-service maakt een **primaire** en verschillende **subtaken** op basis van Hallo meerdere exemplaren instellingen.</span><span class="sxs-lookup"><span data-stu-id="39e44-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="39e44-114">Hallo kunt u het totale aantal taken (primaire plus alle subtaken) overeenkomt met Hallo aantal **exemplaren** (rekenknooppunten) u opgeeft in Hallo meerdere exemplaren instellingen.</span><span class="sxs-lookup"><span data-stu-id="39e44-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="39e44-115">Batch wordt aangegeven dat een Hallo rekenknooppunten hello **master**, en schema's Hallo primaire taak tooexecute op Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="39e44-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="39e44-116">Hiermee plant u Hallo subtaken tooexecute op Hallo rest van de taak met Hallo compute knooppunten toegewezen toohello meerdere instanties, één subtaak per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="39e44-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="39e44-117">Hallo primaire en alle subtaken downloaden **algemene bronbestanden** u opgeeft in Hallo meerdere exemplaren instellingen.</span><span class="sxs-lookup"><span data-stu-id="39e44-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="39e44-118">Nadat u algemene bronbestanden Hallo zijn gedownload, Hallo primaire en subtaken Hallo uitvoeren **coördinatie opdracht** u opgeeft in Hallo meerdere exemplaren instellingen.</span><span class="sxs-lookup"><span data-stu-id="39e44-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="39e44-119">Hallo coördinatie opdracht is gewoonlijk gebruikte tooprepare knooppunten voor het Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="39e44-120">Het kan hierbij gaan Achtergrondservices wordt gestart (zoals [Microsoft MPI][msmpi_msdn]van `smpd.exe`) en verifiëren dat Hallo knooppunten gereed tooprocess tussen knooppunten berichten zijn.</span><span class="sxs-lookup"><span data-stu-id="39e44-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="39e44-121">Hallo primaire taak wordt uitgevoerd Hallo **toepassingsopdracht** op Hallo hoofdknooppunt *nadat* Hallo coördinatie opdracht is voltooid door Hallo primaire en alle subtaken.</span><span class="sxs-lookup"><span data-stu-id="39e44-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="39e44-122">opdracht van de toepassing Hello Hallo vanaf de opdrachtregel van de taak met meerdere instanties Hallo zelf is en alleen op primaire Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="39e44-123">In een [MS MPI][msmpi_msdn]-gebaseerde oplossing, dit is waar u uw MPI-toepassingen met uitvoeren `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="39e44-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="39e44-124">Hoewel functioneel distinct, Hallo 'taak met meerdere instanties' is niet een unieke taaktype zoals Hallo [StartTask] [ net_starttask] of [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="39e44-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="39e44-125">taak met meerdere instanties Hallo is gewoon een Batch standaardtaak ([CloudTask] [ net_task] in Batch .NET) waarvan u meerdere exemplaren de instellingen zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="39e44-126">In dit artikel is toothis als Hallo **taak met meerdere instanties**.</span><span class="sxs-lookup"><span data-stu-id="39e44-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="39e44-127">Vereisten voor taken met meerdere instanties</span><span class="sxs-lookup"><span data-stu-id="39e44-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="39e44-128">Taken met meerdere instanties vereisen een pool met **communicatie tussen knooppunten ingeschakeld**, en met **uitvoering van gelijktijdige taken uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="39e44-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="39e44-129">uitvoering van de toodisable gelijktijdige taak, set Hallo [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) eigenschap too1.</span><span class="sxs-lookup"><span data-stu-id="39e44-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="39e44-130">Dit codefragment toont hoe een pool voor meerdere exemplaren toocreate taken met behulp van Hallo Batch .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="39e44-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="39e44-131">Als u probeert een taak met meerdere instanties in een groep met de communicatie tussen knooppunten uitgeschakeld toorun of met een *maxTasksPerNode* waarde groter dan 1, Hallo nooit taak--voor onbepaalde tijd blijft Hallo 'active' status heeft.</span><span class="sxs-lookup"><span data-stu-id="39e44-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="39e44-132">Taken met meerdere instanties kunnen alleen op knooppunten in groepen die zijn gemaakt na 14 December 2015 uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="39e44-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="39e44-133">Gebruik een StartTask tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="39e44-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="39e44-134">toorun MPI-toepassingen met een taak met meerdere instanties, moet u eerst een MPI-implementatie (MS-MPI of Intel MPI, bijvoorbeeld) op Hallo rekenknooppunten in de groep Hallo tooinstall.</span><span class="sxs-lookup"><span data-stu-id="39e44-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="39e44-135">Dit is een goed moment toouse een [StartTask][net_starttask], die wordt uitgevoerd zodra er een knooppunt aan een pool wordt toegevoegd of opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="39e44-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="39e44-136">Dit codefragment maakt u een StartTask waarmee Hallo MS MPI-installatiepakket als een [bronbestand][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="39e44-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="39e44-137">Hallo begintaak opgegeven vanaf de opdrachtregel wordt uitgevoerd wanneer het Hallo-bronbestand gedownloade toohello knooppunt bevindt.</span><span class="sxs-lookup"><span data-stu-id="39e44-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="39e44-138">In dit geval voert Hallo opdrachtregel een installatie zonder toezicht van MS MPI.</span><span class="sxs-lookup"><span data-stu-id="39e44-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="39e44-139">Remote direct memory access (RDMA)</span><span class="sxs-lookup"><span data-stu-id="39e44-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="39e44-140">Als u kiest een [RDMA-compatibele grootte](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) zoals A9 voor Hallo rekenknooppunten in uw Batch-pool, uw MPI-toepassingen kan profiteren van Azure hoge prestaties, lage latentie remote direct memory access (RDMA) netwerk.</span><span class="sxs-lookup"><span data-stu-id="39e44-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="39e44-141">Hallo-grootten die zijn opgegeven als 'RDMA-compatibele' in de volgende artikelen Hallo zoeken:</span><span class="sxs-lookup"><span data-stu-id="39e44-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="39e44-142">**CloudServiceConfiguration** pools</span><span class="sxs-lookup"><span data-stu-id="39e44-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="39e44-143">[Grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md) (alleen Windows)</span><span class="sxs-lookup"><span data-stu-id="39e44-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="39e44-144">**VirtualMachineConfiguration** pools</span><span class="sxs-lookup"><span data-stu-id="39e44-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="39e44-145">[Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="39e44-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="39e44-146">[Grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="39e44-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="39e44-147">tootake profiteren van RDMA op [Linux-rekenknooppunten](batch-linux-nodes.md), moet u **Intel MPI** op Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="39e44-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="39e44-148">Zie voor meer informatie over CloudServiceConfiguration en VirtualMachineConfiguration pools sectie toepassingen Hallo Hallo [overzicht Batch-functies](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="39e44-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="39e44-149">Een taak meerdere exemplaren maken met de Batch .NET</span><span class="sxs-lookup"><span data-stu-id="39e44-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="39e44-150">Nu dat we Hallo groep vereisten en installatie van het pakket MPI besproken hebben, gaan we Hallo meerdere exemplaren taak te maken.</span><span class="sxs-lookup"><span data-stu-id="39e44-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="39e44-151">In dit fragment maken we een standaard [CloudTask][net_task], configureert u de [MultiInstanceSettings] [ net_multiinstance_prop] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="39e44-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="39e44-152">Zoals eerder gezegd, Hallo meerdere exemplaren taak is niet een afzonderlijke taaktype, maar een Batch standaardtaak geconfigureerd met instellingen voor meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="39e44-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="39e44-153">Primaire taken en subtaken</span><span class="sxs-lookup"><span data-stu-id="39e44-153">Primary task and subtasks</span></span>
<span data-ttu-id="39e44-154">Wanneer u Hallo meerdere exemplaren van instellingen voor een taak maakt, kunt u het aantal rekenknooppunten die tooexecute Hallo taak zijn Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="39e44-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="39e44-155">Wanneer u de taak tooa Hallo indient, Hallo Batch-service maakt een **primaire** taak en er voldoende **subtaken** die samen overeenkomen met Hallo aantal knooppunten dat u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="39e44-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="39e44-156">Deze taken zijn toegewezen een integer-id in Hallo bereik van 0 te*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="39e44-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="39e44-157">Hallo-taak met id 0 is de primaire taak Hallo en andere id's zijn subtaken zijn.</span><span class="sxs-lookup"><span data-stu-id="39e44-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="39e44-158">Als u Hallo na meerdere exemplaren van instellingen voor een taak maakt, de belangrijkste taak Hallo zou een id van 0 hebben en Hallo subtaken moet id's 1 tot en met 9.</span><span class="sxs-lookup"><span data-stu-id="39e44-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="39e44-159">Hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="39e44-159">Master node</span></span>
<span data-ttu-id="39e44-160">Wanneer u een taak met meerdere instanties indient, Hallo Batch-service wijst een Hallo rekenknooppunten als Hallo 'master'-knooppunt en planningen Hallo primaire taak tooexecute op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="39e44-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="39e44-161">Hallo subtaken zijn geplande tooexecute op Hallo rest van de taak met meerdere instanties toohello toegewezen Hallo-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="39e44-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="39e44-162">Coördinatie opdracht</span><span class="sxs-lookup"><span data-stu-id="39e44-162">Coordination command</span></span>
<span data-ttu-id="39e44-163">Hallo **coördinatie opdracht** door zowel de primaire Hallo en subtaken wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="39e44-164">Hallo-aanroep van Hallo coördinatie opdracht blokkeert--Batch niet Hallo toepassingsopdracht wordt uitgevoerd totdat Hallo coördinatie opdracht met succes voor alle subtaken heeft geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="39e44-165">Hallo coördinatie opdracht moet daarom start alle vereiste Achtergrondservices, Ga na of deze klaar voor gebruik en sluit vervolgens af.</span><span class="sxs-lookup"><span data-stu-id="39e44-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="39e44-166">Bijvoorbeeld: met deze opdracht coördinatie voor een oplossing met behulp van MS-MPI versie 7 Hallo SMPD service begint op Hallo knooppunt en vervolgens wordt afgesloten:</span><span class="sxs-lookup"><span data-stu-id="39e44-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="39e44-167">Houd er rekening mee Hallo gebruik van `start` in deze opdracht coördinatie.</span><span class="sxs-lookup"><span data-stu-id="39e44-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="39e44-168">Dit is nodig omdat Hallo `smpd.exe` toepassing geen retourneert onmiddellijk na de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="39e44-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="39e44-169">Zonder het gebruik van Hallo Hallo [start] [ cmd_start] opdracht met deze opdracht coördinatie niet geretourneerd, en daarom blokkeren Hallo toepassingsopdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="39e44-170">Toepassingsopdracht</span><span class="sxs-lookup"><span data-stu-id="39e44-170">Application command</span></span>
<span data-ttu-id="39e44-171">Zodra de belangrijkste taak Hallo en alle subtaken hebt Hallo coördinatie opdracht wordt uitgevoerd, opdrachtregel Hallo meerdere exemplaren van de taak wordt uitgevoerd door de primaire taak Hallo *alleen*.</span><span class="sxs-lookup"><span data-stu-id="39e44-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="39e44-172">We noemen deze Hallo **toepassingsopdracht** toodistinguish op Hallo coördinatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="39e44-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="39e44-173">Voor MS MPI-toepassingen, gebruik Hallo toepassing opdracht tooexecute MPI-toepassingen met `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="39e44-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="39e44-174">Dit is bijvoorbeeld een toepassingsopdracht voor een oplossing met behulp van MS-MPI versie 7:</span><span class="sxs-lookup"><span data-stu-id="39e44-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="39e44-175">Omdat MS-MPI `mpiexec.exe` gebruikt Hallo `CCP_NODES` variabele standaard (Zie [omgevingsvariabelen](#environment-variables)) bovenstaande toepassing vanaf de opdrachtregel worden uitgesloten van het Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="39e44-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="39e44-176">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="39e44-176">Environment variables</span></span>
<span data-ttu-id="39e44-177">Batch maakt verschillende [omgevingsvariabelen] [ msdn_env_var] specifieke toomulti-exemplaar taken op Hallo compute knooppunten taak met meerdere instanties tooa toegewezen.</span><span class="sxs-lookup"><span data-stu-id="39e44-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="39e44-178">Uw opdrachtregels coördinatie en toepassing kunt verwijzen naar van deze omgevingsvariabelen zoals kunt Hallo scripts en programma's die ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="39e44-179">Hallo zijn volgende omgevingsvariabelen gemaakt door Hallo Batch-service voor gebruik door meerdere exemplaren taken:</span><span class="sxs-lookup"><span data-stu-id="39e44-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="39e44-180">Zie voor meer details over deze en Hallo andere Batch compute knooppunt omgevingsvariabelen, waaronder de inhoud en zichtbaarheid, [Compute knooppunt omgevingsvariabelen][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="39e44-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="39e44-181">Hallo Batch Linux MPI-codevoorbeeld bevat een voorbeeld van hoe diverse van deze omgevingsvariabelen kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="39e44-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="39e44-182">Hallo [coördinatie cmd] [ coord_cmd_example] Bash script algemene toepassing en de invoerbestanden van Azure Storage downloadt, kunt een Network File System (NFS)-share op Hallo hoofdknooppunt en configureert u andere knooppunten Hallo taak met meerdere instanties toohello als NFS-clients toegewezen.</span><span class="sxs-lookup"><span data-stu-id="39e44-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="39e44-183">Bronbestanden</span><span class="sxs-lookup"><span data-stu-id="39e44-183">Resource files</span></span>
<span data-ttu-id="39e44-184">Er zijn twee sets met resource bestanden tooconsider voor taken met meerdere instanties: **algemene bronbestanden** die *alle* taken downloaden (zowel de primaire en subtaken), en Hallo **bronbestanden** opgegeven voor hello meerdere exemplaren van de taak zelf, die *alleen Hallo primaire* downloads van de taak.</span><span class="sxs-lookup"><span data-stu-id="39e44-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="39e44-185">U kunt een of meer opgeven **algemene bronbestanden** in Hallo meerdere exemplaren instellingen voor een taak.</span><span class="sxs-lookup"><span data-stu-id="39e44-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="39e44-186">Deze algemene resource-bestanden worden gedownload van [Azure Storage](../storage/common/storage-introduction.md) in elk knooppunt **taak gedeelde map** door Hallo primaire en alle subtaken.</span><span class="sxs-lookup"><span data-stu-id="39e44-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="39e44-187">U kunt gedeelde taakmap Hallo openen vanaf opdrachtregels toepassing en de coördinatie met behulp van Hallo `AZ_BATCH_TASK_SHARED_DIR` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="39e44-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="39e44-188">Hallo `AZ_BATCH_TASK_SHARED_DIR` pad is identiek zijn op elke taak meerdere exemplaren van knooppunt toegewezen toohello, dus kunt u een opdracht één coördinatie tussen Hallo primaire en alle subtaken delen.</span><span class="sxs-lookup"><span data-stu-id="39e44-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="39e44-189">Batch geen 'gedeeld' hello directory in een zin externe toegang, maar u kunt gebruiken als een koppeling of punt zoals eerder beschreven in Hallo tip op omgevingsvariabelen delen.</span><span class="sxs-lookup"><span data-stu-id="39e44-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="39e44-190">Bronbestanden die u opgeeft voor hello taak met meerdere instanties zelf zijn van de taak van de gedownloade toohello werkmap, `AZ_BATCH_TASK_WORKING_DIR`, standaard.</span><span class="sxs-lookup"><span data-stu-id="39e44-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="39e44-191">Zoals gezegd, daarentegen bronbestanden toocommon, alleen Hallo primaire taak downloadt resource opgegeven bestanden voor de taak met meerdere instanties Hallo zelf.</span><span class="sxs-lookup"><span data-stu-id="39e44-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39e44-192">Gebruik altijd de omgevingsvariabelen Hallo `AZ_BATCH_TASK_SHARED_DIR` en `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese mappen in uw opdrachtregels.</span><span class="sxs-lookup"><span data-stu-id="39e44-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="39e44-193">Probeer tooconstruct Hallo paden niet handmatig.</span><span class="sxs-lookup"><span data-stu-id="39e44-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="39e44-194">Taak levensduur</span><span class="sxs-lookup"><span data-stu-id="39e44-194">Task lifetime</span></span>
<span data-ttu-id="39e44-195">Hallo-levensduur van Hallo primaire taak besturingselementen Hallo levensduur van Hallo gehele meerdere exemplaren taak.</span><span class="sxs-lookup"><span data-stu-id="39e44-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="39e44-196">Wanneer primaire hello wordt afgesloten, worden alle Hallo subtaken beëindigd.</span><span class="sxs-lookup"><span data-stu-id="39e44-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="39e44-197">de afsluitcode Hallo Hallo primaire Hallo afsluitcode Hallo-taak is, en kan daarom gebruikte toodetermine Hallo slagen of mislukken van de taak voor opnieuw proberen doeleinden Hallo.</span><span class="sxs-lookup"><span data-stu-id="39e44-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="39e44-198">Als een Hallo subtaken mislukt, afgesloten met een niet-nul-retourcode bijvoorbeeld Hallo gehele meerdere exemplaren taak mislukt.</span><span class="sxs-lookup"><span data-stu-id="39e44-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="39e44-199">taak met meerdere instanties Hallo vervolgens wordt beëindigd en opnieuw worden geprobeerd om de limiet voor opnieuw proberen tooits.</span><span class="sxs-lookup"><span data-stu-id="39e44-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="39e44-200">Wanneer u een taak met meerdere instanties verwijdert, worden ook Hallo primaire en alle subtaken verwijderd door Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="39e44-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="39e44-201">Alle mappen een subtaak en hun bestanden worden verwijderd uit de rekenknooppunten hello, net als voor een taak.</span><span class="sxs-lookup"><span data-stu-id="39e44-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="39e44-202">[TaskConstraints] [ net_taskconstraints] voor een taak met meerdere instanties, zoals Hallo [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], en [RetentionTime] [ net_taskconstraint_retention] -eigenschappen worden gehonoreerd als ze zijn voor een standaardtaak en toepassen van toohello primaire en alle subtaken.</span><span class="sxs-lookup"><span data-stu-id="39e44-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="39e44-203">Echter, als u Hallo wijzigt [RetentionTime] [ net_taskconstraint_retention] eigenschap na het toevoegen van Hallo meerdere exemplaren toohello taak, deze wijziging is de belangrijkste taak toegepaste alleen toohello.</span><span class="sxs-lookup"><span data-stu-id="39e44-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="39e44-204">Alle Hallo subtaken toouse Hallo oorspronkelijke gaan [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="39e44-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="39e44-205">Een rekenknooppunt lijst met recente taken duidt Hallo-id van een subtaak als Hallo recente taak deel van een taak meerdere exemplaren uitmaakte.</span><span class="sxs-lookup"><span data-stu-id="39e44-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="39e44-206">Verzamel informatie over subtaken</span><span class="sxs-lookup"><span data-stu-id="39e44-206">Obtain information about subtasks</span></span>
<span data-ttu-id="39e44-207">tooobtain informatie over subtaken via Hallo Batch .NET-bibliotheek, aanroep Hallo [CloudTask.ListSubtasks] [ net_task_listsubtasks] methode.</span><span class="sxs-lookup"><span data-stu-id="39e44-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="39e44-208">Deze methode retourneert informatie over alle subtaken en informatie over Hallo rekenknooppunt die Hallo taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="39e44-209">Met deze informatie kunt u bepalen de hoofdmap van elke subtaak, Hallo pool-id, de huidige status, afsluitcode en meer.</span><span class="sxs-lookup"><span data-stu-id="39e44-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="39e44-210">U kunt deze informatie gebruiken in combinatie met Hallo [PoolOperations.GetNodeFile] [ poolops_getnodefile] methode tooobtain Hallo subtaak van bestanden.</span><span class="sxs-lookup"><span data-stu-id="39e44-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="39e44-211">Houd er rekening mee dat deze methode geen gegevens voor Hallo primaire taak (id 0 retourneert).</span><span class="sxs-lookup"><span data-stu-id="39e44-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="39e44-212">Tenzij anders vermeld, Batch .NET-methoden die worden uitgevoerd op meerdere exemplaren Hallo [CloudTask] [ net_task] zelf toepassen *alleen* toohello primaire taak.</span><span class="sxs-lookup"><span data-stu-id="39e44-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="39e44-213">Bijvoorbeeld, wanneer u Hallo aanroepen [CloudTask.ListNodeFiles] [ net_task_listnodefiles] methode voor een taak meerdere exemplaren alleen Hallo primaire taak bestanden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="39e44-214">Hallo volgende codefragment toont hoe tooobtain informatie van een subtaak, evenals bestandsinhoud aanvragen bij Hallo knooppunten waarop ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="39e44-215">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="39e44-215">Code sample</span></span>
<span data-ttu-id="39e44-216">Hallo [MultiInstanceTasks] [ github_mpi] codevoorbeeld op GitHub laat zien hoe toouse een meerdere exemplaren van de taak toorun een [MS MPI] [ msmpi_msdn] de toepassing in rekenknooppunten voor Batch.</span><span class="sxs-lookup"><span data-stu-id="39e44-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="39e44-217">Hallo stappen in [voorbereiding](#preparation) en [uitvoering](#execution) toorun Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="39e44-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="39e44-218">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="39e44-218">Preparation</span></span>
1. <span data-ttu-id="39e44-219">Volg de eerste twee stappen Hallo in [hoe toocompile en een eenvoudige MS MPI-programma uitvoeren][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="39e44-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="39e44-220">Dit voldoet aan Hallo prerequesites voor Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="39e44-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="39e44-221">Bouwen een *Release* versie Hallo [MPIHelloWorld] [ helloworld_proj] MPI voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="39e44-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="39e44-222">Dit is Hallo programma dat door de taak met meerdere instanties Hallo op rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e44-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="39e44-223">Maak een zip-bestand met `MPIHelloWorld.exe` (die u hebt gebouwd stap 2) en `MSMpiSetup.exe` (die u hebt gedownload stap 1).</span><span class="sxs-lookup"><span data-stu-id="39e44-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="39e44-224">U hebt dit zipbestand uploaden als een toepassingspakket in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="39e44-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="39e44-225">Gebruik Hallo [Azure-portal] [ portal] toocreate een Batch [toepassing](batch-application-packages.md) 'MPIHelloWorld' genoemd en Hallo u hebt gemaakt in de vorige stap Hallo "1.0" versie van zip-bestand opgeven Hallo-toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="39e44-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="39e44-226">Zie [uploaden en beheren van toepassingen](batch-application-packages.md#upload-and-manage-applications) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="39e44-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="39e44-227">Bouwen een *Release* versie van `MPIHelloWorld.exe` zodat er geen tooinclude eventuele extra afhankelijkheden (bijvoorbeeld `msvcp140d.dll` of `vcruntime140d.dll`) in het toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="39e44-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="39e44-228">Uitvoering</span><span class="sxs-lookup"><span data-stu-id="39e44-228">Execution</span></span>
1. <span data-ttu-id="39e44-229">Hallo downloaden [azure-batch-samples] [ github_samples_zip] vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="39e44-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="39e44-230">Open Hallo MultiInstanceTasks **oplossing** in Visual Studio 2015 of hoger.</span><span class="sxs-lookup"><span data-stu-id="39e44-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="39e44-231">Hallo `MultiInstanceTasks.sln` oplossingsbestand bevindt zich in:</span><span class="sxs-lookup"><span data-stu-id="39e44-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="39e44-232">Voer uw referenties in Batch- en Storage-account in `AccountSettings.settings` in Hallo **Microsoft.Azure.Batch.Samples.Common** project.</span><span class="sxs-lookup"><span data-stu-id="39e44-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="39e44-233">**Bouwen en uitvoeren van** hello MultiInstanceTasks oplossing tooexecute Hallo MPI voorbeeldtoepassing op rekenknooppunten in een Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="39e44-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="39e44-234">*Optionele*: gebruik Hallo [Azure-portal] [ portal] of Hallo [Batch Explorer] [ batch_explorer] tooexamine Hallo voorbeeld van toepassingen, de taak, en taak ('MultiInstanceSamplePool', 'MultiInstanceSampleJob', "MultiInstanceSampleTask") voordat u Hallo resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="39e44-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="39e44-235">U kunt downloaden [Visual Studio Community] [ visual_studio] gratis als u Visual Studio niet hebt.</span><span class="sxs-lookup"><span data-stu-id="39e44-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="39e44-236">De uitvoer van `MultiInstanceTasks.exe` is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="39e44-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="39e44-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39e44-237">Next steps</span></span>
* <span data-ttu-id="39e44-238">Hallo Microsoft HPC & Azure Batch-Team blog besproken [MPI-ondersteuning voor Linux op Azure Batch][blog_mpi_linux], en bevat informatie over het gebruik van [OpenFOAM] [ openfoam] met Batch.</span><span class="sxs-lookup"><span data-stu-id="39e44-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="39e44-239">Vindt u voorbeelden van Python-code voor Hallo [OpenFOAM voorbeeld op GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="39e44-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="39e44-240">Meer informatie over hoe te[maken van groepen van Linux-rekenknooppunten](batch-linux-nodes.md) voor gebruik in uw Azure Batch MPI-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="39e44-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
