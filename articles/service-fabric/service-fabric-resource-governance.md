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
# <a name="resource-governance"></a><span data-ttu-id="542f6-103">Resource governance</span><span class="sxs-lookup"><span data-stu-id="542f6-103">Resource governance</span></span> 

<span data-ttu-id="542f6-104">Wanneer u meerdere services waarop hello hetzelfde knooppunt of cluster, is het mogelijk dat één service kan worden gebruikt voor het gebruik van meer bronnen andere services voldoende bronnen kunnen beschikken.</span><span class="sxs-lookup"><span data-stu-id="542f6-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="542f6-105">Dit probleem is waarnaar wordt verwezen tooas Hallo ruis neighbor probleem.</span><span class="sxs-lookup"><span data-stu-id="542f6-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="542f6-106">Service Fabric kunt Hallo developer toospecify reserveringen en limieten per service tooguarantee bronnen en ook het Resourcegebruik te beperken.</span><span class="sxs-lookup"><span data-stu-id="542f6-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="542f6-107">Metrische gegevens voor het beheer van resources</span><span class="sxs-lookup"><span data-stu-id="542f6-107">Resource governance metrics</span></span> 

<span data-ttu-id="542f6-108">Resource governance wordt ondersteund in Service Fabric per [servicepakket](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="542f6-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="542f6-109">Hallo-resources die zijn toegewezen tooService pakket kunnen verder worden onderverdeeld tussen code pakketten.</span><span class="sxs-lookup"><span data-stu-id="542f6-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="542f6-110">limieten voor Hallo opgegeven ook betekenen Hallo reservering van Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="542f6-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="542f6-111">Service Fabric ondersteunt het opgeven van CPU en geheugen per pakket van de service, met behulp van twee ingebouwde [metrische gegevens](service-fabric-cluster-resource-manager-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="542f6-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="542f6-112">CPU (metrische naam `ServiceFabric:/_CpuCores`): een kern is een logische core die beschikbaar is op de hostmachine Hallo en alle kernen op alle knooppunten worden gewogen Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="542f6-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="542f6-113">Geheugen (metrische naam `ServiceFabric:/_MemoryInMB`): geheugen wordt uitgedrukt in megabytes en toophysical geheugen dat beschikbaar is op Hallo machine wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="542f6-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="542f6-114">Alleen zijn zachte reserveringsgaranties opgegeven - Hallo runtime verwerpt het openen van de nieuwe service pakketten beschikbare resources zijn overschreden.</span><span class="sxs-lookup"><span data-stu-id="542f6-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="542f6-115">Als een ander uitvoerbaar bestand of de container op Hallo-knooppunt wordt geplaatst, kan die de oorspronkelijke reserveringsgaranties Hallo overtreden.</span><span class="sxs-lookup"><span data-stu-id="542f6-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="542f6-116">Voor deze twee metrieken Hallo [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) totale cluster capaciteit Hallo load op elk knooppunt in het cluster hello, houdt en resterende bronnen in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="542f6-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="542f6-117">Deze twee metrische gegevens gelijkwaardige tooany zijn andere gebruikers- of aangepaste metrische gegevens en alle bestaande functies die ermee kunnen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="542f6-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="542f6-118">Cluster kan worden [met gelijke taakverdeling](service-fabric-cluster-resource-manager-balancing.md) op basis van twee toothese metrische gegevens (standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="542f6-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="542f6-119">Cluster kan worden [gedefragmenteerd](service-fabric-cluster-resource-manager-defragmentation-metrics.md) op basis van twee toothese metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="542f6-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="542f6-120">Wanneer [met een beschrijving van een cluster](service-fabric-cluster-resource-manager-cluster-description.md), gebufferde capaciteit kan worden ingesteld voor deze twee metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="542f6-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="542f6-121">[Rapportage van de dynamische belasting bij](service-fabric-cluster-resource-manager-metrics.md) wordt niet ondersteund voor deze metrische gegevens en worden voor deze metrische gegevens zijn gedefinieerd tijdens het maken worden geladen.</span><span class="sxs-lookup"><span data-stu-id="542f6-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="542f6-122">Set-cluster voor resource governance inschakelen</span><span class="sxs-lookup"><span data-stu-id="542f6-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="542f6-123">Capaciteit moet worden gedefinieerd handmatig in elk knooppunttype in Hallo cluster als volgt:</span><span class="sxs-lookup"><span data-stu-id="542f6-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="542f6-124">Resource governance mag alleen op gebruiker services en niet op alle systeemservices.</span><span class="sxs-lookup"><span data-stu-id="542f6-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="542f6-125">Bij het opgeven van capaciteit, een aantal kernen en het geheugen moet worden links niet-toegewezen van systeemservices.</span><span class="sxs-lookup"><span data-stu-id="542f6-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="542f6-126">Voor optimale prestaties moet Hallo instelling na ook worden ingeschakeld in het clustermanifest Hallo:</span><span class="sxs-lookup"><span data-stu-id="542f6-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="542f6-127">Resource governance opgeven</span><span class="sxs-lookup"><span data-stu-id="542f6-127">Specifying resource governance</span></span> 

<span data-ttu-id="542f6-128">Resource governance limieten zijn opgegeven in het toepassingsmanifest hello (ServiceManifestImport sectie) zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="542f6-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

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
  
<span data-ttu-id="542f6-129">In dit voorbeeld servicepakket ServicePackageA één kern opgehaald op Hallo knooppunten waar het wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="542f6-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="542f6-130">Dit servicepakket bevat twee code-pakketten (CodeA1 en CodeA2) en beide Hallo Geef `CpuShares` parameter.</span><span class="sxs-lookup"><span data-stu-id="542f6-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="542f6-131">Hallo-gedeelte van de CpuShares 512:256 verdeelt Hallo core over Hallo twee code pakketten.</span><span class="sxs-lookup"><span data-stu-id="542f6-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="542f6-132">In dit voorbeeld CodeA1 twee derde van een kern opgehaald en CodeA2 een derde van een kern opgehaald (en dus een reservering soft-garantie van dezelfde Hallo).</span><span class="sxs-lookup"><span data-stu-id="542f6-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="542f6-133">Voor het geval wanneer CpuShares niet voor code-pakketten opgegeven zijn, Service Fabric Hallo kernen evenveel ertussen verdeelt.</span><span class="sxs-lookup"><span data-stu-id="542f6-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="542f6-134">Geheugenlimieten zijn absolute, zodat beide code-pakketten beperkt too1024 zijn MB aan geheugen (en een voorlopig garantie reservering van dezelfde Hallo).</span><span class="sxs-lookup"><span data-stu-id="542f6-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="542f6-135">Code-pakketten (containers of processen) zijn niet kunnen tooallocate meer geheugen dan deze limiet en probeert toodo dus in een out-geheugen-uitzondering resulteert.</span><span class="sxs-lookup"><span data-stu-id="542f6-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="542f6-136">Voor de resource limiet afdwinging toowork hebben alle code pakketten binnen een servicepakket geheugenlimieten opgegeven.</span><span class="sxs-lookup"><span data-stu-id="542f6-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="542f6-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="542f6-137">Next steps</span></span>
* <span data-ttu-id="542f6-138">toolearn meer over Cluster Resource Manager worden gelezen dit [artikel](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="542f6-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="542f6-139">toolearn meer informatie over toepassingsmodel, servicepakketten, code pakketten en hoe de toothem voor het toewijzen van replica's Lees dit [artikel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="542f6-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
