---
title: aaaOverview van Azure microservices op basis van actor-levenscyclus | Microsoft Docs
description: Legt uit betrouwbare Service Fabric-Actor levenscyclus, garbagecollection en het handmatig verwijderen actors en hun status
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="03781-103">Actor levenscyclus, garbagecollection automatische en handmatige verwijderen</span><span class="sxs-lookup"><span data-stu-id="03781-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="03781-104">Er is een actor geactiveerd Hallo van de eerste keer wordt een aanroep tooany van de bijbehorende methoden.</span><span class="sxs-lookup"><span data-stu-id="03781-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="03781-105">Een actor is gedeactiveerd (garbage collector zijn verzameld door Hallo actoren runtime) als deze niet wordt gebruikt voor een configureerbare periode.</span><span class="sxs-lookup"><span data-stu-id="03781-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="03781-106">Een actor en de status kunnen ook handmatig worden verwijderd op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="03781-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="03781-107">Actor-activering</span><span class="sxs-lookup"><span data-stu-id="03781-107">Actor activation</span></span>
<span data-ttu-id="03781-108">Wanneer een actor is geactiveerd, wordt Hallo volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="03781-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="03781-109">Wanneer een oproep voor een actor binnenkomt en een nog niet actief, wordt een nieuwe actor gemaakt.</span><span class="sxs-lookup"><span data-stu-id="03781-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="03781-110">Hallo actorstatus is geladen als deze status wordt onderhouden.</span><span class="sxs-lookup"><span data-stu-id="03781-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="03781-111">Hallo `OnActivateAsync` (C#) of `onActivateAsync` (Java)-methode (die kan worden overschreven in Hallo actor-implementatie) wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="03781-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="03781-112">Hallo actor is nu beschouwd als actief.</span><span class="sxs-lookup"><span data-stu-id="03781-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="03781-113">Deactivering van actor</span><span class="sxs-lookup"><span data-stu-id="03781-113">Actor deactivation</span></span>
<span data-ttu-id="03781-114">Wanneer een actor is gedeactiveerd, wordt Hallo volgende gebeurt:</span><span class="sxs-lookup"><span data-stu-id="03781-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="03781-115">Wanneer een actor niet voor een bepaalde tijd gebruikt wordt, wordt dit verwijderd uit Hallo Active Actors tabel.</span><span class="sxs-lookup"><span data-stu-id="03781-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="03781-116">Hallo `OnDeactivateAsync` (C#) of `onDeactivateAsync` (Java)-methode (die kan worden overschreven in Hallo actor-implementatie) wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="03781-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="03781-117">Hiermee worden alle Hallo timers voor Hallo actor.</span><span class="sxs-lookup"><span data-stu-id="03781-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="03781-118">Actor-bewerkingen zoals status wijzigingen moeten niet worden aangeroepen vanuit deze methode.</span><span class="sxs-lookup"><span data-stu-id="03781-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="03781-119">Hallo actoren Fabric-runtime verzendt sommige [gebeurtenissen met betrekking tooactor activering en deactivering](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="03781-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="03781-120">Ze zijn nuttig zijn bij de diagnostische gegevens en prestatiebewaking.</span><span class="sxs-lookup"><span data-stu-id="03781-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="03781-121">Garbagecollection actor</span><span class="sxs-lookup"><span data-stu-id="03781-121">Actor garbage collection</span></span>
<span data-ttu-id="03781-122">Wanneer een actor is gedeactiveerd, references toohello actor-object worden vrijgegeven en wordt deze de garbage collector zijn verzameld normaal door Hallo common language runtime (CLR) of de garbagecollector van de virtuele machine (JVM) java kan worden.</span><span class="sxs-lookup"><span data-stu-id="03781-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="03781-123">Hallo actor object; ruimt garbagecollection alleen Dit gebeurt **niet** in Hallo actor van status Manager opgeslagen status verwijderen.</span><span class="sxs-lookup"><span data-stu-id="03781-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="03781-124">Hallo volgende tijd Hallo actor is geactiveerd, wordt een nieuw actor-object gemaakt en de status wordt teruggezet.</span><span class="sxs-lookup"><span data-stu-id="03781-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="03781-125">Wat wordt geteld als 'wordt gebruikt' hello doel te deactiveren en garbagecollection?</span><span class="sxs-lookup"><span data-stu-id="03781-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="03781-126">Ontvangt een oproep</span><span class="sxs-lookup"><span data-stu-id="03781-126">Receiving a call</span></span>
* <span data-ttu-id="03781-127">`IRemindable.ReceiveReminderAsync`methode wordt aangeroepen (alleen van toepassing als Hallo actor herinneringen gebruikt)</span><span class="sxs-lookup"><span data-stu-id="03781-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="03781-128">Als Hallo actor timers gebruikt en de timer-retouraanroep wordt aangeroepen, wordt **niet** aantal als 'wordt gebruikt'.</span><span class="sxs-lookup"><span data-stu-id="03781-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="03781-129">Voordat we naar de details op Hallo van deactivering overschakelt, is het belangrijk toodefine Hallo volgende voorwaarden:</span><span class="sxs-lookup"><span data-stu-id="03781-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="03781-130">*Controle-interval*.</span><span class="sxs-lookup"><span data-stu-id="03781-130">*Scan interval*.</span></span> <span data-ttu-id="03781-131">Dit is hello-interval op welke Hallo actoren runtime de tabel Active actoren scant naar actors die kunnen worden gedeactiveerd en garbage collector zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="03781-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="03781-132">Hallo-standaardwaarde voor deze is 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="03781-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="03781-133">*Time-out voor inactiviteit*.</span><span class="sxs-lookup"><span data-stu-id="03781-133">*Idle timeout*.</span></span> <span data-ttu-id="03781-134">Dit is Hallo tijdsduur dat een actor tooremain ongebruikte moet (niet-actief) voordat deze worden gedeactiveerd en garbage collector zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="03781-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="03781-135">Hallo-standaardwaarde voor deze is 60 minuten.</span><span class="sxs-lookup"><span data-stu-id="03781-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="03781-136">Normaal gesproken hoeft u niet toochange deze standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="03781-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="03781-137">Indien nodig, deze intervallen kunnen echter worden gewijzigd via `ActorServiceSettings` bij het registreren van uw [Actor Service](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="03781-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
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
    }
}
```
<span data-ttu-id="03781-138">Voor elke actieve actor Hallo actor runtime houdt van Hallo hoeveelheid tijd die inactief is geweest (d.w.z. niet gebruikt).</span><span class="sxs-lookup"><span data-stu-id="03781-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="03781-139">Hallo actor runtime vergelijkt elke Hallo actoren elke `ScanIntervalInSeconds` toosee als garbage collector zijn verzameld en verzamelt deze als gebruikt gedurende is `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="03781-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="03781-140">Telkens wanneer een actor wordt gebruikt, is de niet-actieve tijd too0 opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="03781-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="03781-141">Hierna mag Hallo actor garbage collector zijn verzameld alleen als het opnieuw inactief blijft voor `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="03781-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="03781-142">Intrekken dat toohave wordt beschouwd als een actor is gebruikt als een interfacemethode actor of een herinnering actor retouraanroep is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="03781-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="03781-143">Een actor is **niet** toohave beschouwd als is gebruikt als de timer-retouraanroep is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="03781-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="03781-144">Hallo volgende diagram toont Hallo levenscyclus van een enkele actor tooillustrate deze concepten.</span><span class="sxs-lookup"><span data-stu-id="03781-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Voorbeeld van een niet-actieve tijd][1]

<span data-ttu-id="03781-146">Hallo-voorbeeld ziet u Hallo effect actor methodeaanroepen, herinneringen en timers op Hallo levensduur van deze acteur.</span><span class="sxs-lookup"><span data-stu-id="03781-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="03781-147">Hallo punten over Hallo voorbeeld te volgen zijn opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="03781-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="03781-148">ScanInterval en IdleTimeout ingesteld too5 en 10 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="03781-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="03781-149">(Eenheden niet terzake hier, aangezien we alleen tooillustrate Hallo concept.)</span><span class="sxs-lookup"><span data-stu-id="03781-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="03781-150">Hallo-scan voor actoren toobe garbage collector zijn verzameld op T = 0, 5, 10, 15, 20, 25, gebeurt zoals gedefinieerd door hello controle-interval van 5.</span><span class="sxs-lookup"><span data-stu-id="03781-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="03781-151">Een periodieke timer wordt geactiveerd op T = 4, 8, 12, 16, 20, 24, en de retouraanroep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="03781-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="03781-152">Niet-actieve tijd van Hallo actor Hallo geen gevolgen.</span><span class="sxs-lookup"><span data-stu-id="03781-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="03781-153">Een methodeaanroep actor op T = 7 Hallo niet-actieve tijd too0 herstelt en Hallo-garbagecollection van Hallo actor uitstelt.</span><span class="sxs-lookup"><span data-stu-id="03781-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="03781-154">Een herinnering actor retouraanroep wordt uitgevoerd op T = 14 en verdere vertragingen garbagecollection van Hallo actor Hallo.</span><span class="sxs-lookup"><span data-stu-id="03781-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="03781-155">Tijdens Hallo garbagecollection verzameling scan T = 25 Hallo actor van niet-actieve tijd ten slotte time-out voor inactiviteit van 10 Hallo overschrijdt en Hallo actor is garbage collector zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="03781-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="03781-156">Een actor kan garbage collector zijn verzameld terwijl deze wordt uitgevoerd een van de bijbehorende methoden, ongeacht hoeveel tijd is besteed aan het uitvoeren van deze methode niet.</span><span class="sxs-lookup"><span data-stu-id="03781-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="03781-157">Zoals eerder gezegd, Hallo uitvoering van actor interfacemethoden en herinnering retouraanroepen voorkomt u dat garbagecollection Hallo actor van niet-actieve tijd too0 opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="03781-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="03781-158">Hallo uitvoering van de timer van retouraanroepen Hallo niet-actieve tijd too0 niet opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="03781-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="03781-159">Hallo-garbagecollection van Hallo actor wordt echter uitgesteld totdat de timer-retouraanroep Hallo uitvoering is voltooid.</span><span class="sxs-lookup"><span data-stu-id="03781-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="03781-160">Actors en hun status verwijderen</span><span class="sxs-lookup"><span data-stu-id="03781-160">Deleting actors and their state</span></span>
<span data-ttu-id="03781-161">Hallo actor object garbagecollection van gedeactiveerde actoren alleen ruimt, maar gegevens die zijn opgeslagen in een actor status Manager wordt niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="03781-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="03781-162">Wanneer een actor opnieuw worden geactiveerd, wordt de gegevens beschikbaar tooit via Hallo status Manager opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="03781-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="03781-163">In gevallen waarbij actoren gegevens opslaan in de status Manager en zijn gedeactiveerd maar nooit opnieuw worden geactiveerd, kan het benodigde tooclean van hun gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="03781-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="03781-164">Hallo [Actor Service](service-fabric-reliable-actors-platform.md) geeft een functie voor het verwijderen van actoren van een externe aanroeper:</span><span class="sxs-lookup"><span data-stu-id="03781-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="03781-165">Verwijderen van een actor is Hallo na effecten, afhankelijk van of Hallo actor momenteel actief is:</span><span class="sxs-lookup"><span data-stu-id="03781-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="03781-166">**Actieve Actor**</span><span class="sxs-lookup"><span data-stu-id="03781-166">**Active Actor**</span></span>
  * <span data-ttu-id="03781-167">Acteur wordt verwijderd uit active actoren lijst en wordt gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="03781-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="03781-168">De status wordt permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="03781-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="03781-169">**Inactieve Actor**</span><span class="sxs-lookup"><span data-stu-id="03781-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="03781-170">De status wordt permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="03781-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="03781-171">Let op: een actor kan niet worden aangeroepen op zichzelf uit een van de bijbehorende methoden actor niet verwijderen omdat Hallo acteur kan niet worden verwijderd tijdens het uitvoeren in een context actor-aanroep, in welke Hallo runtime een vergrendeling rond Hallo actor aanroep tooenforce single thread toegang heeft verkregen.</span><span class="sxs-lookup"><span data-stu-id="03781-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03781-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03781-172">Next steps</span></span>
* [<span data-ttu-id="03781-173">Acteur timers en herinneringen</span><span class="sxs-lookup"><span data-stu-id="03781-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="03781-174">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="03781-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="03781-175">Acteur herintreding</span><span class="sxs-lookup"><span data-stu-id="03781-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="03781-176">Acteur diagnostische gegevens en prestatiebewaking</span><span class="sxs-lookup"><span data-stu-id="03781-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="03781-177">Acteur API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="03781-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="03781-178">C# voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="03781-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="03781-179">Voorbeeldcode voor Java</span><span class="sxs-lookup"><span data-stu-id="03781-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
