---
title: Service Fabric aaaAzure omgekeerde proxy | Microsoft Docs
description: Service Fabric van omgekeerde proxy gebruiken voor communicatie toomicroservices van binnen en buiten Hallo-cluster.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="bcffa-103">Azure Service Fabric-omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="bcffa-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="bcffa-104">Hallo omgekeerde proxy die ingebouwd in Azure Service Fabric adressen microservices in Hallo Service Fabric-cluster dat toegang biedt tot HTTP-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="bcffa-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="bcffa-105">Microservices communicatiemodel</span><span class="sxs-lookup"><span data-stu-id="bcffa-105">Microservices communication model</span></span>
<span data-ttu-id="bcffa-106">Microservices in Service Fabric wordt doorgaans uitgevoerd op een subset van virtuele machines in het Hallo-cluster en kunt verplaatsen van een virtuele machine tooanother om verschillende redenen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="bcffa-107">Hallo-eindpunten voor microservices kunnen dus dynamisch wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="bcffa-108">Hallo doorsnee patroon toocommunicate toohello microservice is Hallo volgende lus oplossen:</span><span class="sxs-lookup"><span data-stu-id="bcffa-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="bcffa-109">Los de servicelocatie Hallo in eerste instantie via Hallo naming service.</span><span class="sxs-lookup"><span data-stu-id="bcffa-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="bcffa-110">Verbinding maken met toohello-service.</span><span class="sxs-lookup"><span data-stu-id="bcffa-110">Connect toohello service.</span></span>
3. <span data-ttu-id="bcffa-111">Hallo-oorzaak van verbindingsfouten en Hallo servicelocatie opnieuw los indien nodig.</span><span class="sxs-lookup"><span data-stu-id="bcffa-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="bcffa-112">Dit proces omvat doorgaans wrapping communicatie van client-side '-bibliotheken in een herhalingslus waarmee service Hallo-beleid oplossen en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bcffa-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="bcffa-113">Zie voor meer informatie [Connect en communiceren met services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="bcffa-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="bcffa-114">Communicatie met behulp van Hallo omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="bcffa-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="bcffa-115">Hallo omgekeerde proxy in Service Fabric wordt uitgevoerd op alle Hallo-knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="bcffa-116">Het Hallo hele service omzettingsproces namens een client uitvoert en stuurt Hallo clientaanvraag.</span><span class="sxs-lookup"><span data-stu-id="bcffa-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="bcffa-117">Clients die worden uitgevoerd op Hallo cluster kunnen dus een client-side HTTP-communicatie bibliotheken tootalk toohello target-service gebruiken via Hallo omgekeerde proxy of lokaal uitgevoerd op hetzelfde knooppunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcffa-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Interne communicatie][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="bcffa-119">Microservices uit externe Hallo-cluster is bereikt</span><span class="sxs-lookup"><span data-stu-id="bcffa-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="bcffa-120">Hallo standaard externe communicatiemodel voor microservices is een opt-in-model waarbij elke service rechtstreeks van externe clients kan niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="bcffa-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="bcffa-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), dit is een netwerkgrens tussen microservices en externe clients voert netwerkadresomzetting en forwards externe aanvragen toointernal IP: poort eindpunten.</span><span class="sxs-lookup"><span data-stu-id="bcffa-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="bcffa-122">toomake een microservice eindpunt rechtstreeks toegankelijk tooexternal clients, moet u eerst configureren Load Balancer tooforward verkeer tooeach poort die Hallo service gebruikt in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="bcffa-123">De meeste microservices, met name stateful microservices live niet bovendien op alle knooppunten van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="bcffa-124">Hallo microservices kunt verplaatsen tussen knooppunten op failover.</span><span class="sxs-lookup"><span data-stu-id="bcffa-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="bcffa-125">In dergelijke gevallen Load Balancer effectief Hallo locatie kan niet bepalen van het doelknooppunt Hallo van Hallo replica's toowhich moet het doorsturen van verkeer.</span><span class="sxs-lookup"><span data-stu-id="bcffa-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="bcffa-126">Microservices via een omgekeerde proxy uit cluster buiten Hallo Hallo bereikt</span><span class="sxs-lookup"><span data-stu-id="bcffa-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="bcffa-127">U kunt in plaats van het Hallo-poort van een afzonderlijke service wordt geconfigureerd in de Load Balancer, net Hallo poort van Hallo reverse proxy configureren in de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="bcffa-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="bcffa-128">Deze configuratie kiest, kunnen clients buiten Hallo cluster services in de cluster Hallo bereiken met behulp van de omgekeerde proxy Hallo zonder aanvullende configuratie.</span><span class="sxs-lookup"><span data-stu-id="bcffa-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Externe communicatie][0]

> [!WARNING]
> <span data-ttu-id="bcffa-130">Wanneer u Hallo reverse proxy-poort in de Load Balancer configureert, zijn alle microservices in Hallo cluster die een HTTP-eindpunt adresseerbare van buiten Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="bcffa-131">URI-indeling voor het adresseren van services met behulp van Hallo omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="bcffa-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="bcffa-132">Hallo omgekeerde proxy gebruikt met die een specifieke uniform resource identifier (URI)-indeling tooidentify Hallo partitie toowhich Hallo binnenkomende serviceaanvraag moet worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="bcffa-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="bcffa-133">**HTTP (s):** Hallo omgekeerde proxy kan worden geconfigureerde tooaccept HTTP of HTTPS-verkeer.</span><span class="sxs-lookup"><span data-stu-id="bcffa-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="bcffa-134">Voor het doorsturen van HTTPS, Raadpleeg te[secure tooa-service verbinding met de reverse proxy Hallo](service-fabric-reverseproxy-configure-secure-communication.md) zodra u omgekeerde proxy setup toolisten op HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bcffa-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="bcffa-135">**Cluster volledig gekwalificeerde domeinnaam (FQDN) | intern IP-adres:** voor externe clients, kunt u omgekeerde proxy Hallo configureren zodat deze bereikbaar is via Hallo clusterdomein, zoals mycluster.eastus.cloudapp.azure.com. Hallo omgekeerde proxy wordt standaard uitgevoerd op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bcffa-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="bcffa-136">Voor interne verkeer worden Hallo reverse proxy bereikt op localhost of op een knooppunt van interne IP-adres bijvoorbeeld 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="bcffa-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="bcffa-137">**Poort:** dit Hallo-poort, zoals 19081, die is opgegeven voor de reverse proxy Hallo is.</span><span class="sxs-lookup"><span data-stu-id="bcffa-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="bcffa-138">**ServiceInstanceName:** volledig gekwalificeerde naam op Hallo van Hallo geïmplementeerd service-exemplaar dat u tooreach zonder Hallo probeert "fabric: / ' schema.</span><span class="sxs-lookup"><span data-stu-id="bcffa-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="bcffa-139">Bijvoorbeeld: tooreach hello *fabric: / myapp/MijnService/* service, die u wilt gebruiken *myapp/MijnService*.</span><span class="sxs-lookup"><span data-stu-id="bcffa-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="bcffa-140">Hallo exemplaar servicenaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="bcffa-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="bcffa-141">Gebruik een ander hoofdlettergebruik voor Hallo-exemplaarnaam in Hallo-URL zorgt ervoor dat Hallo aanvragen toofail met 404 (niet gevonden).</span><span class="sxs-lookup"><span data-stu-id="bcffa-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="bcffa-142">**Achtervoegsel-pad:** dit Hallo werkelijke URL-pad, zoals is *myapi/waarden/toevoegen/3*, voor Hallo-service die u wilt dat tooconnect naar.</span><span class="sxs-lookup"><span data-stu-id="bcffa-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="bcffa-143">**PartitionKey:** voor een gepartitioneerde service, is dit Hallo berekende partitiesleutel van dat u wilt dat tooreach Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="bcffa-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="bcffa-144">Dit is *niet* Hallo partitie-ID GUID.</span><span class="sxs-lookup"><span data-stu-id="bcffa-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="bcffa-145">Deze parameter is niet vereist voor services die gebruikmaken van Hallo singleton-partitieschema.</span><span class="sxs-lookup"><span data-stu-id="bcffa-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="bcffa-146">**PartitionKind:** dit partitieschema Hallo-service is.</span><span class="sxs-lookup"><span data-stu-id="bcffa-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="bcffa-147">Dit kan zijn 'Int64Range' of 'Met de naam'.</span><span class="sxs-lookup"><span data-stu-id="bcffa-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="bcffa-148">Deze parameter is niet vereist voor services die gebruikmaken van Hallo singleton-partitieschema.</span><span class="sxs-lookup"><span data-stu-id="bcffa-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="bcffa-149">**ListenerName** Hallo eindpunten van Hallo-service zijn Hallo vorm {"Eindpunten": {'Listener1': '1', 'Listener2': 'Endpoint2'...}}.</span><span class="sxs-lookup"><span data-stu-id="bcffa-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="bcffa-150">Wanneer het Hallo-service geeft meerdere eindpunten, Hallo eindpunt herkent hieraan die clientaanvraag Hallo moet worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="bcffa-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="bcffa-151">Dit kan worden weggelaten als Hallo-service slechts één listener heeft.</span><span class="sxs-lookup"><span data-stu-id="bcffa-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="bcffa-152">**TargetReplicaSelector** Hiermee wordt aangegeven hoe Hallo doelreplica of instantie moet worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="bcffa-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="bcffa-153">Wanneer de doelservice Hallo stateful is, Hallo TargetReplicaSelector kan bestaan uit een van de volgende Hallo: 'PrimaryReplica', 'RandomSecondaryReplica' of 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="bcffa-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="bcffa-154">Als deze parameter niet is opgegeven, is standaard Hallo 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="bcffa-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="bcffa-155">Wanneer de doelservice Hallo staatloze, hervat omgekeerde proxy een willekeurig exemplaar van Hallo partitie tooforward Hallo serviceaanvraag aan.</span><span class="sxs-lookup"><span data-stu-id="bcffa-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="bcffa-156">**Time-out:** Hiermee Hallo time-out voor gemaakt door Hallo omgekeerde proxy toohello service namens de clientaanvraag Hallo Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bcffa-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="bcffa-157">Hallo-standaardwaarde is 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="bcffa-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="bcffa-158">Dit is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="bcffa-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="bcffa-159">Voorbeeld van syntaxis</span><span class="sxs-lookup"><span data-stu-id="bcffa-159">Example usage</span></span>
<span data-ttu-id="bcffa-160">Als u bijvoorbeeld eens Hallo *fabric: / MyApp/MyService* service die Hiermee opent u een HTTP-listener op Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="bcffa-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="bcffa-161">Hieronder vindt u Hallo informatiebronnen voor Hallo-service:</span><span class="sxs-lookup"><span data-stu-id="bcffa-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="bcffa-162">Als Hallo-service Hallo singleton partitieschema gebruikt, Hallo *PartitionKey* en *PartitionKind* queryreeksparameters zijn niet vereist en het Hallo-service kan worden bereikt met behulp van de gateway Hallo als:</span><span class="sxs-lookup"><span data-stu-id="bcffa-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="bcffa-163">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="bcffa-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="bcffa-164">Intern:`http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="bcffa-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="bcffa-165">Als Hallo-service Hallo Uniform Int64 partitieschema gebruikt, Hallo *PartitionKey* en *PartitionKind* queryreeksparameters gebruikte tooreach een partitie van Hallo-service moeten zijn:</span><span class="sxs-lookup"><span data-stu-id="bcffa-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="bcffa-166">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="bcffa-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="bcffa-167">Intern:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="bcffa-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="bcffa-168">Hallo bronpad tooreach Hallo resources die Hallo-service geeft, geplaatst na de servicenaam Hallo Hallo URL:</span><span class="sxs-lookup"><span data-stu-id="bcffa-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="bcffa-169">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="bcffa-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="bcffa-170">Intern:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="bcffa-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="bcffa-171">Hallo gateway stuurt vervolgens deze aanvragen toohello-service-URL:</span><span class="sxs-lookup"><span data-stu-id="bcffa-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="bcffa-172">Speciale verwerking voor het delen van poort services</span><span class="sxs-lookup"><span data-stu-id="bcffa-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="bcffa-173">Azure Application Gateway probeert tooresolve een service adres opnieuw en probeer Hallo aanvraag als een service kan niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="bcffa-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="bcffa-174">Dit is een belangrijk voordeel van Application Gateway omdat clientcode niet tooimplement een eigen service-oplossing nodig en omzetten van de lus.</span><span class="sxs-lookup"><span data-stu-id="bcffa-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="bcffa-175">In het algemeen als een service kan niet worden bereikt, is Hallo service-exemplaar of de replica verplaatst tooa ander knooppunt als onderdeel van de normale levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="bcffa-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="bcffa-176">Als dit gebeurt, kan een netwerk verbinding fout die aangeeft dat een eindpunt is dat niet langer openen op Hallo opgelost oorspronkelijk adres Application Gateway ontvangen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="bcffa-177">Echter replica's of service-exemplaren kunnen delen een hostproces verstrekt en mogelijk ook delen van een poort wanneer deze wordt gehost door een op basis van het http.sys-webserver, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="bcffa-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="bcffa-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="bcffa-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="bcffa-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="bcffa-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="bcffa-180">Katana</span><span class="sxs-lookup"><span data-stu-id="bcffa-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="bcffa-181">In dit geval is het waarschijnlijk dat Hallo webserver is beschikbaar in het hostproces van Hallo en toorequests, maar Hallo opgelost service-exemplaar of replica is niet meer beschikbaar op Hallo host reageert.</span><span class="sxs-lookup"><span data-stu-id="bcffa-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="bcffa-182">Hallo gateway ontvangt in dit geval een HTTP 404-respons van Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="bcffa-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="bcffa-183">Een HTTP 404 is dus twee verschillende betekenis:</span><span class="sxs-lookup"><span data-stu-id="bcffa-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="bcffa-184">Case #1: adres van de Hallo-service correct is, maar Hallo resource die Hallo aangevraagde gebruiker bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="bcffa-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="bcffa-185">Case #2: serviceadres Hallo is onjuist en Hallo resource die Hallo aangevraagde gebruiker bestaat mogelijk op een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bcffa-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="bcffa-186">het eerste geval Hallo is een normale HTTP 404, wordt beschouwd als een gebruikersfout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="bcffa-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="bcffa-187">Hallo gebruiker heeft echter in de tweede geval Hallo aangevraagd een resource die bestaat.</span><span class="sxs-lookup"><span data-stu-id="bcffa-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="bcffa-188">Application Gateway is toolocate die deze omdat het Hallo-service zelf is verplaatst.</span><span class="sxs-lookup"><span data-stu-id="bcffa-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="bcffa-189">Toepassing behoeften tooresolve Hallo gatewayadres opnieuw en probeer het opnieuw Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bcffa-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="bcffa-190">Toepassingsgateway moet dus een toodistinguish manier tussen deze twee gevallen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="bcffa-191">toomake dat onderscheid, een hint van Hallo-server vereist is.</span><span class="sxs-lookup"><span data-stu-id="bcffa-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="bcffa-192">Standaard Application Gateway wordt ervan uitgegaan dat het geval #2 en tooresolve en probleem Hallo aanvraag opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="bcffa-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="bcffa-193">tooindicate geval #1 tooApplication Gateway Hallo-service moet Hallo volgende HTTP-antwoordheader retourneren:</span><span class="sxs-lookup"><span data-stu-id="bcffa-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="bcffa-194">Deze HTTP-antwoordheader geeft een situatie met een normale HTTP 404 in welke Hallo aangevraagde resource niet bestaat en Application Gateway tooresolve Hallo-serviceadres niet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="bcffa-195">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="bcffa-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="bcffa-196">Inschakelen van omgekeerde proxy via Azure portal</span><span class="sxs-lookup"><span data-stu-id="bcffa-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="bcffa-197">Azure portal biedt een optie tooenable omgekeerde proxy tijdens het maken van een nieuwe Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="bcffa-198">Onder **maken Service Fabric-cluster**, stap 2: clusterconfiguratie, configuratie van het type, Hallo selectievakje te selecteren 'Enable reverse proxy'.</span><span class="sxs-lookup"><span data-stu-id="bcffa-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="bcffa-199">Voor het configureren van beveiligde omgekeerde proxy SSL-certificaat kan worden opgegeven in stap 3: beveiliging, beveiligingsinstellingen voor het cluster configureren, selecteer Hallo selectievakje te 'Bevatten een SSL-certificaat voor reverse proxy' en Voer Hallo Certificaatdetails.</span><span class="sxs-lookup"><span data-stu-id="bcffa-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="bcffa-200">Inschakelen van omgekeerde proxy via Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="bcffa-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="bcffa-201">U kunt Hallo [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) tooenable Hallo omgekeerde proxy in Service Fabric voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="bcffa-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="bcffa-202">Raadpleeg te[HTTPS Reverse Proxy configureren in een beveiligde cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) voor Azure Resource Manager-sjabloon tooconfigure beveiligde omgekeerde proxy met een certificaat en verwerking van certificaat rollover voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="bcffa-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="bcffa-203">Eerst, ontvangt u Hallo-sjabloon voor Hallo-cluster dat u wilt dat toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bcffa-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="bcffa-204">U kunt voorbeeldsjablonen hello gebruiken of een aangepaste Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="bcffa-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="bcffa-205">Vervolgens kunt u omgekeerde proxy Hallo inschakelen met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bcffa-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="bcffa-206">Een poort voor de reverse proxy Hallo definiëren in Hallo [gedeelte Parameters](../azure-resource-manager/resource-group-authoring-templates.md) van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="bcffa-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="bcffa-207">Hallo-poort opgeven voor elke Hallo nodetype objecten in Hallo **Cluster** [resourcesectie type](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bcffa-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="bcffa-208">Hallo-poort wordt aangeduid met parameternamen hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="bcffa-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="bcffa-209">tooaddress hello omgekeerde proxy van externe hello Azure cluster hello Azure Load Balancer regels voor Hallo-poort die u hebt opgegeven in stap 1 instellen.</span><span class="sxs-lookup"><span data-stu-id="bcffa-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="bcffa-210">SSL-certificaten op Hallo-poort voor de reverse proxy Hallo tooconfigure toevoegen Hallo certificaat toohello ***reverseProxyCertificate*** eigenschap in Hallo **Cluster** [type resourcesectie](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bcffa-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="bcffa-211">Ondersteuning van een reverse proxycertificaat dat afwijkt van Hallo cluster certificaat</span><span class="sxs-lookup"><span data-stu-id="bcffa-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="bcffa-212">Als Hallo reverse proxy-certificaat af van het Hallo-certificaat dat Hallo cluster beveiligt wijkt, moeten Hallo eerder opgegeven certificaat moet worden geïnstalleerd op Hallo virtuele machine en toohello toegangsbeheerlijst (ACL) toegevoegd zodat Service Fabric kunt toegang tot dit.</span><span class="sxs-lookup"><span data-stu-id="bcffa-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="bcffa-213">Dit kan worden gedaan in Hallo **virtualMachineScaleSets** [resourcesectie type](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bcffa-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="bcffa-214">Voor installatie, voegt u dat certificaat toohello osProfile.</span><span class="sxs-lookup"><span data-stu-id="bcffa-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="bcffa-215">Hallo-extensie-gedeelte van Hallo sjabloon kunt Hallo certificaat in Hallo ACL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="bcffa-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="bcffa-216">Wanneer u certificaten die afwijken van Hallo cluster certificaat tooenable Hallo omgekeerde proxy op een bestaand cluster gebruikt, Hallo reverse proxy-certificaat installeren en bijwerken Hallo ACL op Hallo cluster voordat u Hallo omgekeerde proxy inschakelt.</span><span class="sxs-lookup"><span data-stu-id="bcffa-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="bcffa-217">Volledige Hallo [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) implementatie met behulp van Hallo instellingen vermeld eerder voordat u begint met een omgekeerde proxy voor implementatie tooenable Hallo in stap 1-4.</span><span class="sxs-lookup"><span data-stu-id="bcffa-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcffa-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bcffa-218">Next steps</span></span>
* <span data-ttu-id="bcffa-219">Een voorbeeld bekijken van HTTP-communicatie tussen services in een [voorbeeldproject op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="bcffa-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="bcffa-220">Toosecure HTTP-service doorsturen met de reverse proxy Hallo</span><span class="sxs-lookup"><span data-stu-id="bcffa-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="bcffa-221">Externe procedureaanroepen weer dat met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="bcffa-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="bcffa-222">Web-API die gebruikmaakt van OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bcffa-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="bcffa-223">WCF-communicatie met behulp van Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bcffa-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="bcffa-224">Raadpleeg voor aanvullende reverse proxy-configuratie-opties ApplicationGateway/Http-sectie in [aanpassen Service Fabric-clusterinstellingen](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="bcffa-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
