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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="86b92-103">Betrouwbare actoren herintreding</span><span class="sxs-lookup"><span data-stu-id="86b92-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="86b92-104">Hallo Reliable Actors runtime, kunt standaard, u logische aanroep context gebaseerde herintreding.</span><span class="sxs-lookup"><span data-stu-id="86b92-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="86b92-105">Hiermee kunt u actoren toobe reentrant als ze in Hallo dezelfde context keten aanroep.</span><span class="sxs-lookup"><span data-stu-id="86b92-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="86b92-106">Bijvoorbeeld verzendt Actor A een bericht tooActor B, die een bericht tooActor C. verzendt Als onderdeel van de berichtverwerking Hallo als Actor C Actor A, roept is het Hallo-bericht inspringende, dus wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="86b92-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="86b92-107">Alle berichten die deel van de aanroepcontext van een andere uitmaken wordt geblokkeerd op Actor A totdat het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="86b92-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="86b92-108">Er zijn twee opties beschikbaar voor actor herintreding gedefinieerd in Hallo `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="86b92-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="86b92-109">`LogicalCallContext`(standaardinstelling)</span><span class="sxs-lookup"><span data-stu-id="86b92-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="86b92-110">`Disallowed`-herintreding uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="86b92-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="86b92-111">Herintreding kan worden geconfigureerd in een `ActorService`van instellingen tijdens de registratie.</span><span class="sxs-lookup"><span data-stu-id="86b92-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="86b92-112">Hallo-instelling is van toepassing tooall actor-exemplaren in Hallo actor service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="86b92-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="86b92-113">Hallo volgende voorbeeld ziet u een actor-service die Hallo herintreding modus te ingesteld`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="86b92-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="86b92-114">In dit geval, als een actor verzendt een uitzondering van het type van een inspringende bericht tooanother actor `FabricException` gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="86b92-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="86b92-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86b92-115">Next steps</span></span>
* <span data-ttu-id="86b92-116">Meer informatie over herintreding in Hallo [Actor-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="86b92-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
