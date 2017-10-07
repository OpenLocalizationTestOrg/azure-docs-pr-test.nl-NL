---
title: 'Service Fabric Cluster Resource Manager: gegevensverplaatsing kosten | Microsoft Docs'
description: Overzicht van verplaatsingskosten voor Service Fabric-services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="ddea1-103">Service verplaatsingskosten</span><span class="sxs-lookup"><span data-stu-id="ddea1-103">Service movement cost</span></span>
<span data-ttu-id="ddea1-104">Een factor die Service Fabric-Cluster Resource Manager Hallo overweegt wanneer u probeert toodetermine welke wijzigingen toomake tooa cluster is Hallo kosten van deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="ddea1-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="ddea1-105">Hallo begrip 'kosten' is uitgeschakeld verhandeld tegen hoeveel Hallo-cluster kan worden verbeterd.</span><span class="sxs-lookup"><span data-stu-id="ddea1-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="ddea1-106">Kosten zijn meeberekend bij het verplaatsen van services voor taakverdeling, defragmentatie en andere vereisten.</span><span class="sxs-lookup"><span data-stu-id="ddea1-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="ddea1-107">Hallo-doel is toomeet Hallo vereisten op Hallo minimaal verstoren of dure manier.</span><span class="sxs-lookup"><span data-stu-id="ddea1-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="ddea1-108">Services kosten CPU-tijd verplaatst, en ten minste de netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="ddea1-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="ddea1-109">Voor stateful services vereist het Hallo-status van deze services, verbruikt meer geheugen en schijfruimte te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ddea1-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="ddea1-110">Hallo kosten van oplossingen die hello Azure Service Fabric-Cluster Resource Manager wanneer voordoet minimaliseren, zorgt ervoor dat Hallo clusterbronnen onnodig worden niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ddea1-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="ddea1-111">Wilt u echter ook geen tooignore-oplossingen die zou Hallo toewijzing van bronnen in de cluster Hallo aanzienlijk verbeteren.</span><span class="sxs-lookup"><span data-stu-id="ddea1-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="ddea1-112">Hallo Cluster Resource Manager heeft twee manieren om de kosten computing en ze beperken terwijl wordt geprobeerd toomanage Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ddea1-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="ddea1-113">Hallo eerste mechanisme met elke verplaatsing die zou gewoon tellen.</span><span class="sxs-lookup"><span data-stu-id="ddea1-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="ddea1-114">Als twee oplossingen zijn gegenereerd met over Hallo saldo dezelfde (score), en vervolgens Hallo Cluster Resource Manager Hallo een voorkeur Hello laagste kosten (totaal aantal verplaatst).</span><span class="sxs-lookup"><span data-stu-id="ddea1-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="ddea1-115">Deze strategie werkt goed.</span><span class="sxs-lookup"><span data-stu-id="ddea1-115">This strategy works well.</span></span> <span data-ttu-id="ddea1-116">Maar met standaard of statische belasting is het onwaarschijnlijk dat in een complex systeem dat alle verplaatst gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="ddea1-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="ddea1-117">Sommige zijn waarschijnlijk toobe veel duurder.</span><span class="sxs-lookup"><span data-stu-id="ddea1-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="ddea1-118">Kosten voor instelling verplaatsen</span><span class="sxs-lookup"><span data-stu-id="ddea1-118">Setting Move Costs</span></span> 
<span data-ttu-id="ddea1-119">Hallo standaard verplaatsen kosten voor een service kunt u opgeven wanneer deze wordt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="ddea1-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="ddea1-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ddea1-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="ddea1-121">C#:</span><span class="sxs-lookup"><span data-stu-id="ddea1-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="ddea1-122">U kunt ook opgeven of MoveCost dynamisch bijwerken voor een service nadat Hallo-service is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="ddea1-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="ddea1-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ddea1-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="ddea1-124">C#:</span><span class="sxs-lookup"><span data-stu-id="ddea1-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="ddea1-125">Dynamisch geven verplaatsen kosten op basis van de per-replica</span><span class="sxs-lookup"><span data-stu-id="ddea1-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="ddea1-126">Hallo voorgaande codefragmenten zijn alle voor het MoveCost opgeven voor een hele service tegelijk van externe Hallo-service zelf.</span><span class="sxs-lookup"><span data-stu-id="ddea1-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="ddea1-127">Echter verplaatsen kosten is vooral handig is wanneer Hallo verplaatsen kosten van een specifieke service-object verandert gedurende de levensduur.</span><span class="sxs-lookup"><span data-stu-id="ddea1-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="ddea1-128">Aangezien Hallo waarschijnlijk zelf services Hallo best idee hoe kostbaar toomove een bepaald moment zijn hebt, er is een API voor services tooreport kosten verbonden aan hun eigen afzonderlijke verplaatsen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ddea1-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="ddea1-129">C#:</span><span class="sxs-lookup"><span data-stu-id="ddea1-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="ddea1-130">Gevolgen van het verplaatsen kosten</span><span class="sxs-lookup"><span data-stu-id="ddea1-130">Impact of move cost</span></span>
<span data-ttu-id="ddea1-131">MoveCost heeft vier niveaus: nul, laag, gemiddeld en hoog.</span><span class="sxs-lookup"><span data-stu-id="ddea1-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="ddea1-132">MoveCosts zijn relatieve tooeach andere, met uitzondering van nul.</span><span class="sxs-lookup"><span data-stu-id="ddea1-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="ddea1-133">Nul kosten verplaatsen betekent dat verkeer gratis is en mag niet in mindering gebracht op Hallo score van Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="ddea1-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="ddea1-134">Instelling uw kosten tooHigh verplaatsen biedt *niet* waarborgen dat replica Hallo blijft van toepassing op één plek.</span><span class="sxs-lookup"><span data-stu-id="ddea1-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="ddea1-135"><center>
![Kosten verplaatsen als een factor bij het selecteren van replica's voor gegevensverplaatsing][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="ddea1-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="ddea1-136">MoveCost kunt u vinden Hallo oplossingen oorzaak minimaal onderbreking van de algemene Hallo en de eenvoudigste tooachieve terwijl u nog steeds dat binnenkomt bij gelijkwaardige saldo zijn.</span><span class="sxs-lookup"><span data-stu-id="ddea1-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="ddea1-137">Een service begrip van kosten kan relatieve toomany dingen zijn.</span><span class="sxs-lookup"><span data-stu-id="ddea1-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="ddea1-138">Hallo meest voorkomende factoren bij het berekenen van de kosten van de verplaatsing is zijn:</span><span class="sxs-lookup"><span data-stu-id="ddea1-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="ddea1-139">Hallo hoeveelheid status of gegevens die service Hallo heeft toomove.</span><span class="sxs-lookup"><span data-stu-id="ddea1-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="ddea1-140">Hallo kosten van het verbreken van de verbinding van clients.</span><span class="sxs-lookup"><span data-stu-id="ddea1-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="ddea1-141">Verplaatsen van een primaire replica is meestal duurder dan Hallo kosten van het verplaatsen van een secundaire replica.</span><span class="sxs-lookup"><span data-stu-id="ddea1-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="ddea1-142">Hallo-kosten van een onderweg bewerking te onderbreken.</span><span class="sxs-lookup"><span data-stu-id="ddea1-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="ddea1-143">Bepaalde bewerkingen op Hallo gegevens opslaan niveau of bewerkingen die worden uitgevoerd in de aanroep van de client tooa antwoord kostbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="ddea1-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="ddea1-144">Na een bepaald moment u niet wilt dat toostop indien u niet hoeft te.</span><span class="sxs-lookup"><span data-stu-id="ddea1-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="ddea1-145">Tijdens Hallo bewerking, verhoogt u dus Hallo verplaatsen kosten van deze service object tooreduce Hallo kans dat het wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="ddea1-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="ddea1-146">Als het Hallo-bewerking is voltooid, kunt u Hallo kosten back toonormal instellen.</span><span class="sxs-lookup"><span data-stu-id="ddea1-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="ddea1-147">Inschakelen van kosten in uw cluster verplaatsen</span><span class="sxs-lookup"><span data-stu-id="ddea1-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="ddea1-148">Om meer gedetailleerd MoveCosts toobe rekening gehouden met Hallo, MoveCost moet zijn ingeschakeld in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ddea1-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="ddea1-149">Zonder deze instelling wordt Hallo standaardmodus tellen verplaatsen wordt gebruikt voor het berekenen van MoveCost en MoveCost rapporten worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="ddea1-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="ddea1-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ddea1-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="ddea1-151">gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:</span><span class="sxs-lookup"><span data-stu-id="ddea1-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="ddea1-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ddea1-152">Next steps</span></span>
- <span data-ttu-id="ddea1-153">Service Fabric-Cluster Resource Manager maakt gebruik van metrische gegevens toomanage gebruiks- en capaciteit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ddea1-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="ddea1-154">meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [brongebruik beheren en de belasting in Service Fabric met metrische gegevens](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ddea1-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="ddea1-155">toolearn over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, Bekijk [Balancing Service Fabric-cluster](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="ddea1-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
