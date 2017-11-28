---
title: overzicht van de communicatie aaaReliable Services | Microsoft Docs
description: Overzicht van Hallo Reliable Services communicatiemodel, inclusief openen listeners van services, het omzetten van eindpunten en communicatie tussen services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="c31a3-103">Hoe toouse Hallo Reliable Services communicatie API 's</span><span class="sxs-lookup"><span data-stu-id="c31a3-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="c31a3-104">Azure Service Fabric als platform is volledig agnostisch over de communicatie tussen services.</span><span class="sxs-lookup"><span data-stu-id="c31a3-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="c31a3-105">Alle protocollen en stacks zijn aanvaardbaar van UDP-tooHTTP.</span><span class="sxs-lookup"><span data-stu-id="c31a3-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="c31a3-106">Is toohello service developer toochoose hoe services moeten communiceren.</span><span class="sxs-lookup"><span data-stu-id="c31a3-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="c31a3-107">toepassingsframework voor Hallo Reliable Services biedt ingebouwde communicatie stacks en API's waarmee u toobuild kunt Communicatieonderdelen van uw aangepaste.</span><span class="sxs-lookup"><span data-stu-id="c31a3-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="c31a3-108">Servicecommunicatie instellen</span><span class="sxs-lookup"><span data-stu-id="c31a3-108">Set up service communication</span></span>
<span data-ttu-id="c31a3-109">Hallo betrouwbare Services-API maakt gebruik van een eenvoudige interface voor servicecommunicatie.</span><span class="sxs-lookup"><span data-stu-id="c31a3-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="c31a3-110">een eindpunt voor uw service tooopen gewoon deze interface implementeren:</span><span class="sxs-lookup"><span data-stu-id="c31a3-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="c31a3-111">Vervolgens kunt u uw communicatie-listener-implementatie toevoegen door deze terug te geven in een onderdrukking van de methode op basis van een service-klasse.</span><span class="sxs-lookup"><span data-stu-id="c31a3-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="c31a3-112">Voor stateless services:</span><span class="sxs-lookup"><span data-stu-id="c31a3-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="c31a3-113">Voor stateful services:</span><span class="sxs-lookup"><span data-stu-id="c31a3-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="c31a3-114">Stateful betrouwbare services worden nog niet ondersteund in Java.</span><span class="sxs-lookup"><span data-stu-id="c31a3-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="c31a3-115">In beide gevallen moet u een verzameling van listeners retourneren.</span><span class="sxs-lookup"><span data-stu-id="c31a3-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="c31a3-116">Hierdoor kunnen de toolisten van uw service op meerdere eindpunten, met mogelijk verschillende protocollen, met behulp van meerdere listeners.</span><span class="sxs-lookup"><span data-stu-id="c31a3-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="c31a3-117">Bijvoorbeeld, wellicht u een HTTP-listener en een afzonderlijke WebSocket-listener.</span><span class="sxs-lookup"><span data-stu-id="c31a3-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="c31a3-118">Elke listener haalt u een naam en de resulterende verzameling Hallo *naam: adres* paren worden weergegeven als een JSON-object als een client Hallo luisterende adressen voor een service-exemplaar of een partitie aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="c31a3-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="c31a3-119">In een stateless service retourneert Hallo onderdrukking een verzameling ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="c31a3-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="c31a3-120">Een `ServiceInstanceListener` bevat een functie toocreate een `ICommunicationListener(C#) / CommunicationListener(Java)` en hieraan een naam.</span><span class="sxs-lookup"><span data-stu-id="c31a3-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="c31a3-121">Voor stateful services retourneert Hallo onderdrukking een verzameling ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="c31a3-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="c31a3-122">Dit is enigszins afwijken van het bijbehorende equivalent staatloze omdat een `ServiceReplicaListener` heeft een optie tooopen een `ICommunicationListener` op secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="c31a3-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="c31a3-123">Niet alleen kunt u meerdere communicatielisteners gebruiken in een service, maar u kunt ook opgeven welke listeners accepteren van aanvragen op secundaire replica's en welke luistert alleen op primaire replica's.</span><span class="sxs-lookup"><span data-stu-id="c31a3-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="c31a3-124">Bijvoorbeeld, u kunt een ServiceRemotingListener RPC-aanroepen krijgt alleen op primaire replica's hebben en een tweede, aangepaste listener lezen waarmee aanvragen op de secundaire replica's via HTTP:</span><span class="sxs-lookup"><span data-stu-id="c31a3-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="c31a3-125">Bij het maken van meerdere listeners voor een service wordt elke listener **moet** een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="c31a3-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="c31a3-126">Ten slotte beschrijven Hallo-eindpunten die vereist voor de service in Hallo Hallo zijn [servicemanifest](service-fabric-application-model.md) onder de sectie Hallo voor eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c31a3-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="c31a3-127">Hallo communicatie listener toegang tot de Hallo eindpunt systeembronnen toegewezen tooit van Hallo `CodePackageActivationContext` in Hallo `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="c31a3-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="c31a3-128">Hallo-listener kunt vervolgens luisteren naar aanvragen wanneer deze wordt geopend starten.</span><span class="sxs-lookup"><span data-stu-id="c31a3-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="c31a3-129">Eindpunt resources zijn algemene toohello gehele servicepakket en ze worden toegewezen door de Service Fabric Hallo servicepakket is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="c31a3-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="c31a3-130">Meerdere service replica's die worden gehost in dezelfde ServiceHost kan delen Hallo Hallo dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="c31a3-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="c31a3-131">Dit betekent dat communicatie Hallo listener delen van de poort moet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="c31a3-132">Hallo aanbevolen manier om dit te doen voor Hallo communicatie listener toouse Hallo partitie-ID en replica-exemplaar-ID is bij het genereren van Hallo luister-adres.</span><span class="sxs-lookup"><span data-stu-id="c31a3-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="c31a3-133">Registratie van de service-adres</span><span class="sxs-lookup"><span data-stu-id="c31a3-133">Service address registration</span></span>
<span data-ttu-id="c31a3-134">Een systeemservice aangeroepen Hallo *Naming Service* wordt uitgevoerd op de Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="c31a3-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="c31a3-135">Hallo is Naming Service een registrar voor services en de adressen die elk exemplaar of de replica van Hallo service luistert op.</span><span class="sxs-lookup"><span data-stu-id="c31a3-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="c31a3-136">Wanneer Hallo `OpenAsync(C#) / openAsync(Java)` methode van een `ICommunicationListener(C#) / CommunicationListener(Java)` is voltooid, wordt de return-waarde opgehaald in Hallo Naming Service geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c31a3-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="c31a3-137">Deze waarde die wordt gepubliceerd in Hallo Naming Service is een tekenreeks waarvan de waarde van alles op alle zijn kan retourneren.</span><span class="sxs-lookup"><span data-stu-id="c31a3-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="c31a3-138">Deze waarde is wat clients zien wanneer ze voor een adres voor de service Hallo van Hallo Naming Service vragen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="c31a3-139">Service Fabric bevat API's waarmee de clients en andere services toothen vragen voor dit adres met de servicenaam.</span><span class="sxs-lookup"><span data-stu-id="c31a3-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="c31a3-140">Dit is belangrijk omdat Hallo-serviceadres niet statisch is.</span><span class="sxs-lookup"><span data-stu-id="c31a3-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="c31a3-141">Services worden in Hallo cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c31a3-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="c31a3-142">Dit is Hallo-mechanisme waarmee clients tooresolve Hallo adres voor een service luistert.</span><span class="sxs-lookup"><span data-stu-id="c31a3-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="c31a3-143">Voor een volledig overzicht van hoe toowrite een listener communicatie zien [Service Fabric-Web-API-services met OWIN zelf hosting](service-fabric-reliable-services-communication-webapi.md) voor C#, dat u uw eigen HTTP-server-implementatie voor Java schrijven kunt, Zie EchoServer toepassing voorbeeld op https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="c31a3-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="c31a3-144">Communicatie met een service</span><span class="sxs-lookup"><span data-stu-id="c31a3-144">Communicating with a service</span></span>
<span data-ttu-id="c31a3-145">Hallo betrouwbare Services API biedt Hallo bibliotheken toowrite clients die met de services communiceren te volgen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="c31a3-146">Service-eindpunt resolutie</span><span class="sxs-lookup"><span data-stu-id="c31a3-146">Service endpoint resolution</span></span>
<span data-ttu-id="c31a3-147">eerste stap toocommunication Hallo met een service is tooresolve een eindpuntadres van Hallo partitie of het exemplaar van de gewenste tootalk op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c31a3-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="c31a3-148">Hallo `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` hulpprogrammaklasse is een eenvoudige primitief waarmee clients bepalen Hallo-eindpunt van een service tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="c31a3-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="c31a3-149">In de Service Fabric-terminologie Hallo bepalen Hallo-eindpunt van een service wordt waarnaar wordt verwezen tooas hello *service-eindpunt resolutie*.</span><span class="sxs-lookup"><span data-stu-id="c31a3-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="c31a3-150">tooconnect tooservices binnen een cluster, ServicePartitionResolver kunnen worden gemaakt met de standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="c31a3-151">Dit is Hallo-gebruik voor de meeste gevallen aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="c31a3-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="c31a3-152">tooconnect tooservices in een ander cluster, een ServicePartitionResolver kan worden gemaakt met een reeks cluster gateway eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c31a3-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="c31a3-153">Gateway-eindpunten zijn alleen verschillende eindpunten voor het verbinden van toohello hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="c31a3-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="c31a3-154">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c31a3-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="c31a3-155">U kunt ook `ServicePartitionResolver` kan een functie worden opgegeven voor het maken van een `FabricClient` toouse intern:</span><span class="sxs-lookup"><span data-stu-id="c31a3-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="c31a3-156">`FabricClient`Hallo-object dat is gebruikt toocommunicate met Hallo Service Fabric-cluster voor verschillende bewerkingen op Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="c31a3-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="c31a3-157">Dit is handig als u meer controle wilt over de interactie van een service-omzetter partitie met het cluster.</span><span class="sxs-lookup"><span data-stu-id="c31a3-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="c31a3-158">`FabricClient`voert caching intern en is meestal dure toocreate, dus is het belangrijk tooreuse `FabricClient` exemplaren zo veel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="c31a3-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="c31a3-159">Gebruikte tooretrieve Hallo-adres van een service of de partitie van een service voor gepartitioneerde services is een methode oplossen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="c31a3-160">Een serviceadres kan worden omgezet eenvoudig met een ServicePartitionResolver, maar er is meer werk vereist tooensure Hallo opgelost adres correct kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c31a3-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="c31a3-161">De client moet toodetect of Hallo verbindingspoging is mislukt vanwege een tijdelijke fout en kan opnieuw worden uitgevoerd (bijv, service verplaatst of is tijdelijk niet beschikbaar), of een permanente fout (bijv, service is verwijderd of hello aangevraagde resource bestaat niet meer).</span><span class="sxs-lookup"><span data-stu-id="c31a3-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="c31a3-162">Service-exemplaren of replica's kunnen verplaatsen van knooppunt toonode op elk gewenst moment om verschillende redenen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="c31a3-163">Hallo-serviceadres omgezet via ServicePartitionResolver mogelijk verlopen door de clientcode tooconnect probeert Hallo-tijd.</span><span class="sxs-lookup"><span data-stu-id="c31a3-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="c31a3-164">In dat geval opnieuw Hallo-client moet toore oplossen Hallo adres.</span><span class="sxs-lookup"><span data-stu-id="c31a3-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="c31a3-165">Hallo vorige bieden `ResolvedServicePartition` geeft aan dat omzetter behoeften tootry opnieuw Hallo plaats gewoon een cache-adres ophalen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="c31a3-166">Normaal gesproken moet Hallo clientcode niet rechtstreeks met werken Hallo ServicePartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="c31a3-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="c31a3-167">Het is gemaakt en toocommunication client fabrieken in Hallo betrouwbare Services API doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="c31a3-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="c31a3-168">Hallo fabrieken Hallo conflictoplosser intern gebruiken toogenerate een client-object dat gebruikt toocommunicate met services worden kan.</span><span class="sxs-lookup"><span data-stu-id="c31a3-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="c31a3-169">Communicatie-clients en fabrieken</span><span class="sxs-lookup"><span data-stu-id="c31a3-169">Communication clients and factories</span></span>
<span data-ttu-id="c31a3-170">Hallo communicatie factory bibliotheek implementeert een typische opnieuw patroon voor afhandeling van fouten die gemakkelijker is bezig met opnieuw verbindingen tooresolved service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c31a3-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="c31a3-171">Hallo factory-bibliotheek biedt een mechanisme voor opnieuw proberen Hallo terwijl u fout-handlers Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="c31a3-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="c31a3-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Hiermee definieert u base Hallo-interface geïmplementeerd door een client-factory van communicatie waarmee clients die tooa Service Fabric-service communiceren kunnen wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c31a3-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="c31a3-173">implementatie van CommunicationClientFactory is afhankelijk van Hallo communicatiestack gebruikt door de Service Fabric-service Hallo waar Hallo client wil toocommunicate Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c31a3-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="c31a3-174">Hallo betrouwbare Services API biedt een `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="c31a3-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="c31a3-175">Dit biedt een basisimplementatie van Hallo CommunicationClientFactory interface en taken die algemene tooall Hallo communicatie stacks zijn worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c31a3-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="c31a3-176">(Deze taken omvatten het gebruik van een ServicePartitionResolver toodetermine Hallo service-eindpunt).</span><span class="sxs-lookup"><span data-stu-id="c31a3-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="c31a3-177">Clients implementeren meestal Hallo abstracte CommunicationClientFactoryBase klasse toohandle logica die specifieke toohello communicatie-stack is.</span><span class="sxs-lookup"><span data-stu-id="c31a3-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="c31a3-178">Hallo communicatie-client wordt alleen een adres ontvangt en gebruikt deze tooconnect tooa service.</span><span class="sxs-lookup"><span data-stu-id="c31a3-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="c31a3-179">Hallo-client kan elk protocol dat deze wil gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c31a3-179">hello client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="c31a3-180">de clientfabriek van Hallo is primair verantwoordelijk is voor het maken van clients voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="c31a3-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="c31a3-181">Voor clients die een permanente verbinding, zoals een HTTP-client niet onderhouden moet Hallo factory alleen toocreate en return Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="c31a3-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="c31a3-182">Andere protocollen die een permanente verbinding, zoals sommige binaire protocollen onderhoudt moeten ook worden gevalideerd door Hallo factory toodetermine of Hallo verbinding toobe opnieuw gemaakt moet.</span><span class="sxs-lookup"><span data-stu-id="c31a3-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="c31a3-183">Ten slotte is een uitzonderings-handler verantwoordelijk voor het bepalen welke actie tootake wanneer er een uitzondering optreedt.</span><span class="sxs-lookup"><span data-stu-id="c31a3-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="c31a3-184">Uitzonderingen worden onderverdeeld in **herstelbare** en **niet-herstelbare**.</span><span class="sxs-lookup"><span data-stu-id="c31a3-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="c31a3-185">**Niet-herstelbare** uitzonderingen gewoon back toohello aanroeper ophalen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c31a3-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="c31a3-186">**herstelbare** uitzonderingen kunnen verder worden onderverdeeld in **tijdelijke** en **tijdelijke**.</span><span class="sxs-lookup"><span data-stu-id="c31a3-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="c31a3-187">**Tijdelijke** uitzonderingen zijn die eenvoudig kunnen worden verwerkt zonder het eindpuntadres Hallo-service opnieuw op te lossen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="c31a3-188">Hierbij gaat het tijdelijke netwerkproblemen of service-foutberichten dan degene die aangeven welke eindpuntadres Hallo-service bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="c31a3-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="c31a3-189">**Niet-tijdelijke** uitzonderingen zijn die Hallo service-eindpunt adres toobe opnieuw opgelost vereisen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="c31a3-190">Het gaat hierbij om uitzonderingen die wijzen op Hallo service-eindpunt kan niet worden bereikt, die aangeeft Hallo-service heeft tooa ander knooppunt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c31a3-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="c31a3-191">Hallo `TryHandleException` maakt een beslissing over een bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="c31a3-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="c31a3-192">Als het **niet weet** welke toomake beslissingen over een uitzondering moet retourneren **false**.</span><span class="sxs-lookup"><span data-stu-id="c31a3-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="c31a3-193">Als het **weet** welke toomake besluit moet dienovereenkomstig Hallo resultaat ingesteld en geretourneerd **true**.</span><span class="sxs-lookup"><span data-stu-id="c31a3-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="c31a3-194">Kort samengevat</span><span class="sxs-lookup"><span data-stu-id="c31a3-194">Putting it all together</span></span>
<span data-ttu-id="c31a3-195">Met een `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, en `IExceptionHandler(C#) / ExceptionHandler(Java)` gebaseerd op een communicatieprotocol een `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` helemaal verpakt en biedt Hallo afhandeling van fouten en service partitie adres resolutie lus rond deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="c31a3-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="c31a3-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c31a3-196">Next steps</span></span>
* <span data-ttu-id="c31a3-197">Een voorbeeld bekijken van HTTP-communicatie tussen services in een [C#-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) of [Java-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="c31a3-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="c31a3-198">Externe procedureaanroepen weer dat met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="c31a3-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="c31a3-199">Web-API die gebruikmaakt van OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c31a3-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c31a3-200">WCF-communicatie met behulp van Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c31a3-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
