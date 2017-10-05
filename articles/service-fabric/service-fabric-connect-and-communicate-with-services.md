---
title: Verbinding maken en te communiceren met services in Azure Service Fabric | Microsoft Docs
description: Informatie over het oplossen, verbinding maken en communiceren met Service Fabric-services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="255cc-103">Verbinding maken en te communiceren met Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="255cc-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="255cc-104">In Service Fabric, een service wordt uitgevoerd ergens in een Service Fabric-cluster, doorgaans verdeeld over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="255cc-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="255cc-105">Deze kan worden verplaatst vanaf één locatie naar een andere, door de eigenaar van de service of automatisch door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="255cc-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="255cc-106">Services zijn niet statisch gekoppeld aan een bepaalde machine of een adres.</span><span class="sxs-lookup"><span data-stu-id="255cc-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="255cc-107">Een Service Fabric-toepassing in het algemeen bestaat uit veel verschillende services, waarbij elke service een speciale taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="255cc-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="255cc-108">Deze services kunnen communiceren met elkaar om een volledige functie, zoals de rendering van verschillende onderdelen van een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="255cc-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="255cc-109">Er zijn ook clienttoepassingen die verbinding maken met en communiceren met de services.</span><span class="sxs-lookup"><span data-stu-id="255cc-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="255cc-110">Dit document wordt beschreven hoe u voor het instellen van de communicatie met en tussen uw services in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="255cc-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="255cc-111">Servicecommunicatie wordt ook beschreven in deze video van Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="255cc-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="255cc-112">Breng uw eigen protocol</span><span class="sxs-lookup"><span data-stu-id="255cc-112">Bring your own protocol</span></span>
<span data-ttu-id="255cc-113">Service Fabric helpt de levenscyclus van uw services beheren, maar maakt geen nemen van beslissingen over wat uw services doen.</span><span class="sxs-lookup"><span data-stu-id="255cc-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="255cc-114">Dit omvat communicatie.</span><span class="sxs-lookup"><span data-stu-id="255cc-114">This includes communication.</span></span> <span data-ttu-id="255cc-115">Wanneer uw service wordt geopend door Service Fabric, is dat uw service mogelijkheid voor het instellen van een eindpunt voor binnenkomende aanvragen, ongeacht protocol of communicatie stack die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="255cc-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="255cc-116">Uw service luistert op een normale **IP: poort** adres met behulp van een adresschema gebruiken, zoals een URI.</span><span class="sxs-lookup"><span data-stu-id="255cc-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="255cc-117">Meerdere service-exemplaren of replica's kunnen delen een hostproces in dat geval ze moet verschillende poorten gebruiken of een mechanisme met delen van de poort, zoals het stuurprogramma van de kernel http.sys in Windows.</span><span class="sxs-lookup"><span data-stu-id="255cc-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="255cc-118">In beide gevallen moet elke service-exemplaar of de replica in een hostproces uniek adresseerbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="255cc-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Service-eindpunten][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="255cc-120">Servicedetectie en oplossing</span><span class="sxs-lookup"><span data-stu-id="255cc-120">Service discovery and resolution</span></span>
<span data-ttu-id="255cc-121">In een gedistribueerde systeem kunnen services verplaatsen van de ene machine naar een andere gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="255cc-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="255cc-122">Dit kan gebeuren om verschillende redenen, waaronder resourceverdeling, upgrades, failovers of scale-out.</span><span class="sxs-lookup"><span data-stu-id="255cc-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out.</span></span> <span data-ttu-id="255cc-123">Dit betekent dat adressen van de service-eindpunten wijzigen, omdat de service wordt verplaatst naar de knooppunten met verschillende IP-adressen en op verschillende poorten openen kan als de service gebruikmaakt van een dynamisch geselecteerde poort.</span><span class="sxs-lookup"><span data-stu-id="255cc-123">This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![Distributie van services][7]

<span data-ttu-id="255cc-125">Service Fabric biedt een service voor het opsporen en oplossen met de naam van de Naming Service.</span><span class="sxs-lookup"><span data-stu-id="255cc-125">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="255cc-126">De Naming Service onderhoudt een tabel die is toegewezen met de service-exemplaren en de endpoint-adressen die ze luisteren op naam.</span><span class="sxs-lookup"><span data-stu-id="255cc-126">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="255cc-127">Alle benoemde service-exemplaren in Service Fabric unieke namen weergegeven als URI's, bijvoorbeeld hebben `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="255cc-127">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="255cc-128">De naam van de service niet verandert gedurende de levensduur van de service, is de endpoint-adressen die wijzigen kunnen wanneer services verplaatst.</span><span class="sxs-lookup"><span data-stu-id="255cc-128">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="255cc-129">Dit is vergelijkbaar met websites die constante URL's, maar waarbij het IP-adres kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="255cc-129">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="255cc-130">En vergelijkbare naar DNS op het web en website-URL's worden omgezet in IP-adressen, Service Fabric heeft een registrar die servicenamen wordt toegewezen aan hun eindpuntadres.</span><span class="sxs-lookup"><span data-stu-id="255cc-130">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![Service-eindpunten][2]

<span data-ttu-id="255cc-132">Het omzetten van en verbinding maken met services omvat de volgende stappen uitvoeren in een lus:</span><span class="sxs-lookup"><span data-stu-id="255cc-132">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="255cc-133">**Los**: ophalen van het eindpunt dat een service die beschikbaar heeft gesteld van de Service namen.</span><span class="sxs-lookup"><span data-stu-id="255cc-133">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="255cc-134">**Verbinding maken met**: verbinding maken met de service via het protocol ongeacht gebruikt op dat eindpunt.</span><span class="sxs-lookup"><span data-stu-id="255cc-134">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="255cc-135">**Probeer**: een verbindingspoging kan mislukken voor een aantal redenen, voor als de service is verplaatst sinds de laatste keer dat het eindpuntadres bijvoorbeeld opgelost is.</span><span class="sxs-lookup"><span data-stu-id="255cc-135">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="255cc-136">In dat geval de voorgaande oplossen en stappen moet opnieuw worden geprobeerd verbinding maken en deze cyclus wordt herhaald totdat de verbinding is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="255cc-136">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="255cc-137">Verbinding met andere services</span><span class="sxs-lookup"><span data-stu-id="255cc-137">Connecting to other services</span></span>
<span data-ttu-id="255cc-138">Services met elkaar verbinden in een cluster in het algemeen kunnen rechtstreeks toegang tot de eindpunten van andere services, omdat de knooppunten in een cluster zich op hetzelfde lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="255cc-138">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="255cc-139">Als u wilt maken is eenvoudiger verbinding maken tussen services, Service Fabric bevat aanvullende services die gebruikmaken van de Naming Service.</span><span class="sxs-lookup"><span data-stu-id="255cc-139">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="255cc-140">Een DNS-service en een omgekeerde proxy-service.</span><span class="sxs-lookup"><span data-stu-id="255cc-140">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="255cc-141">DNS-service</span><span class="sxs-lookup"><span data-stu-id="255cc-141">DNS service</span></span>
<span data-ttu-id="255cc-142">Omdat veel services vooral beperkte services, een bestaande URL-naam kunnen hebben, kunnen deze oplossen met behulp van de standaard DNS-protocol (in plaats van het protocol Naming Service) het is zeer handig, met name in scenario's voor toepassing 'lift- en verschuiven'.</span><span class="sxs-lookup"><span data-stu-id="255cc-142">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="255cc-143">Dit is precies wat de DNS-service bestaat.</span><span class="sxs-lookup"><span data-stu-id="255cc-143">This is exactly what the DNS service does.</span></span> <span data-ttu-id="255cc-144">Hiermee kunt u DNS-namen toewijzen aan een servicenaam en daarom eindpunt IP-adressen omzetten.</span><span class="sxs-lookup"><span data-stu-id="255cc-144">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="255cc-145">Zoals u in het volgende diagram, wordt de DNS-service, in het Service Fabric-cluster, DNS-namen toegewezen aan Servicenamen die vervolgens worden opgelost door de Naming Service om te retourneren van de endpoint-adressen verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="255cc-145">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="255cc-146">De DNS-naam voor de service is opgegeven op het moment van maken.</span><span class="sxs-lookup"><span data-stu-id="255cc-146">The DNS name for the service is provided at the time of creation.</span></span> 

![Service-eindpunten][9]

<span data-ttu-id="255cc-148">Voor meer informatie over het gebruik van de DNS-service Zie [DNS-service in Azure Service Fabric](service-fabric-dnsservice.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="255cc-148">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="255cc-149">Reverse proxy-service</span><span class="sxs-lookup"><span data-stu-id="255cc-149">Reverse proxy service</span></span>
<span data-ttu-id="255cc-150">De omgekeerde proxy adressen services in het cluster dat toegang biedt tot HTTP-eindpunten, met inbegrip van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="255cc-150">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="255cc-151">De omgekeerde proxy aanzienlijk vereenvoudigt het aanroepen van andere services en de methoden wanneer er een specifieke URI-indeling en verwerkt de resolve verbinding, probeer stappen die nodig zijn voor één service om te communiceren met een andere met behulp van de service namen.</span><span class="sxs-lookup"><span data-stu-id="255cc-151">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Serivce.</span></span> <span data-ttu-id="255cc-152">Het verborgen met andere woorden, de Naming Service van u bij het aanroepen van andere services door het maken van dit net zo eenvoudig als het aanroepen van een URL.</span><span class="sxs-lookup"><span data-stu-id="255cc-152">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Service-eindpunten][10]

<span data-ttu-id="255cc-154">Zie voor meer informatie over het gebruik van de reverse proxy-service [omgekeerde proxy in Azure Service Fabric](service-fabric-reverseproxy.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="255cc-154">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="255cc-155">Verbindingen met externe clients</span><span class="sxs-lookup"><span data-stu-id="255cc-155">Connections from external clients</span></span>
<span data-ttu-id="255cc-156">Services met elkaar verbinden in een cluster in het algemeen kunnen rechtstreeks toegang tot de eindpunten van andere services, omdat de knooppunten in een cluster zich op hetzelfde lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="255cc-156">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="255cc-157">In sommige omgevingen echter een cluster mogelijk achter een load balancer waarmee externe inkomend verkeer via een beperkte set van poorten.</span><span class="sxs-lookup"><span data-stu-id="255cc-157">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="255cc-158">In dergelijke gevallen services kunnen nog steeds met elkaar communiceren en adressen met behulp van de Naming Service omzetten, maar extra stappen moeten worden genomen om externe clients verbinding maken met services toestaan.</span><span class="sxs-lookup"><span data-stu-id="255cc-158">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="255cc-159">Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="255cc-159">Service Fabric in Azure</span></span>
<span data-ttu-id="255cc-160">Een Service Fabric-cluster in Azure wordt geplaatst achter een Load Balancer van Azure.</span><span class="sxs-lookup"><span data-stu-id="255cc-160">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="255cc-161">Alle externe verkeer naar het cluster moet doorgeven aan de load balancer.</span><span class="sxs-lookup"><span data-stu-id="255cc-161">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="255cc-162">De load balancer wordt automatisch doorsturen van verkeer inkomend verkeer op een opgegeven poort in een willekeurige *knooppunt* die dezelfde poort geopend is.</span><span class="sxs-lookup"><span data-stu-id="255cc-162">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="255cc-163">De Azure Load Balancer alleen bewust van poorten geopend op de *knooppunten*, niet weet over poorten openen door afzonderlijke *services*.</span><span class="sxs-lookup"><span data-stu-id="255cc-163">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure Load Balancer en Service Fabric-topologie][3]

<span data-ttu-id="255cc-165">Bijvoorbeeld, om te kunnen accepteren van externe verkeer op poort **80**, de volgende zaken moeten worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="255cc-165">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="255cc-166">Schrijven van een service die op poort 80 luistert.</span><span class="sxs-lookup"><span data-stu-id="255cc-166">Write a service that listens on port 80.</span></span> <span data-ttu-id="255cc-167">Poort 80 in de service ServiceManifest.xml configureren en open een listener in de service, bijvoorbeeld een host zichzelf webserver.</span><span class="sxs-lookup"><span data-stu-id="255cc-167">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="255cc-168">Een Service Fabric-Cluster in Azure maken en Geef poort **80** als een aangepaste endpoint-poort voor het knooppunttype die als host voor de service fungeert.</span><span class="sxs-lookup"><span data-stu-id="255cc-168">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="255cc-169">Als u meer dan één knooppunttype hebt, kunt u instellen een *plaatsing beperking* op de service zodat deze kan alleen worden uitgevoerd op het knooppunttype met de aangepaste eindpuntpoort geopend.</span><span class="sxs-lookup"><span data-stu-id="255cc-169">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![Een poort op een knooppunttype openen][4]
3. <span data-ttu-id="255cc-171">Zodra het cluster is gemaakt, moet u de Azure Load Balancer configureren in de clusterbrongroep voor het doorsturen van verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="255cc-171">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="255cc-172">Wanneer u een cluster via de Azure portal, is deze ingesteld automatisch voor elke aangepaste endpoint-poort die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="255cc-172">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Doorsturen van verkeer in de Azure Load Balancer][5]
4. <span data-ttu-id="255cc-174">De Azure Load Balancer gebruikmaakt van een test om te bepalen of verkeer te verzenden naar een bepaald knooppunt.</span><span class="sxs-lookup"><span data-stu-id="255cc-174">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="255cc-175">De test controleert regelmatig of er een eindpunt op elk knooppunt om te bepalen of het knooppunt reageert.</span><span class="sxs-lookup"><span data-stu-id="255cc-175">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="255cc-176">Als de test geen reactie ontvangen na een geconfigureerde aantal keren, stopt de load balancer verkeer kunnen verzenden naar dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="255cc-176">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="255cc-177">Bij het maken van een cluster via de Azure portal is een test automatisch ingesteld voor elke aangepaste endpoint-poort die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="255cc-177">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Doorsturen van verkeer in de Azure Load Balancer][8]

<span data-ttu-id="255cc-179">Het is belangrijk te weten dat de Load Balancer van Azure en de test alleen weten over de *knooppunten*, niet de *services* uitgevoerd op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="255cc-179">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="255cc-180">De Azure Load Balancer wordt altijd verkeer verzenden naar knooppunten die op de test, reageren dus wees voorzichtig om ervoor te zorgen services beschikbaar zijn op de knooppunten die kunnen reageren op de test.</span><span class="sxs-lookup"><span data-stu-id="255cc-180">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="255cc-181">Betrouwbare Services: Opties van de ingebouwde communicatie API</span><span class="sxs-lookup"><span data-stu-id="255cc-181">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="255cc-182">Het framework Reliable Services geleverd met verschillende vooraf samengestelde communicatieopties.</span><span class="sxs-lookup"><span data-stu-id="255cc-182">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="255cc-183">De beslissing over welke een voor u geschikt is afhankelijk van de keuze van het programmeermodel, de communicatie-framework en de programmeertaal die uw services zijn geschreven in.</span><span class="sxs-lookup"><span data-stu-id="255cc-183">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="255cc-184">**Er is geen specifieke protocol:** als u niet een bepaalde keuze van communicatie framework hebt, maar u iets up snel gebruiksklaar wilt maken, is de ideale oplossing voor u [remoting service](service-fabric-reliable-services-communication-remoting.md), waardoor externe procedure sterk getypeerde roept voor Reliable Services en Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="255cc-184">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="255cc-185">Dit is het snelst en eenvoudigst manier aan de slag met servicecommunicatie.</span><span class="sxs-lookup"><span data-stu-id="255cc-185">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="255cc-186">Service voor externe toegang zorgt omzetting van de service-adressen, verbinding, probeer het opnieuw en foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="255cc-186">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="255cc-187">Dit is beschikbaar voor zowel C# en Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="255cc-187">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="255cc-188">**HTTP**: voor taal networkdirect communicatie, HTTP biedt een keuze industriestandaard met hulpprogramma's en HTTP-servers die beschikbaar zijn in verschillende talen, geheel ondersteund door Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="255cc-188">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="255cc-189">Services kunnen elke beschikbaar is, met inbegrip van HTTP-stack gebruiken [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) voor C#-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="255cc-189">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="255cc-190">Clients die zijn geschreven in C# kunnen gebruikmaken van de `ICommunicationClient` en `ServicePartitionClient` klassen, terwijl voor Java, gebruikt u de `CommunicationClient` en `FabricServicePartitionClient` klassen, [voor omzetting van de service, HTTP-verbindingen en probeer het opnieuw lussen](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="255cc-190">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="255cc-191">**WCF**: als u bestaande code die gebruikmaakt van WCF als uw communicatie-framework hebt, dan kunt u de `WcfCommunicationListener` voor de serverzijde en `WcfCommunicationClient` en `ServicePartitionClient` klassen voor de client.</span><span class="sxs-lookup"><span data-stu-id="255cc-191">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="255cc-192">Dit echter is alleen beschikbaar voor C#-toepassingen op Windows gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="255cc-192">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="255cc-193">Zie voor meer informatie in dit artikel over [WCF-gebaseerde implementatie van de communicatiestack](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="255cc-193">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="255cc-194">Met behulp van aangepaste protocollen en andere frameworks communicatie</span><span class="sxs-lookup"><span data-stu-id="255cc-194">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="255cc-195">Services kunnen gebruiken elke protocol of elk framework voor communicatie gebruikt, ongeacht of dit een aangepast binaire protocol via TCP-sockets of streaming-gebeurtenissen via [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) of [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="255cc-195">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="255cc-196">Service Fabric bevat communicatie API's die u uw communicatiestack in, sluit kunt terwijl het werk om te detecteren en verbinding maken is gescheiden van u.</span><span class="sxs-lookup"><span data-stu-id="255cc-196">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="255cc-197">Raadpleeg dit artikel over de [betrouwbare Service communicatiemodel](service-fabric-reliable-services-communication.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="255cc-197">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="255cc-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="255cc-198">Next steps</span></span>
<span data-ttu-id="255cc-199">Meer informatie over de concepten en de beschikbare API's in de [Reliable Services communicatiemodel](service-fabric-reliable-services-communication.md), vervolgens snel aan de slag met [remoting service](service-fabric-reliable-services-communication-remoting.md) of Ga voor informatie over het schrijven van een mededeling diepgaande listener met [Web-API met OWIN zelf host](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="255cc-199">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
