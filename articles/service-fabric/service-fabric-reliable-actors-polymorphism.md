---
title: aaaPolymorphism in Hallo Reliable Actors framework | Microsoft Docs
description: "Maak hiërarchieën van .NET-interfaces en de typen in Hallo Reliable Actors framework tooreuse functionaliteit en de API-definities."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polymorfisme in Hallo Reliable Actors framework
Hallo Reliable Actors framework kunt u toobuild actoren met veel van dezelfde technieken die u in objectgeoriënteerde ontwerp gebruiken wilt Hallo. Een van deze methoden is polymorfisme die kunt typen en tooinherit uit meer interfaces ouders gegeneraliseerd. Overname in Hallo Reliable Actors framework volgt doorgaans Hallo .NET model met een paar extra beperkingen. In geval van een Java-/ Linux volgt Hallo Java-model.

## <a name="interfaces"></a>Interfaces
Hallo Reliable Actors framework, moet u toodefine ten minste één interface toobe geïmplementeerd door uw actortype. Deze interface is gebruikte toogenerate proxyklasse die kan worden gebruikt door clients toocommunicate met uw actoren. Interfaces kunnen overnemen van andere interfaces, zolang elke interface die wordt geïmplementeerd met een actortype en alle bijbehorende bovenliggende klassen uiteindelijk worden afgeleid van IActor(C#) of Actor(Java). IActor(C#) en Actor(Java) zijn respectievelijk Hallo platform gedefinieerde basisinterfaces voor actoren in Hallo frameworks .NET en Java. Dus Hallo klassieke polymorfisme voorbeeld met behulp van vormen mogelijk als volgt uitzien:

![Hiërarchie van de interface voor vorm actors][shapes-interface-hierarchy]

## <a name="types"></a>Typen
U kunt ook een hiërarchie van actor-typen die zijn afgeleid van Hallo Actor basisklasse die is opgegeven door Hallo platform maken. In geval van Hallo vormen, moet u wellicht een base `Shape`(C#) of `ShapeImpl`(Java)-type:

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Subtypes van `Shape`(C#) of `ShapeImpl`(Java) kunt u methoden van Hallo base overschrijven.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Opmerking Hallo `ActorService` -kenmerk op Hallo actor-type. Dit kenmerk instrueert Hallo betrouwbare Actor-framework dat een service voor het hosten van actoren van dit type automatisch moeten worden gemaakt. In sommige gevallen toocreate een basistype op dat uitsluitend bestemd is voor het delen van functionaliteit met subtypen kunt desgewenst en gebruikte tooinstantiate concrete actoren kunnen niet. In deze gevallen moet u Hallo `abstract` sleutelwoord tooindicate dat u nooit een actor op basis van dat type maakt.

## <a name="next-steps"></a>Volgende stappen
* Zie [hoe Hallo Reliable Actors framework maakt gebruik van de Service Fabric-platform Hallo](service-fabric-reliable-actors-platform.md) tooprovide betrouwbaarheid, schaalbaarheid en consistente status.
* Meer informatie over Hallo [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
