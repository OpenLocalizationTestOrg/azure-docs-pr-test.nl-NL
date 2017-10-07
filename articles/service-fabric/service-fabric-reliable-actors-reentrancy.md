---
title: aaaReentrancy in Azure microservices actor gebaseerde | Microsoft Docs
description: Inleiding tooreentrancy voor Service Fabric Reliable Actors
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Betrouwbare actoren herintreding
Hallo Reliable Actors runtime, kunt standaard, u logische aanroep context gebaseerde herintreding. Hiermee kunt u actoren toobe reentrant als ze in Hallo dezelfde context keten aanroep. Bijvoorbeeld verzendt Actor A een bericht tooActor B, die een bericht tooActor C. verzendt Als onderdeel van de berichtverwerking Hallo als Actor C Actor A, roept is het Hallo-bericht inspringende, dus wordt toegestaan. Alle berichten die deel van de aanroepcontext van een andere uitmaken wordt geblokkeerd op Actor A totdat het verwerken is voltooid.

Er zijn twee opties beschikbaar voor actor herintreding gedefinieerd in Hallo `ActorReentrancyMode` enum:

* `LogicalCallContext`(standaardinstelling)
* `Disallowed`-herintreding uitgeschakeld

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
Herintreding kan worden geconfigureerd in een `ActorService`van instellingen tijdens de registratie. Hallo-instelling is van toepassing tooall actor-exemplaren in Hallo actor service gemaakt.

Hallo volgende voorbeeld ziet u een actor-service die Hallo herintreding modus te ingesteld`ActorReentrancyMode.Disallowed`. In dit geval, als een actor verzendt een uitzondering van het type van een inspringende bericht tooanother actor `FabricException` gegenereerd.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over herintreding in Hallo [Actor-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn971626.aspx)
