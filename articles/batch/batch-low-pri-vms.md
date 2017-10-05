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
# <a name="use-low-priority-vms-with-batch-preview"></a>Met lage prioriteit virtuele machines, met Batch (Preview)

Azure Batch biedt beperkte priorty virtuele machines (VM's) om de kosten van Batch-workloads te beperken. Prioriteit Laag virtuele machines maken nieuwe typen van Batch-workloads mogelijk doordat een grote hoeveelheid rekenkracht die ook voordelige.

Prioriteit Laag virtuele machines te profiteren van de overtollige capaciteit in Azure. Wanneer u lage prioriteit VM's in uw pools opgeeft, kunt gebruiken Azure Batch automatisch deze teveel indien beschikbaar.

Voor het gebruik van virtuele machines prioriteit Laag afweging is dat deze virtuele machines worden gebruikt wanneer er geen overtollige capaciteit beschikbaar in Azure is. Om deze reden prioriteit Laag VMs meest geschikt zijn voor bepaalde typen werkbelastingen. Prioriteit Laag VM's gebruiken voor batch en asynchrone verwerking werkbelastingen waar de voltooiingstijd van de taak is flexibel en het werk verdeeld is over veel virtuele machines.

Prioriteit Laag VM's zijn aanzienlijk minder duur dan toegewezen virtuele machines. Zie voor prijsinformatie, [prijzen van Batch](https://azure.microsoft.com/pricing/details/batch/).

Voor aanvullende informatie met lage prioriteit VM's, Zie de blogberichtaankondiging: [Batch computing een fractie van de prijs](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Prioriteit Laag VM's zijn momenteel in preview en zijn alleen beschikbaar voor werkbelastingen in Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Gebruiksvoorbeelden voor VM met lage prioriteit

Gezien de kenmerken van virtuele machines prioriteit Laag, werkbelastingen kunnen en deze niet gebruiken? In het algemeen zijn batch verwerkingsbelastingen geschikt, zoals taken worden onderverdeeld in veel parallelle taken of er zijn veel taken die worden uitgebreid en verdeeld over veel virtuele machines.

-   Als u wilt maximaliseren gebruik van overtollige capaciteit in Azure, uitbreiden geschikte taken.

-   Tijd tot tijd VM's mogelijk niet beschikbaar of wordt afgebroken die resulteert in minder capaciteit voor taken en kan leiden tot een onderbreking van de taak en herhalingen. Taken moet daarom flexibele in de tijd die ze ondernemen kunnen om uit te voeren.

-   Taken met langer taken mogelijk meer beïnvloed als onderbroken. Als langlopende taken implementeren plaatsen van controlepunten voor de voortgang opslaan als ze worden uitgevoerd, zou klikt u vervolgens de impact van onderbreking zijn veel minder. Taken met een kortere uitvoeringstijden vaak werken het beste met lage prioriteit VM's zoals de impact van de onderbreking veel minder is.

-   Langlopende MPI-taken die gebruikmaken van meerdere virtuele machines zijn niet geschikt leidt voor het gebruik van VM met lage prioriteit, zoals een VM afgebroken waarschijnlijk tot het gehele project met opnieuw te worden uitgevoerd.

Enkele voorbeelden van batch verwerking gevallen ook geschikt zijn voor het gebruik van prioriteit Laag VM's zijn:

-   **Ontwikkelen en testen van**: In het bijzonder als grootschalige oplossingen worden ontwikkeld aanzienlijke besparing kan worden gerealiseerd. Alle typen van de testen kunnen profiteren, maar grootschalige load testen en regressie testen zijn geweldige gebruikt.

-   **Ter aanvulling van de capaciteit op aanvraag**: prioriteit Laag virtuele machines kunnen worden gebruikt als aanvulling op regular toegewezen virtuele machines - indien beschikbaar, taken kunnen schalen en daarom sneller voltooid voor lagere kosten; wanneer deze niet beschikbaar is, de basislijn is toegewezen virtuele machines beschikbaar zijn.

-   **Flexibele uitvoeringstijd**: als er flexibiliteit in de tijd taken hebt voltooid, en vervolgens potentiële uitvalt capaciteit kunnen verdragen; echter met het toevoegen van virtuele machines prioriteit Laag taken worden regelmatig uitgevoerd sneller en goedkoper.

Batch-pools kunnen worden geconfigureerd voor het gebruik van virtuele machines prioriteit laag in een aantal manieren, afhankelijk van de flexibiliteit in de uitvoeringstijd van de taak:

-   Prioriteit Laag VMs kunnen uitsluitend worden gebruikt in een pool en Batch herstelt gewoon alle preempted capaciteit indien beschikbaar. Dit is de goedkoopste manier uitvoeren van taken, zoals alleen-prioriteit Laag VM's worden gebruikt.

-   Prioriteit Laag VM's kunnen worden gebruikt in combinatie met een vaste basislijn toegewezen virtuele machines. Het vaste aantal toegewezen virtuele machines, zorgt u ervoor is altijd een aantal capaciteit om de voortgang van een taak.

-   Er kan dynamische combinatie van virtuele machines toegewezen en een lage prioriteit, zodat de goedkoper prioriteit Laag virtuele machines worden uitsluitend gebruikt indien beschikbaar, maar de volledige geprijsde toegewezen virtuele machines worden opgeschaald als voor het behouden van de minimale hoeveelheid capaciteit die beschikbaar is om de voortgang taken beperken vereist.

## <a name="batch-support-for-low-priority-vms"></a>Batch-ondersteuning voor VM met lage prioriteit

Azure Batch biedt verschillende mogelijkheden die gemakkelijk te gebruiken en profiteren van virtuele machines prioriteit Laag:

-   Batch-pools kunnen zowel toegewezen virtuele machines en virtuele machines prioriteit Laag bevatten. Het aantal van elk type van de virtuele machine kan worden opgegeven wanneer een groep wordt gemaakt of gewijzigd op elk gewenst moment voor een bestaande pool met de bewerking formaat expliciete of automatisch schalen. Verzending van de taak en kunt blijven ongewijzigd en hoeft niet te worden betrokken zijn bij de VM-typen in de groep. Het is ook mogelijk om een pool volledig met lage prioriteit virtuele machines worden taken goedkoop als mogelijk, maar spin up toegewezen virtuele machines worden uitgevoerd als de capaciteit onder een drempel zakt, zodat taken worden uitgevoerd.

-   Batch-pools zoeken automatisch naar het is het doelaantal van prioriteit Laag VM's. Als VMs zijn gereserveerd, probeer Batch te vervangen door de verloren capaciteit en terug te keren naar het doel.

-   In het geval van taken wordt onderbroken, Batch detecteert en automatisch requeue taken opnieuw te worden uitgevoerd.

-   Prioriteit Laag VM's hebben een quotum voor kernen die van de toegewezen virtuele machines verschilt. 
    Het aanhalingsteken voor virtuele machines prioriteit laag is hoger dan die van de toegewezen virtuele machines, omdat minder VM met lage prioriteit kosten. Zie [Batch-servicequota en limieten](batch-quota-limit.md#resource-quotas) voor meer informatie.    

> [!NOTE]
> Prioriteit Laag virtuele machines worden momenteel niet ondersteund voor Batch-accounts waarvan de modus van de toewijzing van toepassingen is ingesteld op [gebruikerabonnement](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Maken en bijwerken van groepen

Een Batch-pool kan toegewezen en prioriteit Laag virtuele machines (ook wel rekenknooppunten) bevatten. U kunt het nummer van het doel van rekenknooppunten instellen voor virtuele machines toegewezen en lage prioriteit. Het doelaantal knooppunten geeft het aantal virtuele machines die u hebt in de groep wilt maken.

Bijvoorbeeld: voor het maken van een groep met behulp van de cloudservice van Azure VM's met een doel van 5 toegewezen virtuele machines en 20 prioriteit Laag VM's:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

Met behulp van Azure virtuele machines (in dit geval virtuele Linux-machines) met een doel van 5 toegewezen voor het maken van een groep VM's en 20 prioriteit Laag VM's:

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

U kunt het huidige aantal knooppunten voor virtuele machines toegewezen en lage prioriteit krijgen:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Groep knooppunten hebben een eigenschap om aan te geven als het knooppunt een virtuele machine toegewezen of lage prioriteit:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Als een of meer knooppunten in een pool zijn gereserveerd, een lijst met knooppunten-bewerking op de groep wordt nog steeds geretourneerd die knooppunten, het huidige aantal knooppunten prioriteit Laag ongewijzigd blijft, maar die knooppunten de status ingesteld heeft op de **vervallen** status. Batch wordt gezocht naar vervanging virtuele machines en, als dit lukt, de knooppunten doorlopen **maken** en vervolgens **starten** statussen voordat deze beschikbaar voor uitvoering van de taak, net als bij nieuwe knooppunten.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Een groep met lage prioriteit VMs schalen

Net als bij de opslaggroepen die uitsluitend bestaan uit toegewezen virtuele machines, is het mogelijk om te schalen van een groep met lage prioriteit virtuele machines met het aanroepen van de methode formaat of automatisch schalen.

De bewerking van het formaat van toepassingen wordt een tweede optionele parameter waarmee de waarde van bijgewerkt **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

De formule van de groep automatisch schalen ondersteunt prioriteit Laag virtuele machines als volgt:

-   U kunt opvragen of stel de waarde van de service gedefinieerde variabele **$TargetLowPriorityNodes**.

-   U kunt de waarde van de service gedefinieerde variabele opvragen **$CurrentLowPriorityNodes**.

-   U kunt de waarde van de service gedefinieerde variabele opvragen **$PreemptedNodeCount**. 
    Deze variabele retourneert het aantal knooppunten in de status van de preempted en kunt u schalen omhoog of omlaag het aantal toegewezen knooppunten, afhankelijk van het aantal afgebroken knooppunten die niet beschikbaar zijn.

## <a name="jobs-and-tasks"></a>Jobs en taken

Jobs en taken vereist weinig ondersteuning voor knooppunten met lage prioriteit. de enige ondersteuning is als volgt:

-   De eigenschap JobManagerTask van een taak heeft een nieuwe eigenschap **AllowLowPriorityNode**. 
    Wanneer deze eigenschap true is, kan de jobbeheertaak worden gepland op een knooppunt toegewezen of lage prioriteit. Als deze eigenschap ingesteld op false is, wordt de jobbeheertaak naar specifieke knooppunt worden gepland.

-   Een [omgevingsvariabele](batch-compute-node-environment-variables.md) is beschikbaar voor een taaktoepassing zodat deze bepalen kan of deze wordt uitgevoerd op een knooppunt met lage prioriteit of toegewezen. De omgevingsvariabele is AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Afhandeling van voorrang

Virtuele machines kunnen van tijd tot tijd worden gebruikt; Als dit gebeurt, is Batch doet het volgende:

-   De preempted virtuele machines hebben hun status bijgewerkt naar **vervallen**.
-   Als taken zijn uitgevoerd op de virtuele machines van knooppunt afgebroken, zijn deze taken de opnieuw en voer opnieuw.
-   De virtuele machine wordt effectief verwijderd, wat leidt tot alle gegevens die lokaal zijn opgeslagen op de virtuele machine verloren.
-   De pool wordt voortdurend probeert te bereiken van het doelaantal knooppunten van prioriteit Laag beschikbaar. Als u vervangingscapaciteit wordt gevonden, de knooppunten behouden hun id, maar zijn opnieuw geïnitialiseerd, gaan via **maken** en **starten** aangegeven voordat ze beschikbaar voor het plannen van taken zijn.
-   Voorrang aantallen zijn beschikbaar als een waarde in de Azure portal.

## <a name="metrics"></a>Metrische gegevens

Nieuwe metrische gegevens zijn beschikbaar in de [Azure-portal](https://portal.azure.com) voor knooppunten met lage prioriteit. Deze metrische gegevens zijn:

- Aantal knooppunten met lage prioriteit
- Aantal kernen met lage prioriteit 
- Aantal knooppunten afgebroken

Metrische gegevens weergeven in de Azure portal:

1. Navigeer naar uw Batch-account in de portal en bekijk de instellingen voor uw Batch-account.
2. Selecteer **metrische gegevens** van de **bewaking** sectie.
3. Selecteer de metrische gegevens die u van wenst de **beschikbare metrische gegevens** lijst.

![Metrische gegevens voor knooppunten met lage prioriteit](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Volgende stappen

* Bekijk het [overzicht met Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen die Batch wil gaan gebruiken. Het artikel bevat meer gedetailleerde informatie over de Batch-serviceresources zoals groepen, knooppunten, jobs en taken, en de vele API-functies die u tijdens het maken van de Batch-toepassing kunt gebruiken.
* Meer informatie over de [Batch-API's en -hulpprogramma's](batch-apis-tools.md) die beschikbaar zijn voor het bouwen van Batch-oplossingen.
