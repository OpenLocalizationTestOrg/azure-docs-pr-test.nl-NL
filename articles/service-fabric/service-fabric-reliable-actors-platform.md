---
title: aaaReliable actoren in Service Fabric | Microsoft Docs
description: Beschrijft hoe Reliable Actors zijn gelaagd op Reliable Services en functies van Service Fabric-platform Hallo Hallo gebruiken.
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
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="3b6bf-103">Hoe Reliable Actors Hallo Service Fabric-platform gebruiken</span><span class="sxs-lookup"><span data-stu-id="3b6bf-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="3b6bf-104">In dit artikel wordt uitgelegd hoe Reliable Actors op Hallo Azure Service Fabric-platform.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="3b6bf-105">Reliable Actors uitvoeren in een framework dat wordt gehost in een implementatie van een stateful betrouwbare service met de naam van Hallo *actor service*.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="3b6bf-106">Hallo actor service bevat alle Hallo onderdelen nodig toomanage Hallo lifecycle- en tijdens het verzenden van uw gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="3b6bf-107">Hallo Actor Runtime levensduur, garbagecollection, beheert en één thread toegang wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="3b6bf-108">Een actor-service voor externe toegang-listener tooactors voor externe toegang-aanroepen accepteert en verzendt deze tooa dispatcher tooroute toohello juiste actor-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="3b6bf-109">Hallo Actor State-Provider verpakt statusproviders (zoals Hallo betrouwbare verzamelingen state-provider) en biedt een adapter voor actor statusbeheer.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="3b6bf-110">Deze onderdelen samen formulier Hallo betrouwbare Actor framework.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="3b6bf-111">Service gelaagdheid</span><span class="sxs-lookup"><span data-stu-id="3b6bf-111">Service layering</span></span>
<span data-ttu-id="3b6bf-112">Omdat Hallo actor-service zelf betrouwbaar is, alle Hallo [toepassingsmodel](service-fabric-application-model.md), levensduur, [verpakking](service-fabric-package-apps.md), [implementatie](service-fabric-deploy-remove-applications.md), upgrade en concepten van schaal Reliable Services toepassing hello dezelfde manier tooactor services.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Acteur service gelaagdheid][1]

<span data-ttu-id="3b6bf-114">Hallo toont voorgaande diagram Hallo relatie tussen Hallo Service Fabric-toepassingsframeworks en gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="3b6bf-115">Blauw elementen Hallo Reliable Services toepassingsframework vertegenwoordigen, oranje vertegenwoordigt Hallo betrouwbare Actor framework en groen gebruikerscode vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="3b6bf-116">In Reliable Services uw service neemt over Hallo `StatefulService` klasse.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="3b6bf-117">Deze klasse is afgeleid van `StatefulServiceBase` (of `StatelessService` voor stateless services).</span><span class="sxs-lookup"><span data-stu-id="3b6bf-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="3b6bf-118">In Reliable Actors gebruikt u Hallo actor-service.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="3b6bf-119">Hallo actor-service is een andere implementatie van Hallo `StatefulServiceBase` klasse implementeert Hallo actor patroon waar uw actoren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="3b6bf-120">Omdat Hallo actor-service zelf slechts een implementatie van is `StatefulServiceBase`, kunt u uw eigen service die is afgeleid van `ActorService` en implementeer serviceniveau-functies Hallo dezelfde manier als wanneer deze is overgenomen `StatefulService`, zoals:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="3b6bf-121">Service back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-121">Service backup and restore.</span></span>
* <span data-ttu-id="3b6bf-122">Gedeelde functionaliteit voor alle actoren, bijvoorbeeld een Circuitonderbreker.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="3b6bf-123">Externe procedureaanroepen weer dat op Hallo actor-service zelf en op elke afzonderlijke actor.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="3b6bf-124">Stateful services worden momenteel niet ondersteund in Java-/ Linux.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="3b6bf-125">Met behulp van Hallo actor-service</span><span class="sxs-lookup"><span data-stu-id="3b6bf-125">Using hello actor service</span></span>
<span data-ttu-id="3b6bf-126">Actor-exemplaren hebben toegang toohello actor service waarin ze worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="3b6bf-127">Via Hallo actor-service, kunnen actor exemplaren programmatisch Hallo servicecontext verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="3b6bf-128">Hallo servicecontext heeft Hallo partitie-ID, servicenaam, de toepassingsnaam van de en andere Service Fabric-platform-specifieke informatie:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="3b6bf-129">Net als alle Reliable Services, moet de Hallo actor-service zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="3b6bf-130">Voor Hallo actor toorun uw exemplaren actor-service, moet uw actortype ook zijn geregistreerd met Hallo actor-service.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="3b6bf-131">Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="3b6bf-132">In de meest eenvoudige geval Hallo, kunt u alleen uw actortype registreren en impliciet Hallo actor-service met de standaardinstellingen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="3b6bf-133">U kunt ook een lambda geleverd door Hallo methode tooconstruct Hallo actor registratieservice zelf gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="3b6bf-134">U kunt vervolgens configureren Hallo actor-service en expliciet maken uw actor-exemplaren, waar u de afhankelijkheden tooyour actor via de constructor kunt invoeren:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="3b6bf-135">De methoden van actor</span><span class="sxs-lookup"><span data-stu-id="3b6bf-135">Actor service methods</span></span>
<span data-ttu-id="3b6bf-136">Hallo Actor service implementeert `IActorService` (C#) of `ActorService` (Java) die op zijn beurt implementeert `IService` (C#) of `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="3b6bf-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="3b6bf-137">Dit is Hallo interface die wordt gebruikt door externe toegang Reliable Services, waarmee externe procedureaanroepen weer dat op de service-methoden.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="3b6bf-138">Het bevat serviceniveau-methoden die op afstand via de service voor externe toegang kunnen worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="3b6bf-139">Actoren opsommen</span><span class="sxs-lookup"><span data-stu-id="3b6bf-139">Enumerating actors</span></span>
<span data-ttu-id="3b6bf-140">Hallo actor-service kan een client tooenumerate metagegevens over Hallo actors die Hallo-service wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="3b6bf-141">Omdat Hallo actor-service een gepartitioneerde stateful service is, wordt de inventarisatie uitgevoerd per partitie.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="3b6bf-142">Omdat elke partitie veel actoren bevat mogelijk, Hallo opsomming geretourneerd als een set pagina's met zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="3b6bf-143">Hallo-pagina's worden via herhaald totdat alle pagina's worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="3b6bf-144">Hallo volgende voorbeeld wordt getoond hoe toocreate een lijst met alle actieve actoren in een partitie van een actor-service:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="3b6bf-145">Verwijderd actoren</span><span class="sxs-lookup"><span data-stu-id="3b6bf-145">Deleting actors</span></span>
<span data-ttu-id="3b6bf-146">Hallo actor service biedt ook een functie voor het verwijderen van actoren:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="3b6bf-147">Zie voor meer informatie over het verwijderen van actors en hun status Hallo [actor lifecycle documentatie](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bf-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="3b6bf-148">Aangepaste actor-service</span><span class="sxs-lookup"><span data-stu-id="3b6bf-148">Custom actor service</span></span>
<span data-ttu-id="3b6bf-149">U kunt uw eigen aangepaste actor-service die is afgeleid van registreren met behulp van Hallo actor registratie lambda `ActorService` (C#) en `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="3b6bf-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="3b6bf-150">In deze service aangepaste actor u uw eigen serviceniveau-functionaliteit kunt implementeren met het schrijven van een serviceklasse die overneemt `ActorService` (C#) of `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="3b6bf-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="3b6bf-151">Een aangepaste actor-service neemt over alle Hallo actor runtime-functionaliteit van `ActorService` (C#) of `FabricActorService` (Java) en gebruikte tooimplement uw eigen service-methoden kan worden.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="3b6bf-152">Implementatie van actor-back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="3b6bf-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="3b6bf-153">In Hallo voorbeeld te volgen, Hallo aangepaste actor service beschrijft een methode tooback van actor-gegevens door gebruik te maken van Hallo remoting listener al aanwezig in `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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
           // store hello contents of backupInfo.Directory
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
           // store hello contents of backupInfo.Directory
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


<span data-ttu-id="3b6bf-154">In dit voorbeeld `IMyActorService` is een contract voor externe toegang die implementeert `IService` (C#) en `Service` (Java) en vervolgens wordt geïmplementeerd door `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="3b6bf-155">Door dit contract remoting, methoden toe te voegen op `IMyActorService` zijn nu ook de client beschikbare tooa door het maken van een proxy voor externe toegang via `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="3b6bf-156">Toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="3b6bf-156">Application model</span></span>
<span data-ttu-id="3b6bf-157">Actorservices zijn Reliable Services zodat Hallo toepassingsmodel is dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="3b6bf-158">Hallo actor framework build tools genereren echter enkele van de toepassingsbestanden model Hallo voor u.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="3b6bf-159">Servicemanifest</span><span class="sxs-lookup"><span data-stu-id="3b6bf-159">Service manifest</span></span>
<span data-ttu-id="3b6bf-160">Hallo actor framework build tools Hallo inhoud van uw actor-service ServiceManifest.xml bestand automatisch worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="3b6bf-161">Dit bestand bevat:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-161">This file includes:</span></span>

* <span data-ttu-id="3b6bf-162">Actortype-service.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-162">Actor service type.</span></span> <span data-ttu-id="3b6bf-163">Hallo-typenaam is gegenereerd op basis van uw actor projectnaam.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="3b6bf-164">Op basis van Hallo persistentie-kenmerk op uw acteur, wordt Hallo HasPersistedState vlag ook ingesteld dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="3b6bf-165">Codepakket.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-165">Code package.</span></span>
* <span data-ttu-id="3b6bf-166">Configuratiepakket.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-166">Config package.</span></span>
* <span data-ttu-id="3b6bf-167">Bronnen en eindpunten.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="3b6bf-168">Het toepassingsmanifest</span><span class="sxs-lookup"><span data-stu-id="3b6bf-168">Application manifest</span></span>
<span data-ttu-id="3b6bf-169">Hallo actor framework build tools wordt automatisch een standaard-servicedefinitie voor uw service actor maken.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="3b6bf-170">Hallo build tools vullen Hallo standaard service-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="3b6bf-171">Replica set count wordt bepaald door Hallo persistentie-kenmerk op uw actor.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="3b6bf-172">Elk kenmerk tijd Hallo persistentie op uw actor wordt gewijzigd, Hallo replica set in de definitie van de service standaard Hallo beginwaarde dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="3b6bf-173">Partitieschema en bereik ingesteld tooUniform Int64 met Hallo volledige Int64 sleutel bereik.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="3b6bf-174">Concepten van service Fabric-partitie gebruiken</span><span class="sxs-lookup"><span data-stu-id="3b6bf-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="3b6bf-175">Actorservices zijn gepartitioneerde stateful services.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="3b6bf-176">Elke partitie van een actor-service bevat een set van actoren.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="3b6bf-177">Service-partities worden automatisch verdeeld over meerdere knooppunten in het Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="3b6bf-178">Actor-exemplaren worden als gevolg hiervan gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-178">Actor instances are distributed as a result.</span></span>

![Acteur partitioneren en distribueren][5]

<span data-ttu-id="3b6bf-180">Reliable Services kunnen worden gemaakt met verschillende partitieschema's en partitie sleutelbereiken.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="3b6bf-181">Hallo actor-service gebruikt Hallo Int64 partitieschema met Hallo volledige Int64 sleutel bereik toomap actoren toopartitions.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="3b6bf-182">Actor-ID</span><span class="sxs-lookup"><span data-stu-id="3b6bf-182">Actor ID</span></span>
<span data-ttu-id="3b6bf-183">Elke actor dat gemaakt in het Hallo-service heeft een unieke ID die is gekoppeld, vertegenwoordigd door Hallo `ActorId` klasse.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="3b6bf-184">`ActorId`is een ondoorzichtige ID-waarde die kan worden gebruikt voor gelijkmatige verdeling van actoren meerdere partities voor Hallo-service door het genereren van willekeurige id's:</span><span class="sxs-lookup"><span data-stu-id="3b6bf-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="3b6bf-185">Elke `ActorId` hash tooan Int64 is.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="3b6bf-186">Daarom Hallo actor-service moet een partitieschema Int64 met Hallo volledige Int64 sleutel bereik gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="3b6bf-187">Aangepaste ID-waarden kunnen echter worden gebruikt voor een `ActorID`, met inbegrip van GUID's / UUID's, tekenreeksen en Int64s.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="3b6bf-188">Wanneer u van GUID's / UUID's en tekenreeksen gebruikmaakt, betekent dit dat Hallo waarden hash tooan Int64 zijn.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="3b6bf-189">Echter, wanneer u expliciet bieden een gegevenstype Int64 tooan `ActorId`, Hallo Int64 toegewezen rechtstreeks tooa partitie zonder verdere hashing.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="3b6bf-190">U kunt deze techniek toocontrol die partitie Hallo actoren in zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="3b6bf-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b6bf-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b6bf-191">Next steps</span></span>
* [<span data-ttu-id="3b6bf-192">Statusbeheer actor</span><span class="sxs-lookup"><span data-stu-id="3b6bf-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="3b6bf-193">Acteur lifecycle en garbage collection</span><span class="sxs-lookup"><span data-stu-id="3b6bf-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="3b6bf-194">API-naslagdocumentatie actors</span><span class="sxs-lookup"><span data-stu-id="3b6bf-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="3b6bf-195">Voorbeeldcode voor .NET</span><span class="sxs-lookup"><span data-stu-id="3b6bf-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="3b6bf-196">Voorbeeldcode voor Java</span><span class="sxs-lookup"><span data-stu-id="3b6bf-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
