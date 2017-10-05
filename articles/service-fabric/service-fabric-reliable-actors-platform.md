---
title: Reliable Actors op Service Fabric | Microsoft Docs
description: Hierin wordt beschreven hoe Reliable Actors zijn gelaagd op Reliable Services en de functies van het Service Fabric-platform gebruiken.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="37db8-103">Hoe Reliable Actors het Service Fabric-platform gebruiken</span><span class="sxs-lookup"><span data-stu-id="37db8-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="37db8-104">In dit artikel wordt uitgelegd hoe Reliable Actors op de Azure Service Fabric-platform.</span><span class="sxs-lookup"><span data-stu-id="37db8-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="37db8-105">Reliable Actors uitvoeren in een framework dat wordt gehost in een implementatie van een betrouwbare stateful service aangeroepen de *actor service*.</span><span class="sxs-lookup"><span data-stu-id="37db8-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="37db8-106">De service actor bevat alle componenten die vereist zijn voor het beheren van de levenscyclus van en het bericht tijdens het verzenden van uw gebruiken:</span><span class="sxs-lookup"><span data-stu-id="37db8-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="37db8-107">De Runtime Actor levensduur, garbagecollection, beheert en één thread toegang wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="37db8-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="37db8-108">Een actor-service voor externe toegang-listener accepteert de aanroepen van externe toegang actoren en stuurt deze naar een dispatcher doorsturen naar het juiste actor-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="37db8-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="37db8-109">De Actor State-Provider verpakt statusproviders (zoals de betrouwbare verzamelingen state-provider) en biedt een adapter voor actor statusbeheer.</span><span class="sxs-lookup"><span data-stu-id="37db8-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="37db8-110">Deze onderdelen vormen samen het betrouwbare Actor-framework.</span><span class="sxs-lookup"><span data-stu-id="37db8-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="37db8-111">Service gelaagdheid</span><span class="sxs-lookup"><span data-stu-id="37db8-111">Service layering</span></span>
<span data-ttu-id="37db8-112">Omdat de actor-service zelf een betrouwbare service alle de [toepassingsmodel](service-fabric-application-model.md), levensduur, [verpakking](service-fabric-package-apps.md), [implementatie](service-fabric-deploy-remove-applications.md), upgrade en concepten van betrouwbare schalen Services dezelfde manier actorservices van toepassing.</span><span class="sxs-lookup"><span data-stu-id="37db8-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Acteur service gelaagdheid][1]

<span data-ttu-id="37db8-114">Het voorgaande diagram toont de relatie tussen de Service Fabric-toepassingsframeworks en gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="37db8-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="37db8-115">Blauw elementen het toepassingsframework Reliable Services vertegenwoordigen, oranje staat voor het framework betrouwbare Actor en groen voor gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="37db8-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="37db8-116">In Reliable Services uw service neemt over de `StatefulService` klasse.</span><span class="sxs-lookup"><span data-stu-id="37db8-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="37db8-117">Deze klasse is afgeleid van `StatefulServiceBase` (of `StatelessService` voor stateless services).</span><span class="sxs-lookup"><span data-stu-id="37db8-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="37db8-118">In Reliable Actors gebruikt u de actor-service.</span><span class="sxs-lookup"><span data-stu-id="37db8-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="37db8-119">De actor-service is een andere implementatie van de `StatefulServiceBase` klasse die de actor-patroon waar uw actoren uitgevoerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="37db8-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="37db8-120">Omdat de actor-service zelf slechts een implementatie van is `StatefulServiceBase`, kunt u uw eigen service die is afgeleid van `ActorService` en implementeren van serviceniveau-functies dezelfde manier als wanneer wordt overgenomen `StatefulService`, zoals:</span><span class="sxs-lookup"><span data-stu-id="37db8-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="37db8-121">Service back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="37db8-121">Service backup and restore.</span></span>
* <span data-ttu-id="37db8-122">Gedeelde functionaliteit voor alle actoren, bijvoorbeeld een Circuitonderbreker.</span><span class="sxs-lookup"><span data-stu-id="37db8-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="37db8-123">Externe procedureaanroepen weer dat op de actor-service zelf en op elke afzonderlijke actor.</span><span class="sxs-lookup"><span data-stu-id="37db8-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="37db8-124">Stateful services worden momenteel niet ondersteund in Java-/ Linux.</span><span class="sxs-lookup"><span data-stu-id="37db8-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="37db8-125">Met behulp van de service actor</span><span class="sxs-lookup"><span data-stu-id="37db8-125">Using the actor service</span></span>
<span data-ttu-id="37db8-126">Actor-exemplaren hebben toegang tot de actor-service waarin ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37db8-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="37db8-127">Actor-exemplaren kunnen via de service actor programmatisch verkrijgen de servicecontext.</span><span class="sxs-lookup"><span data-stu-id="37db8-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="37db8-128">De servicecontext heeft de partitie-ID, de servicenaam, de toepassingsnaam en andere Service Fabric-platform-specifieke informatie:</span><span class="sxs-lookup"><span data-stu-id="37db8-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="37db8-129">Net als alle Reliable Services, moet de actor-service zijn geregistreerd met een servicetype in de Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="37db8-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="37db8-130">Voor de service actor uw actor-exemplaren uitvoeren, moet uw actortype ook zijn geregistreerd met de actor-service.</span><span class="sxs-lookup"><span data-stu-id="37db8-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="37db8-131">De `ActorRuntime` registratiemethode voert dit werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37db8-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="37db8-132">In het meest eenvoudige geval kunt u alleen uw actortype registreren en de service actor met standaardinstellingen wordt impliciet worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="37db8-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="37db8-133">U kunt ook kunt u een lambda geleverd door de registratiemethode om samen te stellen de actor-service zelf.</span><span class="sxs-lookup"><span data-stu-id="37db8-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="37db8-134">U kunt vervolgens de actor-service te configureren en expliciet opstelt actor-exemplaren, waar u de afhankelijkheden aan uw actor via de constructor kunt invoeren:</span><span class="sxs-lookup"><span data-stu-id="37db8-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="37db8-135">De methoden van actor</span><span class="sxs-lookup"><span data-stu-id="37db8-135">Actor service methods</span></span>
<span data-ttu-id="37db8-136">De service Actor implements `IActorService` (C#) of `ActorService` (Java) die op zijn beurt implementeert `IService` (C#) of `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="37db8-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="37db8-137">Dit is de interface die wordt gebruikt door externe toegang Reliable Services, waarmee externe procedureaanroepen weer dat op de service-methoden.</span><span class="sxs-lookup"><span data-stu-id="37db8-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="37db8-138">Het bevat serviceniveau-methoden die op afstand via de service voor externe toegang kunnen worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="37db8-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="37db8-139">Actoren opsommen</span><span class="sxs-lookup"><span data-stu-id="37db8-139">Enumerating actors</span></span>
<span data-ttu-id="37db8-140">De actor-service kan een client opsommen metagegevens over de actoren waarmee de service wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="37db8-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="37db8-141">Omdat de actor-service een gepartitioneerde stateful service is, wordt de opsomming per partitie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37db8-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="37db8-142">Omdat elke partitie veel actoren bevat mogelijk, wordt de opsomming geretourneerd als een set pagina's met zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="37db8-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="37db8-143">De pagina's worden via herhaald totdat alle pagina's worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="37db8-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="37db8-144">Het volgende voorbeeld ziet u het maken van een lijst met alle actieve actoren in een partitie van een actor-service:</span><span class="sxs-lookup"><span data-stu-id="37db8-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="37db8-145">Verwijderd actoren</span><span class="sxs-lookup"><span data-stu-id="37db8-145">Deleting actors</span></span>
<span data-ttu-id="37db8-146">De actor-service biedt ook een functie voor het verwijderen van actoren:</span><span class="sxs-lookup"><span data-stu-id="37db8-146">The actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="37db8-147">Zie voor meer informatie over het verwijderen van actors en hun status, de [actor lifecycle documentatie](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="37db8-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="37db8-148">Aangepaste actor-service</span><span class="sxs-lookup"><span data-stu-id="37db8-148">Custom actor service</span></span>
<span data-ttu-id="37db8-149">U kunt uw eigen aangepaste actor-service die is afgeleid van registreren met behulp van de registratie actor lambda `ActorService` (C#) en `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="37db8-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="37db8-150">In deze service aangepaste actor u uw eigen serviceniveau-functionaliteit kunt implementeren met het schrijven van een serviceklasse die overneemt `ActorService` (C#) of `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="37db8-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="37db8-151">Een aangepaste actor-service neemt over alle actor runtime functionaliteit van `ActorService` (C#) of `FabricActorService` (Java) en kan worden gebruikt voor het implementeren van uw eigen service-methoden.</span><span class="sxs-lookup"><span data-stu-id="37db8-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="37db8-152">Implementatie van actor-back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="37db8-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="37db8-153">In het volgende voorbeeld wordt de aangepaste actor-service beschrijft een methode voor het back-ups actor door gebruik te maken van de listener voor externe toegang die al aanwezig in `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="37db8-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="37db8-154">In dit voorbeeld `IMyActorService` is een contract voor externe toegang die implementeert `IService` (C#) en `Service` (Java) en vervolgens wordt geïmplementeerd door `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="37db8-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="37db8-155">Door dit contract remoting, methoden toe te voegen op `IMyActorService` zijn nu ook beschikbaar voor een client door het maken van een proxy voor externe toegang via `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="37db8-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="37db8-156">Toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="37db8-156">Application model</span></span>
<span data-ttu-id="37db8-157">Actorservices zijn Reliable Services, zodat de toepassingsmodel hetzelfde is.</span><span class="sxs-lookup"><span data-stu-id="37db8-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="37db8-158">De actor framework build tools genereren echter enkele van de toepassingsbestanden model voor u.</span><span class="sxs-lookup"><span data-stu-id="37db8-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="37db8-159">Servicemanifest</span><span class="sxs-lookup"><span data-stu-id="37db8-159">Service manifest</span></span>
<span data-ttu-id="37db8-160">De actor framework build-hulpprogramma's worden automatisch de inhoud van uw actor-service ServiceManifest.xml bestand genereren.</span><span class="sxs-lookup"><span data-stu-id="37db8-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="37db8-161">Dit bestand bevat:</span><span class="sxs-lookup"><span data-stu-id="37db8-161">This file includes:</span></span>

* <span data-ttu-id="37db8-162">Actortype-service.</span><span class="sxs-lookup"><span data-stu-id="37db8-162">Actor service type.</span></span> <span data-ttu-id="37db8-163">Naam van het type wordt gegenereerd op basis van uw actor projectnaam.</span><span class="sxs-lookup"><span data-stu-id="37db8-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="37db8-164">Op basis van het kenmerk persistentie bij uw acteur, wordt de vlag HasPersistedState ook ingesteld dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="37db8-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="37db8-165">Codepakket.</span><span class="sxs-lookup"><span data-stu-id="37db8-165">Code package.</span></span>
* <span data-ttu-id="37db8-166">Configuratiepakket.</span><span class="sxs-lookup"><span data-stu-id="37db8-166">Config package.</span></span>
* <span data-ttu-id="37db8-167">Bronnen en eindpunten.</span><span class="sxs-lookup"><span data-stu-id="37db8-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="37db8-168">Het toepassingsmanifest</span><span class="sxs-lookup"><span data-stu-id="37db8-168">Application manifest</span></span>
<span data-ttu-id="37db8-169">Een standaard-servicedefinitie voor uw actor-service wordt automatisch gemaakt door de actor framework build-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="37db8-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="37db8-170">De build-hulpprogramma's vullen de standaardeigenschappen voor de service:</span><span class="sxs-lookup"><span data-stu-id="37db8-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="37db8-171">Replica set count wordt bepaald door het kenmerk persistentie bij uw actor.</span><span class="sxs-lookup"><span data-stu-id="37db8-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="37db8-172">Telkens wanneer die de persistentie-kenmerk op uw actor is gewijzigd, de replica set in de servicedefinitie standaard beginwaarde dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="37db8-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="37db8-173">Partitieschema en bereik zijn ingesteld op uniforme Int64 met het volledige bereik van de Int64-sleutel.</span><span class="sxs-lookup"><span data-stu-id="37db8-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="37db8-174">Concepten van service Fabric-partitie gebruiken</span><span class="sxs-lookup"><span data-stu-id="37db8-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="37db8-175">Actorservices zijn gepartitioneerde stateful services.</span><span class="sxs-lookup"><span data-stu-id="37db8-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="37db8-176">Elke partitie van een actor-service bevat een set van actoren.</span><span class="sxs-lookup"><span data-stu-id="37db8-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="37db8-177">Service-partities worden automatisch verdeeld over meerdere knooppunten in het Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="37db8-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="37db8-178">Actor-exemplaren worden als gevolg hiervan gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="37db8-178">Actor instances are distributed as a result.</span></span>

![Acteur partitioneren en distribueren][5]

<span data-ttu-id="37db8-180">Reliable Services kunnen worden gemaakt met verschillende partitieschema's en partitie sleutelbereiken.</span><span class="sxs-lookup"><span data-stu-id="37db8-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="37db8-181">De actor-service gebruikt het partitieschema Int64 alle belangrijke functies Int64 actoren toewijzen aan partities.</span><span class="sxs-lookup"><span data-stu-id="37db8-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="37db8-182">Actor-ID</span><span class="sxs-lookup"><span data-stu-id="37db8-182">Actor ID</span></span>
<span data-ttu-id="37db8-183">Elke actor dat gemaakt in de service heeft een unieke ID die is gekoppeld, vertegenwoordigd door de `ActorId` klasse.</span><span class="sxs-lookup"><span data-stu-id="37db8-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="37db8-184">`ActorId`is een ondoorzichtige ID-waarde die voor gelijkmatige verdeling van actoren kan worden gebruikt tussen de servicepartities door het genereren van willekeurige id's:</span><span class="sxs-lookup"><span data-stu-id="37db8-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="37db8-185">Elke `ActorId` wordt opgedeeld naar een gegevenstype Int64.</span><span class="sxs-lookup"><span data-stu-id="37db8-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="37db8-186">Dit is de reden waarom de actor-service een partitieschema Int64 met het volledige bereik van de Int64-sleutel gebruiken moet.</span><span class="sxs-lookup"><span data-stu-id="37db8-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="37db8-187">Aangepaste ID-waarden kunnen echter worden gebruikt voor een `ActorID`, met inbegrip van GUID's / UUID's, tekenreeksen en Int64s.</span><span class="sxs-lookup"><span data-stu-id="37db8-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="37db8-188">Wanneer u van GUID's / UUID's en tekenreeksen gebruikmaakt, worden de waarden worden opgedeeld in een Int64.</span><span class="sxs-lookup"><span data-stu-id="37db8-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="37db8-189">Echter, wanneer u expliciet bieden een gegevenstype Int64 naar een `ActorId`, de Int64 wordt rechtstreeks verwijzen naar een partitie zonder verdere hashing.</span><span class="sxs-lookup"><span data-stu-id="37db8-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="37db8-190">U kunt deze techniek om te bepalen welke partitie in de actoren worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="37db8-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37db8-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37db8-191">Next steps</span></span>
* [<span data-ttu-id="37db8-192">Statusbeheer actor</span><span class="sxs-lookup"><span data-stu-id="37db8-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="37db8-193">Acteur lifecycle en garbage collection</span><span class="sxs-lookup"><span data-stu-id="37db8-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="37db8-194">API-naslagdocumentatie actors</span><span class="sxs-lookup"><span data-stu-id="37db8-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="37db8-195">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="37db8-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="37db8-196">Voorbeeldcode voor Java</span><span class="sxs-lookup"><span data-stu-id="37db8-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
