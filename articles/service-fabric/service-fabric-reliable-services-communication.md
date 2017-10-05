---
title: Overzicht van de communicatie betrouwbare Services | Microsoft Docs
description: Overzicht van de communicatiemodel Reliable Services, waaronder openen listeners van services, het omzetten van eindpunten en communicatie tussen services.
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
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="ecc48-103">Het gebruik van de communicatie met Reliable Services API 's</span><span class="sxs-lookup"><span data-stu-id="ecc48-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="ecc48-104">Azure Service Fabric als platform is volledig agnostisch over de communicatie tussen services.</span><span class="sxs-lookup"><span data-stu-id="ecc48-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="ecc48-105">Alle protocollen en stacks zijn aanvaardbaar van UDP naar HTTP.</span><span class="sxs-lookup"><span data-stu-id="ecc48-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="ecc48-106">Het is aan de ontwikkelaar van de service om te kiezen hoe services moeten communiceren.</span><span class="sxs-lookup"><span data-stu-id="ecc48-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="ecc48-107">Het framework Reliable Services biedt ingebouwde communicatie stacks, alsmede de API's die u gebruiken kunt voor het bouwen van uw aangepaste communicatie-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="ecc48-108">Servicecommunicatie instellen</span><span class="sxs-lookup"><span data-stu-id="ecc48-108">Set up service communication</span></span>
<span data-ttu-id="ecc48-109">De API voor betrouwbare Services maakt gebruik van een eenvoudige interface voor servicecommunicatie.</span><span class="sxs-lookup"><span data-stu-id="ecc48-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="ecc48-110">U opent een eindpunt voor uw service door deze interface eenvoudig te implementeren:</span><span class="sxs-lookup"><span data-stu-id="ecc48-110">To open an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="ecc48-111">Vervolgens kunt u uw communicatie-listener-implementatie toevoegen door deze terug te geven in een onderdrukking van de methode op basis van een service-klasse.</span><span class="sxs-lookup"><span data-stu-id="ecc48-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="ecc48-112">Voor stateless services:</span><span class="sxs-lookup"><span data-stu-id="ecc48-112">For stateless services:</span></span>

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

<span data-ttu-id="ecc48-113">Voor stateful services:</span><span class="sxs-lookup"><span data-stu-id="ecc48-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="ecc48-114">Stateful betrouwbare services worden nog niet ondersteund in Java.</span><span class="sxs-lookup"><span data-stu-id="ecc48-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="ecc48-115">In beide gevallen moet u een verzameling van listeners retourneren.</span><span class="sxs-lookup"><span data-stu-id="ecc48-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="ecc48-116">Hierdoor kan uw service luisteren op meerdere eindpunten, met mogelijk verschillende protocollen, met behulp van meerdere listeners.</span><span class="sxs-lookup"><span data-stu-id="ecc48-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="ecc48-117">Bijvoorbeeld, wellicht u een HTTP-listener en een afzonderlijke WebSocket-listener.</span><span class="sxs-lookup"><span data-stu-id="ecc48-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="ecc48-118">Elke listener haalt u een naam en de resulterende verzameling *naam: adres* paren worden weergegeven als een JSON-object als een client de luisterende adressen voor een service-exemplaar of een partitie vraagt.</span><span class="sxs-lookup"><span data-stu-id="ecc48-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="ecc48-119">In een stateless service retourneert de onderdrukking een verzameling ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="ecc48-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="ecc48-120">Een `ServiceInstanceListener` bevat een functie voor het maken een `ICommunicationListener(C#) / CommunicationListener(Java)` en hieraan een naam.</span><span class="sxs-lookup"><span data-stu-id="ecc48-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="ecc48-121">De onderdrukking retourneert voor stateful services, een verzameling van ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="ecc48-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="ecc48-122">Dit is enigszins afwijken van het bijbehorende equivalent staatloze omdat een `ServiceReplicaListener` heeft een optie om een `ICommunicationListener` op secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="ecc48-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="ecc48-123">Niet alleen kunt u meerdere communicatielisteners gebruiken in een service, maar u kunt ook opgeven welke listeners accepteren van aanvragen op secundaire replica's en welke luistert alleen op primaire replica's.</span><span class="sxs-lookup"><span data-stu-id="ecc48-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="ecc48-124">Bijvoorbeeld, u kunt een ServiceRemotingListener RPC-aanroepen krijgt alleen op primaire replica's hebben en een tweede, aangepaste listener lezen waarmee aanvragen op de secundaire replica's via HTTP:</span><span class="sxs-lookup"><span data-stu-id="ecc48-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="ecc48-125">Bij het maken van meerdere listeners voor een service wordt elke listener **moet** een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="ecc48-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="ecc48-126">Ten slotte beschrijven de eindpunten die vereist zijn voor de service in de [servicemanifest](service-fabric-application-model.md) onder de sectie voor eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ecc48-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="ecc48-127">De listener communicatie toegang tot de eindpunt-resources toegewezen aan in de `CodePackageActivationContext` in de `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="ecc48-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="ecc48-128">De listener kunt vervolgens luisteren naar aanvragen wanneer deze wordt geopend starten.</span><span class="sxs-lookup"><span data-stu-id="ecc48-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="ecc48-129">Eindpunt bronnen voor het hele servicepakket gelden en ze worden toegewezen door de Service Fabric wanneer het servicepakket is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ecc48-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="ecc48-130">Meerdere service replica's die worden gehost in de dezelfde ServiceHost kunnen delen dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="ecc48-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="ecc48-131">Dit betekent dat de communicatie-listener delen van de poort moet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="ecc48-132">De aanbevolen manier is voor de communicatie-listener voor de partitie-ID en replica-exemplaar-ID gebruiken bij het genereren van het adres luisteren.</span><span class="sxs-lookup"><span data-stu-id="ecc48-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="ecc48-133">Registratie van de service-adres</span><span class="sxs-lookup"><span data-stu-id="ecc48-133">Service address registration</span></span>
<span data-ttu-id="ecc48-134">Een systeemservice aangeroepen de *Naming Service* wordt uitgevoerd op de Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="ecc48-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="ecc48-135">De Naming Service is een registrar voor services en de adressen die op elk exemplaar of de replica van de service luistert.</span><span class="sxs-lookup"><span data-stu-id="ecc48-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="ecc48-136">Wanneer de `OpenAsync(C#) / openAsync(Java)` methode van een `ICommunicationListener(C#) / CommunicationListener(Java)` is voltooid, wordt de return-waarde opgehaald geregistreerd in de Naming Service.</span><span class="sxs-lookup"><span data-stu-id="ecc48-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="ecc48-137">Deze waarde die wordt gepubliceerd in de Naming Service is een tekenreeks waarvan de waarde van alles op alle zijn kan.</span><span class="sxs-lookup"><span data-stu-id="ecc48-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="ecc48-138">Deze waarde is wat clients zien wanneer ze voor een adres voor de service uit de Naming Service vragen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

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

    // the string returned here will be published in the Naming Service.
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

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="ecc48-139">Service Fabric bevat API's waarmee clients en andere services kunnen vervolgens vraagt u voor dit adres met de servicenaam.</span><span class="sxs-lookup"><span data-stu-id="ecc48-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="ecc48-140">Dit is belangrijk omdat het serviceadres niet statisch is.</span><span class="sxs-lookup"><span data-stu-id="ecc48-140">This is important because the service address is not static.</span></span> <span data-ttu-id="ecc48-141">Services worden in het cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst.</span><span class="sxs-lookup"><span data-stu-id="ecc48-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="ecc48-142">Dit is het mechanisme dat clientcomputers kunnen omzetten van het luisterende adres voor een service.</span><span class="sxs-lookup"><span data-stu-id="ecc48-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc48-143">Zie voor een volledig overzicht van het schrijven van een communicatie-listener [Service Fabric-Web-API-services met OWIN zelf hosting](service-fabric-reliable-services-communication-webapi.md) voor C#, dat u uw eigen HTTP-server-implementatie voor Java schrijven kunt, Zie EchoServer toepassing voorbeeld op https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="ecc48-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="ecc48-144">Communicatie met een service</span><span class="sxs-lookup"><span data-stu-id="ecc48-144">Communicating with a service</span></span>
<span data-ttu-id="ecc48-145">De betrouwbare Services API biedt de volgende bibliotheken voor het schrijven van clients die met de services communiceren.</span><span class="sxs-lookup"><span data-stu-id="ecc48-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="ecc48-146">Service-eindpunt resolutie</span><span class="sxs-lookup"><span data-stu-id="ecc48-146">Service endpoint resolution</span></span>
<span data-ttu-id="ecc48-147">De eerste stap voor communicatie met een service is een eindpuntadres van de partitie of het exemplaar van de service die u wilt praten omzetten.</span><span class="sxs-lookup"><span data-stu-id="ecc48-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="ecc48-148">De `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` hulpprogrammaklasse is een eenvoudige primitieve die helpt clients bij het bepalen van het eindpunt van een service tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ecc48-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="ecc48-149">In Service Fabric-terminologie, het proces voor het bepalen van het eindpunt van een service wordt aangeduid als de *service-eindpunt resolutie*.</span><span class="sxs-lookup"><span data-stu-id="ecc48-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="ecc48-150">Als u wilt verbinding maken met services binnen een cluster, kunnen ServicePartitionResolver worden gemaakt met de standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="ecc48-151">Dit is het aanbevolen gebruik voor de meeste situaties:</span><span class="sxs-lookup"><span data-stu-id="ecc48-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="ecc48-152">Als u wilt verbinding maken met services in een ander cluster, kan een ServicePartitionResolver worden gemaakt met een reeks cluster gateway eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ecc48-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="ecc48-153">Houd er rekening mee dat gateway eindpunten alleen verschillende eindpunten zijn voor de verbinding met hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc48-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="ecc48-154">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ecc48-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="ecc48-155">U kunt ook `ServicePartitionResolver` kan een functie worden opgegeven voor het maken van een `FabricClient` intern gebruik:</span><span class="sxs-lookup"><span data-stu-id="ecc48-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

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

<span data-ttu-id="ecc48-156">`FabricClient`het object dat wordt gebruikt om te communiceren met het Service Fabric-cluster voor verschillende bewerkingen op het cluster is.</span><span class="sxs-lookup"><span data-stu-id="ecc48-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="ecc48-157">Dit is handig als u meer controle wilt over de interactie van een service-omzetter partitie met het cluster.</span><span class="sxs-lookup"><span data-stu-id="ecc48-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="ecc48-158">`FabricClient`voert caching intern en is meestal duur voor het maken, dus is het belangrijk om opnieuw te `FabricClient` exemplaren zo veel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ecc48-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="ecc48-159">Een methode resolve wordt vervolgens gebruikt voor het ophalen van het adres van een service of de partitie van een service voor gepartitioneerde services.</span><span class="sxs-lookup"><span data-stu-id="ecc48-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="ecc48-160">Een serviceadres kan worden omgezet eenvoudig met een ServicePartitionResolver, maar meer werk is vereist om te controleren of dat het omgezette adres correct kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecc48-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="ecc48-161">De client moet detecteren of de verbindingspoging is mislukt vanwege een tijdelijke fout en kan opnieuw worden uitgevoerd (bijv, service verplaatst of is tijdelijk niet beschikbaar), of een permanente fout (bijv, service is verwijderd of de aangevraagde resource bestaat niet meer).</span><span class="sxs-lookup"><span data-stu-id="ecc48-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="ecc48-162">Service-exemplaren of replica's kunnen verplaatsen van het knooppunt naar knooppunt op elk gewenst moment om verschillende redenen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="ecc48-163">Het adres van de omgezet via ServicePartitionResolver mogelijk verlopen op het moment dat de clientcode verbinding probeert te maken.</span><span class="sxs-lookup"><span data-stu-id="ecc48-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="ecc48-164">In dat geval opnieuw de client moet opnieuw omzetten van het adres.</span><span class="sxs-lookup"><span data-stu-id="ecc48-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="ecc48-165">De vorige bieden `ResolvedServicePartition` geeft aan dat de omzetter moet opnieuw wilt proberen in plaats van gewoon ophalen een adres in de cache.</span><span class="sxs-lookup"><span data-stu-id="ecc48-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="ecc48-166">Normaal gesproken moet de clientcode werken niet met de ServicePartitionResolver rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="ecc48-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="ecc48-167">Het is gemaakt en doorgegeven aan communicatie client fabrieken in de betrouwbare Services-API.</span><span class="sxs-lookup"><span data-stu-id="ecc48-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="ecc48-168">De factory's gebruiken de resolver intern voor het genereren van een clientobject dat kan worden gebruikt om te communiceren met de services.</span><span class="sxs-lookup"><span data-stu-id="ecc48-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="ecc48-169">Communicatie-clients en fabrieken</span><span class="sxs-lookup"><span data-stu-id="ecc48-169">Communication clients and factories</span></span>
<span data-ttu-id="ecc48-170">De communicatie factory bibliotheek implementeert een typische opnieuw patroon voor afhandeling van fouten die gemakkelijker is bezig met opnieuw verbindingen met opgelost service-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ecc48-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="ecc48-171">De factory-bibliotheek biedt een mechanisme voor het opnieuw proberen terwijl u de fout-handlers opgeven.</span><span class="sxs-lookup"><span data-stu-id="ecc48-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="ecc48-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Hiermee definieert u de basis-interface geïmplementeerd door een client-factory van communicatie waarmee clients die met een Service Fabric-service communiceren kunnen wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="ecc48-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="ecc48-173">De uitvoering van de CommunicationClientFactory is afhankelijk van de communicatiestack gebruikt door de Service Fabric-service waar de client wil communiceren.</span><span class="sxs-lookup"><span data-stu-id="ecc48-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="ecc48-174">De betrouwbare Services API biedt een `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="ecc48-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="ecc48-175">Dit biedt een basisimplementatie van de interface CommunicationClientFactory en taken die gemeenschappelijk voor alle communicatie stapels zijn worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ecc48-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="ecc48-176">(Deze taken omvatten het gebruik van een ServicePartitionResolver om te bepalen van het service-eindpunt).</span><span class="sxs-lookup"><span data-stu-id="ecc48-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="ecc48-177">Clients implementeren meestal de abstracte klasse CommunicationClientFactoryBase voor het afhandelen van logica die specifiek is voor de communicatiestack.</span><span class="sxs-lookup"><span data-stu-id="ecc48-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="ecc48-178">De client communicatie wordt alleen een adres ontvangt en gebruikt deze verbinding maken met een service.</span><span class="sxs-lookup"><span data-stu-id="ecc48-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="ecc48-179">De client kan elk protocol dat deze wil gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ecc48-179">The client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="ecc48-180">Clientfabriek van de is voornamelijk verantwoordelijk voor het maken van clients voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="ecc48-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="ecc48-181">Voor clients die een permanente verbinding, zoals een HTTP-client niet onderhouden moet de factory alleen maken en de client terug.</span><span class="sxs-lookup"><span data-stu-id="ecc48-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="ecc48-182">Andere protocollen die een permanente verbinding, zoals sommige binaire protocollen onderhoudt worden ook gevalideerd door de factory om te bepalen of de verbinding moet opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ecc48-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

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

<span data-ttu-id="ecc48-183">Ten slotte is een uitzonderings-handler verantwoordelijk voor het bepalen welke actie moet worden uitgevoerd wanneer een uitzondering optreedt.</span><span class="sxs-lookup"><span data-stu-id="ecc48-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="ecc48-184">Uitzonderingen worden onderverdeeld in **herstelbare** en **niet-herstelbare**.</span><span class="sxs-lookup"><span data-stu-id="ecc48-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="ecc48-185">**Niet-herstelbare** uitzonderingen ophalen gewoon terug naar de aanroeper opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ecc48-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="ecc48-186">**herstelbare** uitzonderingen kunnen verder worden onderverdeeld in **tijdelijke** en **tijdelijke**.</span><span class="sxs-lookup"><span data-stu-id="ecc48-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="ecc48-187">**Tijdelijke** uitzonderingen zijn die opnieuw kunnen eenvoudig worden verzonden zonder dat het adres van het service-eindpunt opnieuw op te lossen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="ecc48-188">Hierbij wordt tijdelijke netwerkproblemen of service-foutberichten dan degene die wijzen op dat het adres van het service-eindpunt bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="ecc48-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="ecc48-189">**Niet-tijdelijke** uitzonderingen zijn die het adres van het service-eindpunt worden opnieuw opgelost vereisen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="ecc48-190">Het gaat hierbij om uitzonderingen die wijzen op dat het service-eindpunt kan niet worden bereikt, is die aangeeft van de service verplaatst naar een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ecc48-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="ecc48-191">De `TryHandleException` maakt een beslissing over een bepaalde uitzondering.</span><span class="sxs-lookup"><span data-stu-id="ecc48-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="ecc48-192">Als het **niet weet** welke beslissingen nemen over een uitzondering moet deze uitvoer retourneren **false**.</span><span class="sxs-lookup"><span data-stu-id="ecc48-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="ecc48-193">Als het **weet** welke beslissen, moet het resultaat dienovereenkomstig ingesteld en geretourneerd **true**.</span><span class="sxs-lookup"><span data-stu-id="ecc48-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
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

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="ecc48-194">Kort samengevat</span><span class="sxs-lookup"><span data-stu-id="ecc48-194">Putting it all together</span></span>
<span data-ttu-id="ecc48-195">Met een `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, en `IExceptionHandler(C#) / ExceptionHandler(Java)` gebaseerd op een communicatieprotocol een `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` helemaal verpakt en biedt de afhandeling van fouten en service partitie adres resolutie lus om deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="ecc48-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
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
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="ecc48-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ecc48-196">Next steps</span></span>
* <span data-ttu-id="ecc48-197">Een voorbeeld bekijken van HTTP-communicatie tussen services in een [C#-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) of [Java-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="ecc48-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="ecc48-198">Externe procedureaanroepen weer dat met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="ecc48-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="ecc48-199">Web-API die gebruikmaakt van OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ecc48-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="ecc48-200">WCF-communicatie met behulp van Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ecc48-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
