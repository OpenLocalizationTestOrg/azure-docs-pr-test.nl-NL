---
title: aaaReliable actoren status management | Microsoft Docs
description: Beschrijft hoe Reliable Actors status is beheerd, opgeslagen en gerepliceerd voor hoge beschikbaarheid.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="445be-103">Statusbeheer voor betrouwbare Actors</span><span class="sxs-lookup"><span data-stu-id="445be-103">Reliable Actors state management</span></span>
<span data-ttu-id="445be-104">Reliable Actors zijn single thread-objecten die zowel de logica en de status kunnen inkapselen.</span><span class="sxs-lookup"><span data-stu-id="445be-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="445be-105">Omdat actoren op Reliable Services worden uitgevoerd, ze kunnen houden status betrouwbaar via Hallo dezelfde persistentie en replicatie-mechanismen Reliable Services gebruikt.</span><span class="sxs-lookup"><span data-stu-id="445be-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="445be-106">Op deze manier actoren niet hun status na fouten bij het opnieuw te activeren nadat garbagecollection of wanneer ze worden verplaatst tussen knooppunten in een cluster vervaldatum tooresource netwerktaakverdeling of upgrades verliezen.</span><span class="sxs-lookup"><span data-stu-id="445be-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="445be-107">Status persistentie en replicatie</span><span class="sxs-lookup"><span data-stu-id="445be-107">State persistence and replication</span></span>
<span data-ttu-id="445be-108">Alle Reliable Actors worden beschouwd als *stateful* omdat elk exemplaar actor tooa unieke ID toegewezen.</span><span class="sxs-lookup"><span data-stu-id="445be-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="445be-109">Dit betekent dat herhaalde aanroepen toohello dezelfde actor-ID worden gerouteerd toohello hetzelfde actor-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="445be-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="445be-110">In een stateless systeem daarentegen clientaanroepen zijn niet gegarandeerd toobe gerouteerd toohello dezelfde server elke keer.</span><span class="sxs-lookup"><span data-stu-id="445be-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="445be-111">Actorservices zijn daarom altijd stateful services.</span><span class="sxs-lookup"><span data-stu-id="445be-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="445be-112">Hoewel actoren worden beschouwd als stateful die betekent niet dat ze betrouwbaar status moeten bevatten.</span><span class="sxs-lookup"><span data-stu-id="445be-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="445be-113">Actoren kunnen kiezen Hallo status persistentie en replicatie op basis van hun gegevens opslagvereisten:</span><span class="sxs-lookup"><span data-stu-id="445be-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="445be-114">**Status persistent**: status persistente toodisk en gerepliceerde too3 of meer replica's.</span><span class="sxs-lookup"><span data-stu-id="445be-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="445be-115">Dit is Hallo meest duurzame status opslagoptie waarbij status via het volledige cluster storing kunt behouden.</span><span class="sxs-lookup"><span data-stu-id="445be-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="445be-116">**Vluchtige status**: status gerepliceerde too3 of meer replica's en alleen in het geheugen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="445be-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="445be-117">Dit biedt veerkracht tegen storingen van knooppunt en actor-fout en tijdens upgrades en resource netwerktaakverdeling.</span><span class="sxs-lookup"><span data-stu-id="445be-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="445be-118">De status is echter niet persistent gemaakte toodisk.</span><span class="sxs-lookup"><span data-stu-id="445be-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="445be-119">Dus als alle replica's verloren gaan in één keer, Hallo status is verloren gegaan ook.</span><span class="sxs-lookup"><span data-stu-id="445be-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="445be-120">**Er is geen permanente status**: status niet wordt gerepliceerd of toodisk geschreven.</span><span class="sxs-lookup"><span data-stu-id="445be-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="445be-121">Dit niveau is gebruiken die niet gewoon toomaintain status betrouwbaar nodig.</span><span class="sxs-lookup"><span data-stu-id="445be-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="445be-122">Verschillende niveaus van persistentie is gewoon een andere *state-provider* en *replicatie* configuratie van uw service.</span><span class="sxs-lookup"><span data-stu-id="445be-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="445be-123">Al dan niet de status wordt geschreven afhankelijk toodisk Hallo state-provider--hello onderdeel in een betrouwbare service die de status opslaat.</span><span class="sxs-lookup"><span data-stu-id="445be-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="445be-124">Replicatie is afhankelijk van hoeveel replica's een service wordt geïmplementeerd met.</span><span class="sxs-lookup"><span data-stu-id="445be-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="445be-125">Net als bij Reliable Services beide Hallo state-provider en aantal replica's kan gemakkelijk handmatig worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="445be-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="445be-126">Hallo actor-framework biedt een kenmerk dat, wanneer gebruikt op een actor selecteert automatisch een standaard state-provider en instellingen voor de replica aantal tooachieve een van deze drie persistentie-instellingen wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="445be-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="445be-127">Hallo StatePersistence kenmerk wordt niet overgenomen door een afgeleide klasse, elk type Actor het niveau StatePersistence moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="445be-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="445be-128">Permanente status</span><span class="sxs-lookup"><span data-stu-id="445be-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="445be-129">Deze instelling maakt gebruik van een state-provider die gegevens worden opgeslagen op schijf en Hallo service replica aantal too3 wordt automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="445be-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="445be-130">Vluchtige status</span><span class="sxs-lookup"><span data-stu-id="445be-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="445be-131">Deze instelling maakt gebruik van een in-memory-only state-provider en sets Hallo replica aantal too3.</span><span class="sxs-lookup"><span data-stu-id="445be-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="445be-132">Er is geen permanente status</span><span class="sxs-lookup"><span data-stu-id="445be-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="445be-133">Deze instelling maakt gebruik van een in-memory-only state-provider en sets Hallo replica aantal too1.</span><span class="sxs-lookup"><span data-stu-id="445be-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="445be-134">Standaardwaarden en gegenereerde instellingen</span><span class="sxs-lookup"><span data-stu-id="445be-134">Defaults and generated settings</span></span>
<span data-ttu-id="445be-135">Wanneer u Hallo `StatePersistence` kenmerk, een state-provider wordt automatisch geselecteerd voor tijdens runtime wanneer Hallo actor-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="445be-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="445be-136">Hallo-aantal replica's echter is ingesteld tijdens de compilatie door Visual Studio actor Hallo build tools.</span><span class="sxs-lookup"><span data-stu-id="445be-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="445be-137">Hallo build tools genereren automatisch een *standaardservice* voor Hallo actor-service in ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="445be-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="445be-138">Parameters worden gemaakt voor **grootte van de replicaset min** en **doelreplica grootte instellen**.</span><span class="sxs-lookup"><span data-stu-id="445be-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="445be-139">U kunt deze parameters handmatig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="445be-139">You can change these parameters manually.</span></span> <span data-ttu-id="445be-140">Maar elke keer Hallo `StatePersistence` kenmerk is gewijzigd, Hallo-parameters zijn ingesteld toohello replica set grootte standaardwaarden voor de geselecteerde Hallo `StatePersistence` kenmerk, een vorige waarden overschreven.</span><span class="sxs-lookup"><span data-stu-id="445be-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="445be-141">Met andere woorden, Hallo-waarden die u in ServiceManifest.xml instelt zijn *alleen* genegeerd op build-tijd wanneer u Hallo wijzigt `StatePersistence` kenmerkwaarde.</span><span class="sxs-lookup"><span data-stu-id="445be-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="445be-142">Status manager</span><span class="sxs-lookup"><span data-stu-id="445be-142">State manager</span></span>
<span data-ttu-id="445be-143">Elke actor-exemplaar heeft een eigen statusbeheer: een dictionary-achtige gegevensstructuur slaat veilig sleutel/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="445be-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="445be-144">Hallo status manager is een wrapper rond een state-provider.</span><span class="sxs-lookup"><span data-stu-id="445be-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="445be-145">U kunt deze toostore gegevens ongeacht welke persistentie-instelling wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="445be-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="445be-146">Biedt geen garanties dat een actieve actor-service kan worden gewijzigd van een vluchtige (in-memory-only) status instelling tooa persistent statusinstelling via een uitrollende upgrade behoud van gegevens.</span><span class="sxs-lookup"><span data-stu-id="445be-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="445be-147">Het is echter mogelijk toochange aantal replica's voor een actieve service.</span><span class="sxs-lookup"><span data-stu-id="445be-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="445be-148">Status manager sleutels moeten tekenreeksen zijn.</span><span class="sxs-lookup"><span data-stu-id="445be-148">State manager keys must be strings.</span></span> <span data-ttu-id="445be-149">Waarden zijn algemeen en kunnen worden ingesteld, inclusief aangepaste typen.</span><span class="sxs-lookup"><span data-stu-id="445be-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="445be-150">Waarden die zijn opgeslagen in Hallo status manager moeten gegevenscontract serialiseerbaar omdat ze tijdens de replicatie via de netwerkknooppunten tooother Hallo kunnen worden verzonden en toodisk, afhankelijk van een actor persistentie Beleidsstatus kunnen worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="445be-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="445be-151">statusbeheer Hallo beschrijft algemene woordenlijst methoden voor het beheren van status, vergelijkbare toothose in betrouwbare bibliotheek gevonden.</span><span class="sxs-lookup"><span data-stu-id="445be-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="445be-152">Toegang tot de status</span><span class="sxs-lookup"><span data-stu-id="445be-152">Accessing state</span></span>
<span data-ttu-id="445be-153">Status kan worden benaderd via Hallo statusbeheer sleutel.</span><span class="sxs-lookup"><span data-stu-id="445be-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="445be-154">De status manager methoden zijn alle asynchrone omdat ze schijf-i/o vereisen mogelijk wanneer actoren nog status persistent hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="445be-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="445be-155">Na de eerste toegang status objecten in cache zijn opgeslagen in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="445be-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="445be-156">Herhaal toegang operations-objecten rechtstreeks uit het geheugen en retourneren synchroon zonder schijf i/o- of asynchrone context-switching overhead.</span><span class="sxs-lookup"><span data-stu-id="445be-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="445be-157">Een object met de status is verwijderd uit de cache Hallo in de volgende gevallen Hallo:</span><span class="sxs-lookup"><span data-stu-id="445be-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="445be-158">Een actormethode genereert een onverwerkte uitzondering nadat het ophalen van een object uit Hallo status manager.</span><span class="sxs-lookup"><span data-stu-id="445be-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="445be-159">Een actor opnieuw wordt geactiveerd, na wordt gedeactiveerd of na een storing.</span><span class="sxs-lookup"><span data-stu-id="445be-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="445be-160">pagina's Hallo status provider status toodisk.</span><span class="sxs-lookup"><span data-stu-id="445be-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="445be-161">Dit gedrag is afhankelijk van de implementatie van de persistentieprovider status Hallo.</span><span class="sxs-lookup"><span data-stu-id="445be-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="445be-162">Hallo standaard state-provider voor Hallo `Persisted` instelling, heeft dit gedrag.</span><span class="sxs-lookup"><span data-stu-id="445be-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="445be-163">U kunt de status ophalen met behulp van een standaard *ophalen* bewerking die genereert `KeyNotFoundException`(C#) of `NoSuchElementException`(Java) als er een vermelding bestaat niet voor Hallo-sleutel:</span><span class="sxs-lookup"><span data-stu-id="445be-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="445be-164">U kunt ook de status ophalen met behulp van een *TryGet* methode die niet genereren wordt als een vermelding niet voor een sleutel bestaat:</span><span class="sxs-lookup"><span data-stu-id="445be-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="445be-165">Status opslaan</span><span class="sxs-lookup"><span data-stu-id="445be-165">Saving state</span></span>
<span data-ttu-id="445be-166">Hallo status manager ophalen methoden retourneren een referentieobject tooan in het lokale geheugen.</span><span class="sxs-lookup"><span data-stu-id="445be-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="445be-167">Wijzigen van dit object in het lokale geheugen alleen leidt niet tot deze toobe blijvend opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="445be-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="445be-168">Wanneer een object is opgehaald uit Hallo statusbeheer en gewijzigd, moet opnieuw in Hallo status manager toobe blijvend opgeslagen worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="445be-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="445be-169">U kunt de status invoegen met behulp van een onvoorwaardelijke *ingesteld*, die is Hallo equivalent van Hallo `dictionary["key"] = value` syntaxis:</span><span class="sxs-lookup"><span data-stu-id="445be-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="445be-170">U kunt toevoegen met behulp van een *toevoegen* methode.</span><span class="sxs-lookup"><span data-stu-id="445be-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="445be-171">Deze methode genereert `InvalidOperationException`(C#) of `IllegalStateException`(Java) als er wordt geprobeerd tooadd een sleutel die al bestaat.</span><span class="sxs-lookup"><span data-stu-id="445be-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="445be-172">U kunt ook de status toevoegen met behulp van een *TryAdd* methode.</span><span class="sxs-lookup"><span data-stu-id="445be-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="445be-173">Deze methode wordt niet genereren als er wordt geprobeerd tooadd een sleutel die al bestaat.</span><span class="sxs-lookup"><span data-stu-id="445be-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="445be-174">Hallo status manager aan het einde van de Hallo van een actormethode, automatisch alle waarden die zijn toegevoegd of gewijzigd door een bewerking insert of update opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="445be-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="445be-175">Een 'opslaan' kunt opnemen persistent maken toodisk en replicatie, afhankelijk van het Hallo-instellingen die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="445be-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="445be-176">Waarden die niet zijn gewijzigd, zijn niet persistent of gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="445be-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="445be-177">Als geen waarden zijn gewijzigd, wordt er Hallo opslagbewerking geen effect.</span><span class="sxs-lookup"><span data-stu-id="445be-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="445be-178">Als mislukt opslaat, hello gewijzigde status wordt verwijderd en de oorspronkelijke staat Hallo wordt opnieuw geladen.</span><span class="sxs-lookup"><span data-stu-id="445be-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="445be-179">U kunt de status ook handmatig opslaan door de aanroepende Hallo `SaveStateAsync` methode op Hallo actor base:</span><span class="sxs-lookup"><span data-stu-id="445be-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="445be-180">Status verwijderen</span><span class="sxs-lookup"><span data-stu-id="445be-180">Removing state</span></span>
<span data-ttu-id="445be-181">U kunt de status permanent verwijderen uit een actor status manager door de aanroepende Hallo *verwijderen* methode.</span><span class="sxs-lookup"><span data-stu-id="445be-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="445be-182">Deze methode genereert `KeyNotFoundException`(C#) of `NoSuchElementException`(Java) als er wordt geprobeerd tooremove een sleutel die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="445be-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="445be-183">U kunt ook de status permanent verwijderen met behulp van Hallo *TryRemove* methode.</span><span class="sxs-lookup"><span data-stu-id="445be-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="445be-184">Deze methode wordt niet genereren als er wordt geprobeerd tooremove een sleutel die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="445be-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="445be-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="445be-185">Next steps</span></span>

<span data-ttu-id="445be-186">Status die opgeslagen in Reliable Actors moet worden geserialiseerd voordat de schriftelijke toodisk en gerepliceerd voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="445be-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="445be-187">Meer informatie over [Actor type serialisatie](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="445be-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="445be-188">Vervolgens meer wilt weten over [Actor diagnostische gegevens en prestatiebewaking](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="445be-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
