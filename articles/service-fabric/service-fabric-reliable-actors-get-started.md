---
title: aaaCreate uw eerste actor gebaseerde Azure microservice in C# | Microsoft Docs
description: Deze zelfstudie leert u Hallo van maken, foutopsporing en een eenvoudige actor gebaseerde service met behulp van Service Fabric Reliable Actors implementeren.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="cf058-103">Aan de slag met Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="cf058-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf058-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="cf058-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="cf058-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="cf058-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="cf058-106">In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Actors en leidt u door het maken en implementeren van een eenvoudige betrouwbare Actor-toepassing in Visual Studio-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="cf058-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="cf058-107">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="cf058-107">Installation and setup</span></span>
<span data-ttu-id="cf058-108">Voordat u begint, zorg ervoor dat u Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cf058-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="cf058-109">Als u tooset moet deze, gedetailleerde instructies zien op [hoe tooset van Hallo ontwikkelomgeving](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cf058-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="cf058-110">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="cf058-110">Basic concepts</span></span>
<span data-ttu-id="cf058-111">de slag met Reliable Actors, u alleen tooget moet toounderstand enkele basisbeginselen:</span><span class="sxs-lookup"><span data-stu-id="cf058-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="cf058-112">**Acteur service**.</span><span class="sxs-lookup"><span data-stu-id="cf058-112">**Actor service**.</span></span> <span data-ttu-id="cf058-113">Reliable Actors zijn verpakt in Reliable Services die kunnen worden geïmplementeerd in Hallo Service Fabric-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="cf058-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="cf058-114">Actor-exemplaren worden in een benoemd exemplaar geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="cf058-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="cf058-115">**Registratie actor**.</span><span class="sxs-lookup"><span data-stu-id="cf058-115">**Actor registration**.</span></span> <span data-ttu-id="cf058-116">Als met Reliable Services een betrouwbare Actor-service moet toobe geregistreerd bij Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="cf058-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="cf058-117">Bovendien moet Hallo actor-type zijn geregistreerd met Hallo Actor runtime toobe.</span><span class="sxs-lookup"><span data-stu-id="cf058-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="cf058-118">**Actor-interface**.</span><span class="sxs-lookup"><span data-stu-id="cf058-118">**Actor interface**.</span></span> <span data-ttu-id="cf058-119">Hallo actor-interface is gebruikte toodefine een sterk getypeerde openbare interface van een acteur.</span><span class="sxs-lookup"><span data-stu-id="cf058-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="cf058-120">In Hallo betrouwbare Actor model terminologie definieert Hallo actor interface Hallo soorten actor Hallo-berichten kunnen begrijpen en verwerken.</span><span class="sxs-lookup"><span data-stu-id="cf058-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="cf058-121">Hallo actor-interface wordt gebruikt door andere actoren en clienttoepassingen te ' ' (asynchroon verzenden) berichten toohello actor.</span><span class="sxs-lookup"><span data-stu-id="cf058-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="cf058-122">Reliable Actors kunnen meerdere interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="cf058-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="cf058-123">**Klasse ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="cf058-123">**ActorProxy class**.</span></span> <span data-ttu-id="cf058-124">Hallo ActorProxy klasse wordt gebruikt door de client toepassingen tooinvoke Hallo methoden beschikbaar via het Hallo actor-interface.</span><span class="sxs-lookup"><span data-stu-id="cf058-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="cf058-125">Hallo ActorProxy klasse biedt twee belangrijke functies:</span><span class="sxs-lookup"><span data-stu-id="cf058-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="cf058-126">Naamomzetting: is kunnen toolocate Hallo actor in Hallo-cluster (Hallo knooppunt zoeken van Hallo cluster waar deze wordt gehost).</span><span class="sxs-lookup"><span data-stu-id="cf058-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="cf058-127">Afhandeling van taakfouten: kan Probeer methode-aanroepen en opnieuw oplossen Hallo actor locatie na, bijvoorbeeld een fout waarvoor Hallo actor toobe tooanother-knooppunt in Hallo cluster verplaatst.</span><span class="sxs-lookup"><span data-stu-id="cf058-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="cf058-128">Hallo volgens de regels die betrekking tooactor interfaces hebben zijn opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="cf058-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="cf058-129">Kan interfacemethoden acteur kunnen niet overbelast.</span><span class="sxs-lookup"><span data-stu-id="cf058-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="cf058-130">Methoden mogen geen uit actor-interface, ref of optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="cf058-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="cf058-131">Algemene interfaces worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf058-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="cf058-132">Maak een nieuw project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf058-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="cf058-133">Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuw project voor Service Fabric-toepassing:</span><span class="sxs-lookup"><span data-stu-id="cf058-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Service Fabric-tools voor Visual Studio - nieuw project][1]

<span data-ttu-id="cf058-135">In het volgende dialoogvenster hello, kunt u Hallo type project dat u wilt dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="cf058-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Service Fabric-projectsjablonen][5]

<span data-ttu-id="cf058-137">Voor Hallo HelloWorld-project, gebruiken we Hallo Reliable Actors van Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="cf058-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="cf058-138">Nadat u Hallo oplossing hebt gemaakt, ziet u Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="cf058-138">After you have created hello solution, you should see hello following structure:</span></span>

![De structuur van de service Fabric-project][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="cf058-140">Betrouwbare actoren bouwstenen</span><span class="sxs-lookup"><span data-stu-id="cf058-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="cf058-141">Een typische Reliable Actors oplossing bestaat uit drie projecten:</span><span class="sxs-lookup"><span data-stu-id="cf058-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="cf058-142">**Hallo-toepassingsproject (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="cf058-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="cf058-143">Dit is Hallo-project dat alle services samen Hallo voor implementatie van pakketten.</span><span class="sxs-lookup"><span data-stu-id="cf058-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="cf058-144">Het Hallo bevat *ApplicationManifest.xml* en PowerShell-scripts voor het beheren van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="cf058-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="cf058-145">**Hallo-interface-project (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="cf058-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="cf058-146">Dit is Hallo-project dat Hallo interfacedefinitie voor Hallo actor bevat.</span><span class="sxs-lookup"><span data-stu-id="cf058-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="cf058-147">In Hallo MyActor.Interfaces-project kunt u Hallo-interfaces die worden gebruikt door Hallo actoren in Hallo oplossing definiëren.</span><span class="sxs-lookup"><span data-stu-id="cf058-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="cf058-148">Uw actor-interfaces kunnen worden gedefinieerd in een project met een naam, maar Hallo interface Hallo actor contract dat wordt gedeeld door Hallo actor-implementatie en Hallo-clients aanroepen Hallo acteur, dus het meestal wel zinvol toodefine is wordt gedefinieerd in een assembly die is afzonderlijke uit Hallo actor-implementatie en kan worden gedeeld door meerdere andere projecten.</span><span class="sxs-lookup"><span data-stu-id="cf058-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="cf058-149">**Hallo actor service-project (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="cf058-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="cf058-150">Dit is Hallo project gebruikt toodefine Hallo Service Fabric-service gaat toohost Hallo actor.</span><span class="sxs-lookup"><span data-stu-id="cf058-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="cf058-151">Het bevat Hallo-implementatie van Hallo actor.</span><span class="sxs-lookup"><span data-stu-id="cf058-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="cf058-152">Een actor-implementatie is een klasse die is afgeleid van het basistype Hallo `Actor` en implementeert interface (s) die zijn gedefinieerd in Hallo MyActor.Interfaces project Hallo.</span><span class="sxs-lookup"><span data-stu-id="cf058-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="cf058-153">Een actor-klasse moet ook een constructor implementeren een `ActorService` exemplaar en een `ActorId` en geeft deze door toohello base `Actor` klasse.</span><span class="sxs-lookup"><span data-stu-id="cf058-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="cf058-154">Hierdoor constructor afhankelijkheidsinjectie van platform afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="cf058-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="cf058-155">Hallo actor-service moet zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="cf058-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="cf058-156">In volgorde voor Hallo Actor Service toorun uw actor-exemplaren, uw actortype moet ook zijn geregistreerd bij Hallo Actor-Service.</span><span class="sxs-lookup"><span data-stu-id="cf058-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="cf058-157">Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf058-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

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

<span data-ttu-id="cf058-158">Als u vanaf een nieuw project in Visual Studio opstarten en hebt u slechts één definitie van actor, is Hallo-registratie standaard opgenomen in Hallo-code die Visual Studio gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="cf058-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="cf058-159">Als u andere actoren in Hallo service definieert, moet u tooadd Hallo actor registratie met behulp van:</span><span class="sxs-lookup"><span data-stu-id="cf058-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="cf058-160">Hallo actoren van Service Fabric-runtime verzendt sommige [gebeurtenissen en prestatiemeteritems gerelateerde tooactor methoden](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="cf058-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="cf058-161">Ze zijn nuttig zijn bij de diagnostische gegevens en prestatiebewaking.</span><span class="sxs-lookup"><span data-stu-id="cf058-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="cf058-162">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="cf058-162">Debugging</span></span>
<span data-ttu-id="cf058-163">Hallo Service Fabric-tools voor Visual Studio ondersteuning voor foutopsporing op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="cf058-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="cf058-164">U kunt een sessie voor foutopsporing starten door roept Hallo F5-toets.</span><span class="sxs-lookup"><span data-stu-id="cf058-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="cf058-165">Visual Studio maakt (indien nodig) pakketten.</span><span class="sxs-lookup"><span data-stu-id="cf058-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="cf058-166">Ook implementeert de toepassing hello op Hallo lokale Service Fabric-cluster en Hallo foutopsporingsprogramma koppelt.</span><span class="sxs-lookup"><span data-stu-id="cf058-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="cf058-167">Tijdens het implementatieproces Hallo ziet u Hallo voortgang in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="cf058-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Service Fabric foutopsporing uitvoervenster][3]

## <a name="next-steps"></a><span data-ttu-id="cf058-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf058-169">Next steps</span></span>
<span data-ttu-id="cf058-170">Meer informatie over [hoe Reliable Actors Hallo Service Fabric-platform gebruiken](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="cf058-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
