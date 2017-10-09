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
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Hoe Reliable Actors Hallo Service Fabric-platform gebruiken
In dit artikel wordt uitgelegd hoe Reliable Actors op Hallo Azure Service Fabric-platform. Reliable Actors uitvoeren in een framework dat wordt gehost in een implementatie van een stateful betrouwbare service met de naam van Hallo *actor service*. Hallo actor service bevat alle Hallo onderdelen nodig toomanage Hallo lifecycle- en tijdens het verzenden van uw gebruiken:

* Hallo Actor Runtime levensduur, garbagecollection, beheert en één thread toegang wordt afgedwongen.
* Een actor-service voor externe toegang-listener tooactors voor externe toegang-aanroepen accepteert en verzendt deze tooa dispatcher tooroute toohello juiste actor-exemplaar.
* Hallo Actor State-Provider verpakt statusproviders (zoals Hallo betrouwbare verzamelingen state-provider) en biedt een adapter voor actor statusbeheer.

Deze onderdelen samen formulier Hallo betrouwbare Actor framework.

## <a name="service-layering"></a>Service gelaagdheid
Omdat Hallo actor-service zelf betrouwbaar is, alle Hallo [toepassingsmodel](service-fabric-application-model.md), levensduur, [verpakking](service-fabric-package-apps.md), [implementatie](service-fabric-deploy-remove-applications.md), upgrade en concepten van schaal Reliable Services toepassing hello dezelfde manier tooactor services. 

![Acteur service gelaagdheid][1]

Hallo toont voorgaande diagram Hallo relatie tussen Hallo Service Fabric-toepassingsframeworks en gebruikerscode. Blauw elementen Hallo Reliable Services toepassingsframework vertegenwoordigen, oranje vertegenwoordigt Hallo betrouwbare Actor framework en groen gebruikerscode vertegenwoordigt.

In Reliable Services uw service neemt over Hallo `StatefulService` klasse. Deze klasse is afgeleid van `StatefulServiceBase` (of `StatelessService` voor stateless services). In Reliable Actors gebruikt u Hallo actor-service. Hallo actor-service is een andere implementatie van Hallo `StatefulServiceBase` klasse implementeert Hallo actor patroon waar uw actoren uitgevoerd. Omdat Hallo actor-service zelf slechts een implementatie van is `StatefulServiceBase`, kunt u uw eigen service die is afgeleid van `ActorService` en implementeer serviceniveau-functies Hallo dezelfde manier als wanneer deze is overgenomen `StatefulService`, zoals:

* Service back-up en herstel.
* Gedeelde functionaliteit voor alle actoren, bijvoorbeeld een Circuitonderbreker.
* Externe procedureaanroepen weer dat op Hallo actor-service zelf en op elke afzonderlijke actor.

> [!NOTE]
> Stateful services worden momenteel niet ondersteund in Java-/ Linux.

### <a name="using-hello-actor-service"></a>Met behulp van Hallo actor-service
Actor-exemplaren hebben toegang toohello actor service waarin ze worden uitgevoerd. Via Hallo actor-service, kunnen actor exemplaren programmatisch Hallo servicecontext verkrijgen. Hallo servicecontext heeft Hallo partitie-ID, servicenaam, de toepassingsnaam van de en andere Service Fabric-platform-specifieke informatie:

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


Net als alle Reliable Services, moet de Hallo actor-service zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime. Voor Hallo actor toorun uw exemplaren actor-service, moet uw actortype ook zijn geregistreerd met Hallo actor-service. Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken. In de meest eenvoudige geval Hallo, kunt u alleen uw actortype registreren en impliciet Hallo actor-service met de standaardinstellingen worden gebruikt:

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

U kunt ook een lambda geleverd door Hallo methode tooconstruct Hallo actor registratieservice zelf gebruiken. U kunt vervolgens configureren Hallo actor-service en expliciet maken uw actor-exemplaren, waar u de afhankelijkheden tooyour actor via de constructor kunt invoeren:

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

### <a name="actor-service-methods"></a>De methoden van actor
Hallo Actor service implementeert `IActorService` (C#) of `ActorService` (Java) die op zijn beurt implementeert `IService` (C#) of `Service` (Java). Dit is Hallo interface die wordt gebruikt door externe toegang Reliable Services, waarmee externe procedureaanroepen weer dat op de service-methoden. Het bevat serviceniveau-methoden die op afstand via de service voor externe toegang kunnen worden aangeroepen.

#### <a name="enumerating-actors"></a>Actoren opsommen
Hallo actor-service kan een client tooenumerate metagegevens over Hallo actors die Hallo-service wordt gehost. Omdat Hallo actor-service een gepartitioneerde stateful service is, wordt de inventarisatie uitgevoerd per partitie. Omdat elke partitie veel actoren bevat mogelijk, Hallo opsomming geretourneerd als een set pagina's met zoekresultaten. Hallo-pagina's worden via herhaald totdat alle pagina's worden gelezen. Hallo volgende voorbeeld wordt getoond hoe toocreate een lijst met alle actieve actoren in een partitie van een actor-service:

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

#### <a name="deleting-actors"></a>Verwijderd actoren
Hallo actor service biedt ook een functie voor het verwijderen van actoren:

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

Zie voor meer informatie over het verwijderen van actors en hun status Hallo [actor lifecycle documentatie](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Aangepaste actor-service
U kunt uw eigen aangepaste actor-service die is afgeleid van registreren met behulp van Hallo actor registratie lambda `ActorService` (C#) en `FabricActorService` (Java). In deze service aangepaste actor u uw eigen serviceniveau-functionaliteit kunt implementeren met het schrijven van een serviceklasse die overneemt `ActorService` (C#) of `FabricActorService` (Java). Een aangepaste actor-service neemt over alle Hallo actor runtime-functionaliteit van `ActorService` (C#) of `FabricActorService` (Java) en gebruikte tooimplement uw eigen service-methoden kan worden.

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

#### <a name="implementing-actor-backup-and-restore"></a>Implementatie van actor-back-up en herstel
 In Hallo voorbeeld te volgen, Hallo aangepaste actor service beschrijft een methode tooback van actor-gegevens door gebruik te maken van Hallo remoting listener al aanwezig in `ActorService`:

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


In dit voorbeeld `IMyActorService` is een contract voor externe toegang die implementeert `IService` (C#) en `Service` (Java) en vervolgens wordt geïmplementeerd door `MyActorService`. Door dit contract remoting, methoden toe te voegen op `IMyActorService` zijn nu ook de client beschikbare tooa door het maken van een proxy voor externe toegang via `ActorServiceProxy`:

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

## <a name="application-model"></a>Toepassingsmodel
Actorservices zijn Reliable Services zodat Hallo toepassingsmodel is dezelfde Hallo. Hallo actor framework build tools genereren echter enkele van de toepassingsbestanden model Hallo voor u.

### <a name="service-manifest"></a>Servicemanifest
Hallo actor framework build tools Hallo inhoud van uw actor-service ServiceManifest.xml bestand automatisch worden gegenereerd. Dit bestand bevat:

* Actortype-service. Hallo-typenaam is gegenereerd op basis van uw actor projectnaam. Op basis van Hallo persistentie-kenmerk op uw acteur, wordt Hallo HasPersistedState vlag ook ingesteld dienovereenkomstig.
* Codepakket.
* Configuratiepakket.
* Bronnen en eindpunten.

### <a name="application-manifest"></a>Het toepassingsmanifest
Hallo actor framework build tools wordt automatisch een standaard-servicedefinitie voor uw service actor maken. Hallo build tools vullen Hallo standaard service-eigenschappen:

* Replica set count wordt bepaald door Hallo persistentie-kenmerk op uw actor. Elk kenmerk tijd Hallo persistentie op uw actor wordt gewijzigd, Hallo replica set in de definitie van de service standaard Hallo beginwaarde dienovereenkomstig.
* Partitieschema en bereik ingesteld tooUniform Int64 met Hallo volledige Int64 sleutel bereik.

## <a name="service-fabric-partition-concepts-for-actors"></a>Concepten van service Fabric-partitie gebruiken
Actorservices zijn gepartitioneerde stateful services. Elke partitie van een actor-service bevat een set van actoren. Service-partities worden automatisch verdeeld over meerdere knooppunten in het Service Fabric. Actor-exemplaren worden als gevolg hiervan gedistribueerd.

![Acteur partitioneren en distribueren][5]

Reliable Services kunnen worden gemaakt met verschillende partitieschema's en partitie sleutelbereiken. Hallo actor-service gebruikt Hallo Int64 partitieschema met Hallo volledige Int64 sleutel bereik toomap actoren toopartitions.

### <a name="actor-id"></a>Actor-ID
Elke actor dat gemaakt in het Hallo-service heeft een unieke ID die is gekoppeld, vertegenwoordigd door Hallo `ActorId` klasse. `ActorId`is een ondoorzichtige ID-waarde die kan worden gebruikt voor gelijkmatige verdeling van actoren meerdere partities voor Hallo-service door het genereren van willekeurige id's:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Elke `ActorId` hash tooan Int64 is. Daarom Hallo actor-service moet een partitieschema Int64 met Hallo volledige Int64 sleutel bereik gebruiken. Aangepaste ID-waarden kunnen echter worden gebruikt voor een `ActorID`, met inbegrip van GUID's / UUID's, tekenreeksen en Int64s.

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

Wanneer u van GUID's / UUID's en tekenreeksen gebruikmaakt, betekent dit dat Hallo waarden hash tooan Int64 zijn. Echter, wanneer u expliciet bieden een gegevenstype Int64 tooan `ActorId`, Hallo Int64 toegewezen rechtstreeks tooa partitie zonder verdere hashing. U kunt deze techniek toocontrol die partitie Hallo actoren in zijn ingedeeld.

## <a name="next-steps"></a>Volgende stappen
* [Statusbeheer actor](service-fabric-reliable-actors-state-management.md)
* [Acteur lifecycle en garbage collection](service-fabric-reliable-actors-lifecycle.md)
* [API-naslagdocumentatie actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Voorbeeldcode voor .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Voorbeeldcode voor Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
