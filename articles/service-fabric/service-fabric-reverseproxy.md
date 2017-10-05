---
title: Azure Service Fabric omgekeerde proxy | Microsoft Docs
description: Service-Fabric reverse proxy gebruiken voor communicatie met microservices van binnen en buiten het cluster.
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
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="6cad0-103">Azure Service Fabric-omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="6cad0-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="6cad0-104">De omgekeerde proxy die ingebouwd in Azure Service Fabric adressen microservices in het Service Fabric-cluster dat toegang biedt tot HTTP-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="6cad0-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="6cad0-105">Microservices communicatiemodel</span><span class="sxs-lookup"><span data-stu-id="6cad0-105">Microservices communication model</span></span>
<span data-ttu-id="6cad0-106">Microservices in Service Fabric wordt doorgaans uitgevoerd op een subset van virtuele machines in het cluster en kunt verplaatsen van één virtuele machine naar een andere om verschillende redenen.</span><span class="sxs-lookup"><span data-stu-id="6cad0-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="6cad0-107">De eindpunten voor microservices kunnen dus dynamisch wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6cad0-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="6cad0-108">De doorsnee patroon om te communiceren met de microservice is de volgende los lus:</span><span class="sxs-lookup"><span data-stu-id="6cad0-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="6cad0-109">Los de servicelocatie in eerste instantie via de naming service.</span><span class="sxs-lookup"><span data-stu-id="6cad0-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="6cad0-110">Verbinding maken met de service.</span><span class="sxs-lookup"><span data-stu-id="6cad0-110">Connect to the service.</span></span>
3. <span data-ttu-id="6cad0-111">De oorzaak van verbindingsfouten en de servicelocatie opnieuw los indien nodig.</span><span class="sxs-lookup"><span data-stu-id="6cad0-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="6cad0-112">Dit proces omvat doorgaans wrapping communicatie van client-side '-bibliotheken in een herhalingslus waarmee de service-beleid voor resolutie en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6cad0-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="6cad0-113">Zie voor meer informatie [Connect en communiceren met services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="6cad0-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="6cad0-114">Communicatie met behulp van de omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="6cad0-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="6cad0-115">De omgekeerde proxy in Service Fabric wordt uitgevoerd op alle knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="6cad0-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="6cad0-116">Het omzettingsproces van de hele service namens een client uitvoert en stuurt de aanvraag van de client.</span><span class="sxs-lookup"><span data-stu-id="6cad0-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="6cad0-117">Clients die worden uitgevoerd op het cluster kunnen dus alle bibliotheken clientzijde HTTP-communicatie gebruiken voor communicatie met de doelservice met behulp van de omgekeerde proxy die lokaal op hetzelfde knooppunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![Interne communicatie][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="6cad0-119">Microservices van buiten het cluster is bereikt</span><span class="sxs-lookup"><span data-stu-id="6cad0-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="6cad0-120">Het model van de externe communicatie standaard voor microservices is een opt-in-model waarbij elke service rechtstreeks van externe clients kan niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="6cad0-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="6cad0-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), die een netwerkgrens tussen microservices en externe clients voert netwerkadresomzetting en externe aanvragen voor het interne IP: poort eindpunten worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="6cad0-122">U kunt een microservice eindpunt rechtstreeks toegankelijk naar externe clients, moet u eerst de Load Balancer voor het doorsturen van verkeer naar elke poort die de service in het cluster gebruikt configureren.</span><span class="sxs-lookup"><span data-stu-id="6cad0-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="6cad0-123">Bovendien worden de meeste microservices, met name stateful microservices niet live op alle knooppunten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6cad0-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="6cad0-124">De microservices kunt verplaatsen tussen knooppunten op failover.</span><span class="sxs-lookup"><span data-stu-id="6cad0-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="6cad0-125">In dergelijke gevallen Load Balancer kan effectief niet bepalen de locatie van het doelknooppunt van de replica's waarnaar verkeer moet worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="6cad0-126">Microservices via de omgekeerde proxy van buiten het cluster is bereikt</span><span class="sxs-lookup"><span data-stu-id="6cad0-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="6cad0-127">In plaats van de poort van een afzonderlijke service in de Load Balancer configureren, kunt u alleen de poort van de omgekeerde proxy configureren in de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6cad0-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="6cad0-128">Deze configuratie kiest, kunnen clients buiten het cluster te bereiken services binnen het cluster met behulp van de omgekeerde proxy zonder aanvullende configuratie.</span><span class="sxs-lookup"><span data-stu-id="6cad0-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![Externe communicatie][0]

> [!WARNING]
> <span data-ttu-id="6cad0-130">Wanneer u de reverse proxy-poort in de Load Balancer configureert, zijn alle microservices in het cluster die een HTTP-eindpunt adresseerbare van buiten het cluster.</span><span class="sxs-lookup"><span data-stu-id="6cad0-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="6cad0-131">URI-indeling voor het adresseren van services met behulp van de omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="6cad0-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="6cad0-132">De omgekeerde proxy maakt gebruik van een specifieke uniform resource identifier (URI)-indeling voor het identificeren van de service-partitie waarnaar de binnenkomende aanvraag moet worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="6cad0-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="6cad0-133">**HTTP (s):** de omgekeerde proxy voor het accepteren van HTTP of HTTPS-verkeer kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="6cad0-134">Raadpleeg voor HTTPS doorsturen, [verbinding maken met een beveiligde service met de reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) zodra er een omgekeerde proxy-instellingen om te luisteren op HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6cad0-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="6cad0-135">**Cluster volledig gekwalificeerde domeinnaam (FQDN) | intern IP-adres:** voor externe clients, kunt u de omgekeerde proxy configureren zodat deze bereikbaar is via het clusterdomein zoals mycluster.eastus.cloudapp.azure.com. De omgekeerde proxy wordt standaard uitgevoerd op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6cad0-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="6cad0-136">Voor interne verkeer worden de omgekeerde proxy bereikt op localhost of op een knooppunt van interne IP-adres bijvoorbeeld 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="6cad0-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="6cad0-137">**Poort:** dit is de poort, zoals 19081, die is opgegeven voor de omgekeerde proxy.</span><span class="sxs-lookup"><span data-stu-id="6cad0-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="6cad0-138">**ServiceInstanceName:** dit is de volledig gekwalificeerde naam van het geïmplementeerde service-exemplaar dat u probeert te bereiken zonder de "fabric: / ' schema.</span><span class="sxs-lookup"><span data-stu-id="6cad0-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="6cad0-139">Om bijvoorbeeld te bereiken de *fabric: / myapp/MijnService/* service, gebruikt u *myapp/MijnService*.</span><span class="sxs-lookup"><span data-stu-id="6cad0-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="6cad0-140">De naam van de service-exemplaar is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="6cad0-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="6cad0-141">Gebruik een ander hoofdlettergebruik voor de naam van het service-exemplaar in de URL zorgt ervoor dat de aanvragen mislukt met 404 (niet gevonden).</span><span class="sxs-lookup"><span data-stu-id="6cad0-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="6cad0-142">**Achtervoegsel-pad:** dit is het werkelijke URL-pad, zoals *myapi/waarden/toevoegen/3*, voor de service waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="6cad0-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="6cad0-143">**PartitionKey:** voor een gepartitioneerde service, is dit de berekende partitiesleutel van de partitie die u wilt bereiken.</span><span class="sxs-lookup"><span data-stu-id="6cad0-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="6cad0-144">Dit is *niet* de partitie-ID GUID.</span><span class="sxs-lookup"><span data-stu-id="6cad0-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="6cad0-145">Deze parameter is niet vereist voor services die gebruikmaken van het partitieschema singleton.</span><span class="sxs-lookup"><span data-stu-id="6cad0-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="6cad0-146">**PartitionKind:** dit is het partitieschema van de service.</span><span class="sxs-lookup"><span data-stu-id="6cad0-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="6cad0-147">Dit kan zijn 'Int64Range' of 'Met de naam'.</span><span class="sxs-lookup"><span data-stu-id="6cad0-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="6cad0-148">Deze parameter is niet vereist voor services die gebruikmaken van het partitieschema singleton.</span><span class="sxs-lookup"><span data-stu-id="6cad0-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="6cad0-149">**ListenerName** de eindpunten van de service van het formulier zijn {"Eindpunten": {'Listener1': '1', 'Listener2': 'Endpoint2'...}}.</span><span class="sxs-lookup"><span data-stu-id="6cad0-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="6cad0-150">Wanneer de service meerdere eindpunten biedt, herkent hieraan het eindpunt dat de aanvraag van de client moet worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="6cad0-151">Dit kan worden weggelaten als de service slechts één listener heeft.</span><span class="sxs-lookup"><span data-stu-id="6cad0-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="6cad0-152">**TargetReplicaSelector** Hiermee wordt aangegeven hoe de doelreplica of instantie moet worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6cad0-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="6cad0-153">Wanneer de doelservice stateful is, kan de TargetReplicaSelector zijn een van de volgende: 'PrimaryReplica', 'RandomSecondaryReplica' of 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="6cad0-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="6cad0-154">Als deze parameter niet is opgegeven, is de standaardwaarde 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="6cad0-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="6cad0-155">Wanneer de doelservice staatloze, hervat omgekeerde proxy een willekeurig exemplaar van de partitie van de service voor het doorsturen van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6cad0-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="6cad0-156">**Time-out:** Hiermee geeft u de time-out voor de HTTP-aanvragen dat is gemaakt door de omgekeerde proxy voor de service namens de clientaanvraag.</span><span class="sxs-lookup"><span data-stu-id="6cad0-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="6cad0-157">De standaardwaarde is 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="6cad0-157">The default value is 60 seconds.</span></span> <span data-ttu-id="6cad0-158">Dit is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="6cad0-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="6cad0-159">Voorbeeld van syntaxis</span><span class="sxs-lookup"><span data-stu-id="6cad0-159">Example usage</span></span>
<span data-ttu-id="6cad0-160">Als u bijvoorbeeld eens het *fabric: / MyApp/MijnService* service die Hiermee opent u een HTTP-listener op de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="6cad0-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="6cad0-161">Hieronder vindt u de resources voor de service:</span><span class="sxs-lookup"><span data-stu-id="6cad0-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="6cad0-162">Als de service gebruikt de singleton partitieschema, de *PartitionKey* en *PartitionKind* queryreeksparameters zijn niet vereist en de service kan worden bereikt door het gebruik van de gateway als:</span><span class="sxs-lookup"><span data-stu-id="6cad0-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="6cad0-163">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="6cad0-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="6cad0-164">Intern:`http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="6cad0-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="6cad0-165">Als de service het partitieschema Uniform Int64 gebruikt de *PartitionKey* en *PartitionKind* queryreeksparameters worden gebruikt voor het bereiken van een partitie van de service:</span><span class="sxs-lookup"><span data-stu-id="6cad0-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="6cad0-166">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="6cad0-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="6cad0-167">Intern:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="6cad0-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="6cad0-168">Het bereiken van de resources die de service beschikbaar worden gesteld, plaatst u het bronpad achter de servicenaam in de URL:</span><span class="sxs-lookup"><span data-stu-id="6cad0-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="6cad0-169">Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="6cad0-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="6cad0-170">Intern:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="6cad0-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="6cad0-171">De gateway stuurt vervolgens deze aanvragen naar de URL van de service:</span><span class="sxs-lookup"><span data-stu-id="6cad0-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="6cad0-172">Speciale verwerking voor het delen van poort services</span><span class="sxs-lookup"><span data-stu-id="6cad0-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="6cad0-173">Azure Application Gateway probeert omzetten van een serviceadres opnieuw en probeer de aanvraag als een service kan niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="6cad0-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="6cad0-174">Dit is een belangrijk voordeel van Application Gateway omdat clientcode niet hoeft de eigen service-oplossing te implementeren en oplossen van de lus.</span><span class="sxs-lookup"><span data-stu-id="6cad0-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="6cad0-175">In het algemeen als een service kan niet worden bereikt, is de service-exemplaar of de replica verplaatst naar een ander knooppunt als onderdeel van de normale levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="6cad0-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="6cad0-176">Als dit gebeurt, kan een netwerkfout verbinding die wijzen op een eindpunt is niet meer openen op het adres van oorspronkelijk opgelost Application Gateway worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6cad0-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="6cad0-177">Echter replica's of service-exemplaren kunnen delen een hostproces verstrekt en mogelijk ook delen van een poort wanneer deze wordt gehost door een op basis van het http.sys-webserver, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="6cad0-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="6cad0-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="6cad0-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="6cad0-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="6cad0-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="6cad0-180">Katana</span><span class="sxs-lookup"><span data-stu-id="6cad0-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="6cad0-181">In dit geval is het waarschijnlijk dat de webserver is beschikbaar in het hostproces en reageren op aanvragen, maar de opgelost service-exemplaar of de replica niet meer beschikbaar op de host is.</span><span class="sxs-lookup"><span data-stu-id="6cad0-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="6cad0-182">De gateway wordt in dit geval een HTTP 404-reactie ontvangen van de webserver.</span><span class="sxs-lookup"><span data-stu-id="6cad0-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="6cad0-183">Een HTTP 404 is dus twee verschillende betekenis:</span><span class="sxs-lookup"><span data-stu-id="6cad0-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="6cad0-184">Case #1: Het serviceadres juist is, maar de resource die de gebruiker heeft aangevraagd, bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="6cad0-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="6cad0-185">Case #2: Het serviceadres is onjuist en de resource die de gebruiker heeft aangegeven bestaat mogelijk op een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6cad0-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="6cad0-186">Het eerste geval is een normale HTTP 404, wordt beschouwd als een gebruikersfout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="6cad0-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="6cad0-187">De gebruiker heeft echter in het tweede geval verzocht een resource die bestaat.</span><span class="sxs-lookup"><span data-stu-id="6cad0-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="6cad0-188">Application Gateway is niet vinden omdat de service zelf is verplaatst.</span><span class="sxs-lookup"><span data-stu-id="6cad0-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="6cad0-189">Toepassingsgateway moet het omzetten van het adres opnieuw en probeer de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6cad0-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="6cad0-190">Toepassingsgateway moet dus een manier onderscheid maken tussen deze twee gevallen.</span><span class="sxs-lookup"><span data-stu-id="6cad0-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="6cad0-191">Als u dit onderscheid, is een aanwijzing van de server vereist.</span><span class="sxs-lookup"><span data-stu-id="6cad0-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="6cad0-192">Standaard Application Gateway wordt ervan uitgegaan dat het geval #2 en probeert oplossen en de aanvraag opnieuw uitgeven.</span><span class="sxs-lookup"><span data-stu-id="6cad0-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="6cad0-193">Om aan te geven geval #1 aan de toepassingsgateway, moet de service de volgende HTTP-antwoordheader geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="6cad0-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="6cad0-194">Deze HTTP-antwoordheader geeft aan dat een normale HTTP 404-situatie waarin de aangevraagde resource bestaat niet en Application Gateway niet probeert te zetten van het serviceadres opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6cad0-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="6cad0-195">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="6cad0-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="6cad0-196">Inschakelen van omgekeerde proxy via Azure portal</span><span class="sxs-lookup"><span data-stu-id="6cad0-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="6cad0-197">Azure portal biedt een optie voor het inschakelen van omgekeerde proxy tijdens het maken van een nieuwe Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="6cad0-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="6cad0-198">Onder **maken Service Fabric-cluster**, stap 2: clusterconfiguratie, configuratie van het type, schakel het selectievakje wilt inschakelen reverse proxy-'.</span><span class="sxs-lookup"><span data-stu-id="6cad0-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="6cad0-199">Voor het configureren van beveiligde omgekeerde proxy SSL-certificaat kan worden opgegeven in stap 3: beveiliging, beveiligingsinstellingen voor het cluster configureren, schakel het selectievakje ' een SSL-certificaat voor reverse proxy ' en voer de details van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="6cad0-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="6cad0-200">Inschakelen van omgekeerde proxy via Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="6cad0-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="6cad0-201">U kunt de [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) de reverse proxy in Service Fabric voor het cluster in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="6cad0-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="6cad0-202">Raadpleeg [HTTPS Reverse Proxy configureren in een beveiligde cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) voor Azure Resource Manager voorbeelden van de sjabloon voor het configureren van beveiligde reverse proxy gebruikt met een certificaat en verwerking van certificaat rollover.</span><span class="sxs-lookup"><span data-stu-id="6cad0-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="6cad0-203">U krijgt eerst de sjabloon voor het cluster dat u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="6cad0-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="6cad0-204">U kunt de voorbeeldsjablonen gebruiken of een aangepaste Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="6cad0-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="6cad0-205">Vervolgens kunt u de omgekeerde proxy inschakelen met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6cad0-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="6cad0-206">Een poort definiëren voor de reverse proxy in de [gedeelte Parameters](../azure-resource-manager/resource-group-authoring-templates.md) van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6cad0-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="6cad0-207">Geef de poort voor elk van de nodetype objecten in de **Cluster** [resourcesectie type](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6cad0-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="6cad0-208">De poort wordt aangeduid met de parameternaam van de, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="6cad0-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="6cad0-209">Om de omgekeerde proxy van buiten het Azure-cluster op te lossen, regels instellen om de Azure Load Balancer voor de poort die u in stap 1 hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6cad0-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="6cad0-210">Configureren van SSL-certificaten op de poort voor de omgekeerde proxy, het certificaat toevoegen aan de ***reverseProxyCertificate*** eigenschap in de **Cluster** [resourcesectie type](../resource-group-authoring-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="6cad0-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="6cad0-211">Ondersteuning van een reverse proxycertificaat dat afwijkt van de cluster-certificaat</span><span class="sxs-lookup"><span data-stu-id="6cad0-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="6cad0-212">Als de reverse proxy-certificaat van het certificaat dat het cluster beveiligt verschilt, moet klikt u vervolgens het eerder opgegeven certificaat worden geïnstalleerd op de virtuele machine en toegevoegd aan de toegangsbeheerlijst (ACL) zodat de Service Fabric toegang hebt tot het.</span><span class="sxs-lookup"><span data-stu-id="6cad0-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="6cad0-213">Dit kan worden uitgevoerd in de **virtualMachineScaleSets** [resourcesectie type](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6cad0-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="6cad0-214">Voor de installatie, moet u dat certificaat toevoegen aan de osProfile.</span><span class="sxs-lookup"><span data-stu-id="6cad0-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="6cad0-215">De extensie-sectie van de sjabloon kan het certificaat in de ACL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6cad0-215">The extension section of the template can update the certificate in the ACL.</span></span>

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
> <span data-ttu-id="6cad0-216">Wanneer u certificaten die afwijken van het certificaat van de cluster de reverse proxy op een bestaand cluster in te schakelen, de reverse proxy-certificaat installeren en bijwerken van de ACL voor het cluster voordat u de omgekeerde proxy inschakelt.</span><span class="sxs-lookup"><span data-stu-id="6cad0-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="6cad0-217">Voltooi de [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) implementatie met behulp van de instellingen vermeld eerder voordat u begint met een implementatie voor de omgekeerde proxy inschakelen in stap 1-4.</span><span class="sxs-lookup"><span data-stu-id="6cad0-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cad0-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cad0-218">Next steps</span></span>
* <span data-ttu-id="6cad0-219">Een voorbeeld bekijken van HTTP-communicatie tussen services in een [voorbeeldproject op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="6cad0-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="6cad0-220">Met de reverse proxy worden doorgestuurd naar de beveiligde HTTP-service</span><span class="sxs-lookup"><span data-stu-id="6cad0-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="6cad0-221">Externe procedureaanroepen weer dat met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="6cad0-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="6cad0-222">Web-API die gebruikmaakt van OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6cad0-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="6cad0-223">WCF-communicatie met behulp van Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6cad0-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="6cad0-224">Raadpleeg voor aanvullende reverse proxy-configuratie-opties ApplicationGateway/Http-sectie in [aanpassen Service Fabric-clusterinstellingen](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6cad0-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
