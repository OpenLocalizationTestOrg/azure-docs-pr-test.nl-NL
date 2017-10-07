---
title: aaaEvents in Azure microservices actor gebaseerde | Microsoft Docs
description: Inleiding tooevents voor Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="11e25-103">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="11e25-103">Actor events</span></span>
<span data-ttu-id="11e25-104">Acteur gebeurtenissen bieden een manier toosend best-effort meldingen van Hallo actor toohello clients.</span><span class="sxs-lookup"><span data-stu-id="11e25-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="11e25-105">Acteur gebeurtenissen zijn ontworpen voor communicatie actor-naar-client en mag niet worden gebruikt voor actor-actor-communicatie.</span><span class="sxs-lookup"><span data-stu-id="11e25-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="11e25-106">Hallo volgende code codefragmenten tonen hoe toouse actor gebeurtenissen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="11e25-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="11e25-107">Definieer een interface die worden gepubliceerd door Hallo actor Hallo-gebeurtenissen beschreven.</span><span class="sxs-lookup"><span data-stu-id="11e25-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="11e25-108">Deze interface moet worden afgeleid van Hallo `IActorEvents` interface.</span><span class="sxs-lookup"><span data-stu-id="11e25-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="11e25-109">Hallo-argumenten van Hallo-methoden moeten [gegevenscontract serialiseerbaar](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="11e25-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="11e25-110">Hallo methoden moeten als retourtype void, als gebeurtenis meldingen zijn een manier en zo goed mogelijke poging.</span><span class="sxs-lookup"><span data-stu-id="11e25-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="11e25-111">Hallo-gebeurtenissen die zijn gepubliceerd door Hallo actor in Hallo actor-interface declareren.</span><span class="sxs-lookup"><span data-stu-id="11e25-111">Declare hello events published by hello actor in hello actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="11e25-112">Aan de clientzijde hello, Hallo gebeurtenis-handler te implementeren.</span><span class="sxs-lookup"><span data-stu-id="11e25-112">On hello client side, implement hello event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="11e25-113">Maken van een proxy toohello actor die Hallo gebeurtenis publiceert op Hallo van client, en abonneren tooits gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="11e25-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="11e25-114">In geval van failovers Hallo Hallo actor mogelijk een failover tooa ander proces of het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="11e25-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="11e25-115">Hallo actor proxy beheert Hallo actieve abonnementen en automatisch opnieuw op is geabonneerd ze.</span><span class="sxs-lookup"><span data-stu-id="11e25-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="11e25-116">U kunt bepalen hello-interval voor nieuwe abonnement via Hallo `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="11e25-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="11e25-117">toounsubscribe, gebruik Hallo `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="11e25-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="11e25-118">Op het Hallo-actor gewoon Hallo gebeurtenissen publiceren meteen.</span><span class="sxs-lookup"><span data-stu-id="11e25-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="11e25-119">Als er abonnees toohello gebeurtenis zijn, Hallo actoren runtime worden ze Hallo melding verzenden.</span><span class="sxs-lookup"><span data-stu-id="11e25-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="11e25-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11e25-120">Next steps</span></span>
* [<span data-ttu-id="11e25-121">Acteur herintreding</span><span class="sxs-lookup"><span data-stu-id="11e25-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="11e25-122">Acteur diagnostische gegevens en prestatiebewaking</span><span class="sxs-lookup"><span data-stu-id="11e25-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="11e25-123">Acteur API-naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="11e25-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="11e25-124">C# voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="11e25-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="11e25-125">C# .NET Core voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="11e25-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="11e25-126">Voorbeeldcode voor Java</span><span class="sxs-lookup"><span data-stu-id="11e25-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
