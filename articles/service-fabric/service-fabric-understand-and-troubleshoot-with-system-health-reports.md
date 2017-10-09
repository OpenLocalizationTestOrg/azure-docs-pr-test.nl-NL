---
title: aaaTroubleshoot met systeemstatusrapporten | Microsoft Docs
description: Hierin wordt beschreven Hallo statusrapporten verzonden door Azure Service Fabric-onderdelen en hun gebruik voor het oplossen van problemen cluster of problemen met de toepassing.
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="51a76-103">Gebruik system health rapporten tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="51a76-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="51a76-104">Azure Service Fabric-onderdelen rapport out of box Hallo op alle entiteiten in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="51a76-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="51a76-105">Hallo [health store](service-fabric-health-introduction.md#health-store) maken en verwijderen van de entiteiten die zijn gebaseerd op rapporten van Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="51a76-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="51a76-106">Ook ordent ze in een hiërarchie die entiteit interacties worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="51a76-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="51a76-107">toounderstand health-gerelateerde begrippen meer informatie op [Service Fabric-statusmodel](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51a76-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="51a76-108">Systeemstatusrapporten bieden inzicht in het cluster en de functionaliteit van de toepassing en de vlag problemen via health.</span><span class="sxs-lookup"><span data-stu-id="51a76-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="51a76-109">Voor toepassingen en services controleren systeemstatusrapporten of entiteiten worden geïmplementeerd en correct van Hallo Service Fabric-perspectief zich gedragen.</span><span class="sxs-lookup"><span data-stu-id="51a76-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="51a76-110">Hallo rapporten bieden een statuscontrole van de bedrijfslogica Hallo van Hallo service of detectie van vastgelopen processen.</span><span class="sxs-lookup"><span data-stu-id="51a76-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="51a76-111">Gebruiker services kunnen Hallo statusgegevens met informatie specifieke tootheir logica aanvullen.</span><span class="sxs-lookup"><span data-stu-id="51a76-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="51a76-112">Statusrapporten watchdogs zijn alleen zichtbaar *nadat* Hallo-systeemonderdelen maken van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="51a76-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="51a76-113">Wanneer een entiteit wordt verwijderd, worden alle statusrapporten gekoppeld in Hallo health store automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51a76-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="51a76-114">Hallo geldt ook wanneer een nieuw exemplaar van Hallo entiteit is gemaakt (bijvoorbeeld een nieuw exemplaar van de service voor stateful persistente-replica is gemaakt).</span><span class="sxs-lookup"><span data-stu-id="51a76-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="51a76-115">Alle rapporten die zijn gekoppeld aan de oude exemplaar Hallo worden verwijderd en wordt opgeschoond van Hallo store.</span><span class="sxs-lookup"><span data-stu-id="51a76-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="51a76-116">Hallo zijn rapporten van system component geïdentificeerd door Hallo bron, die met de Hallo begint '**System.**'</span><span class="sxs-lookup"><span data-stu-id="51a76-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="51a76-117">voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="51a76-117">prefix.</span></span> <span data-ttu-id="51a76-118">Watchdogs niet Hallo hetzelfde voorvoegsel voor hun bronnen gebruiken, zoals rapporten met ongeldige parameters worden afgewezen.</span><span class="sxs-lookup"><span data-stu-id="51a76-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="51a76-119">Laten we kijken sommige system rapporten toounderstand wat ze activeert en hoe toocorrect Hallo mogelijke problemen staan.</span><span class="sxs-lookup"><span data-stu-id="51a76-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="51a76-120">Service Fabric blijft tooadd rapporten van de voorwaarden van belang ter verbetering van de zichtbaarheid van wat in Hallo-cluster en de toepassing gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="51a76-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="51a76-121">Bestaande rapporten kunnen ook worden uitgebreid met meer details toohelp Hallo probleem sneller kan oplossen.</span><span class="sxs-lookup"><span data-stu-id="51a76-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="51a76-122">Systeemstatusrapporten cluster</span><span class="sxs-lookup"><span data-stu-id="51a76-122">Cluster system health reports</span></span>
<span data-ttu-id="51a76-123">Hallo cluster health entiteit wordt automatisch gemaakt in Hallo health store.</span><span class="sxs-lookup"><span data-stu-id="51a76-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="51a76-124">Als alles goed werkt, heeft geen system-rapport.</span><span class="sxs-lookup"><span data-stu-id="51a76-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="51a76-125">Verlies van groep</span><span class="sxs-lookup"><span data-stu-id="51a76-125">Neighborhood loss</span></span>
<span data-ttu-id="51a76-126">**System.Federation** meldt fout wanneer er een groep verlies wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="51a76-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="51a76-127">Hallo-rapport is van afzonderlijke knooppunten en Hallo knooppunt-ID is opgenomen in de naam van de eigenschap Hallo.</span><span class="sxs-lookup"><span data-stu-id="51a76-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="51a76-128">Als een groep in de hele Service Fabric-ring Hallo verbroken is, kunt u doorgaans twee gebeurtenissen (beide zijden van Hallo hiaat rapport) verwachten.</span><span class="sxs-lookup"><span data-stu-id="51a76-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="51a76-129">Als er meer groepen verloren gaan, moet u er meer gebeurtenissen zijn.</span><span class="sxs-lookup"><span data-stu-id="51a76-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="51a76-130">Hallo-rapport geeft Hallo globale lease time-out Hallo tijd toolive.</span><span class="sxs-lookup"><span data-stu-id="51a76-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="51a76-131">Hallo rapport opnieuw verzonden elke helft van de duur van de TTL Hallo voor zolang Hallo voorwaarde actief blijft.</span><span class="sxs-lookup"><span data-stu-id="51a76-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="51a76-132">Hallo-gebeurtenis wordt automatisch verwijderd wanneer het verloopt.</span><span class="sxs-lookup"><span data-stu-id="51a76-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="51a76-133">Verwijder wanneer verlopen gedrag zorgt ervoor dat Hallo rapport wordt opgeschoond uit Hallo health store correct, zelfs als Hallo reporting knooppunt niet actief is.</span><span class="sxs-lookup"><span data-stu-id="51a76-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="51a76-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="51a76-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="51a76-135">**De eigenschap**: begint met **groep** en bevat knooppuntgegevens</span><span class="sxs-lookup"><span data-stu-id="51a76-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="51a76-136">**Volgende stappen**: onderzoeken waarom Hallo-groep is verbroken (bijvoorbeeld selectievakje Hallo communicatie tussen clusterknooppunten).</span><span class="sxs-lookup"><span data-stu-id="51a76-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="51a76-137">Systeemstatusrapporten knooppunt</span><span class="sxs-lookup"><span data-stu-id="51a76-137">Node system health reports</span></span>
<span data-ttu-id="51a76-138">**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, is Hallo-instantie die het beheer van informatie over de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="51a76-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="51a76-139">Elk knooppunt moet één rapport van System.FM met de status hebben.</span><span class="sxs-lookup"><span data-stu-id="51a76-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="51a76-140">Hallo knooppunt entiteiten worden verwijderd wanneer de status van knooppunt hello wordt verwijderd (Zie [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="51a76-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="51a76-141">Knooppunt omhoog/omlaag</span><span class="sxs-lookup"><span data-stu-id="51a76-141">Node up/down</span></span>
<span data-ttu-id="51a76-142">System.FM rapporteert als OK als lid van knooppunt Hallo Hallo ring (dit is actief en werkend).</span><span class="sxs-lookup"><span data-stu-id="51a76-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="51a76-143">Een fout gemeld wanneer Hallo knooppunt Hallo ring vertrekt (service niet actief is, ofwel voor het upgraden of gewoon omdat deze is mislukt).</span><span class="sxs-lookup"><span data-stu-id="51a76-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="51a76-144">Hallo health hiërarchie gebouwd door Hallo health store neemt actie geïmplementeerde entiteiten in correlatie met System.FM knooppunt rapporten.</span><span class="sxs-lookup"><span data-stu-id="51a76-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="51a76-145">Het beschouwt Hallo-knooppunt een bovenliggende virtuele van alle geïmplementeerde entiteiten.</span><span class="sxs-lookup"><span data-stu-id="51a76-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="51a76-146">Hallo geïmplementeerd entiteiten op dat knooppunt worden query's via als Hallo-knooppunt wordt gerapporteerd als up door System.FM, hello hetzelfde exemplaar als Hallo-exemplaar gekoppeld aan het Hallo-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="51a76-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="51a76-147">Wanneer System.FM meldt dat Hallo-knooppunt is niet beschikbaar of opnieuw opgestart (een nieuw exemplaar), Hallo health store Hallo geïmplementeerd entiteiten die kunnen bestaan alleen op Hallo omlaag knooppunt of op het vorige exemplaar van knooppunt Hallo Hallo automatisch opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="51a76-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="51a76-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="51a76-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="51a76-149">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="51a76-149">**Property**: State</span></span>
* <span data-ttu-id="51a76-150">**Volgende stappen**: als het Hallo-knooppunt niet actief is voor een upgrade, deze moet terugkeren nadat de upgrade is voltooid.</span><span class="sxs-lookup"><span data-stu-id="51a76-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="51a76-151">Hallo-status moet in dit geval back tooOK overschakelen.</span><span class="sxs-lookup"><span data-stu-id="51a76-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="51a76-152">Als Hallo knooppunt niet u terug keert of deze is mislukt, moet Hallo probleem meer onderzoek.</span><span class="sxs-lookup"><span data-stu-id="51a76-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="51a76-153">Hallo volgende voorbeeld wordt weergegeven Hallo System.FM gebeurtenis met een status OK voor knooppunt:</span><span class="sxs-lookup"><span data-stu-id="51a76-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="51a76-154">Vervaldatum van het certificaat</span><span class="sxs-lookup"><span data-stu-id="51a76-154">Certificate expiration</span></span>
<span data-ttu-id="51a76-155">**System.FabricNode** rapporten van een waarschuwing wanneer certificaten worden gebruikt door Hallo-knooppunt bijna is verlopen zijn.</span><span class="sxs-lookup"><span data-stu-id="51a76-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="51a76-156">Er zijn drie certificaten per knooppunt: **Certificate_cluster**, **Certificate_server**, en **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="51a76-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="51a76-157">Wanneer Hallo vervaldatum ten minste twee weken is, is Hallo rapport status in orde.</span><span class="sxs-lookup"><span data-stu-id="51a76-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="51a76-158">Wanneer Hallo verloopt binnen twee weken is, is het rapporttype Hallo een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="51a76-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="51a76-159">TTL van deze gebeurtenissen is oneindig en worden ze verwijderd wanneer een knooppunt Hallo-cluster verlaat.</span><span class="sxs-lookup"><span data-stu-id="51a76-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="51a76-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="51a76-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="51a76-161">**De eigenschap**: begint met **certificaat** en bevat meer informatie over Hallo certificaattype</span><span class="sxs-lookup"><span data-stu-id="51a76-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="51a76-162">**Volgende stappen**: Hallo certificaten bijwerken als ze bijna is verlopen zijn.</span><span class="sxs-lookup"><span data-stu-id="51a76-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="51a76-163">Schending van de Load-capaciteit</span><span class="sxs-lookup"><span data-stu-id="51a76-163">Load capacity violation</span></span>
<span data-ttu-id="51a76-164">Hallo Service Fabric Load Balancer rapporten in een waarschuwing wanneer er een schending van de capaciteit knooppunt wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="51a76-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="51a76-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="51a76-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="51a76-166">**De eigenschap**: begint met **capaciteit**</span><span class="sxs-lookup"><span data-stu-id="51a76-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="51a76-167">**Volgende stappen**: selectievakje opgegeven metrische gegevens en bekijkt hello huidige capaciteit op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="51a76-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="51a76-168">Systeemstatusrapporten toepassing</span><span class="sxs-lookup"><span data-stu-id="51a76-168">Application system health reports</span></span>
<span data-ttu-id="51a76-169">**System.CM**, waarop Hallo Cluster Manager-service vertegenwoordigt, Hallo-instantie die het beheer van informatie over een toepassing is.</span><span class="sxs-lookup"><span data-stu-id="51a76-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="51a76-170">Status</span><span class="sxs-lookup"><span data-stu-id="51a76-170">State</span></span>
<span data-ttu-id="51a76-171">System.CM rapporteert als OK wanneer Hallo-toepassing heeft gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="51a76-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="51a76-172">Informeert het Hallo health store wanneer de toepassing hello is verwijderd, zodat het kan worden verwijderd uit de store.</span><span class="sxs-lookup"><span data-stu-id="51a76-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="51a76-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="51a76-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="51a76-174">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="51a76-174">**Property**: State</span></span>
* <span data-ttu-id="51a76-175">**Volgende stappen**: als Hallo-aanvraag is gemaakt of bijgewerkt, moet het Hallo Clusterbeheer statusrapport opnemen.</span><span class="sxs-lookup"><span data-stu-id="51a76-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="51a76-176">Bekijk anders de status van de toepassing hello Hallo door uitgifte van een query (bijvoorbeeld Hallo PowerShell-cmdlet **Get-ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="51a76-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="51a76-177">Hallo volgende voorbeeld ziet u Hallo statussen van gebeurtenissen op Hallo **fabric: / WordCount** toepassing:</span><span class="sxs-lookup"><span data-stu-id="51a76-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="51a76-178">Systeemstatusrapporten service</span><span class="sxs-lookup"><span data-stu-id="51a76-178">Service system health reports</span></span>
<span data-ttu-id="51a76-179">**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, Hallo-dienst die informatie over services beheert.</span><span class="sxs-lookup"><span data-stu-id="51a76-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="51a76-180">Status</span><span class="sxs-lookup"><span data-stu-id="51a76-180">State</span></span>
<span data-ttu-id="51a76-181">System.FM rapporteert als OK wanneer Hallo-service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51a76-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="51a76-182">Worden verwijderd Hallo entiteit uit Hallo health store wanneer Hallo-service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51a76-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="51a76-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="51a76-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="51a76-184">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="51a76-184">**Property**: State</span></span>

<span data-ttu-id="51a76-185">Hallo volgende voorbeeld ziet u Hallo statussen van gebeurtenissen op Hallo service **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="51a76-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="51a76-186">Fout van de correlatie-service</span><span class="sxs-lookup"><span data-stu-id="51a76-186">Service correlation error</span></span>
<span data-ttu-id="51a76-187">**System.PLB** meldt fout wanneer er wordt gedetecteerd dat een affiniteitsketen bijwerken van een service toobe gecorreleerd met een andere service maakt.</span><span class="sxs-lookup"><span data-stu-id="51a76-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="51a76-188">Hallo-rapport wordt gewist wanneer geslaagde update gebeurt.</span><span class="sxs-lookup"><span data-stu-id="51a76-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="51a76-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="51a76-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="51a76-190">**De eigenschap**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="51a76-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="51a76-191">**Volgende stappen**: selectievakje Hallo gecorreleerde servicebeschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="51a76-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="51a76-192">Systeemstatusrapporten partitie</span><span class="sxs-lookup"><span data-stu-id="51a76-192">Partition system health reports</span></span>
<span data-ttu-id="51a76-193">**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, Hallo-dienst die informatie over servicepartities beheert.</span><span class="sxs-lookup"><span data-stu-id="51a76-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="51a76-194">Status</span><span class="sxs-lookup"><span data-stu-id="51a76-194">State</span></span>
<span data-ttu-id="51a76-195">System.FM rapporteert als OK wanneer Hallo partitie is gemaakt en is in orde.</span><span class="sxs-lookup"><span data-stu-id="51a76-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="51a76-196">Worden verwijderd Hallo entiteit uit Hallo health store wanneer Hallo partitie wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51a76-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="51a76-197">Als het Hallo-partitie is lager dan het Hallo minimale replica aantal, is een fout rapporteert.</span><span class="sxs-lookup"><span data-stu-id="51a76-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="51a76-198">Als Hallo partitie niet lager dan het aantal van Hallo minimale replica is, maar het is lager dan het Hallo doel replica aantal, wordt een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="51a76-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="51a76-199">Als Hallo partitie is sprake van quorumverlies, rapporteert System.FM een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="51a76-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="51a76-200">Andere belangrijke gebeurtenissen bevatten een waarschuwing wanneer Hallo herconfiguratie langer duurt dan verwacht en wanneer Hallo build langer duurt dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="51a76-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="51a76-201">Hallo verwacht tijden voor Hallo build en herconfiguratie worden geconfigureerd op basis van de service-scenario's.</span><span class="sxs-lookup"><span data-stu-id="51a76-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="51a76-202">Bijvoorbeeld, als een service een terabyte van status, zoals SQL-Database heeft, duurt Hallo build langer dan voor een service met een kleine hoeveelheid staat.</span><span class="sxs-lookup"><span data-stu-id="51a76-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="51a76-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="51a76-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="51a76-204">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="51a76-204">**Property**: State</span></span>
* <span data-ttu-id="51a76-205">**Volgende stappen**: als het Hallo-status is niet OK, is het mogelijk dat sommige replica's niet gemaakt, is geopend of gepromoveerde tooprimary of secundaire correct is.</span><span class="sxs-lookup"><span data-stu-id="51a76-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="51a76-206">In veel gevallen is de hoofdoorzaak Hallo een service-fout in Hallo open of implementatie van rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51a76-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="51a76-207">Hallo volgende voorbeeld ziet u een partitie in orde:</span><span class="sxs-lookup"><span data-stu-id="51a76-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="51a76-208">Hallo ziet volgende voorbeeld Hallo status van een partitie die lager is dan het aantal doel-replica's.</span><span class="sxs-lookup"><span data-stu-id="51a76-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="51a76-209">de volgende stap Hallo is tooget Hallo Partitiebeschrijving, waarin configuratie: **MinReplicaSetSize** is drie en **TargetReplicaSetSize** zeven.</span><span class="sxs-lookup"><span data-stu-id="51a76-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="51a76-210">Vervolgens Hallo aantal knooppunten in cluster Hallo ophalen: vijf.</span><span class="sxs-lookup"><span data-stu-id="51a76-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="51a76-211">Dus in dit geval kunnen niet twee replica's worden geplaatst, omdat Hallo doelaantal replica's hoger dan het aantal knooppunten beschikbaar Hallo is.</span><span class="sxs-lookup"><span data-stu-id="51a76-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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

### <a name="replica-constraint-violation"></a><span data-ttu-id="51a76-212">Replica-Beperkingsfout</span><span class="sxs-lookup"><span data-stu-id="51a76-212">Replica constraint violation</span></span>
<span data-ttu-id="51a76-213">**System.PLB** rapporteert een waarschuwing als het een overtreding van een replica wordt gedetecteerd en alle replica's van partitie kan niet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="51a76-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="51a76-214">Hallo rapportdetails weergeven welke beperkingen en eigenschappen Hallo replica plaatsing voorkomen.</span><span class="sxs-lookup"><span data-stu-id="51a76-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="51a76-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="51a76-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="51a76-216">**De eigenschap**: begint met **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="51a76-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="51a76-217">Systeemstatusrapporten replica</span><span class="sxs-lookup"><span data-stu-id="51a76-217">Replica system health reports</span></span>
<span data-ttu-id="51a76-218">**System.RA**, die staat voor onderdeel van het Hallo reconfiguration agent Hallo autoriteit voor Hallo replica de status is.</span><span class="sxs-lookup"><span data-stu-id="51a76-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="51a76-219">Status</span><span class="sxs-lookup"><span data-stu-id="51a76-219">State</span></span>
<span data-ttu-id="51a76-220">**System.RA** OK rapporten wanneer Hallo replica is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51a76-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="51a76-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="51a76-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="51a76-222">**De eigenschap**: status</span><span class="sxs-lookup"><span data-stu-id="51a76-222">**Property**: State</span></span>

<span data-ttu-id="51a76-223">Hallo volgende voorbeeld ziet u een replica in orde:</span><span class="sxs-lookup"><span data-stu-id="51a76-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="51a76-224">Open status van replica</span><span class="sxs-lookup"><span data-stu-id="51a76-224">Replica open status</span></span>
<span data-ttu-id="51a76-225">Hallo beschrijving van dit statusrapport bevat Hallo begintijd (Coordinated Universal Time) wanneer Hallo API-aanroep is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="51a76-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="51a76-226">**System.RA** rapporteert een waarschuwing als Hallo replica open langer dan de periode Hallo geconfigureerd duurt (standaard: 30 minuten).</span><span class="sxs-lookup"><span data-stu-id="51a76-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="51a76-227">Als Hallo API heeft impact op de beschikbaarheid van de service, uitgegeven Hallo rapport is veel sneller (een configureerbare interval, met een standaard 30 seconden).</span><span class="sxs-lookup"><span data-stu-id="51a76-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="51a76-228">Hallo-tijd gemeten omvat Hallo gebruikte tijd voor Hallo replicator openen en Hallo service openen.</span><span class="sxs-lookup"><span data-stu-id="51a76-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="51a76-229">Hallo eigenschap wijzigingen tooOK als Hallo geopend is voltooid.</span><span class="sxs-lookup"><span data-stu-id="51a76-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="51a76-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="51a76-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="51a76-231">**De eigenschap**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="51a76-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="51a76-232">**Volgende stappen**: als het Hallo-status is niet OK, onderzoeken waarom Hallo replica open duurt langer dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="51a76-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="51a76-233">Trage service API-aanroep</span><span class="sxs-lookup"><span data-stu-id="51a76-233">Slow service API call</span></span>
<span data-ttu-id="51a76-234">**System.RAP** en **System.Replicator** rapporteren van een waarschuwing als een aanroep toohello gebruikerscode service langer dan de tijd Hallo geconfigureerd duurt.</span><span class="sxs-lookup"><span data-stu-id="51a76-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="51a76-235">Hallo-waarschuwing wordt gewist wanneer het Hallo-aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="51a76-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="51a76-236">**SourceId**: System.RAP of System.Replicator</span><span class="sxs-lookup"><span data-stu-id="51a76-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="51a76-237">**De eigenschap**: Hallo-naam van trage Hallo-API.</span><span class="sxs-lookup"><span data-stu-id="51a76-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="51a76-238">Hallo beschrijving biedt meer informatie over Hallo tijd Hallo API is in behandeling.</span><span class="sxs-lookup"><span data-stu-id="51a76-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="51a76-239">**Volgende stappen**: onderzoeken waarom Hallo aanroep duurt langer dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="51a76-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="51a76-240">Hallo volgende voorbeeld ziet u een partitie in quorumverlies en toofigure van Hallo onderzoek stappen uitgevoerd om de oorzaak.</span><span class="sxs-lookup"><span data-stu-id="51a76-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="51a76-241">Een van de replica's Hallo heeft een waarschuwingsstatus zodat u beschikt over de status.</span><span class="sxs-lookup"><span data-stu-id="51a76-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="51a76-242">Er wordt weergegeven dat de servicebewerking Hallo langer duurt dan verwacht, een gebeurtenis die is gerapporteerd door System.RAP.</span><span class="sxs-lookup"><span data-stu-id="51a76-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="51a76-243">Nadat deze informatie is ontvangen, wordt de volgende stap Hallo toolook op Hallo servicecode is en er onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="51a76-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="51a76-244">Voor deze aanvraag Hallo **RunAsync** implementatie van de stateful service Hallo genereert een onverwerkte uitzondering.</span><span class="sxs-lookup"><span data-stu-id="51a76-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="51a76-245">Hallo replica's zijn recyclen, zodat alle replica's in de waarschuwingsstatus Hallo mogelijk niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51a76-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="51a76-246">U kunt ophalen Hallo-status opnieuw en zoek naar eventuele verschillen in Hallo replica-ID.</span><span class="sxs-lookup"><span data-stu-id="51a76-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="51a76-247">In bepaalde gevallen krijgt Hallo pogingen u aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="51a76-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="51a76-248">Wanneer u Hallo defecte toepassing onder Hallo foutopsporingsprogramma start, tonen Hallo diagnostische gebeurtenissen van windows hello uitzondering van RunAsync:</span><span class="sxs-lookup"><span data-stu-id="51a76-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Visual Studio 2015 diagnostische gebeurtenissen: RunAsync-fout in de fabric: / HelloWorldStatefulApplication.][1]

<span data-ttu-id="51a76-250">Visual Studio 2015 diagnostische gebeurtenissen: fout in RunAsync **fabric: / HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="51a76-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="51a76-251">Volledige replicatiewachtrij</span><span class="sxs-lookup"><span data-stu-id="51a76-251">Replication queue full</span></span>
<span data-ttu-id="51a76-252">**System.Replicator** rapporten van een waarschuwing wanneer de replicatiewachtrij Hallo vol is.</span><span class="sxs-lookup"><span data-stu-id="51a76-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="51a76-253">Op primaire Hallo raakt wachtrij voor replicatie staan doorgaans vol omdat een of meer secundaire replica's langzaam tooacknowledge bewerkingen zijn.</span><span class="sxs-lookup"><span data-stu-id="51a76-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="51a76-254">Op Hallo secundaire, dit gebeurt meestal wanneer Hallo-service langzaam tooapply Hallo bewerkingen is.</span><span class="sxs-lookup"><span data-stu-id="51a76-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="51a76-255">Hallo-waarschuwing wordt gewist wanneer Hallo wachtrij vol is.</span><span class="sxs-lookup"><span data-stu-id="51a76-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="51a76-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="51a76-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="51a76-257">**De eigenschap**: **PrimaryReplicationQueueStatus** of **SecondaryReplicationQueueStatus**, afhankelijk van de replicarol Hallo</span><span class="sxs-lookup"><span data-stu-id="51a76-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="51a76-258">Trage Naming bewerkingen</span><span class="sxs-lookup"><span data-stu-id="51a76-258">Slow Naming operations</span></span>
<span data-ttu-id="51a76-259">**System.NamingService** rapporteert de status op de primaire replica wanneer u een naam geven bewerking duurt langer dan de aanvaardbare.</span><span class="sxs-lookup"><span data-stu-id="51a76-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="51a76-260">Voorbeelden van Naming bewerkingen zijn [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) of [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="51a76-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="51a76-261">Meer methoden kunnen u vinden onder FabricClient, bijvoorbeeld onder [service beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) of [eigenschap beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="51a76-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="51a76-262">Hallo Naming service namen tooa servicelocatie in Hallo-cluster wordt omgezet en kan gebruikers toomanage servicenamen en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="51a76-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="51a76-263">Het is een Service Fabric gepartitioneerd persistent service.</span><span class="sxs-lookup"><span data-stu-id="51a76-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="51a76-264">Een van de partities Hallo vertegenwoordigt Hallo Authority Owner, die de metagegevens over alle Service Fabric-namen en -services bevat.</span><span class="sxs-lookup"><span data-stu-id="51a76-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="51a76-265">Hallo Service Fabric-namen zijn toegewezen toodifferent partities, genaamd Name Owner partities, zodat het Hallo-service kan worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="51a76-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="51a76-266">Lees meer over [Naming service](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="51a76-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="51a76-267">Wanneer een Naming bewerking langer duurt dan verwacht, Hallo-bewerking is gemarkeerd met een rapport van de waarschuwing op Hallo *primaire replica van Hallo Naming service partitie die fungeert Hallo bewerking*.</span><span class="sxs-lookup"><span data-stu-id="51a76-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="51a76-268">Als het Hallo-bewerking is voltooid, Hallo waarschuwing is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="51a76-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="51a76-269">Als het Hallo-bewerking is voltooid met een fout, Hallo health rapport bevat details over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="51a76-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="51a76-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="51a76-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="51a76-271">**De eigenschap**: begint met het voorvoegsel **Duration_** en identificeert Hallo langzame werking en Hallo Service Fabric-naam op welke Hallo bewerking wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="51a76-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="51a76-272">Bijvoorbeeld, als service maken op de naam van fabric: / MyApp/MijnService is te lang duurt, Hallo eigenschap Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="51a76-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="51a76-273">AO punten toohello rol Hallo Naming partitie voor deze naam en het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="51a76-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="51a76-274">**Volgende stappen**: selectievakje waarom Hallo Naming-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="51a76-275">Elke bewerking kan verschillende oorzaken hebben.</span><span class="sxs-lookup"><span data-stu-id="51a76-275">Each operation can have different root causes.</span></span> <span data-ttu-id="51a76-276">Bijvoorbeeld verwijderen service kan blijven steken op een knooppunt omdat Hallo toepassingshost houdt op een knooppunt vanwege tooa gebruiker fout in de servicecode Hallo gecrasht.</span><span class="sxs-lookup"><span data-stu-id="51a76-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="51a76-277">Hallo volgende voorbeeld toont een servicebewerking maken.</span><span class="sxs-lookup"><span data-stu-id="51a76-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="51a76-278">Hallo bewerking duurt langer dan de duur Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="51a76-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="51a76-279">AO pogingen en werk tooNO verzendt.</span><span class="sxs-lookup"><span data-stu-id="51a76-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="51a76-280">Er is geen voltooide Hallo laatste bewerking met time-out.</span><span class="sxs-lookup"><span data-stu-id="51a76-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="51a76-281">In dit geval is hello dezelfde replica de primaire voor Hallo AO en er zijn geen rollen.</span><span class="sxs-lookup"><span data-stu-id="51a76-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="51a76-282">Systeemstatusrapporten DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="51a76-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="51a76-283">**System.Hosting** Hallo-instantie op geïmplementeerde entiteiten is.</span><span class="sxs-lookup"><span data-stu-id="51a76-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="51a76-284">activering</span><span class="sxs-lookup"><span data-stu-id="51a76-284">Activation</span></span>
<span data-ttu-id="51a76-285">System.Hosting rapporteert als OK als u een toepassing is geactiveerd op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="51a76-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="51a76-286">Anders wordt een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="51a76-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="51a76-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-288">**De eigenschap**: activering, waaronder Hallo implementatie versie</span><span class="sxs-lookup"><span data-stu-id="51a76-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="51a76-289">**Volgende stappen**: als de toepassing hello niet in orde is, onderzoekt waarom Hallo-activering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="51a76-290">Hallo toont volgende voorbeeld geslaagde activering:</span><span class="sxs-lookup"><span data-stu-id="51a76-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="51a76-291">Downloaden</span><span class="sxs-lookup"><span data-stu-id="51a76-291">Download</span></span>
<span data-ttu-id="51a76-292">**System.Hosting** een fout gemeld als het pakket downloaden van Hallo toepassing mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="51a76-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-294">**De eigenschap**:  **downloaden:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="51a76-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="51a76-295">**Volgende stappen**: onderzoeken waarom Hallo downloaden is mislukt op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="51a76-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="51a76-296">Systeemstatusrapporten DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="51a76-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="51a76-297">**System.Hosting** Hallo-instantie op geïmplementeerde entiteiten is.</span><span class="sxs-lookup"><span data-stu-id="51a76-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="51a76-298">Het activeren van service</span><span class="sxs-lookup"><span data-stu-id="51a76-298">Service package activation</span></span>
<span data-ttu-id="51a76-299">System.Hosting rapporteert als OK als Hallo service pakket activering op Hallo-knooppunt geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="51a76-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="51a76-300">Anders wordt een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="51a76-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="51a76-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-302">**De eigenschap**: activering</span><span class="sxs-lookup"><span data-stu-id="51a76-302">**Property**: Activation</span></span>
* <span data-ttu-id="51a76-303">**Volgende stappen**: onderzoeken waarom Hallo-activering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="51a76-304">Pakket-codeactivering</span><span class="sxs-lookup"><span data-stu-id="51a76-304">Code package activation</span></span>
<span data-ttu-id="51a76-305">**System.Hosting** rapporteert als OK voor elk codepakket als Hallo-activering geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="51a76-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="51a76-306">Als Hallo activering mislukt, wordt een waarschuwing zoals geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="51a76-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="51a76-307">Als **CodePackage** tooactivate mislukt of eindigt met een fout die groter zijn dan Hallo geconfigureerd **CodePackageHealthErrorThreshold**, die als host fungeert een fout gemeld.</span><span class="sxs-lookup"><span data-stu-id="51a76-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="51a76-308">Als een servicepakket meerdere code pakketten bevat, wordt een rapport activering gegenereerd voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="51a76-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="51a76-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-310">**De eigenschap**: maakt gebruik van Hallo voorvoegsel **CodePackageActivation** en bevat Hallo-naam van codepakket hello en Hallo toegangspunt als  **CodePackageActivation:* CodePackageName*:*entrypoint/EntryPoint*** (bijvoorbeeld **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="51a76-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="51a76-311">Service type is geregistreerd</span><span class="sxs-lookup"><span data-stu-id="51a76-311">Service type registration</span></span>
<span data-ttu-id="51a76-312">**System.Hosting** rapporteert als OK als Hallo servicetype is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="51a76-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="51a76-313">Een fout gemeld. Als het Hallo-registratie is niet uitgevoerd in de tijd (zoals deze is geconfigureerd met behulp van **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="51a76-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="51a76-314">Als Hallo runtime is gesloten, Hallo servicetype is registratie van het Hallo-knooppunt en Hosting rapporteert een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="51a76-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="51a76-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-316">**De eigenschap**: maakt gebruik van Hallo voorvoegsel **ServiceTypeRegistration** en bevat de servicenaam type Hallo (bijvoorbeeld **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="51a76-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="51a76-317">Hallo volgende voorbeeld ziet u een gezonde geïmplementeerd servicepakket:</span><span class="sxs-lookup"><span data-stu-id="51a76-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="51a76-318">Downloaden</span><span class="sxs-lookup"><span data-stu-id="51a76-318">Download</span></span>
<span data-ttu-id="51a76-319">**System.Hosting** een fout gemeld als het pakket downloaden van Hallo service mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="51a76-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-321">**De eigenschap**:  **downloaden:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="51a76-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="51a76-322">**Volgende stappen**: onderzoeken waarom Hallo downloaden is mislukt op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="51a76-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="51a76-323">Validatie van upgrade</span><span class="sxs-lookup"><span data-stu-id="51a76-323">Upgrade validation</span></span>
<span data-ttu-id="51a76-324">**System.Hosting** meldt een fout als validatie tijdens Hallo upgrade mislukt of als hello upgrade op Hallo-knooppunt mislukt.</span><span class="sxs-lookup"><span data-stu-id="51a76-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="51a76-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="51a76-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="51a76-326">**De eigenschap**: maakt gebruik van Hallo voorvoegsel **FabricUpgradeValidation** en bevat Hallo upgrade-versie</span><span class="sxs-lookup"><span data-stu-id="51a76-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="51a76-327">**Beschrijving**: verwijst toohello-fout opgetreden</span><span class="sxs-lookup"><span data-stu-id="51a76-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="51a76-328">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51a76-328">Next steps</span></span>
[<span data-ttu-id="51a76-329">Service Fabric-statusrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="51a76-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="51a76-330">Hoe tooreport en controleer health service</span><span class="sxs-lookup"><span data-stu-id="51a76-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="51a76-331">Controle en diagnose van lokaal services</span><span class="sxs-lookup"><span data-stu-id="51a76-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="51a76-332">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="51a76-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

