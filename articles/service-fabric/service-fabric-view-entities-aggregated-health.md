---
title: Het weergeven van Azure Service Fabric-entiteiten geaggregeerd health | Microsoft Docs
description: Beschrijft hoe een query, bekijken en evalueren van de Azure Service Fabric-entiteiten geaggregeerde status, door middel van statusquery's en algemene query's.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="b9aa4-103">Service Fabric-statusrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="b9aa4-103">View Service Fabric health reports</span></span>
<span data-ttu-id="b9aa4-104">Azure Service Fabric introduceert een [statusmodel](service-fabric-health-introduction.md) met health entiteiten op welke onderdelen van het systeem en watchdogs kunt rapport lokale voorwaarden die ze bewaken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="b9aa4-105">De [health store](service-fabric-health-introduction.md#health-store) aggregeert alle health gegevens om te bepalen of de entiteiten in orde zijn.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="b9aa4-106">Het cluster wordt automatisch gevuld met statusrapporten dat is verzonden door de onderdelen van het systeem.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="b9aa4-107">Meer informatie op [systeemstatusrapporten gebruiken om op te lossen](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="b9aa4-108">Service Fabric bevat meerdere manieren om op te halen van de cumulatieve status van de entiteiten:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="b9aa4-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) of andere visualisatie hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="b9aa4-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="b9aa4-110">Statusquery's (via PowerShell, API of REST)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="b9aa4-111">Algemene query's dat retourneren een lijst van entiteiten met status als een van de eigenschappen (via PowerShell, API of REST)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="b9aa4-112">Ter illustratie van deze opties we gebruiken een lokaal cluster met vijf knooppunten en de [fabric: / WordCount-toepassing](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="b9aa4-113">De **fabric: / WordCount** toepassing bevat twee standaardservices, een stateful service van het type `WordCountServiceType`, en een stateless service van het type `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="b9aa4-114">Ik heb gewijzigd de `ApplicationManifest.xml` vereisen zeven replica's voor de stateful service en één partitie zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="b9aa4-115">Omdat er slechts vijf knooppunten in het cluster, de onderdelen van het systeem een rapport een waarschuwing over de partitie van de service omdat deze lager dan het aantal doel is.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="b9aa4-116">Status in Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="b9aa4-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="b9aa4-117">Service Fabric Explorer biedt een visuele weergave van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="b9aa4-118">In de onderstaande afbeelding ziet u dat:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="b9aa4-119">De toepassing **fabric: / WordCount** is rood (fout) omdat er een foutgebeurtenis gemeld door **MyWatchdog** voor de eigenschap **beschikbaarheid**.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="b9aa4-120">Een van de services ontvangt, **fabric: / WordCount/WordCountService** geel gekleurd (in de waarschuwing).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="b9aa4-121">De service is geconfigureerd met zeven replica's en het cluster heeft vijf knooppunten en daarom twee repicas kan niet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="b9aa4-122">Hoewel dit niet wordt weergegeven hier, de service-partitie geel is vanwege een rapport van `System.FM` mededeling dat `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="b9aa4-123">De gele partitie activeert de gele service.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="b9aa4-124">Het cluster is rood vanwege de rode toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="b9aa4-125">De evaluatie gebruikt standaardbeleidsregels van het clustermanifest en het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="b9aa4-126">Strikte beleidsregels zijn en niet een storing kan tolereren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="b9aa4-127">Weergave van het cluster met Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-127">View of the cluster with Service Fabric Explorer:</span></span>

![Weergave van het cluster met Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="b9aa4-129">Lees meer over [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="b9aa4-130">Statusquery 's</span><span class="sxs-lookup"><span data-stu-id="b9aa4-130">Health queries</span></span>
<span data-ttu-id="b9aa4-131">Service Fabric statusquery's beschrijft voor elk van de ondersteunde [Entiteitstypen](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="b9aa4-132">Toegankelijk zijn via de API, met behulp van methoden op [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell-cmdlets en REST.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="b9aa4-133">Deze query's retourneren voltooid statusgegevens van de entiteit: de geaggregeerde status, entiteit health gebeurtenissen onderliggende statussen (indien van toepassing), slechte evaluaties (als de entiteit is niet in orde) en statistieken van kinderen health (wanneer van toepassing).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="b9aa4-134">Een health-entiteit wordt geretourneerd wanneer het volledig is gevuld in de health store.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="b9aa4-135">De entiteit moet actief zijn (geen verwijderd) en een rapport.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="b9aa4-136">De bovenliggende entiteiten in de keten van de hiërarchie moeten ook systeemrapporten hebben.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="b9aa4-137">Als een van deze voorwaarden niet wordt voldaan, de status retourneren vraagt een [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) met [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` die ziet waarom de entiteit is niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="b9aa4-138">De health-query's moeten in de entiteit-id is afhankelijk van het entiteitstype doorgeven.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="b9aa4-139">De query's accepteren optionele health beleidsparameters.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="b9aa4-140">Als er geen statusbeleid worden opgegeven, de [statusbeleid](service-fabric-health-introduction.md#health-policies) uit het cluster of application manifest worden gebruikt voor evaluatie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="b9aa4-141">Als de manifesten geen definitie voor statusbeleid bevatten, worden de standaardbeleidsregels voor health gebruikt voor evaluatie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="b9aa4-142">Het standaardbeleid voor health doen niet zonder fouten.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="b9aa4-143">De query's ook accepteren filters voor het retourneren van slechts gedeeltelijk onderliggende elementen of gebeurtenissen--de waarden die de opgegeven filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="b9aa4-144">Een ander filter kunt met uitzondering van de statistieken van de onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="b9aa4-145">De uitvoerfilters worden toegepast op de server, zodat het bericht beantwoorden wordt verkleind.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="b9aa4-146">Het is raadzaam dat u de uitvoerfilters gebruiken om te beperken van de gegevens die zijn geretourneerd, in plaats van filters toepassen op de client.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="b9aa4-147">De status van de entiteit bevat:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-147">An entity's health contains:</span></span>

* <span data-ttu-id="b9aa4-148">De cumulatieve status van de entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="b9aa4-149">Door de health store op basis van entiteit statusrapporten, onderliggende statussen (indien van toepassing) en statusbeleid wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="b9aa4-150">Lees meer over [entiteit de statusevaluatie](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="b9aa4-151">De health-gebeurtenissen voor de entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-151">The health events on the entity.</span></span>
* <span data-ttu-id="b9aa4-152">De verzameling van de status van alle onderliggende items voor de entiteiten die onderliggende elementen kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="b9aa4-153">De statussen bevatten entiteit-id's en de geaggregeerde status.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="b9aa4-154">Als u de status voor een kind, aanroepen van de status van de query voor het entiteitstype onderliggende en in de onderliggende-id.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="b9aa4-155">De slechte evaluaties die naar het rapport dat de status van de entiteit geactiveerd verwijzen als de entiteit is niet in orde.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="b9aa4-156">De beoordelingen zijn recursieve, met de onderliggende elementen health evaluaties waarmee huidige status is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="b9aa4-157">Bijvoorbeeld, een watchdog een fout op basis van een replica gemeld.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="b9aa4-158">De toepassingsstatus bevat een onjuiste evaluatie vanwege een onjuiste service; de service is beschadigd vanwege een partitie in error; de partitie is beschadigd vanwege een replica in error; de replica is beschadigd vanwege het statusrapport watchdog-fout.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="b9aa4-159">De health-statistieken voor alle typen voor onderliggende elementen van de entiteiten die onderliggende elementen hebben.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="b9aa4-160">Bijvoorbeeld, cluster-status toont het totale aantal toepassingen, services, partities, replica's en entiteiten in het cluster wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="b9aa4-161">Servicestatus toont het totale aantal partities en replica's onder de opgegeven service.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="b9aa4-162">Status van de cluster ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-162">Get cluster health</span></span>
<span data-ttu-id="b9aa4-163">Retourneert de status van de entiteit van het cluster en de statussen van toepassingen en de knooppunten (onderliggende elementen van het cluster) bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="b9aa4-164">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-164">Input:</span></span>

* <span data-ttu-id="b9aa4-165">[Optioneel] Het cluster statusbeleid gebruikt voor het evalueren van de knooppunten en de Clustergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="b9aa4-166">[Optioneel] De toepassing health beleid kaart met het statusbeleid dat wordt gebruikt voor het overschrijven van de application manifest beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="b9aa4-167">[Optioneel] Filters voor gebeurtenissen, knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-168">Alle gebeurtenissen, knooppunten en toepassingen worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="b9aa4-169">[Optioneel] Filter moeten worden uitgesloten van de van gezondheidsstatistieken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="b9aa4-170">[Optioneel] Opgenomen fabric: / System health statistieken in de health-statistieken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="b9aa4-171">Alleen van toepassing wanneer de health-statistieken niet worden uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="b9aa4-172">Standaard bevatten de health-statistieken worden alleen de statistieken voor toepassingen en niet de systeemtoepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-173">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-173">API</span></span>
<span data-ttu-id="b9aa4-174">Als u het cluster health, maak een `FabricClient` en roept u de [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) methode op de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="b9aa4-175">De volgende aanroep wordt de status van het cluster:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="b9aa4-176">De volgende code haalt de status van het cluster met behulp van een aangepaste cluster statusbeleid en filters voor knooppunten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="b9aa4-177">Hiermee geeft u dat de health-statistieken de fabric bevatten: / statistieken van het systeem.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="b9aa4-178">Het maken van [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), die de invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-179">PowerShell</span></span>
<span data-ttu-id="b9aa4-180">De cmdlet om op te halen van de status van het cluster is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="b9aa4-181">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-182">De status van het cluster is vijf knooppunten, de systeemtoepassing en fabric: / WordCount geconfigureerd zoals wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="b9aa4-183">De volgende cmdlet haalt de gezondheid van het cluster met behulp van standaard statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="b9aa4-184">De geaggregeerde status waarschuwing, omdat de fabric: / WordCount-toepassing bevindt zich in de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="b9aa4-185">Houd er rekening mee hoe de slechte evaluaties gedetailleerde informatie bevat over de voorwaarden waarmee de geaggregeerde status is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="b9aa4-186">De volgende PowerShell-cmdlet haalt de status van het cluster met een aangepaste toepassing-beleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="b9aa4-187">Deze filtert de resultaten om alleen de toepassingen en de knooppunten in de fout of waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="b9aa4-188">Als gevolg hiervan worden geen knooppunten geretourneerd, omdat ze allemaal in orde.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="b9aa4-189">Alleen de fabric: / WordCount-toepassing rekening wordt gehouden met het filter toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="b9aa4-190">Omdat het aangepaste beleid bepaalt u moet overwegen waarschuwingen als fouten voor de fabric: / WordCount-toepassing, de toepassing wordt geëvalueerd als in de fout en is daarom het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="b9aa4-191">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-191">REST</span></span>
<span data-ttu-id="b9aa4-192">U kunt de status van de cluster met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="b9aa4-193">Ophalen van de gezondheid van knooppunt</span><span class="sxs-lookup"><span data-stu-id="b9aa4-193">Get node health</span></span>
<span data-ttu-id="b9aa4-194">Retourneert de status van de entiteit van een knooppunt en de health-gebeurtenissen gemeld op het knooppunt bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="b9aa4-195">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-195">Input:</span></span>

* <span data-ttu-id="b9aa4-196">[Vereist] De knooppuntnaam waarin het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="b9aa4-197">[Optioneel] De cluster health beleidsinstellingen gebruikt voor het evalueren van de status.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="b9aa4-198">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-199">Alle gebeurtenissen die worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-200">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-200">API</span></span>
<span data-ttu-id="b9aa4-201">Als u het knooppunt status via de API, maakt u een `FabricClient` en roept u de [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9aa4-202">De volgende code wordt de status van het knooppunt voor de naam van het opgegeven knooppunt:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="b9aa4-203">De volgende code haalt u de status van het knooppunt voor de naam van het opgegeven knooppunt en wordt doorgegeven in gebeurtenissen filteren en aangepast beleid via [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="b9aa4-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-204">PowerShell</span></span>
<span data-ttu-id="b9aa4-205">De cmdlet om op te halen van de status van het knooppunt is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="b9aa4-206">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="b9aa4-207">De volgende cmdlet wordt de status van het knooppunt met behulp van standaard statusbeleid opgehaald:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="b9aa4-208">De volgende cmdlet wordt de status van alle knooppunten in het cluster:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="b9aa4-209">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-209">REST</span></span>
<span data-ttu-id="b9aa4-210">U krijgt de gezondheid van knooppunt met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="b9aa4-211">Toepassingsstatus ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-211">Get application health</span></span>
<span data-ttu-id="b9aa4-212">Retourneert de status van een Toepassingsentiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-212">Returns the health of an application entity.</span></span> <span data-ttu-id="b9aa4-213">De statussen van de geïmplementeerde toepassing en service onderliggende items bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="b9aa4-214">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-214">Input:</span></span>

* <span data-ttu-id="b9aa4-215">[Vereist] De toepassingsnaam (URI) die de toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="b9aa4-216">[Optioneel] Het statusbeleid voor toepassing gebruikt voor het overschrijven van de application manifest beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="b9aa4-217">[Optioneel] Filters voor gebeurtenissen, services en geïmplementeerde toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-218">Alle gebeurtenissen, services en geïmplementeerde toepassingen worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="b9aa4-219">[Optioneel] Als u wilt uitsluiten van de health-statistieken filteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="b9aa4-220">Als niet wordt opgegeven, de statistieken health bevatten de ok, waarschuwing en fout aantal voor alle onderliggende objecten van toepassing: services, partities, replica's, geïmplementeerde toepassingen en geïmplementeerde servicepakketten.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-221">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-221">API</span></span>
<span data-ttu-id="b9aa4-222">Als u de toepassing health, maak een `FabricClient` en roept u de [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9aa4-223">De volgende code wordt de toepassingsstatus voor de opgegeven toepassingsnaam (URI):</span><span class="sxs-lookup"><span data-stu-id="b9aa4-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="b9aa4-224">De volgende code wordt de toepassingsstatus voor de opgegeven toepassingsnaam (URI), met filters en aangepaste beleidsregels opgegeven via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-225">PowerShell</span></span>
<span data-ttu-id="b9aa4-226">De cmdlet om op te halen van de toepassingsstatus is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="b9aa4-227">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-228">De volgende cmdlet retourneert de status van de **fabric: / WordCount** toepassing:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="b9aa4-229">De volgende PowerShell-cmdlet wordt doorgegeven in een aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="b9aa4-230">Deze filters ook onderliggende elementen en gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="b9aa4-231">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-231">REST</span></span>
<span data-ttu-id="b9aa4-232">U krijgt toepassingsstatus met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="b9aa4-233">Servicestatus ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-233">Get service health</span></span>
<span data-ttu-id="b9aa4-234">Retourneert de status van een service-entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-234">Returns the health of a service entity.</span></span> <span data-ttu-id="b9aa4-235">Het bevat de statussen van de partitie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-235">It contains the partition health states.</span></span> <span data-ttu-id="b9aa4-236">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-236">Input:</span></span>

* <span data-ttu-id="b9aa4-237">[Vereist] De servicenaam (URI) dat de service identificeert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="b9aa4-238">[Optioneel] Het statusbeleid voor toepassing gebruikt voor het onderdrukken van het application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="b9aa4-239">[Optioneel] Filters voor gebeurtenissen en partities die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-240">Alle gebeurtenissen en partities worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="b9aa4-241">[Optioneel] Filter moeten worden uitgesloten van de van gezondheidsstatistieken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="b9aa4-242">Als dat niet wordt opgegeven, de statistieken van de status ok, waarschuwing, weergeven en fout tellen voor alle partities en replica's van de service.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-243">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-243">API</span></span>
<span data-ttu-id="b9aa4-244">Als u de status van de service via de API, maakt u een `FabricClient` en roept u de [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9aa4-245">Het volgende voorbeeld wordt de status van een service met de opgegeven service-naam (URI):</span><span class="sxs-lookup"><span data-stu-id="b9aa4-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="b9aa4-246">De volgende code haalt de servicestatus voor de opgegeven service-naam (URI), filters en aangepast beleid via geven [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="b9aa4-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-247">PowerShell</span></span>
<span data-ttu-id="b9aa4-248">De cmdlet om op te halen van de status van de service is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="b9aa4-249">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-250">De volgende cmdlet wordt de status van de service met behulp van standaard statusbeleid opgehaald:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9aa4-251">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-251">REST</span></span>
<span data-ttu-id="b9aa4-252">U krijgt de status van de service met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="b9aa4-253">Status van de partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-253">Get partition health</span></span>
<span data-ttu-id="b9aa4-254">Retourneert de status van een entiteit van de partitie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="b9aa4-255">De replica-statussen bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-255">It contains the replica health states.</span></span> <span data-ttu-id="b9aa4-256">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-256">Input:</span></span>

* <span data-ttu-id="b9aa4-257">[Vereist] De partitie-ID (GUID) die de partitie identificeert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="b9aa4-258">[Optioneel] Het statusbeleid voor toepassing gebruikt voor het onderdrukken van het application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="b9aa4-259">[Optioneel] Filters voor gebeurtenissen en replica's die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-260">Alle gebeurtenissen en replica's worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="b9aa4-261">[Optioneel] Filter moeten worden uitgesloten van de van gezondheidsstatistieken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="b9aa4-262">Als niet wordt opgegeven, wordt de health-statistieken weergeven hoeveel replica's in ok, waarschuwing en fout statussen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-263">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-263">API</span></span>
<span data-ttu-id="b9aa4-264">Als u de status van de partitie via de API, maakt u een `FabricClient` en roept u de [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9aa4-265">Optionele als parameters wilt opgeven, maken [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-266">PowerShell</span></span>
<span data-ttu-id="b9aa4-267">De cmdlet om op te halen van de status van de partitie is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="b9aa4-268">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-269">De volgende cmdlet wordt de status voor alle partities van de **fabric: / WordCount/WordCountService** -service en uitsluit replica statussen:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9aa4-270">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-270">REST</span></span>
<span data-ttu-id="b9aa4-271">U kunt de status van de partitie met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="b9aa4-272">De status replica ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-272">Get replica health</span></span>
<span data-ttu-id="b9aa4-273">Retourneert de status van de replica van een stateful service of een staatloze service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="b9aa4-274">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-274">Input:</span></span>

* <span data-ttu-id="b9aa4-275">[Vereist] De partitie-ID (GUID) en de replica-ID waarmee de replica.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="b9aa4-276">[Optioneel] De toepassing health beleidsparameters gebruikt voor het overschrijven van de application manifest beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="b9aa4-277">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-278">Alle gebeurtenissen die worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-279">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-279">API</span></span>
<span data-ttu-id="b9aa4-280">Als u de status replica via de API, maakt u een `FabricClient` en roept u de [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9aa4-281">Geavanceerde als parameters wilt opgeven, gebruikt u [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-282">PowerShell</span></span>
<span data-ttu-id="b9aa4-283">De cmdlet om op te halen van de status van de replica is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="b9aa4-284">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-285">De volgende cmdlet wordt de status van de primaire replica voor alle partities van de service:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="b9aa4-286">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-286">REST</span></span>
<span data-ttu-id="b9aa4-287">U krijgt de status replica met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="b9aa4-288">Status van de geïmplementeerde toepassing ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-288">Get deployed application health</span></span>
<span data-ttu-id="b9aa4-289">Retourneert de status van een toepassing is geïmplementeerd op een knooppunt-entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="b9aa4-290">De statussen van de geïmplementeerde service-pakket bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="b9aa4-291">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-291">Input:</span></span>

* <span data-ttu-id="b9aa4-292">[Vereist] De toepassingsnaam (URI) en de knooppuntnaam (tekenreeks) waarmee de geïmplementeerde toepassing worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="b9aa4-293">[Optioneel] Het statusbeleid voor toepassing gebruikt voor het overschrijven van de application manifest beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="b9aa4-294">[Optioneel] Filters voor gebeurtenissen en geïmplementeerde servicepakketten die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-295">Alle gebeurtenissen en geïmplementeerde servicepakketten worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="b9aa4-296">[Optioneel] Filter moeten worden uitgesloten van de van gezondheidsstatistieken.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="b9aa4-297">Als niet wordt opgegeven, weergeven de statistieken van de gezondheid van het aantal geïmplementeerde servicepakketten in de status ok, waarschuwing en fout.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-298">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-298">API</span></span>
<span data-ttu-id="b9aa4-299">Als u de status van een toepassing is geïmplementeerd op een knooppunt via de API, maakt u een `FabricClient` en roept u de [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9aa4-300">Gebruik het optionele parameters opgeven [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-301">PowerShell</span></span>
<span data-ttu-id="b9aa4-302">De cmdlet om op te halen van de status geïmplementeerde toepassing is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="b9aa4-303">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b9aa4-304">Uitvoeren als u wilt weten waar een toepassing wordt geïmplementeerd, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en kijk in de geïmplementeerde toepassing onderliggende elementen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="b9aa4-305">De volgende cmdlet wordt de status van de **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9aa4-306">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-306">REST</span></span>
<span data-ttu-id="b9aa4-307">U krijgt de status geïmplementeerde toepassing met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="b9aa4-308">Status van geïmplementeerde service pakket ophalen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-308">Get deployed service package health</span></span>
<span data-ttu-id="b9aa4-309">Retourneert de status van een geïmplementeerde service pakket entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="b9aa4-310">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-310">Input:</span></span>

* <span data-ttu-id="b9aa4-311">[Vereist] De toepassingsnaam (URI), knooppuntnaam (tekenreeks) en manifest servicenaam (tekenreeks) die het pakket geïmplementeerde service identificeren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="b9aa4-312">[Optioneel] Het statusbeleid voor toepassing gebruikt voor het onderdrukken van het application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="b9aa4-313">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in het resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9aa4-314">Alle gebeurtenissen die worden gebruikt voor het evalueren van de entiteitsstatus geaggregeerd, ongeacht het filter.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-315">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-315">API</span></span>
<span data-ttu-id="b9aa4-316">Als u de status van een geïmplementeerde service-pakket via de API, maakt u een `FabricClient` en roept u de [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9aa4-317">Gebruik het optionele parameters opgeven [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-318">PowerShell</span></span>
<span data-ttu-id="b9aa4-319">De cmdlet om op te halen van de status geïmplementeerde service-pakket is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="b9aa4-320">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b9aa4-321">Als u wilt zien waar een toepassing wordt geïmplementeerd, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en kijk in de geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="b9aa4-322">Als u wilt zien welke service pakketten in een toepassing zijn, kijken naar de onderliggende geïmplementeerde service pakket in de [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="b9aa4-323">De volgende cmdlet wordt de status van de **WordCountServicePkg** servicepakket van de **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="b9aa4-324">De entiteit heeft **System.Hosting** rapporten voor geslaagde pakket service en ingangspunt activering en succesvolle registratie van het type van de service.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="b9aa4-325">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-325">REST</span></span>
<span data-ttu-id="b9aa4-326">U kunt de status van de geïmplementeerde service pakket met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) die wordt beschreven in de hoofdtekst van het statusbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="b9aa4-327">Health chunk query 's</span><span class="sxs-lookup"><span data-stu-id="b9aa4-327">Health chunk queries</span></span>
<span data-ttu-id="b9aa4-328">Cluster met meerdere niveaus van kinderen (recursief) per invoer filters kunnen worden geretourneerd door de chunk statusquery's.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="b9aa4-329">Biedt ondersteuning voor geavanceerde filters waarmee een grote flexibiliteit bij het kiezen van de onderliggende items moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="b9aa4-330">De filters kunnen onderliggende items opgeven door de unieke id of door andere groeps-id's en/of de statussen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="b9aa4-331">Geen onderliggende elementen zijn standaard opgenomen in plaats van de health-opdrachten die altijd eerste niveau onderliggende elementen bevatten.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="b9aa4-332">De [statusquery's](service-fabric-view-entities-aggregated-health.md#health-queries) alleen eerste niveau onderliggende elementen van de opgegeven entiteit per vereist filters retourneren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="b9aa4-333">Als u de onderliggende leden van de onderliggende elementen, moet u extra health API's voor elke entiteit van belang aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="b9aa4-334">Op dezelfde manier als u de status van specifieke entiteiten, moet u voor elke gewenste entiteit één health API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="b9aa4-335">Chunk kunt geavanceerde filteren u de query voor het aanvragen van meerdere items in een query, de grootte van het bericht en het aantal berichten voor het minimaliseren van belang.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="b9aa4-336">De waarde van de query chunk is dat u de status voor meer cluster entiteiten (mogelijk alle cluster entiteiten starten in de hoofdmap van de vereiste) kunt krijgen in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="b9aa4-337">U kunt de gezondheid van complexe query zoals express:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="b9aa4-338">Retour alleen toepassingen in de fout en voor die toepassingen bevatten alle services in waarschuwing of fout.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="b9aa4-339">Voor de geretourneerde services omvatten alle partities.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="b9aa4-340">Alleen de status van de opgegeven door de namen van de vier toepassingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="b9aa4-341">Retourneert alleen de status van toepassingen van een type van de gewenste toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="b9aa4-342">Retourneert alle geïmplementeerde entiteiten op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="b9aa4-343">Retourneert alle toepassingen, alle toepassingen op het opgegeven knooppunt en alle geïmplementeerde servicepakketten op dat knooppunt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="b9aa4-344">Alle replica's in een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-344">Return all replicas in error.</span></span> <span data-ttu-id="b9aa4-345">Retourneert alle toepassingen, services, partities en alleen replica's in de fout.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="b9aa4-346">Retourneren van alle toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-346">Return all applications.</span></span> <span data-ttu-id="b9aa4-347">Voor een opgegeven service omvatten alle partities.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="b9aa4-348">Op dit moment wordt de status chunk query blootgesteld alleen voor de entiteit van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="b9aa4-349">Een cluster health chunk, waarin wordt:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="b9aa4-350">De status van het cluster geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="b9aa4-351">De health status chunk lijst met knooppunten die fungeren als invoer filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="b9aa4-352">De health status chunk lijst met toepassingen die invoer filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="b9aa4-353">Elk segment application health-status bevat een lijst chunk met alle services die invoer filters en een chunk-lijst met alle geïmplementeerde toepassingen die de filters respecteren respecteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="b9aa4-354">Hetzelfde voor de onderliggende elementen van services en geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="b9aa4-355">Op deze manier alle entiteiten in het cluster kunnen worden mogelijk geretourneerd als in een hiërarchische aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="b9aa4-356">Cluster health chunk query</span><span class="sxs-lookup"><span data-stu-id="b9aa4-356">Cluster health chunk query</span></span>
<span data-ttu-id="b9aa4-357">Retourneert de status van de entiteit van het cluster en de hiërarchische health status segmenten van vereiste onderliggende items bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="b9aa4-358">Invoer:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-358">Input:</span></span>

* <span data-ttu-id="b9aa4-359">[Optioneel] Het cluster statusbeleid gebruikt voor het evalueren van de knooppunten en de Clustergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="b9aa4-360">[Optioneel] De toepassing health beleid kaart met het statusbeleid dat wordt gebruikt voor het overschrijven van de application manifest beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="b9aa4-361">[Optioneel] Filters voor knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="b9aa4-362">De filters zijn specifiek voor een entiteit of de groep van entiteiten of zijn van toepassing op alle entiteiten op dat niveau.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="b9aa4-363">De lijst met filters kan bevatten één algemene filter en/of filters voor specifieke id's voor fijnmazige entiteiten die door de query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="b9aa4-364">Als u niets opgeeft, worden de onderliggende elementen niet standaard geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="b9aa4-365">Meer informatie over de filters op [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) en [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="b9aa4-366">De toepassing filters kunnen recursief geavanceerde filters voor kinderen opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="b9aa4-367">Het resultaat van het segment bevat de onderliggende items waarvan de filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="b9aa4-368">De query chunk levert op dit moment geen slechte evaluaties of entiteit gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="b9aa4-369">Deze extra informatie kan worden verkregen met behulp van de bestaande query van de cluster-status.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="b9aa4-370">API</span><span class="sxs-lookup"><span data-stu-id="b9aa4-370">API</span></span>
<span data-ttu-id="b9aa4-371">Als u het cluster health chunk, maakt een `FabricClient` en roept u de [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) methode op de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="b9aa4-372">U kunt doorgeven [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) te beschrijven statusbeleid en geavanceerde filters.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="b9aa4-373">De volgende code haalt cluster health chunk met geavanceerde filters.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9aa4-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9aa4-374">PowerShell</span></span>
<span data-ttu-id="b9aa4-375">De cmdlet om op te halen van de status van het cluster is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="b9aa4-376">Eerst verbinding met het cluster met behulp van de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9aa4-377">De volgende code haalt knooppunten alleen als deze fout, met uitzondering van een specifiek knooppunt dat moet altijd worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="b9aa4-378">De volgende cmdlet haalt cluster chunk met toepassingsfilters.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="b9aa4-379">De volgende cmdlet retourneert alle geïmplementeerde entiteiten op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="b9aa4-380">REST</span><span class="sxs-lookup"><span data-stu-id="b9aa4-380">REST</span></span>
<span data-ttu-id="b9aa4-381">U krijgt cluster health chunk gevonden met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) die statusbeleid en geavanceerde filters wordt beschreven in de hoofdtekst bevat.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="b9aa4-382">Algemene query 's</span><span class="sxs-lookup"><span data-stu-id="b9aa4-382">General queries</span></span>
<span data-ttu-id="b9aa4-383">Algemene query's retourneren een lijst met Service Fabric-entiteiten van een bepaald type.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="b9aa4-384">Ze beschikbaar worden gesteld via de API (via de methoden op **FabricClient.QueryManager**), PowerShell-cmdlets en REST.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="b9aa4-385">Deze query's samenvoegen subquery's uit meerdere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="b9aa4-386">Een ervan de [health store](service-fabric-health-introduction.md#health-store), die de geaggregeerde status voor elke queryresultaat wordt gevuld.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="b9aa4-387">Algemene query's terug van de cumulatieve status van de entiteit en bevatten geen uitgebreide statusgegevens.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="b9aa4-388">Als u een entiteit is niet in orde, kunt u met statusquery's voor alle de health-informatie, zoals gebeurtenissen, onderliggende statussen en slecht evaluaties opvolgen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="b9aa4-389">Als algemene query's een onbekende status voor een entiteit retourneren, is het mogelijk dat de health store geen volledige gegevens over de entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="b9aa4-390">Het is ook mogelijk dat een subquery naar de health store niet geslaagd is (bijvoorbeeld: Er is een communicatiefout opgetreden of de health store is beperkt).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="b9aa4-391">Opvolgen met een status-query voor de entiteit.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="b9aa4-392">Als de subquery tijdelijke fouten, zoals netwerkproblemen aangetroffen, kan deze vervolgzelfstudie query slagen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="b9aa4-393">Ook kan geven u meer informatie uit de store health over waarom de entiteit is niet beschikbaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="b9aa4-394">De query's met **HealthState** voor entiteiten zijn:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="b9aa4-395">Lijst met knooppunten: de lijst met knooppunten in het cluster (wisselbare) retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="b9aa4-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="b9aa4-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="b9aa4-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="b9aa4-398">Lijst met toepassingen: de lijst met toepassingen in het cluster (wisselbare) retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="b9aa4-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="b9aa4-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b9aa4-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="b9aa4-401">De lijst service: de lijst met services in een toepassing (wisselbare) retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="b9aa4-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="b9aa4-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="b9aa4-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="b9aa4-404">Lijst met partitie: de lijst met partities in een service (wisselbare) retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="b9aa4-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="b9aa4-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="b9aa4-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="b9aa4-407">Lijst met replica's: de lijst met replica's in een partitie (wisselbare) retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="b9aa4-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="b9aa4-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="b9aa4-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="b9aa4-410">Lijst met toepassingen geïmplementeerd: de lijst met geïmplementeerde toepassingen op een knooppunt retourneert.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="b9aa4-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="b9aa4-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="b9aa4-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="b9aa4-413">De lijst van de service-pakket wordt geïmplementeerd: retourneert de lijst met servicepakketten in een geïmplementeerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="b9aa4-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="b9aa4-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="b9aa4-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="b9aa4-416">Sommige van de query's wisselbare resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-416">Some of the queries return paged results.</span></span> <span data-ttu-id="b9aa4-417">Het retourtype van deze query's is een lijst die is afgeleid van [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="b9aa4-418">Als de resultaten een bericht niet past alleen een pagina wordt geretourneerd en een ContinuationToken die houdt waarin de opsomming is gestopt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="b9aa4-419">Aanroepen van dezelfde query- en in het vervolgtoken uit de vorige query ophalen van de volgende resultaten blijven.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="b9aa4-420">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="b9aa4-420">Examples</span></span>
<span data-ttu-id="b9aa4-421">De volgende code haalt de slechte toepassingen in het cluster:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="b9aa4-422">De volgende cmdlet haalt de toepassingsgegevens voor de fabric: / WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="b9aa4-423">U ziet dat de status op de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="b9aa4-424">De volgende cmdlet wordt opgehaald van de services met een status van de fout:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="b9aa4-425">Cluster en de toepassing upgrades</span><span class="sxs-lookup"><span data-stu-id="b9aa4-425">Cluster and application upgrades</span></span>
<span data-ttu-id="b9aa4-426">Tijdens een bewaakte upgrade van het cluster en de toepassing controleert Service Fabric health om ervoor te zorgen dat alles in orde blijft.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="b9aa4-427">Als een entiteit niet in orde is als geëvalueerd met behulp van de geconfigureerde statusbeleid, geldt de upgrade upgrade-specifiek beleid om te bepalen van de volgende actie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="b9aa4-428">De upgrade kan worden onderbroken zodat gebruikersinteractie (zoals de vaststelling van de fout of wijzigen van beleid) of het mogelijk automatisch terugkeren naar de vorige versie goed.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="b9aa4-429">Tijdens een *cluster* bijwerkt, krijgt u de upgradestatus van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="b9aa4-430">De upgradestatus omvat slecht evaluaties die verwijzen naar wat is er niet in orde in het cluster.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="b9aa4-431">Als de upgrade is teruggedraaid vanwege statusproblemen met de, onthoudt de upgradestatus van de laatste slecht redenen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="b9aa4-432">Deze informatie kunt beheerders onderzoeken wat er mis ging nadat de upgrade is teruggedraaid of gestopt.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="b9aa4-433">Op deze manier tijdens een *toepassing* bijwerkt, alle slechte beoordelingen zijn opgenomen in de upgradestatus van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="b9aa4-434">Hieronder vindt u de status van de toepassing bijwerken voor een gewijzigde fabric: / WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="b9aa4-435">Een watchdog heeft een fout gerapporteerd op een van de replica's.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="b9aa4-436">De upgrade is rolling omdat de statuscontroles niet worden nageleefd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="b9aa4-437">Meer informatie over de [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="b9aa4-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="b9aa4-438">Gebruik health evaluaties om op te lossen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="b9aa4-439">Wanneer er een probleem met het cluster of een toepassing wordt gebruikt, bekijkt u de status van het cluster of de toepassing te achterhalen wat is het probleem.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="b9aa4-440">De slechte evaluaties bieden informatie over wat de huidige slecht geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="b9aa4-441">Als u wilt, kunt u inzoomen op beschadigde onderliggende entiteiten voor het identificeren van de hoofdoorzaak te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="b9aa4-442">Neem bijvoorbeeld een toepassing slecht omdat er een foutenrapport op een van de replica's.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="b9aa4-443">De volgende Powershell-cmdlet ziet u de slechte evaluaties:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="b9aa4-444">U kunt de replica voor meer informatie bekijken:</span><span class="sxs-lookup"><span data-stu-id="b9aa4-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="b9aa4-445">De slechte evaluaties weergeven in dat de eerste reden de entiteit wordt geëvalueerd naar de huidige status.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="b9aa4-446">Mogelijk zijn er meerdere andere gebeurtenissen die deze status activeren, maar ze niet zijn doorgevoerd bij de evaluatie.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="b9aa4-447">Voor meer informatie, Inzoomen op de health-entiteiten om alle slechte rapporten in het cluster te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="b9aa4-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b9aa4-448">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-448">Next steps</span></span>
[<span data-ttu-id="b9aa4-449">Use system health reports to troubleshoot (Systeemstatusrapporten gebruiken om problemen op te lossen)</span><span class="sxs-lookup"><span data-stu-id="b9aa4-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="b9aa4-450">Aangepaste Service Fabric-statusrapporten toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9aa4-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="b9aa4-451">Het rapport en controleer de servicestatus van de</span><span class="sxs-lookup"><span data-stu-id="b9aa4-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="b9aa4-452">Controle en diagnose van lokaal services</span><span class="sxs-lookup"><span data-stu-id="b9aa4-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="b9aa4-453">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="b9aa4-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
