---
title: Azure Batch-workloads uitvoeren op virtuele machines rendabele lage prioriteit (Preview) | Microsoft Docs
description: Informatie over het inrichten van virtuele machines prioriteit laag als u wilt de kosten van Azure Batch-workloads.
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
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="38a37-103">Met lage prioriteit virtuele machines, met Batch (Preview)</span><span class="sxs-lookup"><span data-stu-id="38a37-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="38a37-104">Azure Batch biedt beperkte priorty virtuele machines (VM's) om de kosten van Batch-workloads te beperken.</span><span class="sxs-lookup"><span data-stu-id="38a37-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="38a37-105">Prioriteit Laag virtuele machines maken nieuwe typen van Batch-workloads mogelijk doordat een grote hoeveelheid rekenkracht die ook voordelige.</span><span class="sxs-lookup"><span data-stu-id="38a37-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="38a37-106">Prioriteit Laag virtuele machines te profiteren van de overtollige capaciteit in Azure.</span><span class="sxs-lookup"><span data-stu-id="38a37-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="38a37-107">Wanneer u lage prioriteit VM's in uw pools opgeeft, kunt gebruiken Azure Batch automatisch deze teveel indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="38a37-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="38a37-108">Voor het gebruik van virtuele machines prioriteit Laag afweging is dat deze virtuele machines worden gebruikt wanneer er geen overtollige capaciteit beschikbaar in Azure is.</span><span class="sxs-lookup"><span data-stu-id="38a37-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="38a37-109">Om deze reden prioriteit Laag VMs meest geschikt zijn voor bepaalde typen werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="38a37-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="38a37-110">Prioriteit Laag VM's gebruiken voor batch en asynchrone verwerking werkbelastingen waar de voltooiingstijd van de taak is flexibel en het werk verdeeld is over veel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="38a37-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="38a37-111">Prioriteit Laag VM's zijn aanzienlijk minder duur dan toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="38a37-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="38a37-112">Zie voor prijsinformatie, [prijzen van Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="38a37-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="38a37-113">Voor aanvullende informatie met lage prioriteit VM's, Zie de blogberichtaankondiging: [Batch computing een fractie van de prijs](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="38a37-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38a37-114">Prioriteit Laag VM's zijn momenteel in preview en zijn alleen beschikbaar voor werkbelastingen in Batch.</span><span class="sxs-lookup"><span data-stu-id="38a37-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="38a37-115">Gebruiksvoorbeelden voor VM met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="38a37-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="38a37-116">Gezien de kenmerken van virtuele machines prioriteit Laag, werkbelastingen kunnen en deze niet gebruiken?</span><span class="sxs-lookup"><span data-stu-id="38a37-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="38a37-117">In het algemeen zijn batch verwerkingsbelastingen geschikt, zoals taken worden onderverdeeld in veel parallelle taken of er zijn veel taken die worden uitgebreid en verdeeld over veel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="38a37-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="38a37-118">Als u wilt maximaliseren gebruik van overtollige capaciteit in Azure, uitbreiden geschikte taken.</span><span class="sxs-lookup"><span data-stu-id="38a37-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="38a37-119">Tijd tot tijd VM's mogelijk niet beschikbaar of wordt afgebroken die resulteert in minder capaciteit voor taken en kan leiden tot een onderbreking van de taak en herhalingen.</span><span class="sxs-lookup"><span data-stu-id="38a37-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="38a37-120">Taken moet daarom flexibele in de tijd die ze ondernemen kunnen om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="38a37-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="38a37-121">Taken met langer taken mogelijk meer beïnvloed als onderbroken.</span><span class="sxs-lookup"><span data-stu-id="38a37-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="38a37-122">Als langlopende taken implementeren plaatsen van controlepunten voor de voortgang opslaan als ze worden uitgevoerd, zou klikt u vervolgens de impact van onderbreking zijn veel minder.</span><span class="sxs-lookup"><span data-stu-id="38a37-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="38a37-123">Taken met een kortere uitvoeringstijden vaak werken het beste met lage prioriteit VM's zoals de impact van de onderbreking veel minder is.</span><span class="sxs-lookup"><span data-stu-id="38a37-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="38a37-124">Langlopende MPI-taken die gebruikmaken van meerdere virtuele machines zijn niet geschikt leidt voor het gebruik van VM met lage prioriteit, zoals een VM afgebroken waarschijnlijk tot het gehele project met opnieuw te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="38a37-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="38a37-125">Enkele voorbeelden van batch verwerking gevallen ook geschikt zijn voor het gebruik van prioriteit Laag VM's zijn:</span><span class="sxs-lookup"><span data-stu-id="38a37-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="38a37-126">**Ontwikkelen en testen van**: In het bijzonder als grootschalige oplossingen worden ontwikkeld aanzienlijke besparing kan worden gerealiseerd.</span><span class="sxs-lookup"><span data-stu-id="38a37-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="38a37-127">Alle typen van de testen kunnen profiteren, maar grootschalige load testen en regressie testen zijn geweldige gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38a37-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="38a37-128">**Ter aanvulling van de capaciteit op aanvraag**: prioriteit Laag virtuele machines kunnen worden gebruikt als aanvulling op regular toegewezen virtuele machines - indien beschikbaar, taken kunnen schalen en daarom sneller voltooid voor lagere kosten; wanneer deze niet beschikbaar is, de basislijn is toegewezen virtuele machines beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="38a37-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="38a37-129">**Flexibele uitvoeringstijd**: als er flexibiliteit in de tijd taken hebt voltooid, en vervolgens potentiële uitvalt capaciteit kunnen verdragen; echter met het toevoegen van virtuele machines prioriteit Laag taken worden regelmatig uitgevoerd sneller en goedkoper.</span><span class="sxs-lookup"><span data-stu-id="38a37-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="38a37-130">Batch-pools kunnen worden geconfigureerd voor het gebruik van virtuele machines prioriteit laag in een aantal manieren, afhankelijk van de flexibiliteit in de uitvoeringstijd van de taak:</span><span class="sxs-lookup"><span data-stu-id="38a37-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="38a37-131">Prioriteit Laag VMs kunnen uitsluitend worden gebruikt in een pool en Batch herstelt gewoon alle preempted capaciteit indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="38a37-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="38a37-132">Dit is de goedkoopste manier uitvoeren van taken, zoals alleen-prioriteit Laag VM's worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38a37-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="38a37-133">Prioriteit Laag VM's kunnen worden gebruikt in combinatie met een vaste basislijn toegewezen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="38a37-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="38a37-134">Het vaste aantal toegewezen virtuele machines, zorgt u ervoor is altijd een aantal capaciteit om de voortgang van een taak.</span><span class="sxs-lookup"><span data-stu-id="38a37-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="38a37-135">Er kan dynamische combinatie van virtuele machines toegewezen en een lage prioriteit, zodat de goedkoper prioriteit Laag virtuele machines worden uitsluitend gebruikt indien beschikbaar, maar de volledige geprijsde toegewezen virtuele machines worden opgeschaald als voor het behouden van de minimale hoeveelheid capaciteit die beschikbaar is om de voortgang taken beperken vereist.</span><span class="sxs-lookup"><span data-stu-id="38a37-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="38a37-136">Batch-ondersteuning voor VM met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="38a37-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="38a37-137">Azure Batch biedt verschillende mogelijkheden die gemakkelijk te gebruiken en profiteren van virtuele machines prioriteit Laag:</span><span class="sxs-lookup"><span data-stu-id="38a37-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="38a37-138">Batch-pools kunnen zowel toegewezen virtuele machines en virtuele machines prioriteit Laag bevatten.</span><span class="sxs-lookup"><span data-stu-id="38a37-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="38a37-139">Het aantal van elk type van de virtuele machine kan worden opgegeven wanneer een groep wordt gemaakt of gewijzigd op elk gewenst moment voor een bestaande pool met de bewerking formaat expliciete of automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="38a37-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="38a37-140">Verzending van de taak en kunt blijven ongewijzigd en hoeft niet te worden betrokken zijn bij de VM-typen in de groep.</span><span class="sxs-lookup"><span data-stu-id="38a37-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="38a37-141">Het is ook mogelijk om een pool volledig met lage prioriteit virtuele machines worden taken goedkoop als mogelijk, maar spin up toegewezen virtuele machines worden uitgevoerd als de capaciteit onder een drempel zakt, zodat taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="38a37-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="38a37-142">Batch-pools zoeken automatisch naar het is het doelaantal van prioriteit Laag VM's.</span><span class="sxs-lookup"><span data-stu-id="38a37-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="38a37-143">Als VMs zijn gereserveerd, probeer Batch te vervangen door de verloren capaciteit en terug te keren naar het doel.</span><span class="sxs-lookup"><span data-stu-id="38a37-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="38a37-144">In het geval van taken wordt onderbroken, Batch detecteert en automatisch requeue taken opnieuw te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="38a37-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="38a37-145">Prioriteit Laag VM's hebben een quotum voor kernen die van de toegewezen virtuele machines verschilt.</span><span class="sxs-lookup"><span data-stu-id="38a37-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="38a37-146">Het aanhalingsteken voor virtuele machines prioriteit laag is hoger dan die van de toegewezen virtuele machines, omdat minder VM met lage prioriteit kosten.</span><span class="sxs-lookup"><span data-stu-id="38a37-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="38a37-147">Zie [Batch-servicequota en limieten](batch-quota-limit.md#resource-quotas) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="38a37-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="38a37-148">Prioriteit Laag virtuele machines worden momenteel niet ondersteund voor Batch-accounts waarvan de modus van de toewijzing van toepassingen is ingesteld op [gebruikerabonnement](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="38a37-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="38a37-149">Maken en bijwerken van groepen</span><span class="sxs-lookup"><span data-stu-id="38a37-149">Create and update pools</span></span>

<span data-ttu-id="38a37-150">Een Batch-pool kan toegewezen en prioriteit Laag virtuele machines (ook wel rekenknooppunten) bevatten.</span><span class="sxs-lookup"><span data-stu-id="38a37-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="38a37-151">U kunt het nummer van het doel van rekenknooppunten instellen voor virtuele machines toegewezen en lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="38a37-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="38a37-152">Het doelaantal knooppunten geeft het aantal virtuele machines die u hebt in de groep wilt maken.</span><span class="sxs-lookup"><span data-stu-id="38a37-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="38a37-153">Bijvoorbeeld: voor het maken van een groep met behulp van de cloudservice van Azure VM's met een doel van 5 toegewezen virtuele machines en 20 prioriteit Laag VM's:</span><span class="sxs-lookup"><span data-stu-id="38a37-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="38a37-154">Met behulp van Azure virtuele machines (in dit geval virtuele Linux-machines) met een doel van 5 toegewezen voor het maken van een groep VM's en 20 prioriteit Laag VM's:</span><span class="sxs-lookup"><span data-stu-id="38a37-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="38a37-155">U kunt het huidige aantal knooppunten voor virtuele machines toegewezen en lage prioriteit krijgen:</span><span class="sxs-lookup"><span data-stu-id="38a37-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="38a37-156">Groep knooppunten hebben een eigenschap om aan te geven als het knooppunt een virtuele machine toegewezen of lage prioriteit:</span><span class="sxs-lookup"><span data-stu-id="38a37-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="38a37-157">Als een of meer knooppunten in een pool zijn gereserveerd, een lijst met knooppunten-bewerking op de groep wordt nog steeds geretourneerd die knooppunten, het huidige aantal knooppunten prioriteit Laag ongewijzigd blijft, maar die knooppunten de status ingesteld heeft op de **vervallen** status.</span><span class="sxs-lookup"><span data-stu-id="38a37-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="38a37-158">Batch wordt gezocht naar vervanging virtuele machines en, als dit lukt, de knooppunten doorlopen **maken** en vervolgens **starten** statussen voordat deze beschikbaar voor uitvoering van de taak, net als bij nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="38a37-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="38a37-159">Een groep met lage prioriteit VMs schalen</span><span class="sxs-lookup"><span data-stu-id="38a37-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="38a37-160">Net als bij de opslaggroepen die uitsluitend bestaan uit toegewezen virtuele machines, is het mogelijk om te schalen van een groep met lage prioriteit virtuele machines met het aanroepen van de methode formaat of automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="38a37-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="38a37-161">De bewerking van het formaat van toepassingen wordt een tweede optionele parameter waarmee de waarde van bijgewerkt **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="38a37-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="38a37-162">De formule van de groep automatisch schalen ondersteunt prioriteit Laag virtuele machines als volgt:</span><span class="sxs-lookup"><span data-stu-id="38a37-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="38a37-163">U kunt opvragen of stel de waarde van de service gedefinieerde variabele **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="38a37-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="38a37-164">U kunt de waarde van de service gedefinieerde variabele opvragen **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="38a37-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="38a37-165">U kunt de waarde van de service gedefinieerde variabele opvragen **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="38a37-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="38a37-166">Deze variabele retourneert het aantal knooppunten in de status van de preempted en kunt u schalen omhoog of omlaag het aantal toegewezen knooppunten, afhankelijk van het aantal afgebroken knooppunten die niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="38a37-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="38a37-167">Jobs en taken</span><span class="sxs-lookup"><span data-stu-id="38a37-167">Jobs and tasks</span></span>

<span data-ttu-id="38a37-168">Jobs en taken vereist weinig ondersteuning voor knooppunten met lage prioriteit. de enige ondersteuning is als volgt:</span><span class="sxs-lookup"><span data-stu-id="38a37-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="38a37-169">De eigenschap JobManagerTask van een taak heeft een nieuwe eigenschap **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="38a37-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="38a37-170">Wanneer deze eigenschap true is, kan de jobbeheertaak worden gepland op een knooppunt toegewezen of lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="38a37-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="38a37-171">Als deze eigenschap ingesteld op false is, wordt de jobbeheertaak naar specifieke knooppunt worden gepland.</span><span class="sxs-lookup"><span data-stu-id="38a37-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="38a37-172">Een [omgevingsvariabele](batch-compute-node-environment-variables.md) is beschikbaar voor een taaktoepassing zodat deze bepalen kan of deze wordt uitgevoerd op een knooppunt met lage prioriteit of toegewezen.</span><span class="sxs-lookup"><span data-stu-id="38a37-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="38a37-173">De omgevingsvariabele is AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="38a37-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="38a37-174">Afhandeling van voorrang</span><span class="sxs-lookup"><span data-stu-id="38a37-174">Handling preemption</span></span>

<span data-ttu-id="38a37-175">Virtuele machines kunnen van tijd tot tijd worden gebruikt; Als dit gebeurt, is Batch doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="38a37-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="38a37-176">De preempted virtuele machines hebben hun status bijgewerkt naar **vervallen**.</span><span class="sxs-lookup"><span data-stu-id="38a37-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="38a37-177">Als taken zijn uitgevoerd op de virtuele machines van knooppunt afgebroken, zijn deze taken de opnieuw en voer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="38a37-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="38a37-178">De virtuele machine wordt effectief verwijderd, wat leidt tot alle gegevens die lokaal zijn opgeslagen op de virtuele machine verloren.</span><span class="sxs-lookup"><span data-stu-id="38a37-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="38a37-179">De pool wordt voortdurend probeert te bereiken van het doelaantal knooppunten van prioriteit Laag beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="38a37-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="38a37-180">Als u vervangingscapaciteit wordt gevonden, de knooppunten behouden hun id, maar zijn opnieuw geïnitialiseerd, gaan via **maken** en **starten** aangegeven voordat ze beschikbaar voor het plannen van taken zijn.</span><span class="sxs-lookup"><span data-stu-id="38a37-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="38a37-181">Voorrang aantallen zijn beschikbaar als een waarde in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="38a37-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="38a37-182">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="38a37-182">Metrics</span></span>

<span data-ttu-id="38a37-183">Nieuwe metrische gegevens zijn beschikbaar in de [Azure-portal](https://portal.azure.com) voor knooppunten met lage prioriteit.</span><span class="sxs-lookup"><span data-stu-id="38a37-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="38a37-184">Deze metrische gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="38a37-184">These metrics are:</span></span>

- <span data-ttu-id="38a37-185">Aantal knooppunten met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="38a37-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="38a37-186">Aantal kernen met lage prioriteit</span><span class="sxs-lookup"><span data-stu-id="38a37-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="38a37-187">Aantal knooppunten afgebroken</span><span class="sxs-lookup"><span data-stu-id="38a37-187">Preempted Node Count</span></span>

<span data-ttu-id="38a37-188">Metrische gegevens weergeven in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="38a37-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="38a37-189">Navigeer naar uw Batch-account in de portal en bekijk de instellingen voor uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="38a37-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="38a37-190">Selecteer **metrische gegevens** van de **bewaking** sectie.</span><span class="sxs-lookup"><span data-stu-id="38a37-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="38a37-191">Selecteer de metrische gegevens die u van wenst de **beschikbare metrische gegevens** lijst.</span><span class="sxs-lookup"><span data-stu-id="38a37-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Metrische gegevens voor knooppunten met lage prioriteit](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="38a37-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38a37-193">Next steps</span></span>

* <span data-ttu-id="38a37-194">Bekijk het [overzicht met Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen die Batch wil gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38a37-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="38a37-195">Het artikel bevat meer gedetailleerde informatie over de Batch-serviceresources zoals groepen, knooppunten, jobs en taken, en de vele API-functies die u tijdens het maken van de Batch-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38a37-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="38a37-196">Meer informatie over de [Batch-API's en -hulpprogramma's](batch-apis-tools.md) die beschikbaar zijn voor het bouwen van Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="38a37-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
