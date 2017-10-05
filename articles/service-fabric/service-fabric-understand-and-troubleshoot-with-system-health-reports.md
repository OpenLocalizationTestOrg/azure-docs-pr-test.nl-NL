---
title: Problemen oplossen met systeemstatusrapporten | Microsoft Docs
description: Hierin wordt beschreven in de statusrapporten dat is verzonden door Azure Service Fabric-onderdelen en hun gebruik voor het oplossen van problemen cluster of problemen met de toepassing.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="5d457-103">Systeemstatusrapporten gebruiken om fouten op te lossen</span><span class="sxs-lookup"><span data-stu-id="5d457-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="5d457-104">Azure Service Fabric-onderdelen rapport gebruiksklaar op alle entiteiten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="5d457-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="5d457-105">De [health store](service-fabric-health-introduction.md#health-store) maken en verwijderen van de entiteiten die zijn gebaseerd op systeemrapporten van het.</span><span class="sxs-lookup"><span data-stu-id="5d457-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="5d457-106">Ook ordent ze in een hiërarchie die entiteit interacties worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="5d457-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="5d457-107">Om te begrijpen health-gerelateerde begrippen, leest u meer op [Service Fabric-statusmodel](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d457-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="5d457-108">Systeemstatusrapporten bieden inzicht in het cluster en de functionaliteit van de toepassing en de vlag problemen via health.</span><span class="sxs-lookup"><span data-stu-id="5d457-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="5d457-109">Voor toepassingen en services controleren systeemstatusrapporten of entiteiten worden geïmplementeerd en correct vanuit het perspectief van de Service Fabric werkt zijn.</span><span class="sxs-lookup"><span data-stu-id="5d457-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="5d457-110">De rapporten bieden een statuscontrole van de zakelijke logica van de service of detectie van vastgelopen processen.</span><span class="sxs-lookup"><span data-stu-id="5d457-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="5d457-111">Services van de gebruiker kunnen de health-gegevens met informatie die specifiek zijn voor hun logica aanvullen.</span><span class="sxs-lookup"><span data-stu-id="5d457-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="5d457-112">Statusrapporten watchdogs zijn alleen zichtbaar *nadat* Maak een entiteit van de onderdelen van het systeem.</span><span class="sxs-lookup"><span data-stu-id="5d457-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="5d457-113">Wanneer een entiteit wordt verwijderd, worden alle statusrapporten gekoppeld in de health store automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5d457-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="5d457-114">Geldt ook wanneer een nieuw exemplaar van de entiteit is gemaakt (bijvoorbeeld een nieuw exemplaar van de service voor stateful persistente-replica is gemaakt).</span><span class="sxs-lookup"><span data-stu-id="5d457-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="5d457-115">Alle rapporten die zijn gekoppeld aan het oude exemplaar worden verwijderd en opgeschoond vanuit de store.</span><span class="sxs-lookup"><span data-stu-id="5d457-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="5d457-116">Het systeemonderdeel rapporten zijn geïdentificeerd door de bron die met begint de '**System.**'</span><span class="sxs-lookup"><span data-stu-id="5d457-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="5d457-117">voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="5d457-117">prefix.</span></span> <span data-ttu-id="5d457-118">Watchdogs niet hetzelfde voorvoegsel gebruiken voor hun bronnen, zoals rapporten met ongeldige parameters worden afgewezen.</span><span class="sxs-lookup"><span data-stu-id="5d457-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="5d457-119">Bekijken we enkele systeemrapporten om te begrijpen wat ze activeert en hoe u de mogelijke problemen die ze vertegenwoordigen te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="5d457-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="5d457-120">Service Fabric blijft rapporten van de voorwaarden van belang ter verbetering van de zichtbaarheid van wat in het cluster en de toepassing gebeurt er toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5d457-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="5d457-121">Bestaande rapporten kunnen ook worden uitgebreid met meer details bij het oplossen van het probleem sneller.</span><span class="sxs-lookup"><span data-stu-id="5d457-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="5d457-122">Systeemstatusrapporten cluster</span><span class="sxs-lookup"><span data-stu-id="5d457-122">Cluster system health reports</span></span>
<span data-ttu-id="5d457-123">De entiteit van de health cluster wordt automatisch gemaakt in de health store.</span><span class="sxs-lookup"><span data-stu-id="5d457-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="5d457-124">Als alles goed werkt, heeft geen system-rapport.</span><span class="sxs-lookup"><span data-stu-id="5d457-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="5d457-125">Verlies van groep</span><span class="sxs-lookup"><span data-stu-id="5d457-125">Neighborhood loss</span></span>
<span data-ttu-id="5d457-126">**System.Federation** meldt fout wanneer er een groep verlies wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="5d457-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="5d457-127">Het rapport is van afzonderlijke knooppunten en de knooppunt-ID is opgenomen in de eigenschapsnaam.</span><span class="sxs-lookup"><span data-stu-id="5d457-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="5d457-128">Als een groep in de hele Service Fabric-ring verbroken is, kunt u doorgaans twee gebeurtenissen (beide zijden van het rapport gap) verwachten.</span><span class="sxs-lookup"><span data-stu-id="5d457-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="5d457-129">Als er meer groepen verloren gaan, moet u er meer gebeurtenissen zijn.</span><span class="sxs-lookup"><span data-stu-id="5d457-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="5d457-130">Het rapport geeft de algemene lease time-out als time to live.</span><span class="sxs-lookup"><span data-stu-id="5d457-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="5d457-131">Het rapport opnieuw elke helft van de duur van de TTL voor verzonden als de voorwaarde actief blijft.</span><span class="sxs-lookup"><span data-stu-id="5d457-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="5d457-132">De gebeurtenis wordt automatisch verwijderd wanneer het verloopt.</span><span class="sxs-lookup"><span data-stu-id="5d457-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="5d457-133">Verwijder wanneer verlopen gedrag zorgt ervoor dat het rapport wordt opgeschoond van de health store correct, zelfs als het reporting knooppunt niet actief is.</span><span class="sxs-lookup"><span data-stu-id="5d457-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="5d457-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="5d457-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="5d457-135">**De eigenschap**: begint met **groep** en bevat knooppuntgegevens</span><span class="sxs-lookup"><span data-stu-id="5d457-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="5d457-136">**Volgende stappen**: onderzoeken waarom de groep wordt verbroken (bijvoorbeeld de communicatie tussen clusterknooppunten controleren).</span><span class="sxs-lookup"><span data-stu-id="5d457-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="5d457-137">Systeemstatusrapporten knooppunt</span><span class="sxs-lookup"><span data-stu-id="5d457-137">Node system health reports</span></span>
<span data-ttu-id="5d457-138">**System.FM**, die staat voor de Failover Manager service, wordt de instantie die het beheer van informatie over de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="5d457-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="5d457-139">Elk knooppunt moet één rapport van System.FM met de status hebben.</span><span class="sxs-lookup"><span data-stu-id="5d457-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="5d457-140">De knooppunt-entiteiten worden verwijderd wanneer de knooppuntstatus wordt verwijderd (Zie [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="5d457-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="5d457-141">Knooppunt omhoog/omlaag</span><span class="sxs-lookup"><span data-stu-id="5d457-141">Node up/down</span></span>
<span data-ttu-id="5d457-142">System.FM rapporteert als OK als lid van het knooppunt de ring (dit is actief en werkend).</span><span class="sxs-lookup"><span data-stu-id="5d457-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="5d457-143">Een fout gemeld wanneer het knooppunt de ring vertrekt (service niet actief is, ofwel voor het upgraden of gewoon omdat deze is mislukt).</span><span class="sxs-lookup"><span data-stu-id="5d457-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="5d457-144">De health-hiërarchie gebouwd door de health store neemt actie geïmplementeerde entiteiten in correlatie met System.FM knooppunt rapporten.</span><span class="sxs-lookup"><span data-stu-id="5d457-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="5d457-145">Er vanuit het knooppunt een bovenliggende virtuele van alle geïmplementeerde entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5d457-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="5d457-146">De geïmplementeerde entiteiten op dat knooppunt worden weergegeven via query's of het knooppunt als bedrijfs is gemeld door System.FM met hetzelfde exemplaar als de instantie die is gekoppeld aan de entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5d457-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="5d457-147">Wanneer System.FM meldt dat het knooppunt niet beschikbaar is of opnieuw opgestart (een nieuw exemplaar), de health store de geïmplementeerde entiteiten die kunnen bestaan alleen op het knooppunt omlaag of op het vorige exemplaar van het knooppunt automatisch opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="5d457-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="5d457-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5d457-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5d457-149">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="5d457-149">**Property**: State</span></span>
* <span data-ttu-id="5d457-150">**Volgende stappen**: als het knooppunt niet actief voor een upgrade is, deze moet terugkeren nadat de upgrade is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d457-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="5d457-151">In dit geval wordt moet de status overschakelen naar OK.</span><span class="sxs-lookup"><span data-stu-id="5d457-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="5d457-152">Als het knooppunt niet u terug keert of deze is mislukt, moet het probleem meer onderzoek.</span><span class="sxs-lookup"><span data-stu-id="5d457-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="5d457-153">Het volgende voorbeeld ziet de gebeurtenis System.FM met een status OK voor knooppunt:</span><span class="sxs-lookup"><span data-stu-id="5d457-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="5d457-154">Vervaldatum van het certificaat</span><span class="sxs-lookup"><span data-stu-id="5d457-154">Certificate expiration</span></span>
<span data-ttu-id="5d457-155">**System.FabricNode** rapporten van een waarschuwing wanneer certificaten worden gebruikt door het knooppunt bijna is verlopen zijn.</span><span class="sxs-lookup"><span data-stu-id="5d457-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="5d457-156">Er zijn drie certificaten per knooppunt: **Certificate_cluster**, **Certificate_server**, en **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="5d457-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="5d457-157">Wanneer de vervaldatum ten minste twee weken is, is de status van het rapport OK.</span><span class="sxs-lookup"><span data-stu-id="5d457-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="5d457-158">Wanneer de vervaldatum binnen twee weken is, is het rapporttype dat een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5d457-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="5d457-159">TTL van deze gebeurtenissen is oneindig, en ze worden verwijderd wanneer een knooppunt de cluster verlaat.</span><span class="sxs-lookup"><span data-stu-id="5d457-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="5d457-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="5d457-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="5d457-161">**De eigenschap**: begint met **certificaat** en bevat meer informatie over het certificaattype</span><span class="sxs-lookup"><span data-stu-id="5d457-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="5d457-162">**Volgende stappen**: bijwerken van de certificaten als ze bijna is verlopen zijn.</span><span class="sxs-lookup"><span data-stu-id="5d457-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="5d457-163">Schending van de Load-capaciteit</span><span class="sxs-lookup"><span data-stu-id="5d457-163">Load capacity violation</span></span>
<span data-ttu-id="5d457-164">De Service Fabric Load Balancer rapporten in een waarschuwing wanneer er een schending van de capaciteit knooppunt wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="5d457-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="5d457-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5d457-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5d457-166">**De eigenschap**: begint met **capaciteit**</span><span class="sxs-lookup"><span data-stu-id="5d457-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="5d457-167">**Volgende stappen**: Controleer of de opgegeven metrische gegevens en de huidige capaciteit op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5d457-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="5d457-168">Systeemstatusrapporten toepassing</span><span class="sxs-lookup"><span data-stu-id="5d457-168">Application system health reports</span></span>
<span data-ttu-id="5d457-169">**System.CM**, die staat voor de Cluster Manager-service, wordt de instantie van die gegevens over een toepassing beheert.</span><span class="sxs-lookup"><span data-stu-id="5d457-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="5d457-170">Status</span><span class="sxs-lookup"><span data-stu-id="5d457-170">State</span></span>
<span data-ttu-id="5d457-171">System.CM rapporteert als OK wanneer de toepassing heeft gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5d457-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="5d457-172">Informeert de health store wanneer de toepassing is verwijderd, zodat het kan worden verwijderd uit de store.</span><span class="sxs-lookup"><span data-stu-id="5d457-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="5d457-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="5d457-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="5d457-174">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="5d457-174">**Property**: State</span></span>
* <span data-ttu-id="5d457-175">**Volgende stappen**: als de toepassing is gemaakt of bijgewerkt, moet deze het statusrapport Clusterbeheer opnemen.</span><span class="sxs-lookup"><span data-stu-id="5d457-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="5d457-176">Bekijk anders de status van de toepassing door uitgifte van een query (bijvoorbeeld de PowerShell-cmdlet **Get-ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="5d457-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="5d457-177">Het volgende voorbeeld ziet u de gebeurtenis status op de **fabric: / WordCount** toepassing:</span><span class="sxs-lookup"><span data-stu-id="5d457-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="5d457-178">Systeemstatusrapporten service</span><span class="sxs-lookup"><span data-stu-id="5d457-178">Service system health reports</span></span>
<span data-ttu-id="5d457-179">**System.FM**, die staat voor de service Failover Manager is de instantie die informatie over services beheert.</span><span class="sxs-lookup"><span data-stu-id="5d457-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="5d457-180">Status</span><span class="sxs-lookup"><span data-stu-id="5d457-180">State</span></span>
<span data-ttu-id="5d457-181">System.FM rapporteert als OK wanneer de service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d457-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="5d457-182">Worden verwijderd de entiteit van de health store wanneer de service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5d457-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="5d457-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5d457-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5d457-184">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="5d457-184">**Property**: State</span></span>

<span data-ttu-id="5d457-185">Het volgende voorbeeld ziet u de gebeurtenis status van de service **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="5d457-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="5d457-186">Fout van de correlatie-service</span><span class="sxs-lookup"><span data-stu-id="5d457-186">Service correlation error</span></span>
<span data-ttu-id="5d457-187">**System.PLB** meldt fout wanneer er wordt gedetecteerd dat een affiniteitsketen bijwerken van een service worden gecorreleerd met een andere service maakt.</span><span class="sxs-lookup"><span data-stu-id="5d457-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="5d457-188">Het rapport wordt gewist wanneer geslaagde update gebeurt.</span><span class="sxs-lookup"><span data-stu-id="5d457-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="5d457-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5d457-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5d457-190">**De eigenschap**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="5d457-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="5d457-191">**Volgende stappen**: Controleer de servicebeschrijvingen van gecorreleerde.</span><span class="sxs-lookup"><span data-stu-id="5d457-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="5d457-192">Systeemstatusrapporten partitie</span><span class="sxs-lookup"><span data-stu-id="5d457-192">Partition system health reports</span></span>
<span data-ttu-id="5d457-193">**System.FM**, die staat voor de service Failover Manager is de instantie die informatie over servicepartities beheert.</span><span class="sxs-lookup"><span data-stu-id="5d457-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="5d457-194">Status</span><span class="sxs-lookup"><span data-stu-id="5d457-194">State</span></span>
<span data-ttu-id="5d457-195">System.FM rapporteert als OK wanneer de partitie is gemaakt en is in orde.</span><span class="sxs-lookup"><span data-stu-id="5d457-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="5d457-196">Worden verwijderd de entiteit van de health store wanneer de partitie wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5d457-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="5d457-197">Als de partitie lager dan het aantal minimale replica is, is een fout rapporteert.</span><span class="sxs-lookup"><span data-stu-id="5d457-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="5d457-198">Als de partitie niet lager dan het aantal minimale replica is, maar dit lager dan het aantal replica's van doel is, wordt een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5d457-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="5d457-199">Als de partitie is sprake van quorumverlies, rapporteert System.FM een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5d457-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="5d457-200">Andere belangrijke gebeurtenissen bevatten een waarschuwing wanneer de herconfiguratie langer duurt dan verwacht en wanneer de build langer duurt dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="5d457-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="5d457-201">De verwachte tijden voor de build en herconfiguratie geconfigureerd worden op basis van de service-scenario's.</span><span class="sxs-lookup"><span data-stu-id="5d457-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="5d457-202">Bijvoorbeeld, als een service een terabyte van status, zoals SQL-Database heeft, duurt de build langer dan voor een service met een kleine hoeveelheid staat.</span><span class="sxs-lookup"><span data-stu-id="5d457-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="5d457-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5d457-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5d457-204">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="5d457-204">**Property**: State</span></span>
* <span data-ttu-id="5d457-205">**Volgende stappen**: als de status niet OK is, is het mogelijk dat sommige replica's niet zijn gemaakt, geopend, of juist gepromoveerd tot primaire of secundaire site.</span><span class="sxs-lookup"><span data-stu-id="5d457-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="5d457-206">In veel gevallen is de hoofdoorzaak een service-fout in de implementatie open of rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5d457-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="5d457-207">Het volgende voorbeeld ziet u een partitie in orde:</span><span class="sxs-lookup"><span data-stu-id="5d457-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="5d457-208">Het volgende voorbeeld toont de status van een partitie die lager is dan het aantal doel-replica's.</span><span class="sxs-lookup"><span data-stu-id="5d457-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="5d457-209">De volgende stap is om op te halen van de Partitiebeschrijving, waarin configuratie: **MinReplicaSetSize** is drie en **TargetReplicaSetSize** zeven.</span><span class="sxs-lookup"><span data-stu-id="5d457-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="5d457-210">Haal vervolgens het aantal knooppunten in het cluster: vijf.</span><span class="sxs-lookup"><span data-stu-id="5d457-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="5d457-211">Dus in dit geval kunnen niet twee replica's worden geplaatst, omdat het doelaantal replica's hoger dan het aantal knooppunten beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="5d457-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="5d457-212">Replica-Beperkingsfout</span><span class="sxs-lookup"><span data-stu-id="5d457-212">Replica constraint violation</span></span>
<span data-ttu-id="5d457-213">**System.PLB** rapporteert een waarschuwing als het een overtreding van een replica wordt gedetecteerd en alle replica's van partitie kan niet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="5d457-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="5d457-214">Details van het rapport weergeven welke beperkingen en eigenschappen te voorkomen dat de replica-plaatsing.</span><span class="sxs-lookup"><span data-stu-id="5d457-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="5d457-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5d457-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5d457-216">**De eigenschap**: begint met **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="5d457-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="5d457-217">Systeemstatusrapporten replica</span><span class="sxs-lookup"><span data-stu-id="5d457-217">Replica system health reports</span></span>
<span data-ttu-id="5d457-218">**System.RA**, die staat voor het onderdeel reconfiguration agent is de instantie voor de replicastatus van de.</span><span class="sxs-lookup"><span data-stu-id="5d457-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="5d457-219">Status</span><span class="sxs-lookup"><span data-stu-id="5d457-219">State</span></span>
<span data-ttu-id="5d457-220">**System.RA** OK rapporten wanneer de replica is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d457-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="5d457-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5d457-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5d457-222">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="5d457-222">**Property**: State</span></span>

<span data-ttu-id="5d457-223">Het volgende voorbeeld ziet u een replica in orde:</span><span class="sxs-lookup"><span data-stu-id="5d457-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="5d457-224">Open status van replica</span><span class="sxs-lookup"><span data-stu-id="5d457-224">Replica open status</span></span>
<span data-ttu-id="5d457-225">De beschrijving van dit statusrapport bevat de begintijd (Coordinated Universal Time) toen de API-aanroep werd aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5d457-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="5d457-226">**System.RA** rapporten van een waarschuwing als de replica open langer dan de geconfigureerde periode duurt (standaard: 30 minuten).</span><span class="sxs-lookup"><span data-stu-id="5d457-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="5d457-227">Als de API heeft impact op de beschikbaarheid van de service, wordt het rapport is veel sneller uitgegeven (een configureerbare interval, met een standaard 30 seconden).</span><span class="sxs-lookup"><span data-stu-id="5d457-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="5d457-228">De tijd gemeten bevat de benodigde tijd voor de replicator-openen en het openen van de service.</span><span class="sxs-lookup"><span data-stu-id="5d457-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="5d457-229">De eigenschap wordt gewijzigd op OK als u de open is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d457-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="5d457-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5d457-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5d457-231">**De eigenschap**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="5d457-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="5d457-232">**Volgende stappen**: als de status niet OK is, onderzoekt waarom de geopende replica duurt langer dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="5d457-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="5d457-233">Trage service API-aanroep</span><span class="sxs-lookup"><span data-stu-id="5d457-233">Slow service API call</span></span>
<span data-ttu-id="5d457-234">**System.RAP** en **System.Replicator** rapporteren van een waarschuwing als een aanroep van de code van de gebruiker langer dan de geconfigureerde tijd duurt.</span><span class="sxs-lookup"><span data-stu-id="5d457-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="5d457-235">De waarschuwing wordt gewist wanneer de aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d457-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="5d457-236">**SourceId**: System.RAP of System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5d457-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="5d457-237">**De eigenschap**: de naam van de langzaam API.</span><span class="sxs-lookup"><span data-stu-id="5d457-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="5d457-238">De beschrijving biedt meer informatie over de tijd die de API in behandeling is.</span><span class="sxs-lookup"><span data-stu-id="5d457-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="5d457-239">**Volgende stappen**: onderzoeken waarom de aanroep duurt langer dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="5d457-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="5d457-240">Het volgende voorbeeld ziet een partitie in quorumverlies en de onderzoek stappen om erachter te komen waarom gedaan.</span><span class="sxs-lookup"><span data-stu-id="5d457-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="5d457-241">Een van de replica's heeft een waarschuwingsstatus zodat u de status downloaden.</span><span class="sxs-lookup"><span data-stu-id="5d457-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="5d457-242">Er wordt weergegeven dat de servicebewerking langer duurt dan verwacht, een gebeurtenis die is gerapporteerd door System.RAP.</span><span class="sxs-lookup"><span data-stu-id="5d457-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="5d457-243">Nadat deze informatie is ontvangen, wordt de volgende stap is om te kijken naar de code en er onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="5d457-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="5d457-244">Voor deze aanvraag de **RunAsync** implementatie van de stateful service genereert een onverwerkte uitzondering.</span><span class="sxs-lookup"><span data-stu-id="5d457-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="5d457-245">De replica's zijn recyclen, zodat alle replica's in de waarschuwingsstatus mogelijk niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5d457-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="5d457-246">U kunt proberen het ophalen van de status en zoekt u naar eventuele verschillen in de replica-ID.</span><span class="sxs-lookup"><span data-stu-id="5d457-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="5d457-247">In bepaalde gevallen, kunnen de nieuwe pogingen geven u aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="5d457-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="5d457-248">Wanneer u de defecte toepassing onder het foutopsporingsprogramma start, geven de diagnostische gebeurtenissen van windows de uitzondering gegenereerd vanuit RunAsync:</span><span class="sxs-lookup"><span data-stu-id="5d457-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Visual Studio 2015 diagnostische gebeurtenissen: RunAsync-fout in de fabric: / HelloWorldStatefulApplication.][1]

<span data-ttu-id="5d457-250">Visual Studio 2015 diagnostische gebeurtenissen: fout in RunAsync **fabric: / HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="5d457-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="5d457-251">Volledige replicatiewachtrij</span><span class="sxs-lookup"><span data-stu-id="5d457-251">Replication queue full</span></span>
<span data-ttu-id="5d457-252">**System.Replicator** rapporten van een waarschuwing wanneer de replicatiewachtrij vol is.</span><span class="sxs-lookup"><span data-stu-id="5d457-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="5d457-253">Op de primaire raakt wachtrij voor replicatie staan doorgaans vol omdat een of meer secundaire replica's zijn trage operations bevestigen.</span><span class="sxs-lookup"><span data-stu-id="5d457-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="5d457-254">Op de secundaire, dit gebeurt meestal wanneer de service langzaam is worden de bewerkingen toepassen.</span><span class="sxs-lookup"><span data-stu-id="5d457-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="5d457-255">De waarschuwing wordt gewist wanneer de wachtrij vol is.</span><span class="sxs-lookup"><span data-stu-id="5d457-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="5d457-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5d457-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="5d457-257">**De eigenschap**: **PrimaryReplicationQueueStatus** of **SecondaryReplicationQueueStatus**, afhankelijk van de replicarol</span><span class="sxs-lookup"><span data-stu-id="5d457-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="5d457-258">Trage Naming bewerkingen</span><span class="sxs-lookup"><span data-stu-id="5d457-258">Slow Naming operations</span></span>
<span data-ttu-id="5d457-259">**System.NamingService** rapporteert de status op de primaire replica wanneer u een naam geven bewerking duurt langer dan de aanvaardbare.</span><span class="sxs-lookup"><span data-stu-id="5d457-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="5d457-260">Voorbeelden van Naming bewerkingen zijn [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) of [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="5d457-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="5d457-261">Meer methoden kunnen u vinden onder FabricClient, bijvoorbeeld onder [service beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) of [eigenschap beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="5d457-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="5d457-262">De service Naming servicenamen worden omgezet in een locatie in het cluster en kan gebruikers beheren servicenamen en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5d457-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="5d457-263">Het is een Service Fabric gepartitioneerd persistent service.</span><span class="sxs-lookup"><span data-stu-id="5d457-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="5d457-264">Een van de partities vertegenwoordigt een eigenaar van de instantie die de metagegevens over alle Service Fabric-namen en -services bevat.</span><span class="sxs-lookup"><span data-stu-id="5d457-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="5d457-265">De Service Fabric-namen worden toegewezen aan verschillende partities, genaamd Name Owner partities, zodat de service kan uitgebreid worden.</span><span class="sxs-lookup"><span data-stu-id="5d457-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="5d457-266">Lees meer over [Naming service](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="5d457-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="5d457-267">Wanneer een Naming bewerking langer duurt dan verwacht, de bewerking is gemarkeerd met een rapport waarschuwing op het *primaire replica van de Naming service partitie die de bewerking fungeert*.</span><span class="sxs-lookup"><span data-stu-id="5d457-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="5d457-268">Als de bewerking voltooid is, wordt de waarschuwing is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5d457-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="5d457-269">Als de bewerking is voltooid met een fout, bevat het statusrapport meer informatie over de fout.</span><span class="sxs-lookup"><span data-stu-id="5d457-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="5d457-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="5d457-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="5d457-271">**De eigenschap**: begint met het voorvoegsel **Duration_** en identificeert de trage bewerking en de Service Fabric-naam waarop de bewerking wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="5d457-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="5d457-272">Bijvoorbeeld, als service maken op de naam van fabric: / MyApp/MijnService is te lang duurt, is de eigenschap Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="5d457-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="5d457-273">AO verwijst naar de rol van de partitie Naming voor deze naam en het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5d457-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="5d457-274">**Volgende stappen**: selectievakje waarom de Naming-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="5d457-275">Elke bewerking kan verschillende oorzaken hebben.</span><span class="sxs-lookup"><span data-stu-id="5d457-275">Each operation can have different root causes.</span></span> <span data-ttu-id="5d457-276">Bijvoorbeeld verwijderen service kan blijven steken op een knooppunt omdat toepassingshost op een knooppunt als gevolg van een gebruiker fout in de servicecode vastlopen houdt.</span><span class="sxs-lookup"><span data-stu-id="5d457-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="5d457-277">Het volgende voorbeeld ziet een servicebewerking maken.</span><span class="sxs-lookup"><span data-stu-id="5d457-277">The following example shows a create service operation.</span></span> <span data-ttu-id="5d457-278">De bewerking duurt langer dan de geconfigureerde duur.</span><span class="sxs-lookup"><span data-stu-id="5d457-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="5d457-279">AO pogingen en werk verzendt op Nee.</span><span class="sxs-lookup"><span data-stu-id="5d457-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="5d457-280">NIET de laatste bewerking met time-out voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d457-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="5d457-281">In dit geval is de dezelfde replica primaire voor zowel de AO en er zijn geen rollen.</span><span class="sxs-lookup"><span data-stu-id="5d457-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="5d457-282">Systeemstatusrapporten DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="5d457-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="5d457-283">**System.Hosting** is de instantie voor geïmplementeerde entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5d457-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="5d457-284">activering</span><span class="sxs-lookup"><span data-stu-id="5d457-284">Activation</span></span>
<span data-ttu-id="5d457-285">System.Hosting rapporteert als OK als u een toepassing is geactiveerd op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5d457-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="5d457-286">Anders wordt een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5d457-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5d457-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-288">**De eigenschap**: activering, waaronder de implementatie-versie</span><span class="sxs-lookup"><span data-stu-id="5d457-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="5d457-289">**Volgende stappen**: als de toepassing niet in orde is, moet u onderzoeken waarom de activering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="5d457-290">Het volgende voorbeeld ziet u geslaagde activering:</span><span class="sxs-lookup"><span data-stu-id="5d457-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5d457-291">Downloaden</span><span class="sxs-lookup"><span data-stu-id="5d457-291">Download</span></span>
<span data-ttu-id="5d457-292">**System.Hosting** een fout gemeld als het pakket downloaden van de toepassing is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="5d457-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-294">**De eigenschap**:  **downloaden:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5d457-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5d457-295">**Volgende stappen**: onderzoeken waarom het downloaden is mislukt op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5d457-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="5d457-296">Systeemstatusrapporten DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="5d457-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="5d457-297">**System.Hosting** is de instantie voor geïmplementeerde entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5d457-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="5d457-298">Het activeren van service</span><span class="sxs-lookup"><span data-stu-id="5d457-298">Service package activation</span></span>
<span data-ttu-id="5d457-299">System.Hosting rapporten als OK als de activering van de service-pakket op het knooppunt geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="5d457-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="5d457-300">Anders wordt een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5d457-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5d457-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-302">**De eigenschap**: activering</span><span class="sxs-lookup"><span data-stu-id="5d457-302">**Property**: Activation</span></span>
* <span data-ttu-id="5d457-303">**Volgende stappen**: onderzoeken waarom de activering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="5d457-304">Pakket-codeactivering</span><span class="sxs-lookup"><span data-stu-id="5d457-304">Code package activation</span></span>
<span data-ttu-id="5d457-305">**System.Hosting** rapporteert als OK voor elk codepakket als de activering geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="5d457-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="5d457-306">Als de activering mislukt, wordt een waarschuwing weergegeven zoals geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="5d457-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="5d457-307">Als **CodePackage** niet kan activeren of eindigt met een groter is dan de geconfigureerde fout **CodePackageHealthErrorThreshold**, die als host fungeert een fout gemeld.</span><span class="sxs-lookup"><span data-stu-id="5d457-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="5d457-308">Als een servicepakket meerdere code pakketten bevat, wordt een rapport activering gegenereerd voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="5d457-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="5d457-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-310">**De eigenschap**: maakt gebruik van het voorvoegsel **CodePackageActivation** en bevat de naam van het codepakket en het toegangspunt dat als  **CodePackageActivation:*CodePackageName* :*Entrypoint/EntryPoint*** (bijvoorbeeld **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="5d457-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="5d457-311">Service type is geregistreerd</span><span class="sxs-lookup"><span data-stu-id="5d457-311">Service type registration</span></span>
<span data-ttu-id="5d457-312">**System.Hosting** rapporteert als OK als het servicetype is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5d457-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="5d457-313">Een fout gemeld. Als de registratie is niet uitgevoerd in de tijd (zoals deze is geconfigureerd met behulp van **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="5d457-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="5d457-314">Als de runtime is gesloten, type van de service niet is geregistreerd in het knooppunt en Hosting rapporteert een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5d457-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="5d457-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-316">**De eigenschap**: maakt gebruik van het voorvoegsel **ServiceTypeRegistration** en bevat de naam van het servicetype (bijvoorbeeld **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="5d457-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="5d457-317">Het volgende voorbeeld ziet u een gezonde geïmplementeerd servicepakket:</span><span class="sxs-lookup"><span data-stu-id="5d457-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5d457-318">Downloaden</span><span class="sxs-lookup"><span data-stu-id="5d457-318">Download</span></span>
<span data-ttu-id="5d457-319">**System.Hosting** een fout gemeld als het downloaden van het service-pakket is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="5d457-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-321">**De eigenschap**:  **downloaden:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5d457-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5d457-322">**Volgende stappen**: onderzoeken waarom het downloaden is mislukt op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5d457-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="5d457-323">Validatie van upgrade</span><span class="sxs-lookup"><span data-stu-id="5d457-323">Upgrade validation</span></span>
<span data-ttu-id="5d457-324">**System.Hosting** meldt fout als validatie tijdens de upgrade mislukt of als de upgrade op het knooppunt mislukt.</span><span class="sxs-lookup"><span data-stu-id="5d457-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="5d457-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5d457-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5d457-326">**De eigenschap**: maakt gebruik van het voorvoegsel **FabricUpgradeValidation** en bevat de upgrade-versie</span><span class="sxs-lookup"><span data-stu-id="5d457-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="5d457-327">**Beschrijving**: verwijst naar de opgetreden fout</span><span class="sxs-lookup"><span data-stu-id="5d457-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d457-328">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d457-328">Next steps</span></span>
[<span data-ttu-id="5d457-329">Service Fabric-statusrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="5d457-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="5d457-330">Het rapport en controleer de servicestatus van de</span><span class="sxs-lookup"><span data-stu-id="5d457-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="5d457-331">Controle en diagnose van lokaal services</span><span class="sxs-lookup"><span data-stu-id="5d457-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="5d457-332">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="5d457-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

