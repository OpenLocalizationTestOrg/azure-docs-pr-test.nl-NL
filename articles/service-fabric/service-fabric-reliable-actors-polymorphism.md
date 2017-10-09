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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="0fb67-103">Polymorfisme in Hallo Reliable Actors framework</span><span class="sxs-lookup"><span data-stu-id="0fb67-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="0fb67-104">Hallo Reliable Actors framework kunt u toobuild actoren met veel van dezelfde technieken die u in objectgeoriënteerde ontwerp gebruiken wilt Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fb67-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="0fb67-105">Een van deze methoden is polymorfisme die kunt typen en tooinherit uit meer interfaces ouders gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="0fb67-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="0fb67-106">Overname in Hallo Reliable Actors framework volgt doorgaans Hallo .NET model met een paar extra beperkingen.</span><span class="sxs-lookup"><span data-stu-id="0fb67-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="0fb67-107">In geval van een Java-/ Linux volgt Hallo Java-model.</span><span class="sxs-lookup"><span data-stu-id="0fb67-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="0fb67-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="0fb67-108">Interfaces</span></span>
<span data-ttu-id="0fb67-109">Hallo Reliable Actors framework, moet u toodefine ten minste één interface toobe geïmplementeerd door uw actortype.</span><span class="sxs-lookup"><span data-stu-id="0fb67-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="0fb67-110">Deze interface is gebruikte toogenerate proxyklasse die kan worden gebruikt door clients toocommunicate met uw actoren.</span><span class="sxs-lookup"><span data-stu-id="0fb67-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="0fb67-111">Interfaces kunnen overnemen van andere interfaces, zolang elke interface die wordt geïmplementeerd met een actortype en alle bijbehorende bovenliggende klassen uiteindelijk worden afgeleid van IActor(C#) of Actor(Java).</span><span class="sxs-lookup"><span data-stu-id="0fb67-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="0fb67-112">IActor(C#) en Actor(Java) zijn respectievelijk Hallo platform gedefinieerde basisinterfaces voor actoren in Hallo frameworks .NET en Java.</span><span class="sxs-lookup"><span data-stu-id="0fb67-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="0fb67-113">Dus Hallo klassieke polymorfisme voorbeeld met behulp van vormen mogelijk als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="0fb67-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Hiërarchie van de interface voor vorm actors][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="0fb67-115">Typen</span><span class="sxs-lookup"><span data-stu-id="0fb67-115">Types</span></span>
<span data-ttu-id="0fb67-116">U kunt ook een hiërarchie van actor-typen die zijn afgeleid van Hallo Actor basisklasse die is opgegeven door Hallo platform maken.</span><span class="sxs-lookup"><span data-stu-id="0fb67-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="0fb67-117">In geval van Hallo vormen, moet u wellicht een base `Shape`(C#) of `ShapeImpl`(Java)-type:</span><span class="sxs-lookup"><span data-stu-id="0fb67-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="0fb67-118">Subtypes van `Shape`(C#) of `ShapeImpl`(Java) kunt u methoden van Hallo base overschrijven.</span><span class="sxs-lookup"><span data-stu-id="0fb67-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="0fb67-119">Opmerking Hallo `ActorService` -kenmerk op Hallo actor-type.</span><span class="sxs-lookup"><span data-stu-id="0fb67-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="0fb67-120">Dit kenmerk instrueert Hallo betrouwbare Actor-framework dat een service voor het hosten van actoren van dit type automatisch moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0fb67-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="0fb67-121">In sommige gevallen toocreate een basistype op dat uitsluitend bestemd is voor het delen van functionaliteit met subtypen kunt desgewenst en gebruikte tooinstantiate concrete actoren kunnen niet.</span><span class="sxs-lookup"><span data-stu-id="0fb67-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="0fb67-122">In deze gevallen moet u Hallo `abstract` sleutelwoord tooindicate dat u nooit een actor op basis van dat type maakt.</span><span class="sxs-lookup"><span data-stu-id="0fb67-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb67-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fb67-123">Next steps</span></span>
* <span data-ttu-id="0fb67-124">Zie [hoe Hallo Reliable Actors framework maakt gebruik van de Service Fabric-platform Hallo](service-fabric-reliable-actors-platform.md) tooprovide betrouwbaarheid, schaalbaarheid en consistente status.</span><span class="sxs-lookup"><span data-stu-id="0fb67-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="0fb67-125">Meer informatie over Hallo [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0fb67-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
