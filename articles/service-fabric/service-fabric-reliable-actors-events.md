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
# <a name="actor-events"></a>Actor-gebeurtenissen
Acteur gebeurtenissen bieden een manier toosend best-effort meldingen van Hallo actor toohello clients. Acteur gebeurtenissen zijn ontworpen voor communicatie actor-naar-client en mag niet worden gebruikt voor actor-actor-communicatie.

Hallo volgende code codefragmenten tonen hoe toouse actor gebeurtenissen in uw toepassing.

Definieer een interface die worden gepubliceerd door Hallo actor Hallo-gebeurtenissen beschreven. Deze interface moet worden afgeleid van Hallo `IActorEvents` interface. Hallo-argumenten van Hallo-methoden moeten [gegevenscontract serialiseerbaar](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). Hallo methoden moeten als retourtype void, als gebeurtenis meldingen zijn een manier en zo goed mogelijke poging.

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
Hallo-gebeurtenissen die zijn gepubliceerd door Hallo actor in Hallo actor-interface declareren.

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
Aan de clientzijde hello, Hallo gebeurtenis-handler te implementeren.

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

Maken van een proxy toohello actor die Hallo gebeurtenis publiceert op Hallo van client, en abonneren tooits gebeurtenissen.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

In geval van failovers Hallo Hallo actor mogelijk een failover tooa ander proces of het knooppunt. Hallo actor proxy beheert Hallo actieve abonnementen en automatisch opnieuw op is geabonneerd ze. U kunt bepalen hello-interval voor nieuwe abonnement via Hallo `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, gebruik Hallo `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

Op het Hallo-actor gewoon Hallo gebeurtenissen publiceren meteen. Als er abonnees toohello gebeurtenis zijn, Hallo actoren runtime worden ze Hallo melding verzenden.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Volgende stappen
* [Acteur herintreding](service-fabric-reliable-actors-reentrancy.md)
* [Acteur diagnostische gegevens en prestatiebewaking](service-fabric-reliable-actors-diagnostics.md)
* [Acteur API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# voorbeeldcode](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [C# .NET Core voorbeeldcode](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Voorbeeldcode voor Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
