---
title: aaaReliable actoren opmerkingen bij de actor type serialisatie | Microsoft Docs
description: "Basisvereisten voor het definiëren van serialiseerbaar klassen die kunnen worden gebruikt toodefine Service Fabric Reliable Actors statussen en interfaces wordt beschreven"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="30689-103">Opmerkingen bij de Service Fabric Reliable Actors type serialisatie</span><span class="sxs-lookup"><span data-stu-id="30689-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="30689-104">Hallo-argumenten van alle methoden, resultaattypen Hallo taken worden geretourneerd door elke methode in een interface actor en objecten die zijn opgeslagen in een actor statusbeheer moet [gegevenscontract serialiseerbaar](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="30689-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="30689-105">Dit geldt ook toohello argumenten van Hallo-methoden die zijn gedefinieerd in [actor-gebeurtenisinterfaces](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="30689-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="30689-106">(Actor gebeurtenis interfacemethoden altijd void retourneren.)</span><span class="sxs-lookup"><span data-stu-id="30689-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="30689-107">Aangepaste gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="30689-107">Custom data types</span></span>
<span data-ttu-id="30689-108">In dit voorbeeld definieert Hallo na actor-interface een methode die een aangepast gegevenstype aangeroepen retourneert `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="30689-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="30689-109">Hallo-interface wordt geïmplementeerd door een actor die gebruikmaakt van Hallo status manager toostore een `VoicemailBox` object:</span><span class="sxs-lookup"><span data-stu-id="30689-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="30689-110">In dit voorbeeld Hallo `VoicemailBox` object wordt geserialiseerd wanneer:</span><span class="sxs-lookup"><span data-stu-id="30689-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="30689-111">Hallo-object wordt tussen een actor-exemplaar en een aanroeper verzonden.</span><span class="sxs-lookup"><span data-stu-id="30689-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="30689-112">Hallo-object wordt opgeslagen in Hallo statusbeheer waar het persistente toodisk en tooother knooppunten gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="30689-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="30689-113">Hallo betrouwbare Actor framework maakt gebruik van DataContract-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="30689-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="30689-114">Daarom Hallo aangepaste gegevensobjecten en hun leden moeten van aantekeningen worden voorzien met Hallo **DataContract** en **DataMember** kenmerken, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="30689-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="30689-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30689-115">Next steps</span></span>
* [<span data-ttu-id="30689-116">Acteur lifecycle en garbage collection</span><span class="sxs-lookup"><span data-stu-id="30689-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="30689-117">Acteur timers en herinneringen</span><span class="sxs-lookup"><span data-stu-id="30689-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="30689-118">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="30689-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="30689-119">Acteur herintreding</span><span class="sxs-lookup"><span data-stu-id="30689-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="30689-120">Acteur polymorfisme en objectgeoriënteerde ontwerppatronen</span><span class="sxs-lookup"><span data-stu-id="30689-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="30689-121">Acteur diagnostische gegevens en prestatiebewaking</span><span class="sxs-lookup"><span data-stu-id="30689-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
