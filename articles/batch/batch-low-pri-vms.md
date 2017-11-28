---
title: aaaRun Azure Batch-workloads op virtuele machines rendabele lage prioriteit (Preview) | Microsoft Docs
description: Meer informatie over hoe tooprovision prioriteit Laag VMs tooreduce Hallo kosten van Azure Batch-workloads.
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="8e608-103">Met lage prioriteit virtuele machines, met Batch (Preview)</span><span class="sxs-lookup"><span data-stu-id="8e608-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="8e608-104">Azure Batch biedt beperkte priorty virtuele machines (VM's) tooreduce Hallo kosten van Batch-workloads.</span><span class="sxs-lookup"><span data-stu-id="8e608-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="8e608-105">Prioriteit Laag virtuele machines maken nieuwe typen van Batch-workloads mogelijk doordat een grote hoeveelheid rekenkracht die ook voordelige.</span><span class="sxs-lookup"><span data-stu-id="8e608-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="8e608-106">Prioriteit Laag virtuele machines te profiteren van de overtollige capaciteit in Azure.</span><span class="sxs-lookup"><span data-stu-id="8e608-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="8e608-107">Wanneer u lage prioriteit VM's in uw pools opgeeft, kunt gebruiken Azure Batch automatisch deze teveel indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8e608-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="8e608-108">Hallo afweging voor het gebruik van virtuele machines prioriteit laag is dat deze virtuele machines worden gebruikt wanneer er geen overtollige capaciteit beschikbaar in Azure is.</span><span class="sxs-lookup"><span data-stu-id="8e608-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="8e608-109">Om deze reden prioriteit Laag VMs meest geschikt zijn voor bepaalde typen werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="8e608-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="8e608-110">Prioriteit Laag VM's gebruiken voor batch en asynchrone verwerking werkbelastingen waarbij Hallo taak voltooiingstijd is flexibel en Hallo werk verdeeld is over veel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e608-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="8e608-111">Prioriteit Laag VM's zijn aanzienlijk minder duur dan toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e608-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="8e608-112">Zie voor prijsinformatie, [prijzen van Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="8e608-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="8e608-113">Zie voor aanvullende informatie van virtuele machines prioriteit Laag, Hallo blogberichtaankondiging: [Batch computing een fractie van Hallo prijs](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="8e608-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e608-114">Prioriteit Laag VM's zijn momenteel in preview en zijn alleen beschikbaar voor werkbelastingen in Batch.</span><span class="sxs-lookup"><span data-stu-id="8e608-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="8e608-115">Gebruiksvoorbeelden voor VM met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="8e608-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="8e608-116">Hallo-kenmerken van virtuele machines prioriteit Laag gegeven, welke workloads kunnen en deze niet gebruiken?</span><span class="sxs-lookup"><span data-stu-id="8e608-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="8e608-117">In het algemeen zijn batch verwerkingsbelastingen geschikt, zoals taken worden onderverdeeld in veel parallelle taken of er zijn veel taken die worden uitgebreid en verdeeld over veel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e608-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="8e608-118">toomaximize gebruik van overtollige capaciteit in Azure, geschikte taken kunt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="8e608-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="8e608-119">Tijd tot tijd VM's mogelijk niet beschikbaar of wordt afgebroken die resulteert in minder capaciteit voor taken en tootask onderbreking en herhalingen kan leiden.</span><span class="sxs-lookup"><span data-stu-id="8e608-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="8e608-120">Taken moet daarom flexibele tijdig Hallo die toorun kunnen nemen.</span><span class="sxs-lookup"><span data-stu-id="8e608-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="8e608-121">Taken met langer taken mogelijk meer beïnvloed als onderbroken.</span><span class="sxs-lookup"><span data-stu-id="8e608-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="8e608-122">Als langlopende taken uitgevoerd voor het plaatsen van controlepunten toosave implementeren, zoals ze worden uitgevoerd, zou klikt u vervolgens de impact van onderbreking zijn veel minder.</span><span class="sxs-lookup"><span data-stu-id="8e608-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="8e608-123">Taken met een kortere uitvoeringstijden vaak toowork beste met lage prioriteit VMs Hallo impact van de onderbreking is veel minder.</span><span class="sxs-lookup"><span data-stu-id="8e608-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="8e608-124">Langlopende MPI-taken die gebruikmaken van meerdere virtuele machines zijn niet geschikt toouse wordt VMs prioriteit laag als een virtuele machine afgebroken waarschijnlijkheid potentiële toohello hele taak met toobe opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8e608-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="8e608-125">Enkele voorbeelden van batchverwerking gebruik gevallen geschikt toouse prioriteit Laag VM's zijn:</span><span class="sxs-lookup"><span data-stu-id="8e608-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="8e608-126">**Ontwikkelen en testen van**: In het bijzonder als grootschalige oplossingen worden ontwikkeld aanzienlijke besparing kan worden gerealiseerd.</span><span class="sxs-lookup"><span data-stu-id="8e608-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="8e608-127">Alle typen van de testen kunnen profiteren, maar grootschalige load testen en regressie testen zijn geweldige gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e608-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="8e608-128">**Ter aanvulling van de capaciteit op aanvraag**: prioriteit Laag virtuele machines kunnen worden gebruikt als aanvulling op regular toegewezen virtuele machines - indien beschikbaar, taken kunnen schalen en daarom sneller voltooid voor lagere kosten; wanneer niet beschikbaar is, Hallo basislijn van specifieke virtuele machines beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="8e608-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="8e608-129">**Flexibele uitvoeringstijd**: als er flexibiliteit in Hallo tijd taken hebt toocomplete, en vervolgens potentiële uitvalt capaciteit kunnen verdragen; echter Hello prioriteit Laag VMs taken toe te voegen wordt vaak uitgevoerd sneller en goedkoper.</span><span class="sxs-lookup"><span data-stu-id="8e608-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="8e608-130">Batch-pools kunnen geconfigureerde toouse prioriteit Laag VM's in een aantal manieren afhankelijk van Hallo flexibiliteit in de taak uitvoeringstijd zijn:</span><span class="sxs-lookup"><span data-stu-id="8e608-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="8e608-131">Prioriteit Laag VMs kunnen uitsluitend worden gebruikt in een pool en Batch herstelt gewoon alle preempted capaciteit indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8e608-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="8e608-132">Dit is Hallo goedkoopste manier tooexecute taken, zoals alleen-prioriteit Laag VM's worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e608-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="8e608-133">Prioriteit Laag VM's kunnen worden gebruikt in combinatie met een vaste basislijn toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e608-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="8e608-134">Hallo zorgt vast aantal toegewezen virtuele machines dat er is altijd een aantal tookeep capaciteit de voortgang van een taak.</span><span class="sxs-lookup"><span data-stu-id="8e608-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="8e608-135">Er mag dynamische combinatie van virtuele machines toegewezen en een lage prioriteit, zodat de goedkoper prioriteit Laag virtuele machines worden uitsluitend gebruikt indien beschikbaar, maar Hallo volledige geprijsde toegewezen virtuele machines worden opgeschaald indien nodig, de minimale hoeveelheid capaciteit beschikbaar tookeep Hallo taken tookeep voortgang hebben.</span><span class="sxs-lookup"><span data-stu-id="8e608-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="8e608-136">Batch-ondersteuning voor VM met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="8e608-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="8e608-137">Azure Batch biedt verschillende mogelijkheden die maken het gemakkelijk tooconsume en profiteren van virtuele machines prioriteit Laag:</span><span class="sxs-lookup"><span data-stu-id="8e608-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="8e608-138">Batch-pools kunnen zowel toegewezen virtuele machines en virtuele machines prioriteit Laag bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e608-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="8e608-139">Hallo aantal van elk type van de virtuele machine kan worden opgegeven wanneer een groep wordt gemaakt of gewijzigd op elk gewenst moment voor een bestaande pool met expliciete Hallo/verkleinbewerking of automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="8e608-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="8e608-140">Verzending van de taak en kunt blijven ongewijzigd en hoeft niet te worden betrokken met Hallo VM typen in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8e608-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="8e608-141">Het is ook mogelijk toohave een pool volledig gebruik prioriteit Laag VMs toorun taken goedkoop als mogelijk, maar spin up toegewezen virtuele machines als Hallo capaciteit zakt onder een drempel, zodat taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8e608-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="8e608-142">Batch-pools zoeken automatisch toohello doelaantal prioriteit Laag virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8e608-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="8e608-143">Als VMs zijn gereserveerd, proberen Batch tooreplace Hallo capaciteit en het doel van de geretourneerde toohello verloren.</span><span class="sxs-lookup"><span data-stu-id="8e608-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="8e608-144">In geval van taken wordt onderbroken Hallo Batch detecteert en automatisch requeue taken toobe opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8e608-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="8e608-145">Prioriteit Laag VM's hebben een quotum voor kernen die van de toegewezen virtuele machines verschilt.</span><span class="sxs-lookup"><span data-stu-id="8e608-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="8e608-146">Hallo aanhalingsteken voor prioriteit Laag virtuele machines is hoger dan die van de toegewezen virtuele machines, omdat minder VM met lage prioriteit kosten.</span><span class="sxs-lookup"><span data-stu-id="8e608-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="8e608-147">Zie [Batch-servicequota en limieten](batch-quota-limit.md#resource-quotas) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8e608-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="8e608-148">Prioriteit Laag virtuele machines worden momenteel niet ondersteund voor Batch-accounts waarbij Hallo groep toewijzing modus te is ingesteld[gebruikerabonnement](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="8e608-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="8e608-149">Maken en bijwerken van groepen</span><span class="sxs-lookup"><span data-stu-id="8e608-149">Create and update pools</span></span>

<span data-ttu-id="8e608-150">Een Batch-pool kan toegewezen en prioriteit Laag virtuele machines (ook waarnaar wordt verwezen tooas rekenknooppunten) bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e608-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="8e608-151">U kunt Hallo doelaantal rekenknooppunten instellen voor virtuele machines toegewezen en lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="8e608-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="8e608-152">Hallo doelaantal knooppunten bevat Hallo nummer van virtuele machines die u wilt toohave in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8e608-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="8e608-153">Bijvoorbeeld, toocreate een pool met behulp van de cloudservice van Azure VM's met een doel van 5 VM's en 20 prioriteit Laag VM's toegewezen:</span><span class="sxs-lookup"><span data-stu-id="8e608-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="8e608-154">toocreate een pool met virtuele Azure-machines (in dit geval virtuele Linux-machines) met een doel van 5 toegewezen virtuele machines en 20 prioriteit Laag VM's:</span><span class="sxs-lookup"><span data-stu-id="8e608-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="8e608-155">U kunt Hallo Huidig aantal knooppunten voor virtuele machines toegewezen en lage prioriteit krijgen:</span><span class="sxs-lookup"><span data-stu-id="8e608-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="8e608-156">Groep knooppunten hebben een eigenschap tooindicate als Hallo knooppunt een virtuele machine toegewezen of lage prioriteit:</span><span class="sxs-lookup"><span data-stu-id="8e608-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="8e608-157">Als een of meer knooppunten in een pool zijn gereserveerd, een lijst met knooppunten-bewerking op de toepassingen nog steeds die knooppunten retourneert, Huidig aantal prioriteit Laag knooppunten Hallo ongewijzigd blijft, maar die knooppunten hebben hun status toothe ingesteld **vervallen**status.</span><span class="sxs-lookup"><span data-stu-id="8e608-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="8e608-158">Batch zal proberen toofind vervanging virtuele machines en, als dit lukt, Hallo knooppunten doorlopen **maken** en vervolgens **starten** statussen voordat deze beschikbaar voor uitvoering van de taak, net als bij nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="8e608-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="8e608-159">Een groep met lage prioriteit VMs schalen</span><span class="sxs-lookup"><span data-stu-id="8e608-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="8e608-160">Net als bij de opslaggroepen die uitsluitend bestaan uit toegewezen virtuele machines, is mogelijk tooscale een groep met lage prioriteit virtuele machines Hallo formaat methode aanroepen of met automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="8e608-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="8e608-161">Hallo groep formaat duurt een tweede optionele parameter waarmee de waarde van bijgewerkt **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="8e608-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="8e608-162">Hallo pool automatisch schalen formule ondersteunt prioriteit Laag virtuele machines als volgt:</span><span class="sxs-lookup"><span data-stu-id="8e608-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="8e608-163">U kunt ophalen of instellen van Hallo-waarde van Hallo service gedefinieerde variabele **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="8e608-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="8e608-164">U kunt de waarde Hallo van Hallo service gedefinieerde variabele opvragen **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="8e608-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="8e608-165">U kunt de waarde Hallo van Hallo service gedefinieerde variabele opvragen **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="8e608-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="8e608-166">Deze variabele retourneert het aantal knooppunten in Hallo Hallo status afgebroken en kunt u omhoog of omlaag Hallo aantal toegewezen knooppunten, afhankelijk van het aantal afgebroken knooppunten die niet beschikbaar zijn Hallo schalen.</span><span class="sxs-lookup"><span data-stu-id="8e608-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="8e608-167">Jobs en taken</span><span class="sxs-lookup"><span data-stu-id="8e608-167">Jobs and tasks</span></span>

<span data-ttu-id="8e608-168">Jobs en taken vereist weinig ondersteuning voor knooppunten met lage prioriteit. alleen ondersteuning voor Hallo is als volgt:</span><span class="sxs-lookup"><span data-stu-id="8e608-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="8e608-169">Hallo JobManagerTask-eigenschap van een taak heeft een nieuwe eigenschap **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="8e608-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="8e608-170">Wanneer deze eigenschap true is, kan de jobbeheertaak Hallo worden gepland op een knooppunt toegewezen of lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="8e608-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="8e608-171">Als deze eigenschap ingesteld op false is, worden jobbeheertaak Hallo geplande tooa alleen specifieke knooppunt.</span><span class="sxs-lookup"><span data-stu-id="8e608-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="8e608-172">Een [omgevingsvariabele](batch-compute-node-environment-variables.md) beschikbaar tooa taaktoepassing is zodat deze bepalen kan of deze wordt uitgevoerd op een knooppunt met lage prioriteit of toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8e608-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="8e608-173">Hallo-omgevingsvariabele is AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="8e608-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="8e608-174">Afhandeling van voorrang</span><span class="sxs-lookup"><span data-stu-id="8e608-174">Handling preemption</span></span>

<span data-ttu-id="8e608-175">Virtuele machines kunnen van tijd tot tijd worden gebruikt; Als dit gebeurt, Batch Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e608-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="8e608-176">Hallo afgebroken virtuele machines hebben hun status bijgewerkt**vervallen**.</span><span class="sxs-lookup"><span data-stu-id="8e608-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="8e608-177">Als er taken zijn uitgevoerd op afgebroken Hallo knooppunt virtuele machines, en vervolgens deze taken worden opnieuw en voer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8e608-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="8e608-178">Hallo VM wordt effectief verwijderd, voorloopspaties tooany gegevens die lokaal zijn opgeslagen op Hallo VM verloren.</span><span class="sxs-lookup"><span data-stu-id="8e608-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="8e608-179">Hallo groep probeert voortdurend tooreach hello doelaantal prioriteit Laag knooppunten beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8e608-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="8e608-180">Als u vervangingscapaciteit wordt gevonden, de knooppunten behouden hun id, maar zijn opnieuw geïnitialiseerd, gaan via **maken** en **starten** aangegeven voordat ze beschikbaar voor het plannen van taken zijn.</span><span class="sxs-lookup"><span data-stu-id="8e608-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="8e608-181">Voorrang aantallen zijn beschikbaar als een waarde in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8e608-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="8e608-182">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="8e608-182">Metrics</span></span>

<span data-ttu-id="8e608-183">Nieuwe metrische gegevens zijn beschikbaar in Hallo [Azure-portal](https://portal.azure.com) voor knooppunten met lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="8e608-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="8e608-184">Deze metrische gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="8e608-184">These metrics are:</span></span>

- <span data-ttu-id="8e608-185">Aantal knooppunten met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="8e608-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="8e608-186">Aantal kernen met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="8e608-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="8e608-187">Aantal knooppunten afgebroken</span><span class="sxs-lookup"><span data-stu-id="8e608-187">Preempted Node Count</span></span>

<span data-ttu-id="8e608-188">tooview metrische gegevens in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="8e608-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="8e608-189">Navigeer tooyour Batch-account in de portal Hallo en Hallo-instellingen voor uw Batch-account weergeven.</span><span class="sxs-lookup"><span data-stu-id="8e608-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="8e608-190">Selecteer **metrische gegevens** van Hallo **bewaking** sectie.</span><span class="sxs-lookup"><span data-stu-id="8e608-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="8e608-191">Selecteer Hallo metrische gegevens die u wenst in Hallo **beschikbare metrische gegevens** lijst.</span><span class="sxs-lookup"><span data-stu-id="8e608-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Metrische gegevens voor knooppunten met lage prioriteit](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="8e608-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e608-193">Next steps</span></span>

* <span data-ttu-id="8e608-194">Lees Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen toouse Batch voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="8e608-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="8e608-195">Hallo artikel bevat meer gedetailleerde informatie over Batch-service-resources zoals pools, knooppunten, jobs en taken en Hallo veel API-functies die u tijdens het bouwen van uw Batch-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e608-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="8e608-196">Meer informatie over Hallo [Batch-API's en hulpprogramma's](batch-apis-tools.md) beschikbaar voor het bouwen van Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="8e608-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
