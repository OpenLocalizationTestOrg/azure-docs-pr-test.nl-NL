---
title: aaaHow tooview Azure Service Fabric entiteiten geaggregeerd health | Microsoft Docs
description: Hierin wordt beschreven hoe u tooquery, bekijken en evalueren van de Azure Service Fabric-entiteiten geaggregeerde status, door middel van statusquery's en algemene query's.
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="3c99e-103">Service Fabric-statusrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="3c99e-103">View Service Fabric health reports</span></span>
<span data-ttu-id="3c99e-104">Azure Service Fabric introduceert een [statusmodel](service-fabric-health-introduction.md) met health entiteiten op welke onderdelen van het systeem en watchdogs kunt rapport lokale voorwaarden die ze bewaken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="3c99e-105">Hallo [health store](service-fabric-health-introduction.md#health-store) alle health gegevens toodetermine aggregeert of entiteiten zijn in orde.</span><span class="sxs-lookup"><span data-stu-id="3c99e-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="3c99e-106">Hallo-cluster wordt automatisch gevuld met statusrapporten dat is verzonden door de onderdelen van het systeem Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c99e-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="3c99e-107">Meer informatie op [gebruik systeemstatusrapporten tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="3c99e-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="3c99e-108">Service Fabric bevat meerdere manieren tooget Hallo geaggregeerd health Hallo entiteiten:</span><span class="sxs-lookup"><span data-stu-id="3c99e-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="3c99e-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) of andere visualisatie hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="3c99e-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="3c99e-110">Statusquery's (via PowerShell, API of REST)</span><span class="sxs-lookup"><span data-stu-id="3c99e-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="3c99e-111">Algemene query's dat retourneren een lijst van entiteiten die status als een van de eigenschappen hello (via PowerShell, API of REST hebben)</span><span class="sxs-lookup"><span data-stu-id="3c99e-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="3c99e-112">Deze opties we toodemonstrate gebruik van een lokaal cluster met vijf knooppunten en Hallo [fabric: / WordCount-toepassing](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="3c99e-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="3c99e-113">Hallo **fabric: / WordCount** toepassing bevat twee standaardservices, een stateful service van het type `WordCountServiceType`, en een stateless service van het type `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="3c99e-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="3c99e-114">Ik heb Hallo gewijzigd `ApplicationManifest.xml` toorequire zeven doel replica's voor Hallo stateful service en een partitie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="3c99e-115">Omdat er slechts vijf knooppunten in cluster hello, rapporteren Hallo-systeemonderdelen een waarschuwing op Hallo service partitie omdat deze lager dan Hallo doel count is.</span><span class="sxs-lookup"><span data-stu-id="3c99e-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="3c99e-116">Status in Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3c99e-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="3c99e-117">Service Fabric Explorer biedt een visuele weergave van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c99e-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="3c99e-118">In onderstaande Hallo afbeelding, kunt u zien dat:</span><span class="sxs-lookup"><span data-stu-id="3c99e-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="3c99e-119">toepassing Hello **fabric: / WordCount** is rood (fout) omdat er een foutgebeurtenis gemeld door **MyWatchdog** voor de eigenschap Hallo **beschikbaarheid**.</span><span class="sxs-lookup"><span data-stu-id="3c99e-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="3c99e-120">Een van de services ontvangt, **fabric: / WordCount/WordCountService** geel gekleurd (in de waarschuwing).</span><span class="sxs-lookup"><span data-stu-id="3c99e-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="3c99e-121">Hallo-service is geconfigureerd met zeven replica's en Hallo cluster heeft vijf knooppunten, zodat er twee repicas kan niet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3c99e-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="3c99e-122">Hoewel dit niet wordt weergegeven hier, Hallo service partitie geel is vanwege een rapport van `System.FM` mededeling dat `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="3c99e-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="3c99e-123">Hallo gele partitie triggers Hallo gele service.</span><span class="sxs-lookup"><span data-stu-id="3c99e-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="3c99e-124">Hallo-cluster is rood vanwege Hallo rode toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="3c99e-125">Hallo evaluatie gebruikt standaardbeleidsregels van clustermanifest hello en manifest van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="3c99e-126">Strikte beleidsregels zijn en niet een storing kan tolereren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="3c99e-127">Weergave van Hallo-cluster met Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Weergave van Hallo-cluster met Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="3c99e-129">Lees meer over [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3c99e-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="3c99e-130">Statusquery 's</span><span class="sxs-lookup"><span data-stu-id="3c99e-130">Health queries</span></span>
<span data-ttu-id="3c99e-131">Service Fabric statusquery's beschrijft voor elk ondersteund Hallo [Entiteitstypen](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="3c99e-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="3c99e-132">Toegankelijk zijn via API, met behulp van methoden op Hallo [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell-cmdlets en REST.</span><span class="sxs-lookup"><span data-stu-id="3c99e-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="3c99e-133">Deze query's retourneren voltooid statusinformatie over Hallo entiteit: Hallo geaggregeerd status, entiteit health gebeurtenissen onderliggende statussen (indien van toepassing), slecht evaluaties (wanneer Hallo entiteit is niet in orde) en onderliggende items health statistieken (wanneer van toepassing).</span><span class="sxs-lookup"><span data-stu-id="3c99e-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="3c99e-134">Een health-entiteit wordt geretourneerd wanneer het volledig is gevuld in Hallo health store.</span><span class="sxs-lookup"><span data-stu-id="3c99e-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="3c99e-135">Hallo-entiteit moet actief zijn (geen verwijderd) en een rapport.</span><span class="sxs-lookup"><span data-stu-id="3c99e-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="3c99e-136">De bovenliggende entiteiten van Hallo hiërarchie keten moeten ook systeemrapporten hebben.</span><span class="sxs-lookup"><span data-stu-id="3c99e-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="3c99e-137">Als een van deze voorwaarden niet wordt voldaan, Hallo health return vraagt een [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) met [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` die ziet waarom Hallo entiteit wordt niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="3c99e-138">Hallo statusquery's moeten in Hallo entiteits-id, die afhankelijk van het entiteitstype Hallo is doorgeven.</span><span class="sxs-lookup"><span data-stu-id="3c99e-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="3c99e-139">Hallo-query's accepteren optionele health beleidsparameters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="3c99e-140">Als er geen statusbeleid worden opgegeven, Hallo [statusbeleid](service-fabric-health-introduction.md#health-policies) van het cluster of toepassingsmanifest hello worden gebruikt voor evaluatie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="3c99e-141">Als Hallo manifesten geen definitie voor statusbeleid bevatten, gebruikt Hallo standaard statusbeleid voor evaluatie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="3c99e-142">Hallo standaard statusbeleid komen niet zonder fouten.</span><span class="sxs-lookup"><span data-stu-id="3c99e-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="3c99e-143">Hallo-query's ook filters voor het retourneren van alleen gedeeltelijke onderliggende accepteren of gebeurtenissen--Hallo waarden die respecteren Hallo opgegeven filters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="3c99e-144">Een ander filter kunt exclusief Hallo kinderen statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="3c99e-145">Hallo uitvoerfilters worden toegepast aan serverzijde hello, zodat het Hallo-bericht beantwoorden grootte wordt verkleind.</span><span class="sxs-lookup"><span data-stu-id="3c99e-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="3c99e-146">Het is raadzaam Hallo uitvoerfilters toolimit Hallo gegevens geretourneerd, in plaats van filters toepassen op de client hello te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="3c99e-147">De status van de entiteit bevat:</span><span class="sxs-lookup"><span data-stu-id="3c99e-147">An entity's health contains:</span></span>

* <span data-ttu-id="3c99e-148">status van entiteit Hallo Hallo geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="3c99e-149">Door Hallo health store op basis van entiteit statusrapporten, onderliggende statussen (indien van toepassing) en statusbeleid wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="3c99e-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="3c99e-150">Lees meer over [entiteit de statusevaluatie](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="3c99e-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="3c99e-151">Hallo health gebeurtenissen op Hallo entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="3c99e-152">Hallo-verzameling van de status van alle onderliggende items voor Hallo entiteiten die onderliggende elementen kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="3c99e-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="3c99e-153">Hallo-statussen entiteit-id's bevatten en Hallo geaggregeerde status.</span><span class="sxs-lookup"><span data-stu-id="3c99e-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="3c99e-154">tooget status voor een kind Hallo query health aanroepen voor Hallo onderliggende entiteitstype en Hallo onderliggende id doorgeven.</span><span class="sxs-lookup"><span data-stu-id="3c99e-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="3c99e-155">Hallo slecht evaluaties dat punt toohello rapporteren die geactiveerd Hallo-status van het Hallo-entiteit als Hallo entiteit is niet in orde.</span><span class="sxs-lookup"><span data-stu-id="3c99e-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="3c99e-156">Hallo-beoordelingen zijn recursieve, met Hallo kinderen health evaluaties waarmee huidige status is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="3c99e-157">Bijvoorbeeld, een watchdog een fout op basis van een replica gemeld.</span><span class="sxs-lookup"><span data-stu-id="3c99e-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="3c99e-158">Hallo toepassingsstatus toont een slecht evaluatie vanwege tooan slecht service; Hallo-service is beschadigd vanwege tooa partitie in error; Hallo-partitie is beschadigd vanwege tooa replica in een fout. Hallo-replica is beschadigd vanwege toohello watchdog foutenrapport health.</span><span class="sxs-lookup"><span data-stu-id="3c99e-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="3c99e-159">Hallo health statistieken voor alle typen voor onderliggende elementen van Hallo entiteiten die onderliggende elementen hebben.</span><span class="sxs-lookup"><span data-stu-id="3c99e-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="3c99e-160">Bijvoorbeeld, cluster health toont Hallo totale aantal toepassingen, services, partities, replica's en entiteiten in de cluster Hallo geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="3c99e-161">Status van de service bevat Hallo kunt u het totale aantal partities en replica's onder Hallo opgegeven service.</span><span class="sxs-lookup"><span data-stu-id="3c99e-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="3c99e-162">Status van de cluster ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-162">Get cluster health</span></span>
<span data-ttu-id="3c99e-163">Retourneert Hallo health van Hallo cluster entiteit en Hallo statussen van toepassingen en knooppunten (kinderen van Hallo cluster) bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="3c99e-164">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-164">Input:</span></span>

* <span data-ttu-id="3c99e-165">[Optioneel] Hallo cluster statusbeleid gebruikt tooevaluate Hallo knooppunten en Hallo Clustergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="3c99e-166">[Optioneel] Hallo application health beleid kaart gebruikt toooverride Hallo application manifest beleid met Hallo statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="3c99e-167">[Optioneel] Filters voor gebeurtenissen, knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-168">Alle gebeurtenissen, knooppunten en toepassingen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="3c99e-169">[Optioneel] Filter tooexclude health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="3c99e-170">[Optioneel] Filteren tooinclude fabric: / System health statistieken in Hallo health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="3c99e-171">Alleen van toepassing als Hallo health statistieken niet worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="3c99e-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="3c99e-172">Standaard bevatten Hallo health statistieken alleen statistieken voor toepassingen en niet Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-173">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-173">API</span></span>
<span data-ttu-id="3c99e-174">tooget cluster health, maak een `FabricClient` en aanroep Hallo [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) methode op de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="3c99e-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="3c99e-175">Hallo volgende oproep verzenden opgehaald Hallo cluster health:</span><span class="sxs-lookup"><span data-stu-id="3c99e-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="3c99e-176">Hallo volgende code Hallo cluster health opgehaald met behulp van een aangepaste cluster statusbeleid en filters voor knooppunten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="3c99e-177">Hiermee geeft u dat Hallo health statistieken Hallo fabric bevatten: / statistieken van het systeem.</span><span class="sxs-lookup"><span data-stu-id="3c99e-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="3c99e-178">Het maken van [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), die Hallo invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="3c99e-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-179">PowerShell</span></span>
<span data-ttu-id="3c99e-180">Hallo cmdlet tooget Hallo cluster status is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="3c99e-181">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-182">Hallo status van de cluster Hallo is vijf knooppunten Hallo systeemtoepassing en fabric: / WordCount geconfigureerd zoals wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="3c99e-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="3c99e-183">Hallo volgende cmdlet haalt status van de cluster met behulp van standaard statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="3c99e-184">Hallo geaggregeerde status is waarschuwing, omdat Hallo fabric: / WordCount-toepassing bevindt zich in de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="3c99e-185">Houd er rekening mee hoe Hallo slecht evaluaties gedetailleerde informatie bevat over Hallo voorwaarden waarmee Hallo geaggregeerd status is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="3c99e-186">Hallo haalt volgende PowerShell-cmdlet Hallo-status van het Hallo-cluster met behulp van een aangepaste toepassingenbeleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="3c99e-187">Deze filtert de resultaten tooget alleen toepassingen en knooppunten in de fout of waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="3c99e-188">Als gevolg hiervan worden geen knooppunten geretourneerd, omdat ze allemaal in orde.</span><span class="sxs-lookup"><span data-stu-id="3c99e-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="3c99e-189">Alleen Hallo fabric: / WordCount-toepassing hello toepassingen filter respecteert.</span><span class="sxs-lookup"><span data-stu-id="3c99e-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="3c99e-190">Omdat Hallo aangepaste beleid tooconsider waarschuwingen als fouten voor Hallo fabric bepaalt: / WordCount-toepassing hello toepassing wordt geëvalueerd als in de fout en is daarom Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c99e-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-191">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-191">REST</span></span>
<span data-ttu-id="3c99e-192">U kunt de status van de cluster met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="3c99e-193">Ophalen van de gezondheid van knooppunt</span><span class="sxs-lookup"><span data-stu-id="3c99e-193">Get node health</span></span>
<span data-ttu-id="3c99e-194">Retourneert Hallo status van de entiteit van een knooppunt en bevat Hallo health gebeurtenissen die zijn gerapporteerd op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="3c99e-195">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-195">Input:</span></span>

* <span data-ttu-id="3c99e-196">[Vereist] Hallo knooppuntnaam die Hallo knooppunt aangeeft.</span><span class="sxs-lookup"><span data-stu-id="3c99e-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="3c99e-197">[Optioneel] Hallo cluster health beleidsinstellingen tooevaluate health gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="3c99e-198">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-199">Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-200">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-200">API</span></span>
<span data-ttu-id="3c99e-201">tooget knooppunt health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="3c99e-202">Hallo haalt volgende code Hallo knooppunt status voor naam van het opgegeven knooppunt Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c99e-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="3c99e-203">Hallo volgende code haalt Hallo knooppunt health voor Hallo node name en geeft gebeurtenissen filteren en aangepast beleid via opgegeven [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="3c99e-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="3c99e-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-204">PowerShell</span></span>
<span data-ttu-id="3c99e-205">Hallo cmdlet tooget Hallo de status van knooppunt is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="3c99e-206">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="3c99e-207">Hallo knooppunt health Hallo volgende cmdlet opgehaald met behulp van standaard statusbeleid:</span><span class="sxs-lookup"><span data-stu-id="3c99e-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="3c99e-208">Hallo volgende cmdlet wordt opgehaald Hallo status van alle knooppunten in cluster Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c99e-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-209">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-209">REST</span></span>
<span data-ttu-id="3c99e-210">U krijgt de gezondheid van knooppunt met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="3c99e-211">Toepassingsstatus ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-211">Get application health</span></span>
<span data-ttu-id="3c99e-212">Retourneert Hallo de status van een Toepassingsentiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="3c99e-213">Het bevat Hallo-statussen van Hallo geïmplementeerd toepassing en service onderliggende items.</span><span class="sxs-lookup"><span data-stu-id="3c99e-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="3c99e-214">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-214">Input:</span></span>

* <span data-ttu-id="3c99e-215">[Vereist] Hallo toepassingsnaam (URI) die de toepassing hello identificeert.</span><span class="sxs-lookup"><span data-stu-id="3c99e-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="3c99e-216">[Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="3c99e-217">[Optioneel] Filters voor gebeurtenissen, services en geïmplementeerde toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-218">Alle gebeurtenissen, services en geïmplementeerde toepassingen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="3c99e-219">[Optioneel] Filter tooexclude Hallo health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="3c99e-220">Als niet wordt opgegeven, Hallo health statistieken Hallo ok, waarschuwing en fout aantal voor alle onderliggende objecten van toepassing zijn: services, partities, replica's, geïmplementeerde toepassingen en geïmplementeerde servicepakketten.</span><span class="sxs-lookup"><span data-stu-id="3c99e-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-221">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-221">API</span></span>
<span data-ttu-id="3c99e-222">tooget toepassingsstatus, maak een `FabricClient` en aanroep Hallo [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="3c99e-223">Hallo haalt volgende code de toepassingsstatus Hallo voor Hallo opgegeven toepassingsnaam (URI):</span><span class="sxs-lookup"><span data-stu-id="3c99e-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="3c99e-224">Hallo volgende code haalt Hallo toepassingsstatus voor Hallo opgegeven toepassingsnaam (URI), met filters en aangepaste beleidsregels opgegeven via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="3c99e-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="3c99e-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-225">PowerShell</span></span>
<span data-ttu-id="3c99e-226">Hallo cmdlet tooget Hallo de status van toepassing is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="3c99e-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="3c99e-227">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-228">Hallo volgende cmdlet retourneert Hallo health Hallo **fabric: / WordCount** toepassing:</span><span class="sxs-lookup"><span data-stu-id="3c99e-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="3c99e-229">Hallo volgende PowerShell-cmdlet geeft in het aangepaste beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="3c99e-230">Deze filters ook onderliggende elementen en gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-231">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-231">REST</span></span>
<span data-ttu-id="3c99e-232">U krijgt toepassingsstatus met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="3c99e-233">Servicestatus ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-233">Get service health</span></span>
<span data-ttu-id="3c99e-234">Retourneert Hallo de status van een service-entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="3c99e-235">Het bevat Hallo partitie statussen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-235">It contains hello partition health states.</span></span> <span data-ttu-id="3c99e-236">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-236">Input:</span></span>

* <span data-ttu-id="3c99e-237">[Vereist] Hallo servicenaam (URI) dat Hallo service identificeert.</span><span class="sxs-lookup"><span data-stu-id="3c99e-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="3c99e-238">[Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="3c99e-239">[Optioneel] Filters voor gebeurtenissen en partities die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-240">Alle gebeurtenissen en partities zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="3c99e-241">[Optioneel] Filter tooexclude health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="3c99e-242">Als niet wordt opgegeven, Hallo health statistieken weergeven Hallo ok, waarschuwing en fout tellen voor alle partities en replica's van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="3c99e-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-243">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-243">API</span></span>
<span data-ttu-id="3c99e-244">servicestatus tooget via Hallo-API maken een `FabricClient` en aanroep Hallo [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="3c99e-245">Hallo wordt volgende voorbeeld Hallo status van een service met de opgegeven service-naam (URI):</span><span class="sxs-lookup"><span data-stu-id="3c99e-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="3c99e-246">Hallo volgende code haalt Hallo servicestatus voor de opgegeven servicenaam hello (URI), filters en aangepast beleid via geven [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="3c99e-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="3c99e-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-247">PowerShell</span></span>
<span data-ttu-id="3c99e-248">Hallo cmdlet tooget Hallo-servicestatus is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="3c99e-249">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-250">Hallo-servicestatus Hallo volgende cmdlet opgehaald met behulp van standaard statusbeleid:</span><span class="sxs-lookup"><span data-stu-id="3c99e-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-251">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-251">REST</span></span>
<span data-ttu-id="3c99e-252">U krijgt de status van de service met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="3c99e-253">Status van de partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-253">Get partition health</span></span>
<span data-ttu-id="3c99e-254">Retourneert Hallo de status van een entiteit van de partitie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="3c99e-255">Het bevat Hallo replica statussen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-255">It contains hello replica health states.</span></span> <span data-ttu-id="3c99e-256">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-256">Input:</span></span>

* <span data-ttu-id="3c99e-257">[Vereist] Hallo partitie-ID (GUID) die Hallo partitie identificeert.</span><span class="sxs-lookup"><span data-stu-id="3c99e-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="3c99e-258">[Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="3c99e-259">[Optioneel] Filters voor gebeurtenissen en replica's die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-260">Alle gebeurtenissen en replica's zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="3c99e-261">[Optioneel] Filter tooexclude health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="3c99e-262">Als niet wordt opgegeven, wordt Hallo health statistieken weergeven hoeveel replica's in ok, waarschuwing en fout statussen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-263">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-263">API</span></span>
<span data-ttu-id="3c99e-264">tooget partitie health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="3c99e-265">maken van de volgende optionele parameters toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="3c99e-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="3c99e-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-266">PowerShell</span></span>
<span data-ttu-id="3c99e-267">Hallo cmdlet tooget Hallo partitie status is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="3c99e-268">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-269">Hallo volgende cmdlet opgehaald Hallo status voor alle partities van Hallo **fabric: / WordCount/WordCountService** -service en uitsluit replica statussen:</span><span class="sxs-lookup"><span data-stu-id="3c99e-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="rest"></a><span data-ttu-id="3c99e-270">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-270">REST</span></span>
<span data-ttu-id="3c99e-271">U kunt de status van de partitie met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="3c99e-272">De status replica ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-272">Get replica health</span></span>
<span data-ttu-id="3c99e-273">Hallo-status van de replica van een stateful service of een staatloze service-exemplaar geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="3c99e-274">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-274">Input:</span></span>

* <span data-ttu-id="3c99e-275">[Vereist] Hallo partitie-ID (GUID) en de replica-ID die Hallo replica identificeert.</span><span class="sxs-lookup"><span data-stu-id="3c99e-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="3c99e-276">[Optioneel] Hallo application health beleidsparameters gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="3c99e-277">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-278">Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-279">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-279">API</span></span>
<span data-ttu-id="3c99e-280">tooget hello replica health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="3c99e-281">geavanceerde parameters, gebruik toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="3c99e-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="3c99e-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-282">PowerShell</span></span>
<span data-ttu-id="3c99e-283">Hallo cmdlet tooget Hallo replica de status is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="3c99e-284">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-285">Hallo volgende cmdlet opgehaald Hallo status van de primaire replica Hallo voor alle partities van Hallo-service:</span><span class="sxs-lookup"><span data-stu-id="3c99e-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-286">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-286">REST</span></span>
<span data-ttu-id="3c99e-287">U krijgt de status replica met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="3c99e-288">Status van de geïmplementeerde toepassing ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-288">Get deployed application health</span></span>
<span data-ttu-id="3c99e-289">Retourneert Hallo de status van een toepassing is geïmplementeerd op een knooppunt-entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="3c99e-290">Het bevat Hallo geïmplementeerd service pakket statussen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="3c99e-291">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-291">Input:</span></span>

* <span data-ttu-id="3c99e-292">Naam van de toepassing [vereist] hello (URI) en knooppuntnaam (tekenreeks) die Hallo identificeren toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="3c99e-293">[Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="3c99e-294">[Optioneel] Filters voor gebeurtenissen en geïmplementeerde servicepakketten die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-295">Alle gebeurtenissen en geïmplementeerde servicepakketten zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="3c99e-296">[Optioneel] Filter tooexclude health statistieken.</span><span class="sxs-lookup"><span data-stu-id="3c99e-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="3c99e-297">Als niet wordt opgegeven, weergeven Hallo health statistieken Hallo aantal geïmplementeerde servicepakketten in de status ok, waarschuwing en fout.</span><span class="sxs-lookup"><span data-stu-id="3c99e-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-298">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-298">API</span></span>
<span data-ttu-id="3c99e-299">tooget hello status van een toepassing is geïmplementeerd op een knooppunt via Hallo-API maken een `FabricClient` en aanroep Hallo [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="3c99e-300">optionele parameters toospecify, gebruik [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="3c99e-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="3c99e-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-301">PowerShell</span></span>
<span data-ttu-id="3c99e-302">Hallo cmdlet tooget Hallo geïmplementeerd toepassingsstatus is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="3c99e-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="3c99e-303">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="3c99e-304">toofind uit waarop een toepassing wordt geïmplementeerd, voeren [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en bekijkt hello kinderen toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="3c99e-305">Hallo volgende cmdlet opgehaald Hallo health Hallo **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="3c99e-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="3c99e-306">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-306">REST</span></span>
<span data-ttu-id="3c99e-307">U krijgt de status geïmplementeerde toepassing met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="3c99e-308">Status van geïmplementeerde service pakket ophalen</span><span class="sxs-lookup"><span data-stu-id="3c99e-308">Get deployed service package health</span></span>
<span data-ttu-id="3c99e-309">Retourneert Hallo status van een geïmplementeerde service pakket entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="3c99e-310">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-310">Input:</span></span>

* <span data-ttu-id="3c99e-311">[Vereist] Hallo toepassingsnaam (URI), knooppuntnaam (tekenreeks) en manifest servicenaam (tekenreeks) die Hallo identificeren geïmplementeerd servicepakket.</span><span class="sxs-lookup"><span data-stu-id="3c99e-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="3c99e-312">[Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="3c99e-313">[Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten).</span><span class="sxs-lookup"><span data-stu-id="3c99e-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="3c99e-314">Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="3c99e-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-315">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-315">API</span></span>
<span data-ttu-id="3c99e-316">tooget hello status van een geïmplementeerde servicepakket via Hallo-API maken een `FabricClient` en aanroep Hallo [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) methode op de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="3c99e-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="3c99e-317">optionele parameters toospecify, gebruik [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="3c99e-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="3c99e-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-318">PowerShell</span></span>
<span data-ttu-id="3c99e-319">Hallo cmdlet tooget Hallo geïmplementeerd servicestatus-pakket is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="3c99e-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="3c99e-320">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="3c99e-321">toosee waarop een toepassing wordt geïmplementeerd, voeren [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en bekijkt hello geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="3c99e-322">toosee die servicepakketten in een toepassing, zoekt u naar op Hallo geïmplementeerd service pakket kinderen in Hallo [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3c99e-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="3c99e-323">Hallo volgende cmdlet opgehaald Hallo health Hallo **WordCountServicePkg** servicepakket Hallo **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="3c99e-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="3c99e-324">Hallo entiteit heeft **System.Hosting** rapporten voor geslaagde pakket service en ingangspunt activering en succesvolle registratie van het type van de service.</span><span class="sxs-lookup"><span data-stu-id="3c99e-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="3c99e-325">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-325">REST</span></span>
<span data-ttu-id="3c99e-326">U kunt de status van de geïmplementeerde service pakket met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="3c99e-327">Health chunk query 's</span><span class="sxs-lookup"><span data-stu-id="3c99e-327">Health chunk queries</span></span>
<span data-ttu-id="3c99e-328">Hallo health chunk query's kunnen cluster met meerdere niveaus van kinderen (recursief) per invoer filters worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="3c99e-329">Ondersteunt geavanceerde filters waarmee een grote flexibiliteit bij het kiezen van de onderliggende hello toobe geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="3c99e-330">Hallo filters kunnen onderliggende items met de unieke id Hallo of door andere groeps-id's en/of de statussen opgeven.</span><span class="sxs-lookup"><span data-stu-id="3c99e-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="3c99e-331">Geen onderliggende elementen zijn standaard opgenomen als tegengestelde toohealth-opdrachten die altijd eerste niveau onderliggende elementen bevatten.</span><span class="sxs-lookup"><span data-stu-id="3c99e-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="3c99e-332">Hallo [statusquery's](service-fabric-view-entities-aggregated-health.md#health-queries) return alleen eerste niveau kinderen Hallo opgegeven entiteit per vereist filters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="3c99e-333">tooget hello kinderen van onderliggende items hello, moet u extra health API's voor elke entiteit van belang aanroepen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="3c99e-334">Op deze manier tooget Hallo status van specifieke entiteiten, moet u aanroepen één health API voor elke gewenste entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="3c99e-335">Hallo chunk geavanceerde filteren kunt u query toorequest meerdere items in één query op het Hallo-berichtgrootte en Hallo aantal berichten voor het minimaliseren van belang.</span><span class="sxs-lookup"><span data-stu-id="3c99e-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="3c99e-336">Hallo-waarde van Hallo chunk query is dat u de status voor meer cluster entiteiten (mogelijk alle cluster entiteiten starten in de hoofdmap van de vereiste) kunt krijgen in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="3c99e-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="3c99e-337">U kunt de gezondheid van complexe query zoals express:</span><span class="sxs-lookup"><span data-stu-id="3c99e-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="3c99e-338">Retour alleen toepassingen in de fout en voor die toepassingen bevatten alle services in waarschuwing of fout.</span><span class="sxs-lookup"><span data-stu-id="3c99e-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="3c99e-339">Voor de geretourneerde services omvatten alle partities.</span><span class="sxs-lookup"><span data-stu-id="3c99e-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="3c99e-340">Alleen Hallo status van de opgegeven door de namen van de vier toepassingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="3c99e-341">Alleen Hallo status van toepassingen van een type van de gewenste toepassing retourneren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="3c99e-342">Retourneert alle geïmplementeerde entiteiten op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="3c99e-343">Retourneert alle toepassingen, alle geïmplementeerde toepassingen op Hallo opgegeven knooppunt en alle Hallo geïmplementeerde servicepakketten op dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="3c99e-344">Alle replica's in een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-344">Return all replicas in error.</span></span> <span data-ttu-id="3c99e-345">Retourneert alle toepassingen, services, partities en alleen replica's in de fout.</span><span class="sxs-lookup"><span data-stu-id="3c99e-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="3c99e-346">Retourneren van alle toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-346">Return all applications.</span></span> <span data-ttu-id="3c99e-347">Voor een opgegeven service omvatten alle partities.</span><span class="sxs-lookup"><span data-stu-id="3c99e-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="3c99e-348">Hallo health chunk query is momenteel toegankelijk alleen voor Hallo cluster entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="3c99e-349">Een cluster health chunk, waarin wordt:</span><span class="sxs-lookup"><span data-stu-id="3c99e-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="3c99e-350">Hallo cluster geaggregeerd status.</span><span class="sxs-lookup"><span data-stu-id="3c99e-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="3c99e-351">Hallo health status chunk lijst met knooppunten die fungeren als invoer filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="3c99e-352">Hallo health status chunk lijst met toepassingen die invoer filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="3c99e-353">Elk segment application health-status bevat een lijst chunk met alle services die respecteren invoer filters en een chunk-lijst met alle geïmplementeerde toepassingen die Hallo filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="3c99e-354">Hetzelfde voor Hallo onderliggende elementen van services en geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="3c99e-355">Op deze manier alle entiteiten in Hallo cluster kunnen worden mogelijk geretourneerd als in een hiërarchische aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="3c99e-356">Cluster health chunk query</span><span class="sxs-lookup"><span data-stu-id="3c99e-356">Cluster health chunk query</span></span>
<span data-ttu-id="3c99e-357">Retourneert Hallo health van Hallo cluster entiteit en Hallo hiërarchische health status segmenten van vereiste onderliggende items bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="3c99e-358">Invoer:</span><span class="sxs-lookup"><span data-stu-id="3c99e-358">Input:</span></span>

* <span data-ttu-id="3c99e-359">[Optioneel] Hallo cluster statusbeleid gebruikt tooevaluate Hallo knooppunten en Hallo Clustergebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="3c99e-360">[Optioneel] Hallo application health beleid kaart gebruikt toooverride Hallo application manifest beleid met Hallo statusbeleid.</span><span class="sxs-lookup"><span data-stu-id="3c99e-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="3c99e-361">[Optioneel] Filters voor knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="3c99e-362">Hallo filters specifieke tooan entiteit of groep van entiteiten zijn of zijn van toepassing tooall entiteiten op dat niveau.</span><span class="sxs-lookup"><span data-stu-id="3c99e-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="3c99e-363">lijst met filters Hallo kan bevatten één algemene filter en/of filters voor specifieke id's toofine-gebruikerssegmentatie entiteiten die door Hallo query zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="3c99e-364">Als u niets opgeeft, worden niet Hallo kinderen standaard geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="3c99e-365">Meer informatie over filters op Hallo [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) en [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="3c99e-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="3c99e-366">Hallo toepassing filters kunnen recursief geavanceerde filters voor kinderen opgeven.</span><span class="sxs-lookup"><span data-stu-id="3c99e-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="3c99e-367">Hallo chunk resultaat bevat Hallo onderliggende items waarvan Hallo filters respecteren.</span><span class="sxs-lookup"><span data-stu-id="3c99e-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="3c99e-368">Hallo chunk query retourneert op dit moment geen slechte evaluaties of entiteit gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="3c99e-369">Deze extra informatie kan worden verkregen met behulp van Hallo bestaande cluster health query.</span><span class="sxs-lookup"><span data-stu-id="3c99e-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="3c99e-370">API</span><span class="sxs-lookup"><span data-stu-id="3c99e-370">API</span></span>
<span data-ttu-id="3c99e-371">tooget cluster health Segmentselectie, maakt u een `FabricClient` en aanroep Hallo [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) methode op de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="3c99e-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="3c99e-372">U kunt doorgeven [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe statusbeleid en geavanceerde filters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="3c99e-373">Hallo haalt volgende code cluster health chunk met geavanceerde filters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="3c99e-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c99e-374">PowerShell</span></span>
<span data-ttu-id="3c99e-375">Hallo cmdlet tooget Hallo cluster status is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="3c99e-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="3c99e-376">Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c99e-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="3c99e-377">Hallo haalt volgende code knooppunten alleen als deze fout, met uitzondering van een specifiek knooppunt dat moet altijd worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="3c99e-378">Hallo volgende cmdlet haalt cluster chunk met toepassingsfilters.</span><span class="sxs-lookup"><span data-stu-id="3c99e-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="3c99e-379">Hallo retourneert volgende cmdlet alle geïmplementeerde entiteiten op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="3c99e-380">REST</span><span class="sxs-lookup"><span data-stu-id="3c99e-380">REST</span></span>
<span data-ttu-id="3c99e-381">U krijgt cluster health chunk gevonden met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) die statusbeleid en geavanceerde filters beschreven in de hoofdtekst van het Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="3c99e-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="3c99e-382">Algemene query 's</span><span class="sxs-lookup"><span data-stu-id="3c99e-382">General queries</span></span>
<span data-ttu-id="3c99e-383">Algemene query's retourneren een lijst met Service Fabric-entiteiten van een bepaald type.</span><span class="sxs-lookup"><span data-stu-id="3c99e-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="3c99e-384">Ze worden weergegeven via Hallo API (via de methoden op Hallo **FabricClient.QueryManager**), PowerShell-cmdlets en REST.</span><span class="sxs-lookup"><span data-stu-id="3c99e-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="3c99e-385">Deze query's samenvoegen subquery's uit meerdere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="3c99e-386">Een van beide is Hallo [health store](service-fabric-health-introduction.md#health-store), de status voor elke queryresultaat die Hallo gevuld geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="3c99e-387">Algemene query's terug Hallo geaggregeerd status van de entiteit Hallo en bevatten geen uitgebreide statusgegevens.</span><span class="sxs-lookup"><span data-stu-id="3c99e-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="3c99e-388">Als u een entiteit is niet in orde, kunt u volgen met health-query's tooget alle de health-gegevens, inclusief gebeurtenissen, onderliggende statussen en slecht evaluaties.</span><span class="sxs-lookup"><span data-stu-id="3c99e-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="3c99e-389">Als algemene query's een onbekende status voor een entiteit retourneren, is het mogelijk dat Hallo health store bevat geen volledige gegevens over Hallo entiteit.</span><span class="sxs-lookup"><span data-stu-id="3c99e-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="3c99e-390">Het is ook mogelijk dat een subquery toohello health store niet geslaagd is (bijvoorbeeld: Er is een communicatiefout opgetreden of Hallo health store is beperkt).</span><span class="sxs-lookup"><span data-stu-id="3c99e-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="3c99e-391">Een health-query voor de entiteit Hallo opvolgen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="3c99e-392">Als de subquery Hallo tijdelijke fouten, zoals netwerkproblemen optreden, kan deze vervolgzelfstudie query slagen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="3c99e-393">Ook kan geven u meer informatie uit health store Hallo over waarom Hallo entiteit is niet beschikbaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="3c99e-394">query's met Hallo **HealthState** voor entiteiten zijn:</span><span class="sxs-lookup"><span data-stu-id="3c99e-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="3c99e-395">Lijst met knooppunten: retourneert Hallo lijst met knooppunten in Hallo-cluster (wisselbare).</span><span class="sxs-lookup"><span data-stu-id="3c99e-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="3c99e-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="3c99e-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="3c99e-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="3c99e-398">Lijst met toepassingen: retourneert Hallo lijst met toepassingen in Hallo-cluster (wisselbare).</span><span class="sxs-lookup"><span data-stu-id="3c99e-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="3c99e-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="3c99e-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="3c99e-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="3c99e-401">Lijst met Services: retourneert Hallo lijst met services in een toepassing (wisselbare).</span><span class="sxs-lookup"><span data-stu-id="3c99e-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="3c99e-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="3c99e-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="3c99e-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="3c99e-404">Lijst met partitie: retourneert Hallo lijst met partities in een service (wisselbare).</span><span class="sxs-lookup"><span data-stu-id="3c99e-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="3c99e-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="3c99e-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="3c99e-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="3c99e-407">Lijst met replica's: retourneert Hallo lijst met replica's in een partitie (wisselbare).</span><span class="sxs-lookup"><span data-stu-id="3c99e-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="3c99e-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="3c99e-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="3c99e-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="3c99e-410">Lijst met toepassingen geïmplementeerd: retourneert Hallo lijst met geïmplementeerde toepassingen op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="3c99e-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="3c99e-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="3c99e-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="3c99e-413">De lijst van de service-pakket wordt geïmplementeerd: retourneert Hallo lijst met servicepakketten in een geïmplementeerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="3c99e-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="3c99e-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="3c99e-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="3c99e-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="3c99e-416">Hallo zoekopdrachten wisselbare resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="3c99e-417">Hallo retourtype van deze query's is een lijst die is afgeleid van [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="3c99e-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="3c99e-418">Hallo resultaten een bericht niet passen, alleen een pagina wordt geretourneerd als een ContinuationToken die houdt waarin de opsomming is gestopt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="3c99e-419">Blijven toocall Hallo dezelfde query- en in vervolgtoken Hallo van Hallo vorige tooget volgende queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="3c99e-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="3c99e-420">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="3c99e-420">Examples</span></span>
<span data-ttu-id="3c99e-421">Hallo volgende code wordt opgehaald Hallo slecht toepassingen in Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="3c99e-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="3c99e-422">Hallo volgende cmdlet opgehaald Hallo toepassingsgegevens voor Hallo fabric: / WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="3c99e-423">U ziet dat de status op de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="3c99e-424">Hallo volgende cmdlet opgehaald Hallo services met een status van de fout:</span><span class="sxs-lookup"><span data-stu-id="3c99e-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="3c99e-425">Cluster en de toepassing upgrades</span><span class="sxs-lookup"><span data-stu-id="3c99e-425">Cluster and application upgrades</span></span>
<span data-ttu-id="3c99e-426">Tijdens een bewaakte upgrade van het Hallo-cluster en de toepassing controleert Service Fabric health tooensure dat alles in orde blijft.</span><span class="sxs-lookup"><span data-stu-id="3c99e-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="3c99e-427">Als een entiteit niet in orde is als geëvalueerd met behulp van de geconfigureerde statusbeleid, geldt Hallo upgrade upgrade-specifiek beleid toodetermine Hallo volgende actie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="3c99e-428">Hallo upgrade mogelijk onderbroken tooallow gebruikersinteractie (zoals de vaststelling van de fout of wijzigen van beleid) of het mogelijk automatisch terugdraaien toohello vorige goede versie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="3c99e-429">Tijdens een *cluster* bijwerkt, kunt u Hallo cluster upgradestatus krijgen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="3c99e-430">Hallo upgradestatus omvat slecht evaluaties, welke toowhat punt niet in orde in Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="3c99e-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="3c99e-431">Als het Hallo-upgrade is teruggedraaid vanwege toohealth problemen, onthoudt upgradestatus Hallo Hallo laatste slecht redenen.</span><span class="sxs-lookup"><span data-stu-id="3c99e-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="3c99e-432">Deze informatie kunt beheerders onderzoeken wat er mis ging nadat het Hallo-upgrade is teruggedraaid of gestopt.</span><span class="sxs-lookup"><span data-stu-id="3c99e-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="3c99e-433">Op deze manier tijdens een *toepassing* bijwerkt, alle slechte beoordelingen zijn opgenomen in upgradestatus Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="3c99e-434">Hallo hieronder vindt u upgradestatus Hallo-toepassing voor een gewijzigde fabric: / WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c99e-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="3c99e-435">Een watchdog heeft een fout gerapporteerd op een van de replica's.</span><span class="sxs-lookup"><span data-stu-id="3c99e-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="3c99e-436">Hallo upgrade ongedaan omdat Hallo statuscontroles niet worden nageleefd.</span><span class="sxs-lookup"><span data-stu-id="3c99e-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="3c99e-437">Lees meer over Hallo [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="3c99e-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="3c99e-438">Gebruik health evaluaties tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="3c99e-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="3c99e-439">Wanneer er een probleem met het Hallo-cluster of een toepassing, bekijkt hello cluster of de toepassing health toopinpoint wat is het probleem.</span><span class="sxs-lookup"><span data-stu-id="3c99e-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="3c99e-440">Hallo slecht evaluaties bieden informatie over welke triggered Hallo huidige slecht.</span><span class="sxs-lookup"><span data-stu-id="3c99e-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="3c99e-441">Als u wilt, kunt u inzoomen op Hallo hoofdoorzaak voor beschadigde onderliggende entiteiten tooidentify.</span><span class="sxs-lookup"><span data-stu-id="3c99e-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="3c99e-442">Neem bijvoorbeeld een toepassing slecht omdat er een foutenrapport op een van de replica's.</span><span class="sxs-lookup"><span data-stu-id="3c99e-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="3c99e-443">Hallo toont volgende Powershell-cmdlet Hallo slecht evaluaties:</span><span class="sxs-lookup"><span data-stu-id="3c99e-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="3c99e-444">U kunt bekijkt hello replica tooget meer informatie:</span><span class="sxs-lookup"><span data-stu-id="3c99e-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="3c99e-445">Hallo slecht evaluaties weergeven Hallo eerste reden Hallo entiteit is geëvalueerd toocurrent status heeft.</span><span class="sxs-lookup"><span data-stu-id="3c99e-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="3c99e-446">Mogelijk zijn er meerdere andere gebeurtenissen die deze status activeren, maar worden ze niet worden doorgevoerd in Hallo evaluaties.</span><span class="sxs-lookup"><span data-stu-id="3c99e-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="3c99e-447">tooget zoomen op Hallo health entiteiten toofigure uit alle slechte Hallo-rapporten in Hallo-cluster met meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c99e-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3c99e-448">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c99e-448">Next steps</span></span>
[<span data-ttu-id="3c99e-449">Gebruik system health rapporten tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="3c99e-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="3c99e-450">Aangepaste Service Fabric-statusrapporten toevoegen</span><span class="sxs-lookup"><span data-stu-id="3c99e-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="3c99e-451">Hoe tooreport en controleer health service</span><span class="sxs-lookup"><span data-stu-id="3c99e-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="3c99e-452">Controle en diagnose van lokaal services</span><span class="sxs-lookup"><span data-stu-id="3c99e-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="3c99e-453">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="3c99e-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
