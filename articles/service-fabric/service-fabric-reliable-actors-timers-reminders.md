---
title: aaaReliable actoren timers en herinneringen | Microsoft Docs
description: Inleiding tootimers en herinneringen voor Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="3416e-103">Acteur timers en herinneringen</span><span class="sxs-lookup"><span data-stu-id="3416e-103">Actor timers and reminders</span></span>
<span data-ttu-id="3416e-104">Actoren kunnen periodieke werk op zichzelf registreert timers of herinneringen plannen.</span><span class="sxs-lookup"><span data-stu-id="3416e-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="3416e-105">Dit artikel laat zien hoe toouse timers en herinneringen en Hallo verschillen uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="3416e-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="3416e-106">Acteur timers</span><span class="sxs-lookup"><span data-stu-id="3416e-106">Actor timers</span></span>
<span data-ttu-id="3416e-107">Acteur timers bieden een eenvoudige wrapper rond een timer .NET of Java tooensure dat de callback-methoden Hallo Hallo Schakel gebaseerde gelijktijdigheid van taken wordt gegarandeerd dat Hallo actoren runtime biedt naleven.</span><span class="sxs-lookup"><span data-stu-id="3416e-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="3416e-108">Actoren kunt Hallo `RegisterTimer`(C#) of `registerTimer`(Java) en `UnregisterTimer`(C#) of `unregisterTimer`(Java) methoden op hun base tooregister klasse en ongedaan maken van hun timers.</span><span class="sxs-lookup"><span data-stu-id="3416e-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="3416e-109">Hallo in het volgende voorbeeld ziet u Hallo gebruik van de timer-API's.</span><span class="sxs-lookup"><span data-stu-id="3416e-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="3416e-110">Hallo API's zijn vergelijkbaar toohello .NET timer of Java-timer.</span><span class="sxs-lookup"><span data-stu-id="3416e-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="3416e-111">In dit voorbeeld wanneer Hallo timer vervalt, Hallo actoren runtime belt Hallo `MoveObject`(C#) of `moveObject`(Java)-methode.</span><span class="sxs-lookup"><span data-stu-id="3416e-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="3416e-112">Hallo-methode is gegarandeerd toorespect Hallo Schakel gebaseerde gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="3416e-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="3416e-113">Dit betekent dat er geen andere actor-methoden of timer/herinnering retouraanroepen wordt uitgevoerd totdat deze retouraanroep uitvoering is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3416e-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="3416e-114">Hallo volgende periode Hallo timer wordt gestart nadat het Hallo-callback uitvoering is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3416e-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="3416e-115">Dit betekent dat Hallo-timer is gestopt tijdens het Hallo-callback wordt uitgevoerd en wordt gestart wanneer Hallo retouraanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3416e-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="3416e-116">Hallo actoren runtime Hiermee slaat u wijzigingen in toohello actor van status Manager wanneer Hallo retouraanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3416e-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="3416e-117">Als een fout optreedt bij het opslaan van Hallo status, dat actor-object wordt gedeactiveerd en een nieuw exemplaar wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3416e-118">Alle timers worden gestopt als Hallo actor als onderdeel van de garbagecollection wordt gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="3416e-119">Er is geen retouraanroepen timer worden na die aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3416e-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="3416e-120">Bovendien behouden Hallo actoren runtime niet geen gegevens over Hallo timers die werden uitgevoerd voordat de deactivering.</span><span class="sxs-lookup"><span data-stu-id="3416e-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="3416e-121">Is toohello actor tooregister de vernieuwingstimer die nodig is wanneer het in toekomstige Hallo opnieuw wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="3416e-122">Zie voor meer informatie Hallo-sectie op [actor garbagecollection](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="3416e-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="3416e-123">Acteur herinneringen</span><span class="sxs-lookup"><span data-stu-id="3416e-123">Actor reminders</span></span>
<span data-ttu-id="3416e-124">Herinneringen zijn een mechanisme tootrigger permanente retouraanroepen op een actor op keren opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3416e-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="3416e-125">De functionaliteit is vergelijkbaar tootimers.</span><span class="sxs-lookup"><span data-stu-id="3416e-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="3416e-126">Maar in tegenstelling tot timers, herinneringen onder alle omstandigheden worden geactiveerd totdat Hallo actor expliciet deregistreren of Hallo actor expliciet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3416e-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="3416e-127">In het bijzonder worden herinneringen geactiveerd via actor deactivations en failovers, omdat de Hallo actoren runtime informatie over de Hallo actor herinneringen blijft bestaan.</span><span class="sxs-lookup"><span data-stu-id="3416e-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="3416e-128">een herinnering tooregister, een actor roept Hallo `RegisterReminderAsync` methode opgegeven op Hallo basisklasse, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="3416e-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="3416e-129">In dit voorbeeld `"Pay cell phone bill"` Hallo herinnering naam.</span><span class="sxs-lookup"><span data-stu-id="3416e-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="3416e-130">Dit is een tekenreeks die Hallo actor gebruikt toouniquely een herinnering identificeren.</span><span class="sxs-lookup"><span data-stu-id="3416e-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="3416e-131">`BitConverter.GetBytes(amountInDollars)`(C#) is Hallo context die is gekoppeld aan Hallo herinnering.</span><span class="sxs-lookup"><span data-stu-id="3416e-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="3416e-132">Deze wordt doorgegeven back toohello actor als een argument toohello herinnering retouraanroep, dat wil zeggen `IRemindable.ReceiveReminderAsync`(C#) of `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="3416e-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="3416e-133">Actoren die gebruikmaken van herinneringen Hallo moeten implementeren `IRemindable` interface, zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="3416e-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="3416e-134">Wanneer een herinnering wordt geactiveerd, Hallo Reliable Actors runtime Hallo worden ingeroepen `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-methode op Hallo Actor.</span><span class="sxs-lookup"><span data-stu-id="3416e-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="3416e-135">Een actor meerdere herinneringen registreren en Hallo `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-methode wordt aangeroepen wanneer een van deze herinneringen is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="3416e-136">Hallo actor kunt Hallo herinnering naam die wordt doorgegeven in toohello `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java) methode toofigure uit die herinnering is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="3416e-137">Hallo actoren runtime slaat Hallo actorstatus wanneer hello `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3416e-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="3416e-138">Als een fout optreedt bij het opslaan van Hallo status, dat actor-object wordt gedeactiveerd en een nieuw exemplaar wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3416e-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3416e-139">een herinnering toounregister, een actor roept Hallo `UnregisterReminderAsync`(C#) of `unregisterReminderAsync`(Java)-methode, zoals wordt weergegeven in onderstaande Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3416e-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="3416e-140">Zoals hierboven beschreven, Hallo `UnregisterReminderAsync`(C#) of `unregisterReminderAsync`(Java) methode accepteert een `IActorReminder`(C#) of `ActorReminder`(Java)-interface.</span><span class="sxs-lookup"><span data-stu-id="3416e-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="3416e-141">Hallo actor basisklasse ondersteunt een `GetReminder`(C#) of `getReminder`(Java)-methode die gebruikt tooretrieve hello worden kan `IActorReminder`(C#) of `ActorReminder`(Java) interface door door te geven in Hallo herinnering naam.</span><span class="sxs-lookup"><span data-stu-id="3416e-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="3416e-142">Dit is handig omdat Hallo actor niet toopersist hello hoeft `IActorReminder`(C#) of `ActorReminder`(Java)-interface die is geretourneerd van Hallo `RegisterReminder`(C#) of `registerReminder`methodeaanroep (Java).</span><span class="sxs-lookup"><span data-stu-id="3416e-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3416e-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3416e-143">Next Steps</span></span>
<span data-ttu-id="3416e-144">Meer informatie over betrouwbare Actor gebeurtenissen en herintreding:</span><span class="sxs-lookup"><span data-stu-id="3416e-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="3416e-145">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="3416e-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="3416e-146">Acteur herintreding</span><span class="sxs-lookup"><span data-stu-id="3416e-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
