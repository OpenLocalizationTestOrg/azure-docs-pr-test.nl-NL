---
title: "Taken uitvoeren ter aanvulling van rekenresources efficiënt - gebruik Azure Batch | Microsoft Docs"
description: "Hogere efficiëntie en lagere kosten via minder rekenknooppunten en actief gelijktijdige taken op elk knooppunt in een Azure Batch-pool"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="93b29-103">Taken uitvoeren gelijktijdig maximaal gebruik van de Batch-rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="93b29-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="93b29-104">Door meer dan één taak tegelijkertijd uitgevoerd op elk rekenknooppunt in uw Azure Batch-pool, kunt u gebruik van bronnen op een kleiner aantal knooppunten in de pool maximaliseren.</span><span class="sxs-lookup"><span data-stu-id="93b29-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="93b29-105">Voor sommige werkbelastingen, kan dit resulteren in een kortere taaktijden en lagere kosten.</span><span class="sxs-lookup"><span data-stu-id="93b29-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="93b29-106">Hoewel sommige scenario's profiteren van alle resources van een knooppunt dat aan een enkele taak, profiteert verschillende situaties zodat meerdere taken die resources delen:</span><span class="sxs-lookup"><span data-stu-id="93b29-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="93b29-107">**Overdracht van gegevens voor het minimaliseren** wanneer taken kunnen geen gegevens delen.</span><span class="sxs-lookup"><span data-stu-id="93b29-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="93b29-108">In dit scenario kunt u gegevensoverdracht kosten aanzienlijk verminderen door gedeelde gegevens kopiëren naar een kleiner aantal knooppunten en het uitvoeren van taken parallel op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="93b29-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="93b29-109">Dit geldt vooral als de gegevens worden gekopieerd naar elk knooppunt moet worden overgebracht tussen geografische regio's.</span><span class="sxs-lookup"><span data-stu-id="93b29-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="93b29-110">**Het optimaliseren van geheugengebruik** wanneer taken vereisen dat een grote hoeveelheid geheugen, maar alleen gedurende korte perioden tijd en op variabele momenten tijdens de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="93b29-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="93b29-111">U kunt gebruikmaken van meer geheugen voor het afhandelen van dergelijke pieken efficiënt minder, maar groter, rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="93b29-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="93b29-112">Deze knooppunten zou hebben meerdere taken parallel uitgevoerd op elk knooppunt, maar elke taak wilt profiteren van de knooppunten grote hoeveelheid geheugen op verschillende tijdstippen.</span><span class="sxs-lookup"><span data-stu-id="93b29-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="93b29-113">**Aantal grenzen knooppunt beperkende** wanneer de communicatie tussen knooppunten is vereist in een pool.</span><span class="sxs-lookup"><span data-stu-id="93b29-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="93b29-114">Toepassingen die zijn geconfigureerd voor communicatie tussen knooppunten zijn momenteel beperkt tot 50 rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="93b29-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="93b29-115">Als elk knooppunt in deze groep kunnen taken parallel uitvoeren, kan een groter aantal taken tegelijkertijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="93b29-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="93b29-116">**Bezig met het repliceren van een lokale compute cluster**, zoals wanneer u eerst een compute-omgeving naar Azure verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="93b29-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="93b29-117">Als uw huidige on-premises-oplossing wordt meerdere taken per rekenknooppunt uitgevoerd, kunt u het maximum aantal taken voor het spiegelen van nauwkeuriger die configuratie knooppunt verhogen.</span><span class="sxs-lookup"><span data-stu-id="93b29-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="93b29-118">Voorbeeldscenario 's</span><span class="sxs-lookup"><span data-stu-id="93b29-118">Example scenario</span></span>
<span data-ttu-id="93b29-119">Als voorbeeld ter illustratie van de voordelen van de uitvoering van parallelle taken, Stel dat uw taaktoepassing CPU en geheugen heeft dat [standaard\_D1](../cloud-services/cloud-services-sizes-specs.md) knooppunten zijn voldoende.</span><span class="sxs-lookup"><span data-stu-id="93b29-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="93b29-120">Maar als u klaar bent met de taak in de tijd die nodig, 1.000 van deze knooppunten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="93b29-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="93b29-121">In plaats van met behulp van standaard\_D1 knooppunten die 1 CPU-kern hebt, kunt u [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten met 16 kernen en uitvoering van de parallelle taak inschakelen.</span><span class="sxs-lookup"><span data-stu-id="93b29-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="93b29-122">Daarom *16 keer minder knooppunten* kan alleen worden gebruikt--in plaats van 1000 knooppunten 63 zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="93b29-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="93b29-123">Bovendien, als grote toepassingsbestanden of referentiegegevens vereist voor elk knooppunt zijn, zijn duur van de taak en efficiëntie opnieuw verbeterd omdat de gegevens gekopieerd naar alleen 16 knooppunten.</span><span class="sxs-lookup"><span data-stu-id="93b29-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="93b29-124">Uitvoering van de parallelle taak inschakelen</span><span class="sxs-lookup"><span data-stu-id="93b29-124">Enable parallel task execution</span></span>
<span data-ttu-id="93b29-125">Bij het configureren van rekenknooppunten voor parallelle uitvoering op het niveau van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="93b29-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="93b29-126">Met de Batch .NET-bibliotheek, stel de [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap bij het maken van een groep.</span><span class="sxs-lookup"><span data-stu-id="93b29-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="93b29-127">Als u de Batch REST-API gebruikt, stelt u de [maxTasksPerNode] [ rest_addpool] element in de aanvraagtekst tijdens het maken van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="93b29-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="93b29-128">Azure Batch kunt u maximum aantal taken per knooppunt maximaal vier keer instellen (x 4) het aantal kernen knooppunt.</span><span class="sxs-lookup"><span data-stu-id="93b29-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="93b29-129">Bijvoorbeeld, als de groep van toepassingen is geconfigureerd met de knooppunten van het formaat van 'Groot' (vier kernen) vervolgens `maxTasksPerNode` kan worden ingesteld op 16.</span><span class="sxs-lookup"><span data-stu-id="93b29-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="93b29-130">Zie voor meer informatie over het aantal kernen voor elk van de grootte van het knooppunt, [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="93b29-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="93b29-131">Zie voor meer informatie over Servicelimieten [quota en limieten voor de Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="93b29-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="93b29-132">Zorg ervoor dat in aanmerking te nemen de `maxTasksPerNode` waarde als u een [formule voor automatisch schalen] [ enable_autoscaling] voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="93b29-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="93b29-133">Bijvoorbeeld, een formule waarvan de evaluatie `$RunningTasks` aanzienlijk kunnen worden beïnvloed door een toename van de taken per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="93b29-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="93b29-134">Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](batch-automatic-scaling.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="93b29-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="93b29-135">Verdeling van taken</span><span class="sxs-lookup"><span data-stu-id="93b29-135">Distribution of tasks</span></span>
<span data-ttu-id="93b29-136">Wanneer de rekenknooppunten in een groep gelijktijdig taken uitvoeren kunnen, is het belangrijk om te geven hoe u wilt dat de taken verdeeld over de knooppunten in de pool.</span><span class="sxs-lookup"><span data-stu-id="93b29-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="93b29-137">Met behulp van de [CloudPool.TaskSchedulingPolicy] [ task_schedule] eigenschap, kunt u opgeven dat taken gelijkmatig over alle knooppunten in de groep ('spreiden") moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="93b29-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="93b29-138">Of u kunt opgeven dat zo zo veel mogelijk taken moeten worden toegewezen aan elk knooppunt voordat er taken zijn toegewezen aan een ander knooppunt in de groep ('verpakking').</span><span class="sxs-lookup"><span data-stu-id="93b29-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="93b29-139">Een voorbeeld van hoe deze functie waardevolle is, kunt u de groep van [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten (in het bovenstaande voorbeeld) die is geconfigureerd met een [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] waarde van 16.</span><span class="sxs-lookup"><span data-stu-id="93b29-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="93b29-140">Als de [CloudPool.TaskSchedulingPolicy] [ task_schedule] is geconfigureerd met een [ComputeNodeFillType] [ fill_type] van *Pack*, zou het gebruik van alle 16 kernen van elk knooppunt maximaliseren en toestaan een [automatisch schalen van toepassingen](batch-automatic-scaling.md) te verwijderen van ongebruikte knooppunten uit de groep (knooppunten zonder geen taken toegewezen).</span><span class="sxs-lookup"><span data-stu-id="93b29-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="93b29-141">Hierdoor minimaliseert brongebruik en bespaart u geld.</span><span class="sxs-lookup"><span data-stu-id="93b29-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="93b29-142">Batch .NET-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93b29-142">Batch .NET example</span></span>
<span data-ttu-id="93b29-143">Dit [Batch .NET] [ api_net] API codefragment toont een aanvraag voor het maken van een groep die vier grote knooppunten met een maximum van vier taken per knooppunt bevat.</span><span class="sxs-lookup"><span data-stu-id="93b29-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="93b29-144">Hiermee wordt een taak plannen beleid dat elk knooppunt worden gevuld met taken vóór de taken toe te wijzen naar een ander knooppunt in de groep.</span><span class="sxs-lookup"><span data-stu-id="93b29-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="93b29-145">Zie voor meer informatie over het toevoegen van groepen met behulp van de Batch .NET API [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="93b29-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="93b29-146">Batch REST-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93b29-146">Batch REST example</span></span>
<span data-ttu-id="93b29-147">Dit [Batch REST] [ api_rest] API fragment toont een aanvraag voor het maken van een groep die twee grote knooppunten met een maximum van vier taken per knooppunt bevat.</span><span class="sxs-lookup"><span data-stu-id="93b29-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="93b29-148">Zie voor meer informatie over het toevoegen van groepen met behulp van de REST-API [een groep toevoegen aan een account][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="93b29-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="93b29-149">U kunt instellen de `maxTasksPerNode` element en [MaxTasksPerComputeNode] [ maxtasks_net] eigenschap alleen tijdens de aanmaak van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="93b29-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="93b29-150">Ze kunnen niet worden gewijzigd nadat een pool al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93b29-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="93b29-151">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="93b29-151">Code sample</span></span>
<span data-ttu-id="93b29-152">De [ParallelNodeTasks] [ parallel_tasks_sample] project op GitHub ziet u het gebruik van de [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="93b29-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="93b29-153">Deze C#-consoletoepassing maakt gebruik van de [Batch .NET] [ api_net] bibliotheek aan een pool maken met een of meer rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="93b29-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="93b29-154">Een configureerbare aantal taken wordt uitgevoerd op die knooppunten om te simuleren variabele laden.</span><span class="sxs-lookup"><span data-stu-id="93b29-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="93b29-155">Uitvoer van de toepassing geeft aan welke knooppunten uitgevoerd elke taak.</span><span class="sxs-lookup"><span data-stu-id="93b29-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="93b29-156">De toepassing bevat ook een samenvatting van de taakparameters en duur.</span><span class="sxs-lookup"><span data-stu-id="93b29-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="93b29-157">Het gedeelte van de samenvatting van de uitvoer van twee verschillende uitvoeringen van de voorbeeldtoepassing wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="93b29-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="93b29-158">De eerste uitvoering van de voorbeeldtoepassing blijkt dat met één knooppunt in de groep en de standaardinstelling van één taak per knooppunt, de duur van de taak is meer dan 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="93b29-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="93b29-159">De tweede uitvoering van het voorbeeld bevat een aanzienlijke daling van de duur van de taak.</span><span class="sxs-lookup"><span data-stu-id="93b29-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="93b29-160">Dit is omdat de groep met vier taken per knooppunt, waarmee voor parallelle uitvoering van de taak voltooid in bijna een kwartaal van de tijd die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="93b29-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="93b29-161">De duur van de taak in de bovenstaande samenvattingen omvatten geen tijd voor het maken van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="93b29-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="93b29-162">Elk van de bovenstaande taken is ingediend bij de eerder gemaakte groepen waarvan rekenknooppunten zijn in de *inactief* status tijdens verzending.</span><span class="sxs-lookup"><span data-stu-id="93b29-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="93b29-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93b29-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="93b29-164">Batch Explorer-Heatmap</span><span class="sxs-lookup"><span data-stu-id="93b29-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="93b29-165">De [Azure Batch Explorer][batch_explorer], een van de Azure Batch [voorbeeldtoepassingen][github_samples], bevat een *Heatmap*functie waarmee visualisatie van de uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="93b29-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="93b29-166">Wanneer u bent uitvoeren van de [ParallelTasks] [ parallel_tasks_sample] voorbeeldtoepassing, kunt u de functie Heatmap eenvoudig visualiseren parallelle taken op elk knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="93b29-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Batch Explorer-Heatmap][1]

<span data-ttu-id="93b29-168">*Batch Explorer Heat Map met een pool met vier knooppunten, met elk knooppunt vier taken momenteel worden uitgevoerd*</span><span class="sxs-lookup"><span data-stu-id="93b29-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
