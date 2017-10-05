---
title: Maken van uw eerste Azure op basis van actor-microservice in C# | Microsoft Docs
description: Deze zelfstudie leert u de stappen voor het maken en implementeren van een eenvoudige actor-service met behulp van Service Fabric Reliable Actors foutopsporing.
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
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="e0054-103">Aan de slag met Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="e0054-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0054-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="e0054-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="e0054-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="e0054-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="e0054-106">Dit artikel vindt u de basisbeginselen van Azure Service Fabric Reliable Actors en leidt u door het maken en implementeren van een eenvoudige betrouwbare Actor-toepassing in Visual Studio-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="e0054-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="e0054-107">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="e0054-107">Installation and setup</span></span>
<span data-ttu-id="e0054-108">Voordat u begint, zorg ervoor dat u de Service Fabric-ontwikkelomgeving instellen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e0054-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="e0054-109">Als u instellen wilt, raadpleegt u gedetailleerde instructies op [het instellen van de ontwikkelomgeving](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0054-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="e0054-110">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="e0054-110">Basic concepts</span></span>
<span data-ttu-id="e0054-111">Om aan de slag met Reliable Actors, moet u slechts enkele basisbeginselen begrijpen:</span><span class="sxs-lookup"><span data-stu-id="e0054-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="e0054-112">**Acteur service**.</span><span class="sxs-lookup"><span data-stu-id="e0054-112">**Actor service**.</span></span> <span data-ttu-id="e0054-113">Reliable Actors zijn verpakt in Reliable Services die in de Service Fabric-infrastructuur kan worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e0054-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="e0054-114">Actor-exemplaren worden in een benoemd exemplaar geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e0054-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="e0054-115">**Registratie actor**.</span><span class="sxs-lookup"><span data-stu-id="e0054-115">**Actor registration**.</span></span> <span data-ttu-id="e0054-116">Met Reliable Services moet een betrouwbare Actor-service worden geregistreerd met de Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="e0054-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="e0054-117">Bovendien moet het actortype worden geregistreerd met de Actor-runtime.</span><span class="sxs-lookup"><span data-stu-id="e0054-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="e0054-118">**Actor-interface**.</span><span class="sxs-lookup"><span data-stu-id="e0054-118">**Actor interface**.</span></span> <span data-ttu-id="e0054-119">De actor-interface wordt gebruikt voor het definiëren van een sterk getypeerde openbare interface van een acteur.</span><span class="sxs-lookup"><span data-stu-id="e0054-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="e0054-120">In de terminologie betrouwbare Actor-model definieert de actor-interface de soorten berichten die de actor kunt begrijpen en proces.</span><span class="sxs-lookup"><span data-stu-id="e0054-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="e0054-121">De actor-interface wordt gebruikt door andere actors en clienttoepassingen ' ' (asynchroon) om berichten te verzenden naar de actor.</span><span class="sxs-lookup"><span data-stu-id="e0054-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="e0054-122">Reliable Actors kunnen meerdere interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="e0054-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="e0054-123">**Klasse ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="e0054-123">**ActorProxy class**.</span></span> <span data-ttu-id="e0054-124">De klasse ActorProxy wordt gebruikt door clienttoepassingen aanroepen van de methoden die toegankelijk is via de actor-interface.</span><span class="sxs-lookup"><span data-stu-id="e0054-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="e0054-125">De klasse ActorProxy biedt twee belangrijke functies:</span><span class="sxs-lookup"><span data-stu-id="e0054-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="e0054-126">Naamomzetting: kan de actor niet vinden in het cluster (zoeken naar het knooppunt van het cluster waar deze wordt gehost).</span><span class="sxs-lookup"><span data-stu-id="e0054-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="e0054-127">Afhandeling van taakfouten: kan Probeer methode-aanroepen en de locatie actor te zetten na, bijvoorbeeld een storing waarvoor de actor moet worden verplaatst naar een ander knooppunt in het cluster.</span><span class="sxs-lookup"><span data-stu-id="e0054-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="e0054-128">De volgende regels die betrekking op actor-interfaces hebben zijn opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="e0054-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="e0054-129">Kan interfacemethoden acteur kunnen niet overbelast.</span><span class="sxs-lookup"><span data-stu-id="e0054-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="e0054-130">Methoden mogen geen uit actor-interface, ref of optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="e0054-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="e0054-131">Algemene interfaces worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e0054-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="e0054-132">Maak een nieuw project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0054-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="e0054-133">Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuw project voor Service Fabric-toepassing:</span><span class="sxs-lookup"><span data-stu-id="e0054-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Service Fabric-tools voor Visual Studio - nieuw project][1]

<span data-ttu-id="e0054-135">In het volgende dialoogvenster kunt u het type project dat u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="e0054-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Service Fabric-projectsjablonen][5]

<span data-ttu-id="e0054-137">We gebruiken de Reliable Actors van Service Fabric-service voor het project HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="e0054-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="e0054-138">Nadat u de oplossing hebt gemaakt, ziet u de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="e0054-138">After you have created the solution, you should see the following structure:</span></span>

![De structuur van de service Fabric-project][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="e0054-140">Betrouwbare actoren bouwstenen</span><span class="sxs-lookup"><span data-stu-id="e0054-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="e0054-141">Een typische Reliable Actors oplossing bestaat uit drie projecten:</span><span class="sxs-lookup"><span data-stu-id="e0054-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="e0054-142">**Het toepassingsproject (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="e0054-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="e0054-143">Dit is het project uit dat alle services samen voor de implementatie van pakketten.</span><span class="sxs-lookup"><span data-stu-id="e0054-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="e0054-144">Bevat de *ApplicationManifest.xml* en PowerShell-scripts voor het beheren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e0054-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="e0054-145">**De interface-project (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="e0054-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="e0054-146">Dit is het project met de interfacedefinitie van de voor de actor.</span><span class="sxs-lookup"><span data-stu-id="e0054-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="e0054-147">U kunt de interfaces die worden gebruikt door de actoren in de oplossing definiëren in het project MyActor.Interfaces.</span><span class="sxs-lookup"><span data-stu-id="e0054-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="e0054-148">Uw actor-interfaces kunnen worden gedefinieerd in een project met een naam, maar de interface het contract actor die wordt gedeeld door de actor-implementatie en het aanroepen van de actor definieert dus meestal is het verstandig om te definiëren in een assembly die is gescheiden van clients de implementatie van de actor en kunnen worden gedeeld door meerdere andere projecten.</span><span class="sxs-lookup"><span data-stu-id="e0054-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="e0054-149">**Het serviceproject actor (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="e0054-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="e0054-150">Dit is het project dat wordt gebruikt voor het definiëren van de Service Fabric-service die als host voor de actor gaat.</span><span class="sxs-lookup"><span data-stu-id="e0054-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="e0054-151">De uitvoering van de actor bevat.</span><span class="sxs-lookup"><span data-stu-id="e0054-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="e0054-152">Een actor-implementatie is een klasse die is afgeleid van het basistype `Actor` en implementeert de interface (s) die zijn gedefinieerd in het project MyActor.Interfaces.</span><span class="sxs-lookup"><span data-stu-id="e0054-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="e0054-153">Een actor-klasse moet ook een constructor implementeren een `ActorService` exemplaar en een `ActorId` en geeft deze door aan de base `Actor` klasse.</span><span class="sxs-lookup"><span data-stu-id="e0054-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="e0054-154">Hierdoor constructor afhankelijkheidsinjectie van platform afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e0054-154">This allows for constructor dependency injection of platform dependencies.</span></span>

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

<span data-ttu-id="e0054-155">De actor-service moet zijn geregistreerd met een servicetype in de Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="e0054-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="e0054-156">In de volgorde voor de Actor-Service voor uw exemplaren actor uitvoeren, moet uw actortype ook zijn geregistreerd met de Actor-Service.</span><span class="sxs-lookup"><span data-stu-id="e0054-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="e0054-157">De `ActorRuntime` registratiemethode voert dit werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0054-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

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

<span data-ttu-id="e0054-158">Als u vanaf een nieuw project in Visual Studio opstarten en hebt u slechts één definitie van acteur, is de registratie standaard opgenomen in de code die Visual Studio gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="e0054-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="e0054-159">Als u andere actoren in de service definiëren, moet u de registratie actor toevoegen met behulp van:</span><span class="sxs-lookup"><span data-stu-id="e0054-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="e0054-160">De Service Fabric actoren runtime verzendt sommige [gebeurtenissen en prestatiemeteritems met betrekking tot actor methoden](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="e0054-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="e0054-161">Ze zijn nuttig zijn bij de diagnostische gegevens en prestatiebewaking.</span><span class="sxs-lookup"><span data-stu-id="e0054-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="e0054-162">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="e0054-162">Debugging</span></span>
<span data-ttu-id="e0054-163">De Service Fabric-tools voor Visual Studio ondersteuning voor foutopsporing op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="e0054-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="e0054-164">U kunt een sessie voor foutopsporing starten kunt u door op de toets F5.</span><span class="sxs-lookup"><span data-stu-id="e0054-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="e0054-165">Visual Studio maakt (indien nodig) pakketten.</span><span class="sxs-lookup"><span data-stu-id="e0054-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="e0054-166">Ook de toepassing op de lokale Service Fabric-cluster worden geïmplementeerd en wordt het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="e0054-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="e0054-167">Tijdens de implementatie, ziet u de voortgang op het **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="e0054-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Service Fabric foutopsporing uitvoervenster][3]

## <a name="next-steps"></a><span data-ttu-id="e0054-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0054-169">Next steps</span></span>
<span data-ttu-id="e0054-170">Meer informatie over [hoe Reliable Actors gebruiken voor het Service Fabric-platform](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="e0054-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
