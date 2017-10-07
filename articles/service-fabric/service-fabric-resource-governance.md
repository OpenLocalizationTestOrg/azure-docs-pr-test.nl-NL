---
title: aaaAzure Service Fabric Resource Governance voor Containers en -Services | Microsoft Docs
description: Azure Service Fabric kunt u limieten voor toospecify voor services die worden uitgevoerd binnen of buiten containers.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>Resource governance 

Wanneer u meerdere services waarop hello hetzelfde knooppunt of cluster, is het mogelijk dat één service kan worden gebruikt voor het gebruik van meer bronnen andere services voldoende bronnen kunnen beschikken. Dit probleem is waarnaar wordt verwezen tooas Hallo ruis neighbor probleem. Service Fabric kunt Hallo developer toospecify reserveringen en limieten per service tooguarantee bronnen en ook het Resourcegebruik te beperken. 

## <a name="resource-governance-metrics"></a>Metrische gegevens voor het beheer van resources 

Resource governance wordt ondersteund in Service Fabric per [servicepakket](service-fabric-application-model.md). Hallo-resources die zijn toegewezen tooService pakket kunnen verder worden onderverdeeld tussen code pakketten. limieten voor Hallo opgegeven ook betekenen Hallo reservering van Hallo resources. Service Fabric ondersteunt het opgeven van CPU en geheugen per pakket van de service, met behulp van twee ingebouwde [metrische gegevens](service-fabric-cluster-resource-manager-metrics.md):

* CPU (metrische naam `ServiceFabric:/_CpuCores`): een kern is een logische core die beschikbaar is op de hostmachine Hallo en alle kernen op alle knooppunten worden gewogen Hallo dezelfde.
* Geheugen (metrische naam `ServiceFabric:/_MemoryInMB`): geheugen wordt uitgedrukt in megabytes en toophysical geheugen dat beschikbaar is op Hallo machine wordt toegewezen.

Alleen zijn zachte reserveringsgaranties opgegeven - Hallo runtime verwerpt het openen van de nieuwe service pakketten beschikbare resources zijn overschreden. Als een ander uitvoerbaar bestand of de container op Hallo-knooppunt wordt geplaatst, kan die de oorspronkelijke reserveringsgaranties Hallo overtreden.

Voor deze twee metrieken Hallo [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) totale cluster capaciteit Hallo load op elk knooppunt in het cluster hello, houdt en resterende bronnen in Hallo-cluster. Deze twee metrische gegevens gelijkwaardige tooany zijn andere gebruikers- of aangepaste metrische gegevens en alle bestaande functies die ermee kunnen worden gebruikt:
* Cluster kan worden [met gelijke taakverdeling](service-fabric-cluster-resource-manager-balancing.md) op basis van twee toothese metrische gegevens (standaardinstelling).
* Cluster kan worden [gedefragmenteerd](service-fabric-cluster-resource-manager-defragmentation-metrics.md) op basis van twee toothese metrische gegevens.
* Wanneer [met een beschrijving van een cluster](service-fabric-cluster-resource-manager-cluster-description.md), gebufferde capaciteit kan worden ingesteld voor deze twee metrische gegevens.

[Rapportage van de dynamische belasting bij](service-fabric-cluster-resource-manager-metrics.md) wordt niet ondersteund voor deze metrische gegevens en worden voor deze metrische gegevens zijn gedefinieerd tijdens het maken worden geladen.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Set-cluster voor resource governance inschakelen

Capaciteit moet worden gedefinieerd handmatig in elk knooppunttype in Hallo cluster als volgt:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Resource governance mag alleen op gebruiker services en niet op alle systeemservices. Bij het opgeven van capaciteit, een aantal kernen en het geheugen moet worden links niet-toegewezen van systeemservices. Voor optimale prestaties moet Hallo instelling na ook worden ingeschakeld in het clustermanifest Hallo: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Resource governance opgeven 

Resource governance limieten zijn opgegeven in het toepassingsmanifest hello (ServiceManifestImport sectie) zoals weergegeven in het volgende voorbeeld Hallo:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
In dit voorbeeld servicepakket ServicePackageA één kern opgehaald op Hallo knooppunten waar het wordt geplaatst. Dit servicepakket bevat twee code-pakketten (CodeA1 en CodeA2) en beide Hallo Geef `CpuShares` parameter. Hallo-gedeelte van de CpuShares 512:256 verdeelt Hallo core over Hallo twee code pakketten. In dit voorbeeld CodeA1 twee derde van een kern opgehaald en CodeA2 een derde van een kern opgehaald (en dus een reservering soft-garantie van dezelfde Hallo). Voor het geval wanneer CpuShares niet voor code-pakketten opgegeven zijn, Service Fabric Hallo kernen evenveel ertussen verdeelt.

Geheugenlimieten zijn absolute, zodat beide code-pakketten beperkt too1024 zijn MB aan geheugen (en een voorlopig garantie reservering van dezelfde Hallo). Code-pakketten (containers of processen) zijn niet kunnen tooallocate meer geheugen dan deze limiet en probeert toodo dus in een out-geheugen-uitzondering resulteert. Voor de resource limiet afdwinging toowork hebben alle code pakketten binnen een servicepakket geheugenlimieten opgegeven.


## <a name="next-steps"></a>Volgende stappen
* toolearn meer over Cluster Resource Manager worden gelezen dit [artikel](service-fabric-cluster-resource-manager-introduction.md).
* toolearn meer informatie over toepassingsmodel, servicepakketten, code pakketten en hoe de toothem voor het toewijzen van replica's Lees dit [artikel](service-fabric-application-model.md).
