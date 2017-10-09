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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Taken uitvoeren gelijktijdig gebruik van Batch-rekenknooppunten toomaximize 

U kunt door meer dan één taak tegelijkertijd uitgevoerd op elk rekenknooppunt in uw Azure Batch-pool, brongebruik op een kleiner aantal knooppunten in de pool Hallo maximaliseren. Voor sommige werkbelastingen, kan dit resulteren in een kortere taaktijden en lagere kosten.

Hoewel sommige scenario's profiteren van dat alle één taak van een knooppunt resources tooa, profiteert verschillende situaties zodat meerdere taken tooshare die bronnen:

* **Overdracht van gegevens voor het minimaliseren** wanneer taken kunnen tooshare gegevens zijn. In dit scenario kunt u gegevensoverdracht kosten aanzienlijk verkleinen door het kopiëren van gedeelde gegevens tooa kleiner aantal knooppunten en het uitvoeren van taken parallel op elk knooppunt. Dit geldt vooral als Hallo gegevens toobe gekopieerde tooeach knooppunt moet worden overgedragen tussen geografische regio's.
* **Het optimaliseren van geheugengebruik** wanneer taken vereisen dat een grote hoeveelheid geheugen, maar alleen gedurende korte perioden tijd en op variabele momenten tijdens de uitvoering. U kunt gebruiken minder maar groter, compute knooppunten met meer geheugen tooefficiently verwerken van dergelijke pieken. Deze knooppunten zou hebben meerdere taken parallel uitgevoerd op elk knooppunt, maar elke taak wilt profiteren van de grote hoeveelheid geheugen Hallo-knooppunten op verschillende tijdstippen.
* **Aantal grenzen knooppunt beperkende** wanneer de communicatie tussen knooppunten is vereist in een pool. Toepassingen die zijn geconfigureerd voor communicatie tussen knooppunten zijn momenteel beperkt too50 rekenknooppunten. Als elk knooppunt in deze groep kunnen tooexecute taken parallel is, kan een groter aantal taken tegelijkertijd worden uitgevoerd.
* **Bezig met het repliceren van een lokale compute cluster**, zoals wanneer u een tooAzure compute-omgeving voor het eerst hebt verplaatst. Als uw huidige on-premises-oplossing wordt meerdere taken per rekenknooppunt uitgevoerd, kunt u het maximum aantal Hallo verhogen van knooppunt taken spiegelen toomore nauw dat de configuratie.

## <a name="example-scenario"></a>Voorbeeldscenario 's
Als een voorbeeld tooillustrate Hallo voordelen van de uitvoering van parallelle taken, Stel dat uw taaktoepassing heeft CPU en geheugen vereisten zodat [standaard\_D1](../cloud-services/cloud-services-sizes-specs.md) knooppunten zijn voldoende. Maar in volgorde toofinish Hallo taak Hallo vereist tijdig 1.000 van deze knooppunten nodig zijn.

In plaats van met behulp van standaard\_D1 knooppunten die 1 CPU-kern hebt, kunt u [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten met 16 kernen en uitvoering van de parallelle taak inschakelen. Daarom *16 keer minder knooppunten* kan alleen worden gebruikt--in plaats van 1000 knooppunten 63 zijn vereist. Bovendien als grote toepassingsbestanden of referentiegegevens vereist voor elk knooppunt zijn, zijn de duur van de taak en efficiëntie opnieuw verbeterd omdat Hallo gegevens gekopieerde tooonly 16 knooppunten.

## <a name="enable-parallel-task-execution"></a>Uitvoering van de parallelle taak inschakelen
Bij het configureren van rekenknooppunten voor parallelle uitvoering op Hallo van toepassingen niveau. Hallo Batch .NET-bibliotheek, stel Hallo [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap bij het maken van een groep. Als u Hallo Batch REST-API gebruikt, stelt u Hallo [maxTasksPerNode] [ rest_addpool] element in de aanvraagtekst Hallo tijdens het maken van de groep van toepassingen.

Azure Batch kunt u tooset maximum aantal taken per knooppunt een toofour tijden (4 x) Hallo aantal kernen knooppunt. Bijvoorbeeld, als hello van toepassingen is geconfigureerd met knooppunten met een grootte van 'Groot' (vier kernen), vervolgens `maxTasksPerNode` too16 kan worden ingesteld. Zie voor meer informatie op het aantal kernen voor elk van de knooppuntgrootten Hallo Hallo [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md). Zie voor meer informatie over Servicelimieten [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).

> [!TIP]
> Ervoor tootake in account Hallo worden `maxTasksPerNode` waarde als u een [formule voor automatisch schalen] [ enable_autoscaling] voor uw toepassingen. Bijvoorbeeld, een formule waarvan de evaluatie `$RunningTasks` aanzienlijk kunnen worden beïnvloed door een toename van de taken per knooppunt. Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](batch-automatic-scaling.md) voor meer informatie.
>
>

## <a name="distribution-of-tasks"></a>Verdeling van taken
Wanneer Hallo rekenknooppunten in een groep gelijktijdig taken uitvoeren kunnen, is het belangrijk toospecify Hallo taken toobe verdeeld over Hallo knooppunten in Hallo pool gewenste.

Met behulp van Hallo [CloudPool.TaskSchedulingPolicy] [ task_schedule] eigenschap, kunt u opgeven dat taken gelijkmatig over alle knooppunten in Hallo-groep ('spreiden") moeten worden toegewezen. Of u kunt opgeven dat zo zo veel mogelijk taken moeten worden toegewezen tooeach knooppunt voordat taken tooanother-knooppunt in Hallo-pool ('verpakking') worden toegewezen.

Een voorbeeld van hoe deze functie waardevolle is, kunt u beter Hallo-pool van [standaard\_D14](../cloud-services/cloud-services-sizes-specs.md) knooppunten (in de bovenstaande Hallo voorbeeld) die is geconfigureerd met een [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] waarde van 16. Als hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] is geconfigureerd met een [ComputeNodeFillType] [ fill_type] van *Pack*, zou het gebruik van alle 16 kernen van elk knooppunt maximaliseren en toestaan een [automatisch schalen van toepassingen](batch-automatic-scaling.md) tooprune ongebruikte knooppunten uit Hallo-groep (knooppunten zonder geen taken toegewezen). Hierdoor minimaliseert brongebruik en bespaart u geld.

## <a name="batch-net-example"></a>Batch .NET-voorbeeld
Dit [Batch .NET] [ api_net] API-codefragment toont een toocreate aanvraag een groep die vier grote knooppunten met een maximum van vier taken per knooppunt bevat. Hiermee wordt een taak plannen beleid dat elk knooppunt met taken voorafgaande tooassigning taken tooanother-knooppunt in het Hallo-groep wordt gevuld. Zie voor meer informatie over het toevoegen van groepen met behulp van Batch .NET API Hallo [BatchClient.PoolOperations.CreatePool][poolcreate_net].

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

## <a name="batch-rest-example"></a>Batch REST-voorbeeld
Dit [Batch REST] [ api_rest] API fragment toont een toocreate aanvraag een groep die twee grote knooppunten met een maximum van vier taken per knooppunt bevat. Zie voor meer informatie over het toevoegen van groepen met behulp van REST-API Hallo [toevoegen van een account voor toepassingsgroep tooan][rest_addpool].

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
> U kunt instellen Hallo `maxTasksPerNode` element en [MaxTasksPerComputeNode] [ maxtasks_net] eigenschap alleen tijdens de aanmaak van toepassingen. Ze kunnen niet worden gewijzigd nadat een pool al zijn gemaakt.
>
>

## <a name="code-sample"></a>Codevoorbeeld
Hallo [ParallelNodeTasks] [ parallel_tasks_sample] project op GitHub illustreert Hallo gebruik van Hallo [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] eigenschap.

Deze C#-consoletoepassing maakt gebruik van Hallo [Batch .NET] [ api_net] bibliotheek toocreate een groep met een of meer rekenknooppunten. Een configureerbare aantal taken wordt uitgevoerd op die knooppunten toosimulate variabele laden. Uitvoer van de toepassing hello geeft aan welke knooppunten uitgevoerd elke taak. Hallo-toepassing bevat ook een samenvatting van taakparameters Hallo en duur. Hallo samenvatting deel van Hallo-uitvoer van twee verschillende uitvoeringen van de voorbeeldtoepassing hello wordt hieronder weergegeven.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

eerste uitvoering van de voorbeeldtoepassing Hallo Hallo blijkt dat met één knooppunt in het Hallo-pool en de standaardinstelling Hallo van één taak per knooppunt Hallo taak duur is meer dan 30 minuten.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Hallo tweede run van Hallo voorbeeld toont een aanzienlijke daling van de duur van de taak. Dit is omdat Hallo van toepassingen is geconfigureerd met vier taken per knooppunt, waardoor de parallelle uitvoering toocomplete Hallo taak in bijna een kwartaal Hallo tijd.

> [!NOTE]
> duur van de taak Hallo in Hallo samenvattingen van de bovenstaande omvatten geen tijd voor het maken van toepassingen. Elk van de bovenstaande Hallo-taken is verzonden toopreviously gemaakt groepen waarvan rekenknooppunten in Hallo zijn *inactief* status tijdens verzending.
>
>

## <a name="next-steps"></a>Volgende stappen
### <a name="batch-explorer-heat-map"></a>Batch Explorer-Heatmap
Hallo [Azure Batch Explorer][batch_explorer], een hello Azure Batch [voorbeeldtoepassingen][github_samples], bevat een *Heatmap* functie waarmee visualisatie van de uitvoering van de taak. Wanneer u bent uitvoeren van Hallo [ParallelTasks] [ parallel_tasks_sample] voorbeeldtoepassing, kunt u Hallo Heat Map functie tooeasily visualiseren Hallo parallelle taken op elk knooppunt worden uitgevoerd.

![Batch Explorer-Heatmap][1]

*Batch Explorer Heat Map met een pool met vier knooppunten, met elk knooppunt vier taken momenteel worden uitgevoerd*

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
