---
title: "aaaRun taken in parallelle toouse rekenresources efficiënt - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="0ce1c-103">Taken uitvoeren gelijktijdig gebruik van Batch-rekenknooppunten toomaximize</span><span class="sxs-lookup"><span data-stu-id="0ce1c-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="0ce1c-104">U kunt door meer dan één taak tegelijkertijd uitgevoerd op elk rekenknooppunt in uw Azure Batch-pool, brongebruik op een kleiner aantal knooppunten in de pool Hallo maximaliseren.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="0ce1c-105">Voor sommige werkbelastingen, kan dit resulteren in een kortere taaktijden en lagere kosten.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="0ce1c-106">Hoewel sommige scenario's profiteren van dat alle één taak van een knooppunt resources tooa, profiteert verschillende situaties zodat meerdere taken tooshare die bronnen:</span><span class="sxs-lookup"><span data-stu-id="0ce1c-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="0ce1c-107">**Overdracht van gegevens voor het minimaliseren** wanneer taken kunnen tooshare gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="0ce1c-108">In dit scenario kunt u gegevensoverdracht kosten aanzienlijk verkleinen door het kopiëren van gedeelde gegevens tooa kleiner aantal knooppunten en het uitvoeren van taken parallel op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="0ce1c-109">Dit geldt vooral als Hallo gegevens toobe gekopieerde tooeach knooppunt moet worden overgedragen tussen geografische regio's.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="0ce1c-110">**Het optimaliseren van geheugengebruik** wanneer taken vereisen dat een grote hoeveelheid geheugen, maar alleen gedurende korte perioden tijd en op variabele momenten tijdens de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="0ce1c-111">U kunt gebruiken minder maar groter, compute knooppunten met meer geheugen tooefficiently verwerken van dergelijke pieken.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="0ce1c-112">Deze knooppunten zou hebben meerdere taken parallel uitgevoerd op elk knooppunt, maar elke taak wilt profiteren van de grote hoeveelheid geheugen Hallo-knooppunten op verschillende tijdstippen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="0ce1c-113">**Aantal grenzen knooppunt beperkende** wanneer de communicatie tussen knooppunten is vereist in een pool.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="0ce1c-114">Toepassingen die zijn geconfigureerd voor communicatie tussen knooppunten zijn momenteel beperkt too50 rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="0ce1c-115">Als elk knooppunt in deze groep kunnen tooexecute taken parallel is, kan een groter aantal taken tegelijkertijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="0ce1c-116">**Bezig met het repliceren van een lokale compute cluster**, zoals wanneer u een tooAzure compute-omgeving voor het eerst hebt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="0ce1c-117">Als uw huidige on-premises-oplossing wordt meerdere taken per rekenknooppunt uitgevoerd, kunt u het maximum aantal Hallo verhogen van knooppunt taken spiegelen toomore nauw dat de configuratie.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="0ce1c-118">Voorbeeldscenario 's</span><span class="sxs-lookup"><span data-stu-id="0ce1c-118">Example scenario</span></span>
<span data-ttu-id="0ce1c-119">Als een voorbeeld tooillustrate Hallo voordelen van de uitvoering van parallelle taken, Stel dat uw taaktoepassing heeft CPU en geheugen vereisten zodat [standaard\_D1](../cloud-services/cloud-services-sizes-specs.md) knooppunten zijn voldoende.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="0ce1c-120">Maar in volgorde toofinish Hallo taak Hallo vereist tijdig 1.000 van deze knooppunten nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="0ce1c-121">In plaats van met behulp van standaard\_D1 knooppunten die 1 CPU-kern hebt, kunt u [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten met 16 kernen en uitvoering van de parallelle taak inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="0ce1c-122">Daarom *16 keer minder knooppunten* kan alleen worden gebruikt--in plaats van 1000 knooppunten 63 zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="0ce1c-123">Bovendien als grote toepassingsbestanden of referentiegegevens vereist voor elk knooppunt zijn, zijn de duur van de taak en efficiëntie opnieuw verbeterd omdat Hallo gegevens gekopieerde tooonly 16 knooppunten.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="0ce1c-124">Uitvoering van de parallelle taak inschakelen</span><span class="sxs-lookup"><span data-stu-id="0ce1c-124">Enable parallel task execution</span></span>
<span data-ttu-id="0ce1c-125">Bij het configureren van rekenknooppunten voor parallelle uitvoering op Hallo van toepassingen niveau.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="0ce1c-126">Hallo Batch .NET-bibliotheek, stel Hallo [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap bij het maken van een groep.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="0ce1c-127">Als u Hallo Batch REST-API gebruikt, stelt u Hallo [maxTasksPerNode] [ rest_addpool] element in de aanvraagtekst Hallo tijdens het maken van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="0ce1c-128">Azure Batch kunt u tooset maximum aantal taken per knooppunt een toofour tijden (4 x) Hallo aantal kernen knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="0ce1c-129">Bijvoorbeeld, als hello van toepassingen is geconfigureerd met knooppunten met een grootte van 'Groot' (vier kernen), vervolgens `maxTasksPerNode` too16 kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="0ce1c-130">Zie voor meer informatie op het aantal kernen voor elk van de knooppuntgrootten Hallo Hallo [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0ce1c-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="0ce1c-131">Zie voor meer informatie over Servicelimieten [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="0ce1c-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="0ce1c-132">Ervoor tootake in account Hallo worden `maxTasksPerNode` waarde als u een [formule voor automatisch schalen] [ enable_autoscaling] voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="0ce1c-133">Bijvoorbeeld, een formule waarvan de evaluatie `$RunningTasks` aanzienlijk kunnen worden beïnvloed door een toename van de taken per knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="0ce1c-134">Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](batch-automatic-scaling.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="0ce1c-135">Verdeling van taken</span><span class="sxs-lookup"><span data-stu-id="0ce1c-135">Distribution of tasks</span></span>
<span data-ttu-id="0ce1c-136">Wanneer Hallo rekenknooppunten in een groep gelijktijdig taken uitvoeren kunnen, is het belangrijk toospecify Hallo taken toobe verdeeld over Hallo knooppunten in Hallo pool gewenste.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="0ce1c-137">Met behulp van Hallo [CloudPool.TaskSchedulingPolicy] [ task_schedule] eigenschap, kunt u opgeven dat taken gelijkmatig over alle knooppunten in Hallo-groep ('spreiden") moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="0ce1c-138">Of u kunt opgeven dat zo zo veel mogelijk taken moeten worden toegewezen tooeach knooppunt voordat taken tooanother-knooppunt in Hallo-pool ('verpakking') worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="0ce1c-139">Een voorbeeld van hoe deze functie waardevolle is, kunt u beter Hallo-pool van [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten (in de bovenstaande Hallo voorbeeld) die is geconfigureerd met een [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] waarde van 16.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="0ce1c-140">Als hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] is geconfigureerd met een [ComputeNodeFillType] [ fill_type] van *Pack*, zou het gebruik van alle 16 kernen van elk knooppunt maximaliseren en toestaan een [automatisch schalen van toepassingen](batch-automatic-scaling.md) tooprune ongebruikte knooppunten uit Hallo-groep (knooppunten zonder geen taken toegewezen).</span><span class="sxs-lookup"><span data-stu-id="0ce1c-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="0ce1c-141">Hierdoor minimaliseert brongebruik en bespaart u geld.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="0ce1c-142">Batch .NET-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0ce1c-142">Batch .NET example</span></span>
<span data-ttu-id="0ce1c-143">Dit [Batch .NET] [ api_net] API-codefragment toont een toocreate aanvraag een groep die vier grote knooppunten met een maximum van vier taken per knooppunt bevat.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="0ce1c-144">Hiermee wordt een taak plannen beleid dat elk knooppunt met taken voorafgaande tooassigning taken tooanother-knooppunt in het Hallo-groep wordt gevuld.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="0ce1c-145">Zie voor meer informatie over het toevoegen van groepen met behulp van Batch .NET API Hallo [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="0ce1c-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="0ce1c-146">Batch REST-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0ce1c-146">Batch REST example</span></span>
<span data-ttu-id="0ce1c-147">Dit [Batch REST] [ api_rest] API fragment toont een toocreate aanvraag een groep die twee grote knooppunten met een maximum van vier taken per knooppunt bevat.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="0ce1c-148">Zie voor meer informatie over het toevoegen van groepen met behulp van REST-API Hallo [toevoegen van een account voor toepassingsgroep tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="0ce1c-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

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
> <span data-ttu-id="0ce1c-149">U kunt instellen Hallo `maxTasksPerNode` element en [MaxTasksPerComputeNode] [ maxtasks_net] eigenschap alleen tijdens de aanmaak van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="0ce1c-150">Ze kunnen niet worden gewijzigd nadat een pool al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="0ce1c-151">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="0ce1c-151">Code sample</span></span>
<span data-ttu-id="0ce1c-152">Hallo [ParallelNodeTasks] [ parallel_tasks_sample] project op GitHub illustreert Hallo gebruik van Hallo [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="0ce1c-153">Deze C#-consoletoepassing maakt gebruik van Hallo [Batch .NET] [ api_net] bibliotheek toocreate een groep met een of meer rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="0ce1c-154">Een configureerbare aantal taken wordt uitgevoerd op die knooppunten toosimulate variabele laden.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="0ce1c-155">Uitvoer van de toepassing hello geeft aan welke knooppunten uitgevoerd elke taak.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="0ce1c-156">Hallo-toepassing bevat ook een samenvatting van taakparameters Hallo en duur.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="0ce1c-157">Hallo samenvatting deel van Hallo-uitvoer van twee verschillende uitvoeringen van de voorbeeldtoepassing hello wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="0ce1c-158">eerste uitvoering van de voorbeeldtoepassing Hallo Hallo blijkt dat met één knooppunt in het Hallo-pool en de standaardinstelling Hallo van één taak per knooppunt Hallo taak duur is meer dan 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="0ce1c-159">Hallo tweede run van Hallo voorbeeld toont een aanzienlijke daling van de duur van de taak.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="0ce1c-160">Dit is omdat Hallo van toepassingen is geconfigureerd met vier taken per knooppunt, waardoor de parallelle uitvoering toocomplete Hallo taak in bijna een kwartaal Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="0ce1c-161">duur van de taak Hallo in Hallo samenvattingen van de bovenstaande omvatten geen tijd voor het maken van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="0ce1c-162">Elk van de bovenstaande Hallo-taken is verzonden toopreviously gemaakt groepen waarvan rekenknooppunten in Hallo zijn *inactief* status tijdens verzending.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0ce1c-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ce1c-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="0ce1c-164">Batch Explorer-Heatmap</span><span class="sxs-lookup"><span data-stu-id="0ce1c-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="0ce1c-165">Hallo [Azure Batch Explorer][batch_explorer], een hello Azure Batch [voorbeeldtoepassingen][github_samples], bevat een *Heatmap* functie waarmee visualisatie van de uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="0ce1c-166">Wanneer u bent uitvoeren van Hallo [ParallelTasks] [ parallel_tasks_sample] voorbeeldtoepassing, kunt u Hallo Heat Map functie tooeasily visualiseren Hallo parallelle taken op elk knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ce1c-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Batch Explorer-Heatmap][1]

<span data-ttu-id="0ce1c-168">*Batch Explorer Heat Map met een pool met vier knooppunten, met elk knooppunt vier taken momenteel worden uitgevoerd*</span><span class="sxs-lookup"><span data-stu-id="0ce1c-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
