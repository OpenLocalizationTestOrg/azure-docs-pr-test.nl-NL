---
title: aaaConnect en communiceren met services in Azure Service Fabric | Microsoft Docs
description: Ontdek hoe tooresolve, verbinding maken en communiceren met Service Fabric-services.
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
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="231b3-103">Verbinding maken en te communiceren met Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="231b3-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="231b3-104">In Service Fabric, een service wordt uitgevoerd ergens in een Service Fabric-cluster, doorgaans verdeeld over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="231b3-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="231b3-105">Het kan worden verplaatst vanaf één locatie-tooanother op Hallo service-eigenaar, hetzij automatisch door Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="231b3-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="231b3-106">Services is niet statisch gebonden tooa bepaalde machine of het adres.</span><span class="sxs-lookup"><span data-stu-id="231b3-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="231b3-107">Een Service Fabric-toepassing in het algemeen bestaat uit veel verschillende services, waarbij elke service een speciale taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="231b3-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="231b3-108">Deze services kunnen communiceren met elkaar tooform een volledige functie, zoals de rendering van verschillende onderdelen van een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="231b3-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="231b3-109">Er zijn ook toepassingen die verbinding tooand maken met services communiceren client.</span><span class="sxs-lookup"><span data-stu-id="231b3-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="231b3-110">Dit document wordt beschreven hoe tooset communicatie met en tussen uw services in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="231b3-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="231b3-111">Servicecommunicatie wordt ook beschreven in deze video van Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="231b3-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="231b3-112">Breng uw eigen protocol</span><span class="sxs-lookup"><span data-stu-id="231b3-112">Bring your own protocol</span></span>
<span data-ttu-id="231b3-113">Service Fabric helpt Hallo levenscyclus van uw services beheren, maar maakt geen nemen van beslissingen over wat uw services doen.</span><span class="sxs-lookup"><span data-stu-id="231b3-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="231b3-114">Dit omvat communicatie.</span><span class="sxs-lookup"><span data-stu-id="231b3-114">This includes communication.</span></span> <span data-ttu-id="231b3-115">Wanneer uw service wordt geopend door Service Fabric, dat wil zeggen van uw service kans tooset u een eindpunt voor binnenkomende aanvragen, u ongeacht stack-protocol of communicatie met.</span><span class="sxs-lookup"><span data-stu-id="231b3-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="231b3-116">Uw service luistert op een normale **IP: poort** adres met behulp van een adresschema gebruiken, zoals een URI.</span><span class="sxs-lookup"><span data-stu-id="231b3-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="231b3-117">Meerdere service-exemplaren of replica's kunnen een hostproces delen in dat geval ze hetzij toouse verschillende poorten moet of gebruik een mechanisme met delen van de poort, zoals Hallo http.sys kernelstuurprogramma in Windows.</span><span class="sxs-lookup"><span data-stu-id="231b3-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="231b3-118">In beide gevallen moet elke service-exemplaar of de replica in een hostproces uniek adresseerbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="231b3-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Service-eindpunten][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="231b3-120">Servicedetectie en oplossing</span><span class="sxs-lookup"><span data-stu-id="231b3-120">Service discovery and resolution</span></span>
<span data-ttu-id="231b3-121">Services kunnen in een gedistribueerde systeem verplaatsen van één machine tooanother gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="231b3-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="231b3-122">Dit kan gebeuren om verschillende redenen, waaronder resourceverdeling, upgrades, failovers of scale-out. Dit betekent dat adressen van de service-eindpunten wijzigen, omdat de service Hallo toonodes met verschillende IP-adressen wordt verplaatst en op andere poorten kan openen als Hallo-service een dynamisch geselecteerde poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="231b3-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Distributie van services][7]

<span data-ttu-id="231b3-124">Service Fabric bevat een detectie en de resolutie service genoemd Hallo Naming Service.</span><span class="sxs-lookup"><span data-stu-id="231b3-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="231b3-125">Hallo onderhoudt Naming Service een tabel die is toegewezen met de naam service-exemplaren toohello eindpuntadressen die ze luisteren op.</span><span class="sxs-lookup"><span data-stu-id="231b3-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="231b3-126">Alle benoemde service-exemplaren in Service Fabric unieke namen weergegeven als URI's, bijvoorbeeld hebben `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="231b3-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="231b3-127">Hallo-naam van Hallo-service wordt niet gewijzigd tijdens de levensduur Hallo van Hallo-service, maar alleen Hallo endpoint-adressen die wijzigen kunnen wanneer services verplaatst.</span><span class="sxs-lookup"><span data-stu-id="231b3-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="231b3-128">Dit is vergelijkbaar toowebsites die constante URL's, maar waarbij Hallo IP-adres kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="231b3-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="231b3-129">En vergelijkbare tooDNS op Hallo web, die wordt omgezet websiteadressen URL's tooIP, Service Fabric heeft een registrar dat is toegewezen adres van de service namen tootheir-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="231b3-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![Service-eindpunten][2]

<span data-ttu-id="231b3-131">Op te lossen en verbinding maken met tooservices omvat Hallo volgende stappen uit in een lus uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="231b3-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="231b3-132">**Los**: Get Hallo eindpunt dat een service is gepubliceerd vanuit Hallo Naming Service.</span><span class="sxs-lookup"><span data-stu-id="231b3-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="231b3-133">**Verbinding maken met**: toohello service verbinding kunnen maken via het protocol ongeacht gebruikt op dat eindpunt.</span><span class="sxs-lookup"><span data-stu-id="231b3-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="231b3-134">**Probeer**: een verbindingspoging kan mislukken voor een willekeurig aantal redenen, bijvoorbeeld als Hallo-service is verplaatst, omdat het eindpuntadres voor Hallo laatste tijd Hallo is opgelost.</span><span class="sxs-lookup"><span data-stu-id="231b3-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="231b3-135">In dat geval Hallo los voorafgaand aan en maak verbinding stappen moeten toobe opnieuw geprobeerd en deze cyclus wordt herhaald totdat het Hallo-verbinding is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="231b3-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="231b3-136">Verbinding maken met tooother services</span><span class="sxs-lookup"><span data-stu-id="231b3-136">Connecting tooother services</span></span>
<span data-ttu-id="231b3-137">Services tooeach verbinding maken met andere in een cluster in het algemeen rechtstreeks toegang tot Hallo eindpunten van andere services omdat Hallo knooppunten in een cluster op Hallo hetzelfde lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="231b3-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="231b3-138">toomake is eenvoudiger tooconnect tussen services, Service Fabric bevat aanvullende services die gebruikmaken van Hallo Naming Service.</span><span class="sxs-lookup"><span data-stu-id="231b3-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="231b3-139">Een DNS-service en een omgekeerde proxy-service.</span><span class="sxs-lookup"><span data-stu-id="231b3-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="231b3-140">DNS-service</span><span class="sxs-lookup"><span data-stu-id="231b3-140">DNS service</span></span>
<span data-ttu-id="231b3-141">Aangezien veel services, vooral beperkte services, een bestaande URL-naam hebben kunnen, kunnen tooresolve wordt deze met Hallo standaard DNS-protocol (plaats Hallo Naming Service protocol) is zeer handig, met name in de toepassing 'lift- en verschuiven' scenario's.</span><span class="sxs-lookup"><span data-stu-id="231b3-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="231b3-142">Dit is precies welke Hallo DNS-service gebruikt.</span><span class="sxs-lookup"><span data-stu-id="231b3-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="231b3-143">Dit kunt u toomap DNS-namen tooa servicenaam en daarom los eindpunt IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="231b3-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="231b3-144">Als weergegeven in Hallo maps volgende diagram wordt Hallo DNS-service, die wordt uitgevoerd in Hallo Service Fabric-cluster, DNS-namen tooservice namen, die vervolgens door Hallo Naming Service tooreturn Hallo eindpunt adressen tooconnect om te worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="231b3-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="231b3-145">Hallo DNS-naam voor het Hallo-service is opgegeven op Hallo moment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="231b3-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Service-eindpunten][9]

<span data-ttu-id="231b3-147">Voor meer informatie over hoe toouse Hallo DNS-service zien [DNS-service in Azure Service Fabric](service-fabric-dnsservice.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="231b3-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="231b3-148">Reverse proxy-service</span><span class="sxs-lookup"><span data-stu-id="231b3-148">Reverse proxy service</span></span>
<span data-ttu-id="231b3-149">Hallo omgekeerde proxy adressen services in Hallo cluster die beschrijft de HTTP-eindpunten, met inbegrip van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="231b3-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="231b3-150">Hallo omgekeerde proxy vereenvoudigt het aanroepen van andere services en hun methoden wanneer er een specifieke URI-notatie ingangen Hallo oplossen, verbinding maken, opnieuw proberen stappen die nodig zijn voor één service toocommunicate met het gebruik van een andere Hallo Naming Service.</span><span class="sxs-lookup"><span data-stu-id="231b3-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="231b3-151">Met andere woorden, verbergt het Hallo Naming Service van u bij het aanroepen van andere services door het maken van dit net zo eenvoudig als het aanroepen van een URL.</span><span class="sxs-lookup"><span data-stu-id="231b3-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Service-eindpunten][10]

<span data-ttu-id="231b3-153">Raadpleeg voor meer informatie over hoe toouse Hallo reverse proxy-service [omgekeerde proxy in Azure Service Fabric](service-fabric-reverseproxy.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="231b3-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="231b3-154">Verbindingen met externe clients</span><span class="sxs-lookup"><span data-stu-id="231b3-154">Connections from external clients</span></span>
<span data-ttu-id="231b3-155">Services tooeach verbinding maken met andere in een cluster in het algemeen rechtstreeks toegang tot Hallo eindpunten van andere services omdat Hallo knooppunten in een cluster op Hallo hetzelfde lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="231b3-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="231b3-156">In sommige omgevingen echter een cluster mogelijk achter een load balancer waarmee externe inkomend verkeer via een beperkte set van poorten.</span><span class="sxs-lookup"><span data-stu-id="231b3-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="231b3-157">Services kunnen nog steeds in dergelijke gevallen met elkaar communiceren en -adressen in door Hallo Naming Service, maar extra stappen moeten worden genomen tooallow externe clients tooconnect tooservices oplossen.</span><span class="sxs-lookup"><span data-stu-id="231b3-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="231b3-158">Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="231b3-158">Service Fabric in Azure</span></span>
<span data-ttu-id="231b3-159">Een Service Fabric-cluster in Azure wordt geplaatst achter een Load Balancer van Azure.</span><span class="sxs-lookup"><span data-stu-id="231b3-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="231b3-160">Alle externe verkeer toohello cluster moet voldoen via Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="231b3-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="231b3-161">Hallo load balancer wordt automatisch doorsturen van verkeer inkomend verkeer op een willekeurige opgegeven poort tooa *knooppunt* die Hallo dezelfde poort open is.</span><span class="sxs-lookup"><span data-stu-id="231b3-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="231b3-162">Hello Azure Load Balancer alleen bewust van poorten geopend op Hallo *knooppunten*, niet weet over poorten openen door afzonderlijke *services*.</span><span class="sxs-lookup"><span data-stu-id="231b3-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure Load Balancer en Service Fabric-topologie][3]

<span data-ttu-id="231b3-164">Bijvoorbeeld, in volgorde tooaccept externe verkeer op poort **80**, Hallo dingen na moet worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="231b3-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="231b3-165">Schrijven van een service die op poort 80 luistert.</span><span class="sxs-lookup"><span data-stu-id="231b3-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="231b3-166">Configureren van poort 80 in ServiceManifest.xml Hallo-service en open een listener in Hallo-service, bijvoorbeeld een host zichzelf webserver.</span><span class="sxs-lookup"><span data-stu-id="231b3-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="231b3-167">Een Service Fabric-Cluster in Azure maken en Geef poort **80** als aangepaste endpoint-poort voor het knooppunttype Hallo die als host Hallo-service fungeert.</span><span class="sxs-lookup"><span data-stu-id="231b3-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="231b3-168">Als u meer dan één knooppunttype hebt, kunt u instellen een *plaatsing beperking* op Hallo service tooensure alleen wordt uitgevoerd op Hallo knooppunttype met aangepaste eindpuntpoort Hallo geopend.</span><span class="sxs-lookup"><span data-stu-id="231b3-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Een poort op een knooppunttype openen][4]
3. <span data-ttu-id="231b3-170">Nadat u Hallo-cluster is gemaakt, configureert u hello Azure Load Balancer in van het cluster Hallo resourcegroep tooforward verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="231b3-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="231b3-171">Wanneer u een cluster via hello Azure-portal, is deze ingesteld automatisch voor elke aangepaste endpoint-poort die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="231b3-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Doorsturen van verkeer in hello Azure Load Balancer][5]
4. <span data-ttu-id="231b3-173">maakt gebruik van Azure Load Balancer of een test-toodetermine Hallo of niet toosend verkeer tooa bepaald knooppunt.</span><span class="sxs-lookup"><span data-stu-id="231b3-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="231b3-174">Hallo-test regelmatig controles een eindpunt op elk knooppunt toodetermine of Hallo knooppunt reageert.</span><span class="sxs-lookup"><span data-stu-id="231b3-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="231b3-175">Als tooreceive een antwoord Hallo test na een geconfigureerde aantal keren mislukt, stopt Hallo load balancer verkeer toothat knooppunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="231b3-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="231b3-176">Bij het maken van een cluster via hello Azure-portal is een test automatisch ingesteld voor elke aangepaste endpoint-poort die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="231b3-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Doorsturen van verkeer in hello Azure Load Balancer][8]

<span data-ttu-id="231b3-178">Het is belangrijk tooremember die hello Azure Load Balancer- en Hallo test alleen Hallo kent *knooppunten*, niet Hallo *services* uitgevoerd op Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="231b3-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="231b3-179">Hello Azure Load Balancer wordt altijd verkeer toonodes die toohello test reageren verzenden, dus wees voorzichtig tooensure services beschikbaar zijn op Hallo knooppunten die kunnen toorespond toohello test.</span><span class="sxs-lookup"><span data-stu-id="231b3-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="231b3-180">Betrouwbare Services: Opties van de ingebouwde communicatie API</span><span class="sxs-lookup"><span data-stu-id="231b3-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="231b3-181">Hallo Reliable Services framework wordt geleverd met verschillende vooraf samengestelde communicatieopties.</span><span class="sxs-lookup"><span data-stu-id="231b3-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="231b3-182">Hallo beslissing over welke een voor u geschikt is afhankelijk van Hallo keuze Hallo programming model, Hallo communicatie framework en Hallo programmeertaal die uw services zijn geschreven in.</span><span class="sxs-lookup"><span data-stu-id="231b3-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="231b3-183">**Er is geen specifieke protocol:** als u niet een bepaalde keuze van communicatie framework hebt, maar u wilt dat tooget iets up-to-date en actieve snel, is Hallo ideale oplossing voor u [remoting service](service-fabric-reliable-services-communication-remoting.md), waardoor externe procedure sterk getypeerde roept voor Reliable Services en Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="231b3-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="231b3-184">Dit is Hallo eenvoudigste en snelste manier tooget gestart met servicecommunicatie.</span><span class="sxs-lookup"><span data-stu-id="231b3-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="231b3-185">Service voor externe toegang zorgt omzetting van de service-adressen, verbinding, probeer het opnieuw en foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="231b3-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="231b3-186">Dit is beschikbaar voor zowel C# en Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="231b3-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="231b3-187">**HTTP**: voor taal networkdirect communicatie, HTTP biedt een keuze industriestandaard met hulpprogramma's en HTTP-servers die beschikbaar zijn in verschillende talen, geheel ondersteund door Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="231b3-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="231b3-188">Services kunnen elke beschikbaar is, met inbegrip van HTTP-stack gebruiken [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) voor C#-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="231b3-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="231b3-189">Hallo kunnen gebruikmaken van clients die zijn geschreven in C# `ICommunicationClient` en `ServicePartitionClient` klassen, terwijl voor Java, gebruik Hallo `CommunicationClient` en `FabricServicePartitionClient` klassen, [voor omzetting van de service, HTTP-verbindingen en probeer het opnieuw lussen](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="231b3-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="231b3-190">**WCF**: als u bestaande code die gebruikmaakt van WCF als uw communicatie-framework hebt, dan kunt u Hallo `WcfCommunicationListener` voor serverzijde Hallo en `WcfCommunicationClient` en `ServicePartitionClient` klassen voor het Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="231b3-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="231b3-191">Dit echter is alleen beschikbaar voor C#-toepassingen op Windows gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="231b3-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="231b3-192">Zie voor meer informatie in dit artikel over [WCF-gebaseerde implementatie van Hallo communicatiestack](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="231b3-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="231b3-193">Met behulp van aangepaste protocollen en andere frameworks communicatie</span><span class="sxs-lookup"><span data-stu-id="231b3-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="231b3-194">Services kunnen gebruiken elke protocol of elk framework voor communicatie gebruikt, ongeacht of dit een aangepast binaire protocol via TCP-sockets of streaming-gebeurtenissen via [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) of [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="231b3-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="231b3-195">Service Fabric bevat communicatie API's die u uw communicatiestack in, sluit kunt terwijl alle Hallo toodiscover werken en verbinding maken is gescheiden van u.</span><span class="sxs-lookup"><span data-stu-id="231b3-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="231b3-196">Raadpleeg dit artikel over Hallo [betrouwbare Service communicatiemodel](service-fabric-reliable-services-communication.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="231b3-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="231b3-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="231b3-197">Next steps</span></span>
<span data-ttu-id="231b3-198">Meer informatie over concepten Hallo en beschikbare API's in Hallo [Reliable Services communicatiemodel](service-fabric-reliable-services-communication.md), vervolgens snel aan de slag met [remoting service](service-fabric-reliable-services-communication-remoting.md) of gedetailleerde toolearn hoe ga toowrite een communicatie-listener met [Web-API met OWIN zelf host](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="231b3-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
