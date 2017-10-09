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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Actor levenscyclus, garbagecollection automatische en handmatige verwijderen
Er is een actor geactiveerd Hallo van de eerste keer wordt een aanroep tooany van de bijbehorende methoden. Een actor is gedeactiveerd (garbage collector zijn verzameld door Hallo actoren runtime) als deze niet wordt gebruikt voor een configureerbare periode. Een actor en de status kunnen ook handmatig worden verwijderd op elk gewenst moment.

## <a name="actor-activation"></a>Actor-activering
Wanneer een actor is geactiveerd, wordt Hallo volgende gebeurt:

* Wanneer een oproep voor een actor binnenkomt en een nog niet actief, wordt een nieuwe actor gemaakt.
* Hallo actorstatus is geladen als deze status wordt onderhouden.
* Hallo `OnActivateAsync` (C#) of `onActivateAsync` (Java)-methode (die kan worden overschreven in Hallo actor-implementatie) wordt aangeroepen.
* Hallo actor is nu beschouwd als actief.

## <a name="actor-deactivation"></a>Deactivering van actor
Wanneer een actor is gedeactiveerd, wordt Hallo volgende gebeurt:

* Wanneer een actor niet voor een bepaalde tijd gebruikt wordt, wordt dit verwijderd uit Hallo Active Actors tabel.
* Hallo `OnDeactivateAsync` (C#) of `onDeactivateAsync` (Java)-methode (die kan worden overschreven in Hallo actor-implementatie) wordt aangeroepen. Hiermee worden alle Hallo timers voor Hallo actor. Actor-bewerkingen zoals status wijzigingen moeten niet worden aangeroepen vanuit deze methode.

> [!TIP]
> Hallo actoren Fabric-runtime verzendt sommige [gebeurtenissen met betrekking tooactor activering en deactivering](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Ze zijn nuttig zijn bij de diagnostische gegevens en prestatiebewaking.
>
>

### <a name="actor-garbage-collection"></a>Garbagecollection actor
Wanneer een actor is gedeactiveerd, references toohello actor-object worden vrijgegeven en wordt deze de garbage collector zijn verzameld normaal door Hallo common language runtime (CLR) of de garbagecollector van de virtuele machine (JVM) java kan worden. Hallo actor object; ruimt garbagecollection alleen Dit gebeurt **niet** in Hallo actor van status Manager opgeslagen status verwijderen. Hallo volgende tijd Hallo actor is geactiveerd, wordt een nieuw actor-object gemaakt en de status wordt teruggezet.

Wat wordt geteld als 'wordt gebruikt' hello doel te deactiveren en garbagecollection?

* Ontvangt een oproep
* `IRemindable.ReceiveReminderAsync`methode wordt aangeroepen (alleen van toepassing als Hallo actor herinneringen gebruikt)

> [!NOTE]
> Als Hallo actor timers gebruikt en de timer-retouraanroep wordt aangeroepen, wordt **niet** aantal als 'wordt gebruikt'.
>
>

Voordat we naar de details op Hallo van deactivering overschakelt, is het belangrijk toodefine Hallo volgende voorwaarden:

* *Controle-interval*. Dit is hello-interval op welke Hallo actoren runtime de tabel Active actoren scant naar actors die kunnen worden gedeactiveerd en garbage collector zijn verzameld. Hallo-standaardwaarde voor deze is 1 minuut.
* *Time-out voor inactiviteit*. Dit is Hallo tijdsduur dat een actor tooremain ongebruikte moet (niet-actief) voordat deze worden gedeactiveerd en garbage collector zijn verzameld. Hallo-standaardwaarde voor deze is 60 minuten.

Normaal gesproken hoeft u niet toochange deze standaardinstellingen. Indien nodig, deze intervallen kunnen echter worden gewijzigd via `ActorServiceSettings` bij het registreren van uw [Actor Service](service-fabric-reliable-actors-platform.md):

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
Voor elke actieve actor Hallo actor runtime houdt van Hallo hoeveelheid tijd die inactief is geweest (d.w.z. niet gebruikt). Hallo actor runtime vergelijkt elke Hallo actoren elke `ScanIntervalInSeconds` toosee als garbage collector zijn verzameld en verzamelt deze als gebruikt gedurende is `IdleTimeoutInSeconds`.

Telkens wanneer een actor wordt gebruikt, is de niet-actieve tijd too0 opnieuw instellen. Hierna mag Hallo actor garbage collector zijn verzameld alleen als het opnieuw inactief blijft voor `IdleTimeoutInSeconds`. Intrekken dat toohave wordt beschouwd als een actor is gebruikt als een interfacemethode actor of een herinnering actor retouraanroep is uitgevoerd. Een actor is **niet** toohave beschouwd als is gebruikt als de timer-retouraanroep is uitgevoerd.

Hallo volgende diagram toont Hallo levenscyclus van een enkele actor tooillustrate deze concepten.

![Voorbeeld van een niet-actieve tijd][1]

Hallo-voorbeeld ziet u Hallo effect actor methodeaanroepen, herinneringen en timers op Hallo levensduur van deze acteur. Hallo punten over Hallo voorbeeld te volgen zijn opgemerkt:

* ScanInterval en IdleTimeout ingesteld too5 en 10 respectievelijk. (Eenheden niet terzake hier, aangezien we alleen tooillustrate Hallo concept.)
* Hallo-scan voor actoren toobe garbage collector zijn verzameld op T = 0, 5, 10, 15, 20, 25, gebeurt zoals gedefinieerd door hello controle-interval van 5.
* Een periodieke timer wordt geactiveerd op T = 4, 8, 12, 16, 20, 24, en de retouraanroep wordt uitgevoerd. Niet-actieve tijd van Hallo actor Hallo geen gevolgen.
* Een methodeaanroep actor op T = 7 Hallo niet-actieve tijd too0 herstelt en Hallo-garbagecollection van Hallo actor uitstelt.
* Een herinnering actor retouraanroep wordt uitgevoerd op T = 14 en verdere vertragingen garbagecollection van Hallo actor Hallo.
* Tijdens Hallo garbagecollection verzameling scan T = 25 Hallo actor van niet-actieve tijd ten slotte time-out voor inactiviteit van 10 Hallo overschrijdt en Hallo actor is garbage collector zijn verzameld.

Een actor kan garbage collector zijn verzameld terwijl deze wordt uitgevoerd een van de bijbehorende methoden, ongeacht hoeveel tijd is besteed aan het uitvoeren van deze methode niet. Zoals eerder gezegd, Hallo uitvoering van actor interfacemethoden en herinnering retouraanroepen voorkomt u dat garbagecollection Hallo actor van niet-actieve tijd too0 opnieuw instellen. Hallo uitvoering van de timer van retouraanroepen Hallo niet-actieve tijd too0 niet opnieuw ingesteld. Hallo-garbagecollection van Hallo actor wordt echter uitgesteld totdat de timer-retouraanroep Hallo uitvoering is voltooid.

## <a name="deleting-actors-and-their-state"></a>Actors en hun status verwijderen
Hallo actor object garbagecollection van gedeactiveerde actoren alleen ruimt, maar gegevens die zijn opgeslagen in een actor status Manager wordt niet verwijderd. Wanneer een actor opnieuw worden geactiveerd, wordt de gegevens beschikbaar tooit via Hallo status Manager opnieuw gemaakt. In gevallen waarbij actoren gegevens opslaan in de status Manager en zijn gedeactiveerd maar nooit opnieuw worden geactiveerd, kan het benodigde tooclean van hun gegevens zijn.

Hallo [Actor Service](service-fabric-reliable-actors-platform.md) geeft een functie voor het verwijderen van actoren van een externe aanroeper:

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

Verwijderen van een actor is Hallo na effecten, afhankelijk van of Hallo actor momenteel actief is:

* **Actieve Actor**
  * Acteur wordt verwijderd uit active actoren lijst en wordt gedeactiveerd.
  * De status wordt permanent verwijderd.
* **Inactieve Actor**
  * De status wordt permanent verwijderd.

Let op: een actor kan niet worden aangeroepen op zichzelf uit een van de bijbehorende methoden actor niet verwijderen omdat Hallo acteur kan niet worden verwijderd tijdens het uitvoeren in een context actor-aanroep, in welke Hallo runtime een vergrendeling rond Hallo actor aanroep tooenforce single thread toegang heeft verkregen.

## <a name="next-steps"></a>Volgende stappen
* [Acteur timers en herinneringen](service-fabric-reliable-actors-timers-reminders.md)
* [Actor-gebeurtenissen](service-fabric-reliable-actors-events.md)
* [Acteur herintreding](service-fabric-reliable-actors-reentrancy.md)
* [Acteur diagnostische gegevens en prestatiebewaking](service-fabric-reliable-actors-diagnostics.md)
* [Acteur API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# voorbeeldcode](https://github.com/Azure/servicefabric-samples)
* [Voorbeeldcode voor Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
