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
# <a name="actor-timers-and-reminders"></a>Acteur timers en herinneringen
Actoren kunnen periodieke werk op zichzelf registreert timers of herinneringen plannen. Dit artikel laat zien hoe toouse timers en herinneringen en Hallo verschillen uitgelegd.

## <a name="actor-timers"></a>Acteur timers
Acteur timers bieden een eenvoudige wrapper rond een timer .NET of Java tooensure dat de callback-methoden Hallo Hallo Schakel gebaseerde gelijktijdigheid van taken wordt gegarandeerd dat Hallo actoren runtime biedt naleven.

Actoren kunt Hallo `RegisterTimer`(C#) of `registerTimer`(Java) en `UnregisterTimer`(C#) of `unregisterTimer`(Java) methoden op hun base tooregister klasse en ongedaan maken van hun timers. Hallo in het volgende voorbeeld ziet u Hallo gebruik van de timer-API's. Hallo API's zijn vergelijkbaar toohello .NET timer of Java-timer. In dit voorbeeld wanneer Hallo timer vervalt, Hallo actoren runtime belt Hallo `MoveObject`(C#) of `moveObject`(Java)-methode. Hallo-methode is gegarandeerd toorespect Hallo Schakel gebaseerde gelijktijdigheid van taken. Dit betekent dat er geen andere actor-methoden of timer/herinnering retouraanroepen wordt uitgevoerd totdat deze retouraanroep uitvoering is voltooid.

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

Hallo volgende periode Hallo timer wordt gestart nadat het Hallo-callback uitvoering is voltooid. Dit betekent dat Hallo-timer is gestopt tijdens het Hallo-callback wordt uitgevoerd en wordt gestart wanneer Hallo retouraanroep is voltooid.

Hallo actoren runtime Hiermee slaat u wijzigingen in toohello actor van status Manager wanneer Hallo retouraanroep is voltooid. Als een fout optreedt bij het opslaan van Hallo status, dat actor-object wordt gedeactiveerd en een nieuw exemplaar wordt geactiveerd.

Alle timers worden gestopt als Hallo actor als onderdeel van de garbagecollection wordt gedeactiveerd. Er is geen retouraanroepen timer worden na die aangeroepen. Bovendien behouden Hallo actoren runtime niet geen gegevens over Hallo timers die werden uitgevoerd voordat de deactivering. Is toohello actor tooregister de vernieuwingstimer die nodig is wanneer het in toekomstige Hallo opnieuw wordt geactiveerd. Zie voor meer informatie Hallo-sectie op [actor garbagecollection](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Acteur herinneringen
Herinneringen zijn een mechanisme tootrigger permanente retouraanroepen op een actor op keren opgegeven. De functionaliteit is vergelijkbaar tootimers. Maar in tegenstelling tot timers, herinneringen onder alle omstandigheden worden geactiveerd totdat Hallo actor expliciet deregistreren of Hallo actor expliciet worden verwijderd. In het bijzonder worden herinneringen geactiveerd via actor deactivations en failovers, omdat de Hallo actoren runtime informatie over de Hallo actor herinneringen blijft bestaan.

een herinnering tooregister, een actor roept Hallo `RegisterReminderAsync` methode opgegeven op Hallo basisklasse, zoals wordt weergegeven in Hallo voorbeeld te volgen:

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

In dit voorbeeld `"Pay cell phone bill"` Hallo herinnering naam. Dit is een tekenreeks die Hallo actor gebruikt toouniquely een herinnering identificeren. `BitConverter.GetBytes(amountInDollars)`(C#) is Hallo context die is gekoppeld aan Hallo herinnering. Deze wordt doorgegeven back toohello actor als een argument toohello herinnering retouraanroep, dat wil zeggen `IRemindable.ReceiveReminderAsync`(C#) of `Remindable.receiveReminderAsync`(Java).

Actoren die gebruikmaken van herinneringen Hallo moeten implementeren `IRemindable` interface, zoals weergegeven in Hallo voorbeeld hieronder.

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

Wanneer een herinnering wordt geactiveerd, Hallo Reliable Actors runtime Hallo worden ingeroepen `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-methode op Hallo Actor. Een actor meerdere herinneringen registreren en Hallo `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-methode wordt aangeroepen wanneer een van deze herinneringen is geactiveerd. Hallo actor kunt Hallo herinnering naam die wordt doorgegeven in toohello `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java) methode toofigure uit die herinnering is geactiveerd.

Hallo actoren runtime slaat Hallo actorstatus wanneer hello `ReceiveReminderAsync`(C#) of `receiveReminderAsync`(Java)-aanroep is voltooid. Als een fout optreedt bij het opslaan van Hallo status, dat actor-object wordt gedeactiveerd en een nieuw exemplaar wordt geactiveerd.

een herinnering toounregister, een actor roept Hallo `UnregisterReminderAsync`(C#) of `unregisterReminderAsync`(Java)-methode, zoals wordt weergegeven in onderstaande Hallo voorbeelden.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Zoals hierboven beschreven, Hallo `UnregisterReminderAsync`(C#) of `unregisterReminderAsync`(Java) methode accepteert een `IActorReminder`(C#) of `ActorReminder`(Java)-interface. Hallo actor basisklasse ondersteunt een `GetReminder`(C#) of `getReminder`(Java)-methode die gebruikt tooretrieve hello worden kan `IActorReminder`(C#) of `ActorReminder`(Java) interface door door te geven in Hallo herinnering naam. Dit is handig omdat Hallo actor niet toopersist hello hoeft `IActorReminder`(C#) of `ActorReminder`(Java)-interface die is geretourneerd van Hallo `RegisterReminder`(C#) of `registerReminder`methodeaanroep (Java).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over betrouwbare Actor gebeurtenissen en herintreding:
* [Actor-gebeurtenissen](service-fabric-reliable-actors-events.md)
* [Acteur herintreding](service-fabric-reliable-actors-reentrancy.md)
