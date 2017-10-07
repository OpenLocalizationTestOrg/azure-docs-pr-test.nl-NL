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
# <a name="use-low-priority-vms-with-batch-preview"></a>Met lage prioriteit virtuele machines, met Batch (Preview)

Azure Batch biedt beperkte priorty virtuele machines (VM's) tooreduce Hallo kosten van Batch-workloads. Prioriteit Laag virtuele machines maken nieuwe typen van Batch-workloads mogelijk doordat een grote hoeveelheid rekenkracht die ook voordelige.

Prioriteit Laag virtuele machines te profiteren van de overtollige capaciteit in Azure. Wanneer u lage prioriteit VM's in uw pools opgeeft, kunt gebruiken Azure Batch automatisch deze teveel indien beschikbaar.

Hallo afweging voor het gebruik van virtuele machines prioriteit laag is dat deze virtuele machines worden gebruikt wanneer er geen overtollige capaciteit beschikbaar in Azure is. Om deze reden prioriteit Laag VMs meest geschikt zijn voor bepaalde typen werkbelastingen. Prioriteit Laag VM's gebruiken voor batch en asynchrone verwerking werkbelastingen waarbij Hallo taak voltooiingstijd is flexibel en Hallo werk verdeeld is over veel virtuele machines.

Prioriteit Laag VM's zijn aanzienlijk minder duur dan toegewezen virtuele machines. Zie voor prijsinformatie, [prijzen van Batch](https://azure.microsoft.com/pricing/details/batch/).

Zie voor aanvullende informatie van virtuele machines prioriteit Laag, Hallo blogberichtaankondiging: [Batch computing een fractie van Hallo prijs](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Prioriteit Laag VM's zijn momenteel in preview en zijn alleen beschikbaar voor werkbelastingen in Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Gebruiksvoorbeelden voor VM met lage prioriteit

Hallo-kenmerken van virtuele machines prioriteit Laag gegeven, welke workloads kunnen en deze niet gebruiken? In het algemeen zijn batch verwerkingsbelastingen geschikt, zoals taken worden onderverdeeld in veel parallelle taken of er zijn veel taken die worden uitgebreid en verdeeld over veel virtuele machines.

-   toomaximize gebruik van overtollige capaciteit in Azure, geschikte taken kunt uitbreiden.

-   Tijd tot tijd VM's mogelijk niet beschikbaar of wordt afgebroken die resulteert in minder capaciteit voor taken en tootask onderbreking en herhalingen kan leiden. Taken moet daarom flexibele tijdig Hallo die toorun kunnen nemen.

-   Taken met langer taken mogelijk meer beïnvloed als onderbroken. Als langlopende taken uitgevoerd voor het plaatsen van controlepunten toosave implementeren, zoals ze worden uitgevoerd, zou klikt u vervolgens de impact van onderbreking zijn veel minder. Taken met een kortere uitvoeringstijden vaak toowork beste met lage prioriteit VMs Hallo impact van de onderbreking is veel minder.

-   Langlopende MPI-taken die gebruikmaken van meerdere virtuele machines zijn niet geschikt toouse wordt VMs prioriteit laag als een virtuele machine afgebroken waarschijnlijkheid potentiële toohello hele taak met toobe opnieuw uitvoeren.

Enkele voorbeelden van batchverwerking gebruik gevallen geschikt toouse prioriteit Laag VM's zijn:

-   **Ontwikkelen en testen van**: In het bijzonder als grootschalige oplossingen worden ontwikkeld aanzienlijke besparing kan worden gerealiseerd. Alle typen van de testen kunnen profiteren, maar grootschalige load testen en regressie testen zijn geweldige gebruikt.

-   **Ter aanvulling van de capaciteit op aanvraag**: prioriteit Laag virtuele machines kunnen worden gebruikt als aanvulling op regular toegewezen virtuele machines - indien beschikbaar, taken kunnen schalen en daarom sneller voltooid voor lagere kosten; wanneer niet beschikbaar is, Hallo basislijn van specifieke virtuele machines beschikbaar zijn.

-   **Flexibele uitvoeringstijd**: als er flexibiliteit in Hallo tijd taken hebt toocomplete, en vervolgens potentiële uitvalt capaciteit kunnen verdragen; echter Hello prioriteit Laag VMs taken toe te voegen wordt vaak uitgevoerd sneller en goedkoper.

Batch-pools kunnen geconfigureerde toouse prioriteit Laag VM's in een aantal manieren afhankelijk van Hallo flexibiliteit in de taak uitvoeringstijd zijn:

-   Prioriteit Laag VMs kunnen uitsluitend worden gebruikt in een pool en Batch herstelt gewoon alle preempted capaciteit indien beschikbaar. Dit is Hallo goedkoopste manier tooexecute taken, zoals alleen-prioriteit Laag VM's worden gebruikt.

-   Prioriteit Laag VM's kunnen worden gebruikt in combinatie met een vaste basislijn toegewezen virtuele machines. Hallo zorgt vast aantal toegewezen virtuele machines dat er is altijd een aantal tookeep capaciteit de voortgang van een taak.

-   Er mag dynamische combinatie van virtuele machines toegewezen en een lage prioriteit, zodat de goedkoper prioriteit Laag virtuele machines worden uitsluitend gebruikt indien beschikbaar, maar Hallo volledige geprijsde toegewezen virtuele machines worden opgeschaald indien nodig, de minimale hoeveelheid capaciteit beschikbaar tookeep Hallo taken tookeep voortgang hebben.

## <a name="batch-support-for-low-priority-vms"></a>Batch-ondersteuning voor VM met lage prioriteit

Azure Batch biedt verschillende mogelijkheden die maken het gemakkelijk tooconsume en profiteren van virtuele machines prioriteit Laag:

-   Batch-pools kunnen zowel toegewezen virtuele machines en virtuele machines prioriteit Laag bevatten. Hallo aantal van elk type van de virtuele machine kan worden opgegeven wanneer een groep wordt gemaakt of gewijzigd op elk gewenst moment voor een bestaande pool met expliciete Hallo/verkleinbewerking of automatisch schalen. Verzending van de taak en kunt blijven ongewijzigd en hoeft niet te worden betrokken met Hallo VM typen in Hallo van toepassingen. Het is ook mogelijk toohave een pool volledig gebruik prioriteit Laag VMs toorun taken goedkoop als mogelijk, maar spin up toegewezen virtuele machines als Hallo capaciteit zakt onder een drempel, zodat taken worden uitgevoerd.

-   Batch-pools zoeken automatisch toohello doelaantal prioriteit Laag virtuele machines. Als VMs zijn gereserveerd, proberen Batch tooreplace Hallo capaciteit en het doel van de geretourneerde toohello verloren.

-   In geval van taken wordt onderbroken Hallo Batch detecteert en automatisch requeue taken toobe opnieuw uitvoeren.

-   Prioriteit Laag VM's hebben een quotum voor kernen die van de toegewezen virtuele machines verschilt. 
    Hallo aanhalingsteken voor prioriteit Laag virtuele machines is hoger dan die van de toegewezen virtuele machines, omdat minder VM met lage prioriteit kosten. Zie [Batch-servicequota en limieten](batch-quota-limit.md#resource-quotas) voor meer informatie.    

> [!NOTE]
> Prioriteit Laag virtuele machines worden momenteel niet ondersteund voor Batch-accounts waarbij Hallo groep toewijzing modus te is ingesteld[gebruikerabonnement](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Maken en bijwerken van groepen

Een Batch-pool kan toegewezen en prioriteit Laag virtuele machines (ook waarnaar wordt verwezen tooas rekenknooppunten) bevatten. U kunt Hallo doelaantal rekenknooppunten instellen voor virtuele machines toegewezen en lage prioriteit. Hallo doelaantal knooppunten bevat Hallo nummer van virtuele machines die u wilt toohave in Hallo van toepassingen.

Bijvoorbeeld, toocreate een pool met behulp van de cloudservice van Azure VM's met een doel van 5 VM's en 20 prioriteit Laag VM's toegewezen:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

toocreate een pool met virtuele Azure-machines (in dit geval virtuele Linux-machines) met een doel van 5 toegewezen virtuele machines en 20 prioriteit Laag VM's:

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

U kunt Hallo Huidig aantal knooppunten voor virtuele machines toegewezen en lage prioriteit krijgen:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Groep knooppunten hebben een eigenschap tooindicate als Hallo knooppunt een virtuele machine toegewezen of lage prioriteit:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Als een of meer knooppunten in een pool zijn gereserveerd, een lijst met knooppunten-bewerking op de toepassingen nog steeds die knooppunten retourneert, Huidig aantal prioriteit Laag knooppunten Hallo ongewijzigd blijft, maar die knooppunten hebben hun status toothe ingesteld **vervallen**status. Batch zal proberen toofind vervanging virtuele machines en, als dit lukt, Hallo knooppunten doorlopen **maken** en vervolgens **starten** statussen voordat deze beschikbaar voor uitvoering van de taak, net als bij nieuwe knooppunten.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Een groep met lage prioriteit VMs schalen

Net als bij de opslaggroepen die uitsluitend bestaan uit toegewezen virtuele machines, is mogelijk tooscale een groep met lage prioriteit virtuele machines Hallo formaat methode aanroepen of met automatisch schalen.

Hallo groep formaat duurt een tweede optionele parameter waarmee de waarde van bijgewerkt **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

Hallo pool automatisch schalen formule ondersteunt prioriteit Laag virtuele machines als volgt:

-   U kunt ophalen of instellen van Hallo-waarde van Hallo service gedefinieerde variabele **$TargetLowPriorityNodes**.

-   U kunt de waarde Hallo van Hallo service gedefinieerde variabele opvragen **$CurrentLowPriorityNodes**.

-   U kunt de waarde Hallo van Hallo service gedefinieerde variabele opvragen **$PreemptedNodeCount**. 
    Deze variabele retourneert het aantal knooppunten in Hallo Hallo status afgebroken en kunt u omhoog of omlaag Hallo aantal toegewezen knooppunten, afhankelijk van het aantal afgebroken knooppunten die niet beschikbaar zijn Hallo schalen.

## <a name="jobs-and-tasks"></a>Jobs en taken

Jobs en taken vereist weinig ondersteuning voor knooppunten met lage prioriteit. alleen ondersteuning voor Hallo is als volgt:

-   Hallo JobManagerTask-eigenschap van een taak heeft een nieuwe eigenschap **AllowLowPriorityNode**. 
    Wanneer deze eigenschap true is, kan de jobbeheertaak Hallo worden gepland op een knooppunt toegewezen of lage prioriteit. Als deze eigenschap ingesteld op false is, worden jobbeheertaak Hallo geplande tooa alleen specifieke knooppunt.

-   Een [omgevingsvariabele](batch-compute-node-environment-variables.md) beschikbaar tooa taaktoepassing is zodat deze bepalen kan of deze wordt uitgevoerd op een knooppunt met lage prioriteit of toegewezen. Hallo-omgevingsvariabele is AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Afhandeling van voorrang

Virtuele machines kunnen van tijd tot tijd worden gebruikt; Als dit gebeurt, Batch Hallo te volgen:

-   Hallo afgebroken virtuele machines hebben hun status bijgewerkt**vervallen**.
-   Als er taken zijn uitgevoerd op afgebroken Hallo knooppunt virtuele machines, en vervolgens deze taken worden opnieuw en voer het opnieuw.
-   Hallo VM wordt effectief verwijderd, voorloopspaties tooany gegevens die lokaal zijn opgeslagen op Hallo VM verloren.
-   Hallo groep probeert voortdurend tooreach hello doelaantal prioriteit Laag knooppunten beschikbaar. Als u vervangingscapaciteit wordt gevonden, de knooppunten behouden hun id, maar zijn opnieuw geïnitialiseerd, gaan via **maken** en **starten** aangegeven voordat ze beschikbaar voor het plannen van taken zijn.
-   Voorrang aantallen zijn beschikbaar als een waarde in hello Azure-portal.

## <a name="metrics"></a>Metrische gegevens

Nieuwe metrische gegevens zijn beschikbaar in Hallo [Azure-portal](https://portal.azure.com) voor knooppunten met lage prioriteit. Deze metrische gegevens zijn:

- Aantal knooppunten met lage prioriteit
- Aantal kernen met lage prioriteit 
- Aantal knooppunten afgebroken

tooview metrische gegevens in hello Azure-portal:

1. Navigeer tooyour Batch-account in de portal Hallo en Hallo-instellingen voor uw Batch-account weergeven.
2. Selecteer **metrische gegevens** van Hallo **bewaking** sectie.
3. Selecteer Hallo metrische gegevens die u wenst in Hallo **beschikbare metrische gegevens** lijst.

![Metrische gegevens voor knooppunten met lage prioriteit](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Volgende stappen

* Lees Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen toouse Batch voorbereiden. Hallo artikel bevat meer gedetailleerde informatie over Batch-service-resources zoals pools, knooppunten, jobs en taken en Hallo veel API-functies die u tijdens het bouwen van uw Batch-toepassing kunt gebruiken.
* Meer informatie over Hallo [Batch-API's en hulpprogramma's](batch-apis-tools.md) beschikbaar voor het bouwen van Batch-oplossingen.
