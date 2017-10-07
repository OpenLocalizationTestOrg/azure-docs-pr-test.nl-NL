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
# <a name="service-movement-cost"></a>Service verplaatsingskosten
Een factor die Service Fabric-Cluster Resource Manager Hallo overweegt wanneer u probeert toodetermine welke wijzigingen toomake tooa cluster is Hallo kosten van deze wijzigingen. Hallo begrip 'kosten' is uitgeschakeld verhandeld tegen hoeveel Hallo-cluster kan worden verbeterd. Kosten zijn meeberekend bij het verplaatsen van services voor taakverdeling, defragmentatie en andere vereisten. Hallo-doel is toomeet Hallo vereisten op Hallo minimaal verstoren of dure manier. 

Services kosten CPU-tijd verplaatst, en ten minste de netwerkbandbreedte. Voor stateful services vereist het Hallo-status van deze services, verbruikt meer geheugen en schijfruimte te kopiëren. Hallo kosten van oplossingen die hello Azure Service Fabric-Cluster Resource Manager wanneer voordoet minimaliseren, zorgt ervoor dat Hallo clusterbronnen onnodig worden niet gebruikt. Wilt u echter ook geen tooignore-oplossingen die zou Hallo toewijzing van bronnen in de cluster Hallo aanzienlijk verbeteren.

Hallo Cluster Resource Manager heeft twee manieren om de kosten computing en ze beperken terwijl wordt geprobeerd toomanage Hallo-cluster. Hallo eerste mechanisme met elke verplaatsing die zou gewoon tellen. Als twee oplossingen zijn gegenereerd met over Hallo saldo dezelfde (score), en vervolgens Hallo Cluster Resource Manager Hallo een voorkeur Hello laagste kosten (totaal aantal verplaatst).

Deze strategie werkt goed. Maar met standaard of statische belasting is het onwaarschijnlijk dat in een complex systeem dat alle verplaatst gelijk zijn. Sommige zijn waarschijnlijk toobe veel duurder.

## <a name="setting-move-costs"></a>Kosten voor instelling verplaatsen 
Hallo standaard verplaatsen kosten voor een service kunt u opgeven wanneer deze wordt gemaakt:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

U kunt ook opgeven of MoveCost dynamisch bijwerken voor een service nadat Hallo-service is gemaakt: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Dynamisch geven verplaatsen kosten op basis van de per-replica

Hallo voorgaande codefragmenten zijn alle voor het MoveCost opgeven voor een hele service tegelijk van externe Hallo-service zelf. Echter verplaatsen kosten is vooral handig is wanneer Hallo verplaatsen kosten van een specifieke service-object verandert gedurende de levensduur. Aangezien Hallo waarschijnlijk zelf services Hallo best idee hoe kostbaar toomove een bepaald moment zijn hebt, er is een API voor services tooreport kosten verbonden aan hun eigen afzonderlijke verplaatsen tijdens runtime. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Gevolgen van het verplaatsen kosten
MoveCost heeft vier niveaus: nul, laag, gemiddeld en hoog. MoveCosts zijn relatieve tooeach andere, met uitzondering van nul. Nul kosten verplaatsen betekent dat verkeer gratis is en mag niet in mindering gebracht op Hallo score van Hallo-oplossing. Instelling uw kosten tooHigh verplaatsen biedt *niet* waarborgen dat replica Hallo blijft van toepassing op één plek.

<center>
![Kosten verplaatsen als een factor bij het selecteren van replica's voor gegevensverplaatsing][Image1]
</center>

MoveCost kunt u vinden Hallo oplossingen oorzaak minimaal onderbreking van de algemene Hallo en de eenvoudigste tooachieve terwijl u nog steeds dat binnenkomt bij gelijkwaardige saldo zijn. Een service begrip van kosten kan relatieve toomany dingen zijn. Hallo meest voorkomende factoren bij het berekenen van de kosten van de verplaatsing is zijn:

- Hallo hoeveelheid status of gegevens die service Hallo heeft toomove.
- Hallo kosten van het verbreken van de verbinding van clients. Verplaatsen van een primaire replica is meestal duurder dan Hallo kosten van het verplaatsen van een secundaire replica.
- Hallo-kosten van een onderweg bewerking te onderbreken. Bepaalde bewerkingen op Hallo gegevens opslaan niveau of bewerkingen die worden uitgevoerd in de aanroep van de client tooa antwoord kostbaar zijn. Na een bepaald moment u niet wilt dat toostop indien u niet hoeft te. Tijdens Hallo bewerking, verhoogt u dus Hallo verplaatsen kosten van deze service object tooreduce Hallo kans dat het wordt verplaatst. Als het Hallo-bewerking is voltooid, kunt u Hallo kosten back toonormal instellen.

## <a name="enabling-move-cost-in-your-cluster"></a>Inschakelen van kosten in uw cluster verplaatsen
Om meer gedetailleerd MoveCosts toobe rekening gehouden met Hallo, MoveCost moet zijn ingeschakeld in uw cluster. Zonder deze instelling wordt Hallo standaardmodus tellen verplaatsen wordt gebruikt voor het berekenen van MoveCost en MoveCost rapporten worden genegeerd.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

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

## <a name="next-steps"></a>Volgende stappen
- Service Fabric-Cluster Resource Manager maakt gebruik van metrische gegevens toomanage gebruiks- en capaciteit Hallo-cluster. meer informatie over metrische gegevens toolearn en hoe tooconfigure, Bekijk [brongebruik beheren en de belasting in Service Fabric met metrische gegevens](service-fabric-cluster-resource-manager-metrics.md).
- toolearn over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, Bekijk [Balancing Service Fabric-cluster](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
