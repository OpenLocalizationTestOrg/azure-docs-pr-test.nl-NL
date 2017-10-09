---
title: aaaService Fabric Cluster Resource Manager - toepassingsgroepen | Microsoft Docs
description: Overzicht van Hallo functionaliteit van de groep toepassingen in Hallo Service Fabric-Cluster Resource Manager
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="aca95-103">Inleiding tooApplication groepen</span><span class="sxs-lookup"><span data-stu-id="aca95-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="aca95-104">Service-Fabric Cluster Resource Manager beheert doorgaans clusterbronnen door te spreiden Hallo load (vertegenwoordigd [metrische gegevens](service-fabric-cluster-resource-manager-metrics.md)) gelijkmatig in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aca95-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="aca95-105">Service Fabric beheert Hallo capaciteit van Hallo knooppunten in het Hallo en Hallo cluster als geheel via [capaciteit](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="aca95-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="aca95-106">Metrische gegevens en capaciteit werken geweldig voor veel werkbelastingen, maar de patronen die maken intensief gebruik van verschillende exemplaren van Service Fabric-toepassing soms Breng in aanvullende vereisten.</span><span class="sxs-lookup"><span data-stu-id="aca95-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="aca95-107">U kunt bijvoorbeeld naar:</span><span class="sxs-lookup"><span data-stu-id="aca95-107">For example you may want to:</span></span>

- <span data-ttu-id="aca95-108">Sommige capaciteit op Hallo knooppunten in cluster Hallo voor Hallo services binnen een exemplaar van de benoemde reserveren</span><span class="sxs-lookup"><span data-stu-id="aca95-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="aca95-109">Totale aantal knooppunten dat Hallo services binnen een benoemd exemplaar op worden uitgevoerd (in plaats van ze uit te spreiden over het hele cluster Hallo) Hallo beperken</span><span class="sxs-lookup"><span data-stu-id="aca95-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="aca95-110">Capaciteit op Hallo benoemde toepassingsexemplaar zelf toolimit Hallo aantal services of totaal resourceverbruik van Hallo services erin definiëren</span><span class="sxs-lookup"><span data-stu-id="aca95-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="aca95-111">toomeet deze vereisten, Hallo Service Fabric-Cluster Resource Manager ondersteunt de functie toepassingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="aca95-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="aca95-112">Maximum aantal knooppunten Hallo beperken</span><span class="sxs-lookup"><span data-stu-id="aca95-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="aca95-113">Hallo eenvoudigste gebruiksvoorbeeld capaciteit van de toepassing is wanneer een toepassingsexemplaar moet toobe beperkt tooa bepaalde maximum aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aca95-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="aca95-114">Dit consolideert alle services in dat toepassingsexemplaar naar een bepaald aantal machines.</span><span class="sxs-lookup"><span data-stu-id="aca95-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="aca95-115">Consolidatie is nuttig wanneer u toopredict probeert of fysieke resource gebruik cap door Hallo services binnen die benoemde exemplaar.</span><span class="sxs-lookup"><span data-stu-id="aca95-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="aca95-116">Hallo volgende afbeelding ziet u de instantie van een toepassing met en zonder een maximum aantal knooppunten gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="aca95-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="aca95-117"><center>
![Toepassingsexemplaar Maximum aantal knooppunten definiëren][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="aca95-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="aca95-118">In Hallo links bijvoorbeeld Hallo toepassing geen een maximum aantal knooppunten dat is gedefinieerd en hieraan de drie services.</span><span class="sxs-lookup"><span data-stu-id="aca95-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="aca95-119">Hallo Cluster Resource Manager heeft alle replica's over verspreid zes beschikbare knooppunten tooachieve Hallo beste balans in Hallo-cluster (Hallo standaardgedrag).</span><span class="sxs-lookup"><span data-stu-id="aca95-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="aca95-120">In de juiste Hallo voorbeeld zien we Hallo dezelfde toepassing beperkt toothree knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aca95-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="aca95-121">Hallo-parameter die dit gedrag bepaalt wordt MaximumNodes genoemd.</span><span class="sxs-lookup"><span data-stu-id="aca95-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="aca95-122">Deze parameter worden ingesteld tijdens het maken van de toepassing of bijgewerkt in verband met de instantie van een toepassing die al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aca95-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="aca95-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aca95-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="aca95-124">C#</span><span class="sxs-lookup"><span data-stu-id="aca95-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="aca95-125">Geen binnen Hallo set knooppunten garantie Hallo Cluster Resource Manager welke serviceobjecten samen worden geplaatst of welke knooppunten ophalen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aca95-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="aca95-126">Metrische gegevens van toepassing, laden en capaciteit</span><span class="sxs-lookup"><span data-stu-id="aca95-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="aca95-127">Toepassingsgroepen kunnen u ook toodefine metrische gegevens die zijn gekoppeld aan een bepaalde toepassing van de benoemde exemplaar, en die van het toepassingsexemplaar capaciteit voor deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="aca95-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="aca95-128">Toepassing metrische gegevens kunt u tootrack, reserveren en limiet Hallo resourceverbruik van Hallo services binnen dat toepassingsexemplaar.</span><span class="sxs-lookup"><span data-stu-id="aca95-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="aca95-129">Er zijn twee waarden kunnen worden ingesteld voor elke metriek toepassing:</span><span class="sxs-lookup"><span data-stu-id="aca95-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="aca95-130">**Totale capaciteit van de toepassing** – deze instelling geeft Hallo totale capaciteit van de Hallo-toepassing voor een bepaalde waarde.</span><span class="sxs-lookup"><span data-stu-id="aca95-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="aca95-131">Hallo Cluster Resource Manager Hallo maken van de nieuwe services binnen deze toepassingsexemplaar die totale belasting tooexceed deze waarde veroorzaken is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="aca95-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="aca95-132">Stel dat bijvoorbeeld Hallo toepassingsexemplaar had een capaciteit van 10 en laden van vijf al had.</span><span class="sxs-lookup"><span data-stu-id="aca95-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="aca95-133">Hallo maken van een service met een totale standaard belasting van 10 zou niet worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="aca95-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="aca95-134">**Maximale capaciteit van het knooppunt** – deze instelling bepaalt u Hallo maximale totale belasting voor de toepassing hello op één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="aca95-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="aca95-135">Als de belasting toeneemt via deze capaciteit, verplaatst u Hallo Cluster Resource Manager replica's tooother knooppunten zodat hello belasting afneemt.</span><span class="sxs-lookup"><span data-stu-id="aca95-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="aca95-136">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aca95-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="aca95-137">C#:</span><span class="sxs-lookup"><span data-stu-id="aca95-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="aca95-138">Capaciteit reserveren</span><span class="sxs-lookup"><span data-stu-id="aca95-138">Reserving Capacity</span></span>
<span data-ttu-id="aca95-139">Er wordt een andere vaak gebruikt voor toepassingsgroepen tooensure dat resources binnen een cluster Hallo zijn gereserveerd voor het exemplaar van een bepaalde toepassing.</span><span class="sxs-lookup"><span data-stu-id="aca95-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="aca95-140">Hallo-ruimte is altijd gereserveerd wanneer Hallo toepassingsexemplaar wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aca95-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="aca95-141">Ruimte in de cluster Hallo reserveren voor toepassing hello onmiddellijk gebeurt ook wanneer:</span><span class="sxs-lookup"><span data-stu-id="aca95-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="aca95-142">Hallo-toepassingsexemplaar is gemaakt, maar geen binnen deze services nog</span><span class="sxs-lookup"><span data-stu-id="aca95-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="aca95-143">aantal services binnen het toepassingsexemplaar Hallo Hallo verandert telkens wanneer</span><span class="sxs-lookup"><span data-stu-id="aca95-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="aca95-144">Hallo-services bestaat, maar worden niet Hallo resources verbruikt</span><span class="sxs-lookup"><span data-stu-id="aca95-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="aca95-145">Resources worden gereserveerd voor een toepassingsexemplaar vereist twee extra parameters opgeven: *MinimumNodes* en *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="aca95-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="aca95-146">**MinimumNodes** -bepaalt het minimumaantal Hallo van knooppunten die toepassing hello exemplaar mag worden uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="aca95-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="aca95-147">**NodeReservationCapacity** -deze instelling is per metrische gegevens voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="aca95-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="aca95-148">Hallo-waarde is Hallo hoeveelheid die metriek gereserveerd voor de toepassing hello op elk knooppunt waar dat Hallo services in de desbetreffende toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="aca95-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="aca95-149">Combineren **MinimumNodes** en **NodeReservationCapacity** wordt gegarandeerd dat een minimale belasting reservering voor de toepassing hello binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aca95-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="aca95-150">Als er minder resterende capaciteit in Hallo cluster dan de totale reservering Hallo vereist, mislukt het maken van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="aca95-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="aca95-151">Bekijk een voorbeeld van capaciteitsreservering:</span><span class="sxs-lookup"><span data-stu-id="aca95-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="aca95-152"><center>
![Exemplaren van een toepassing gereserveerde capaciteit definiëren][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="aca95-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="aca95-153">In Hallo links bijvoorbeeld hoeft toepassingen niet elke toepassing capaciteit gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="aca95-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="aca95-154">Alles op basis van regels toonormal compromis tussen de Hallo Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aca95-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="aca95-155">Stel de dat Toepassing1 is gemaakt met de Hallo instellingen te volgen in voorbeeld Hallo op Hallo rechts:</span><span class="sxs-lookup"><span data-stu-id="aca95-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="aca95-156">MinimumNodes instellen tootwo</span><span class="sxs-lookup"><span data-stu-id="aca95-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="aca95-157">Een waarde die is gedefinieerd met de van toepassing</span><span class="sxs-lookup"><span data-stu-id="aca95-157">An application Metric defined with</span></span>
  - <span data-ttu-id="aca95-158">NodeReservationCapacity van 20</span><span class="sxs-lookup"><span data-stu-id="aca95-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="aca95-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aca95-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="aca95-160">C#</span><span class="sxs-lookup"><span data-stu-id="aca95-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="aca95-161">Service Fabric reserveert capaciteit op twee knooppunten voor Toepassing1 en niet-services toestaan van Toepassing2 tooconsume die capaciteit zelfs als er dat geen load wordt verbruikt door Hallo services binnen Toepassing1 Hallo tegelijk.</span><span class="sxs-lookup"><span data-stu-id="aca95-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="aca95-162">Deze toepassing gereserveerde capaciteit wordt beschouwd als verbruikt en wordt in mindering gebracht op Hallo resterende capaciteit op dat knooppunt en binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aca95-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="aca95-163">Hallo-reservering wordt afgetrokken van de capaciteit van het cluster onmiddellijk resterende hello, maar Hallo gereserveerd verbruik wordt afgetrokken van Hallo-capaciteit van een specifiek knooppunt alleen als er ten minste één service-object is geplaatst op het.</span><span class="sxs-lookup"><span data-stu-id="aca95-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="aca95-164">Deze reservering hoger kunt u flexibiliteit en beter brongebruik omdat alleen de bronnen worden gereserveerd op de knooppunten wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="aca95-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="aca95-165">Hallo toepassing werklast informatie verkrijgen</span><span class="sxs-lookup"><span data-stu-id="aca95-165">Obtaining hello application load information</span></span>
<span data-ttu-id="aca95-166">U kunt voor elke toepassing met een capaciteit van toepassingen gedefinieerd voor een of meer waarden Hallo informatie over Hallo cumulatieve load gerapporteerd door de replica's van de services verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="aca95-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="aca95-167">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aca95-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="aca95-168">C#</span><span class="sxs-lookup"><span data-stu-id="aca95-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="aca95-169">Hallo ApplicationLoad query retourneert Hallo algemene informatie over de capaciteit van de toepassingen die is opgegeven voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="aca95-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="aca95-170">Deze informatie omvat het Hallo-knooppunten van de Minimum en maximum aantal knooppunten info en Hallo nummer Hallo toepassing momenteel wordt ingenomen.</span><span class="sxs-lookup"><span data-stu-id="aca95-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="aca95-171">Dit omvat ook informatie over elke toepassing werklast metriek, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="aca95-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="aca95-172">Metrische naam: Naam van Hallo metriek.</span><span class="sxs-lookup"><span data-stu-id="aca95-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="aca95-173">Reserveringscapaciteit: Cluster de capaciteit die is gereserveerd in Hallo cluster voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="aca95-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="aca95-174">Laden van toepassingen: Totale belasting van deze toepassing onderliggende replica's.</span><span class="sxs-lookup"><span data-stu-id="aca95-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="aca95-175">Capaciteit van de toepassing: De maximaal toegestane waarde van het laden van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="aca95-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="aca95-176">Capaciteit van de toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="aca95-176">Removing Application Capacity</span></span>
<span data-ttu-id="aca95-177">Zodra Hallo toepassing capaciteit parameters zijn ingesteld voor een toepassing, kunnen ze worden verwijderd met behulp van de Update toepassing API's of PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="aca95-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="aca95-178">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aca95-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="aca95-179">Deze opdracht verwijdert u alle management parameters van de toepassing capaciteit van het toepassingsexemplaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="aca95-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="aca95-180">Dit omvat MinimumNodes, MaximumNodes en metrische gegevens van de toepassing hello, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="aca95-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="aca95-181">Hallo effect van Hallo-opdracht is direct.</span><span class="sxs-lookup"><span data-stu-id="aca95-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="aca95-182">Nadat u deze opdracht is voltooid, Hallo Cluster Resource Manager Hallo standaardgedrag gebruikt voor het beheren van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="aca95-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="aca95-183">Capaciteit parameters voor de toepassing opnieuw kunnen worden opgegeven `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="aca95-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="aca95-184">Beperkingen voor de capaciteit van toepassingen</span><span class="sxs-lookup"><span data-stu-id="aca95-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="aca95-185">Er zijn enkele beperkingen van toepassing capaciteit parameters die moeten worden voldaan.</span><span class="sxs-lookup"><span data-stu-id="aca95-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="aca95-186">Als er validatiefouten zijn plaatsvinden geen wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="aca95-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="aca95-187">Alle parameters van geheel getal moet niet-negatieve getallen.</span><span class="sxs-lookup"><span data-stu-id="aca95-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="aca95-188">Nooit moet MinimumNodes groter zijn dan MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="aca95-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="aca95-189">Als de capaciteit voor een load-metriek zijn gedefinieerd, moeten ze deze regels volgen:</span><span class="sxs-lookup"><span data-stu-id="aca95-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="aca95-190">Knooppunt Reserveringscapaciteit mag niet groter zijn dan de maximale capaciteit van het knooppunt zijn.</span><span class="sxs-lookup"><span data-stu-id="aca95-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="aca95-191">U kan bijvoorbeeld Hallo capaciteit voor Hallo metriek 'CPU' op Hallo knooppunt tootwo eenheden beperken en probeer de drie eenheden tooreserve op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="aca95-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="aca95-192">Als MaximumNodes is opgegeven, vervolgens moet Hallo product van MaximumNodes en de maximale capaciteit van het knooppunt niet groter dan de totale capaciteit van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aca95-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="aca95-193">Stel bijvoorbeeld Hallo maximumcapaciteit knooppunt voor load metriek 'CPU' tooeight is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="aca95-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="aca95-194">Stel ook dat u Hallo too10 maximum aantal knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aca95-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="aca95-195">In dit geval moet totale capaciteit van de toepassing groter zijn dan 80 voor deze metriek laden.</span><span class="sxs-lookup"><span data-stu-id="aca95-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="aca95-196">Hallo-beperkingen afgedwongen zowel tijdens het maken van de toepassing en updates.</span><span class="sxs-lookup"><span data-stu-id="aca95-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="aca95-197">Hoe niet toouse capaciteit van toepassingen</span><span class="sxs-lookup"><span data-stu-id="aca95-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="aca95-198">Probeer niet toouse Hallo toepassingsgroep functies tooconstrain Hallo toepassing tooa _specifieke_ deelverzameling met knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aca95-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="aca95-199">Met andere woorden, u kunt opgeven dat Hallo toepassing wordt uitgevoerd op maximaal vijf knooppunten, maar niet welke specifieke vijf knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="aca95-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="aca95-200">Een toepassing toospecific met beperkingen kunnen knooppunten worden bereikt met plaatsingsbeperkingen voor services.</span><span class="sxs-lookup"><span data-stu-id="aca95-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="aca95-201">Probeer niet toouse Hallo toepassing capaciteit tooensure dat twee services van dezelfde toepassing worden geplaatst op Hallo Hallo dezelfde knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aca95-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="aca95-202">Gebruik in plaats daarvan [affiniteit](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) of [plaatsingsbeperkingen](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="aca95-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aca95-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aca95-203">Next steps</span></span>
- <span data-ttu-id="aca95-204">Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="aca95-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="aca95-205">toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="aca95-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="aca95-206">Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="aca95-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="aca95-207">Voor meer informatie over de werking metrische gegevens over het algemeen tot lezen op [Service Fabric Load metrische gegevens](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="aca95-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="aca95-208">Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aca95-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="aca95-209">toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="aca95-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
