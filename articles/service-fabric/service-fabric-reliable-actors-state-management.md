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
# <a name="reliable-actors-state-management"></a>Statusbeheer voor betrouwbare Actors
Reliable Actors zijn single thread-objecten die zowel de logica en de status kunnen inkapselen. Omdat actoren op Reliable Services worden uitgevoerd, ze kunnen houden status betrouwbaar via Hallo dezelfde persistentie en replicatie-mechanismen Reliable Services gebruikt. Op deze manier actoren niet hun status na fouten bij het opnieuw te activeren nadat garbagecollection of wanneer ze worden verplaatst tussen knooppunten in een cluster vervaldatum tooresource netwerktaakverdeling of upgrades verliezen.

## <a name="state-persistence-and-replication"></a>Status persistentie en replicatie
Alle Reliable Actors worden beschouwd als *stateful* omdat elk exemplaar actor tooa unieke ID toegewezen. Dit betekent dat herhaalde aanroepen toohello dezelfde actor-ID worden gerouteerd toohello hetzelfde actor-exemplaar. In een stateless systeem daarentegen clientaanroepen zijn niet gegarandeerd toobe gerouteerd toohello dezelfde server elke keer. Actorservices zijn daarom altijd stateful services.

Hoewel actoren worden beschouwd als stateful die betekent niet dat ze betrouwbaar status moeten bevatten. Actoren kunnen kiezen Hallo status persistentie en replicatie op basis van hun gegevens opslagvereisten:

* **Status persistent**: status persistente toodisk en gerepliceerde too3 of meer replica's. Dit is Hallo meest duurzame status opslagoptie waarbij status via het volledige cluster storing kunt behouden.
* **Vluchtige status**: status gerepliceerde too3 of meer replica's en alleen in het geheugen worden bewaard. Dit biedt veerkracht tegen storingen van knooppunt en actor-fout en tijdens upgrades en resource netwerktaakverdeling. De status is echter niet persistent gemaakte toodisk. Dus als alle replica's verloren gaan in één keer, Hallo status is verloren gegaan ook.
* **Er is geen permanente status**: status niet wordt gerepliceerd of toodisk geschreven. Dit niveau is gebruiken die niet gewoon toomaintain status betrouwbaar nodig.

Verschillende niveaus van persistentie is gewoon een andere *state-provider* en *replicatie* configuratie van uw service. Al dan niet de status wordt geschreven afhankelijk toodisk Hallo state-provider--hello onderdeel in een betrouwbare service die de status opslaat. Replicatie is afhankelijk van hoeveel replica's een service wordt geïmplementeerd met. Net als bij Reliable Services beide Hallo state-provider en aantal replica's kan gemakkelijk handmatig worden ingesteld. Hallo actor-framework biedt een kenmerk dat, wanneer gebruikt op een actor selecteert automatisch een standaard state-provider en instellingen voor de replica aantal tooachieve een van deze drie persistentie-instellingen wordt automatisch gegenereerd. Hallo StatePersistence kenmerk wordt niet overgenomen door een afgeleide klasse, elk type Actor het niveau StatePersistence moet opgeven.

### <a name="persisted-state"></a>Permanente status
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
Deze instelling maakt gebruik van een state-provider die gegevens worden opgeslagen op schijf en Hallo service replica aantal too3 wordt automatisch ingesteld.

### <a name="volatile-state"></a>Vluchtige status
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
Deze instelling maakt gebruik van een in-memory-only state-provider en sets Hallo replica aantal too3.

### <a name="no-persisted-state"></a>Er is geen permanente status
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
Deze instelling maakt gebruik van een in-memory-only state-provider en sets Hallo replica aantal too1.

### <a name="defaults-and-generated-settings"></a>Standaardwaarden en gegenereerde instellingen
Wanneer u Hallo `StatePersistence` kenmerk, een state-provider wordt automatisch geselecteerd voor tijdens runtime wanneer Hallo actor-service wordt gestart. Hallo-aantal replica's echter is ingesteld tijdens de compilatie door Visual Studio actor Hallo build tools. Hallo build tools genereren automatisch een *standaardservice* voor Hallo actor-service in ApplicationManifest.xml. Parameters worden gemaakt voor **grootte van de replicaset min** en **doelreplica grootte instellen**.

U kunt deze parameters handmatig wijzigen. Maar elke keer Hallo `StatePersistence` kenmerk is gewijzigd, Hallo-parameters zijn ingesteld toohello replica set grootte standaardwaarden voor de geselecteerde Hallo `StatePersistence` kenmerk, een vorige waarden overschreven. Met andere woorden, Hallo-waarden die u in ServiceManifest.xml instelt zijn *alleen* genegeerd op build-tijd wanneer u Hallo wijzigt `StatePersistence` kenmerkwaarde.

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

## <a name="state-manager"></a>Status manager
Elke actor-exemplaar heeft een eigen statusbeheer: een dictionary-achtige gegevensstructuur slaat veilig sleutel/waarde-paren. Hallo status manager is een wrapper rond een state-provider. U kunt deze toostore gegevens ongeacht welke persistentie-instelling wordt gebruikt. Biedt geen garanties dat een actieve actor-service kan worden gewijzigd van een vluchtige (in-memory-only) status instelling tooa persistent statusinstelling via een uitrollende upgrade behoud van gegevens. Het is echter mogelijk toochange aantal replica's voor een actieve service.

Status manager sleutels moeten tekenreeksen zijn. Waarden zijn algemeen en kunnen worden ingesteld, inclusief aangepaste typen. Waarden die zijn opgeslagen in Hallo status manager moeten gegevenscontract serialiseerbaar omdat ze tijdens de replicatie via de netwerkknooppunten tooother Hallo kunnen worden verzonden en toodisk, afhankelijk van een actor persistentie Beleidsstatus kunnen worden geschreven.

statusbeheer Hallo beschrijft algemene woordenlijst methoden voor het beheren van status, vergelijkbare toothose in betrouwbare bibliotheek gevonden.

### <a name="accessing-state"></a>Toegang tot de status
Status kan worden benaderd via Hallo statusbeheer sleutel. De status manager methoden zijn alle asynchrone omdat ze schijf-i/o vereisen mogelijk wanneer actoren nog status persistent hebt gemaakt. Na de eerste toegang status objecten in cache zijn opgeslagen in het geheugen. Herhaal toegang operations-objecten rechtstreeks uit het geheugen en retourneren synchroon zonder schijf i/o- of asynchrone context-switching overhead. Een object met de status is verwijderd uit de cache Hallo in de volgende gevallen Hallo:

* Een actormethode genereert een onverwerkte uitzondering nadat het ophalen van een object uit Hallo status manager.
* Een actor opnieuw wordt geactiveerd, na wordt gedeactiveerd of na een storing.
* pagina's Hallo status provider status toodisk. Dit gedrag is afhankelijk van de implementatie van de persistentieprovider status Hallo. Hallo standaard state-provider voor Hallo `Persisted` instelling, heeft dit gedrag.

U kunt de status ophalen met behulp van een standaard *ophalen* bewerking die genereert `KeyNotFoundException`(C#) of `NoSuchElementException`(Java) als er een vermelding bestaat niet voor Hallo-sleutel:

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

U kunt ook de status ophalen met behulp van een *TryGet* methode die niet genereren wordt als een vermelding niet voor een sleutel bestaat:

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

### <a name="saving-state"></a>Status opslaan
Hallo status manager ophalen methoden retourneren een referentieobject tooan in het lokale geheugen. Wijzigen van dit object in het lokale geheugen alleen leidt niet tot deze toobe blijvend opgeslagen. Wanneer een object is opgehaald uit Hallo statusbeheer en gewijzigd, moet opnieuw in Hallo status manager toobe blijvend opgeslagen worden ingevoegd.

U kunt de status invoegen met behulp van een onvoorwaardelijke *ingesteld*, die is Hallo equivalent van Hallo `dictionary["key"] = value` syntaxis:

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

U kunt toevoegen met behulp van een *toevoegen* methode. Deze methode genereert `InvalidOperationException`(C#) of `IllegalStateException`(Java) als er wordt geprobeerd tooadd een sleutel die al bestaat.

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

U kunt ook de status toevoegen met behulp van een *TryAdd* methode. Deze methode wordt niet genereren als er wordt geprobeerd tooadd een sleutel die al bestaat.

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

Hallo status manager aan het einde van de Hallo van een actormethode, automatisch alle waarden die zijn toegevoegd of gewijzigd door een bewerking insert of update opgeslagen. Een 'opslaan' kunt opnemen persistent maken toodisk en replicatie, afhankelijk van het Hallo-instellingen die worden gebruikt. Waarden die niet zijn gewijzigd, zijn niet persistent of gerepliceerd. Als geen waarden zijn gewijzigd, wordt er Hallo opslagbewerking geen effect. Als mislukt opslaat, hello gewijzigde status wordt verwijderd en de oorspronkelijke staat Hallo wordt opnieuw geladen.

U kunt de status ook handmatig opslaan door de aanroepende Hallo `SaveStateAsync` methode op Hallo actor base:

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

### <a name="removing-state"></a>Status verwijderen
U kunt de status permanent verwijderen uit een actor status manager door de aanroepende Hallo *verwijderen* methode. Deze methode genereert `KeyNotFoundException`(C#) of `NoSuchElementException`(Java) als er wordt geprobeerd tooremove een sleutel die niet bestaat.

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

U kunt ook de status permanent verwijderen met behulp van Hallo *TryRemove* methode. Deze methode wordt niet genereren als er wordt geprobeerd tooremove een sleutel die niet bestaat.

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

## <a name="next-steps"></a>Volgende stappen

Status die opgeslagen in Reliable Actors moet worden geserialiseerd voordat de schriftelijke toodisk en gerepliceerd voor hoge beschikbaarheid. Meer informatie over [Actor type serialisatie](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Vervolgens meer wilt weten over [Actor diagnostische gegevens en prestatiebewaking](service-fabric-reliable-actors-diagnostics.md).
