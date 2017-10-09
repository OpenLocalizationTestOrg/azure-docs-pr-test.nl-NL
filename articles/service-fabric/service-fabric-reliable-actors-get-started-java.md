---
title: aaaCreate uw eerste actor gebaseerde Azure microservice in Java | Microsoft Docs
description: Deze zelfstudie leert u Hallo van maken, foutopsporing en een eenvoudige actor gebaseerde service met behulp van Service Fabric Reliable Actors implementeren.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="6b0bd-103">Aan de slag met Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6b0bd-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b0bd-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="6b0bd-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="6b0bd-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="6b0bd-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="6b0bd-106">In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Actors en leidt u door het maken en implementeren van een eenvoudige toepassing betrouwbare Actor in Java.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="6b0bd-107">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="6b0bd-107">Installation and setup</span></span>
<span data-ttu-id="6b0bd-108">Voordat u begint, zorg er dan voor dat u hebt Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6b0bd-109">Als u tooset moet deze, gaat u te[aan de slag op Mac](service-fabric-get-started-mac.md) of [aan de slag op Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6b0bd-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6b0bd-110">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="6b0bd-110">Basic concepts</span></span>
<span data-ttu-id="6b0bd-111">de slag met Reliable Actors, u alleen tooget moet toounderstand enkele basisbeginselen:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="6b0bd-112">**Acteur service**.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-112">**Actor service**.</span></span> <span data-ttu-id="6b0bd-113">Reliable Actors zijn verpakt in Reliable Services die kunnen worden geïmplementeerd in Hallo Service Fabric-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="6b0bd-114">Actor-exemplaren worden in een benoemd exemplaar geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="6b0bd-115">**Registratie actor**.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-115">**Actor registration**.</span></span> <span data-ttu-id="6b0bd-116">Als met Reliable Services een betrouwbare Actor-service moet toobe geregistreerd bij Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="6b0bd-117">Bovendien moet Hallo actor-type zijn geregistreerd met Hallo Actor runtime toobe.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="6b0bd-118">**Actor-interface**.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-118">**Actor interface**.</span></span> <span data-ttu-id="6b0bd-119">Hallo actor-interface is gebruikte toodefine een sterk getypeerde openbare interface van een acteur.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="6b0bd-120">In Hallo betrouwbare Actor model terminologie definieert Hallo actor interface Hallo soorten actor Hallo-berichten kunnen begrijpen en verwerken.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="6b0bd-121">Hallo actor-interface wordt gebruikt door andere actoren en clienttoepassingen te ' ' (asynchroon verzenden) berichten toohello actor.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="6b0bd-122">Reliable Actors kunnen meerdere interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="6b0bd-123">**Klasse ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-123">**ActorProxy class**.</span></span> <span data-ttu-id="6b0bd-124">Hallo ActorProxy klasse wordt gebruikt door de client toepassingen tooinvoke Hallo methoden beschikbaar via het Hallo actor-interface.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="6b0bd-125">Hallo ActorProxy klasse biedt twee belangrijke functies:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="6b0bd-126">Naamomzetting: is kunnen toolocate Hallo actor in Hallo-cluster (Hallo knooppunt zoeken van Hallo cluster waar deze wordt gehost).</span><span class="sxs-lookup"><span data-stu-id="6b0bd-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="6b0bd-127">Afhandeling van taakfouten: kan Probeer methode-aanroepen en opnieuw oplossen Hallo actor locatie na, bijvoorbeeld een fout waarvoor Hallo actor toobe tooanother-knooppunt in Hallo cluster verplaatst.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="6b0bd-128">Hallo volgens de regels die betrekking tooactor interfaces hebben zijn opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="6b0bd-129">Kan interfacemethoden acteur kunnen niet overbelast.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="6b0bd-130">Methoden mogen geen uit actor-interface, ref of optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="6b0bd-131">Algemene interfaces worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="6b0bd-132">Maak een actor-service</span><span class="sxs-lookup"><span data-stu-id="6b0bd-132">Create an actor service</span></span>
<span data-ttu-id="6b0bd-133">Begint met het maken van een nieuwe Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="6b0bd-134">Hallo Service Fabric SDK voor Linux bevat een Yeoman generator tooprovide Hallo steigers voor een Service Fabric-toepassing met een stateless service.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="6b0bd-135">Start met Hallo na Yeoman opdracht:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="6b0bd-136">Ga als volgt Hallo instructies toocreate een **betrouwbare Actor Service**.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="6b0bd-137">Naam voor deze zelfstudie Hallo application 'HelloWorldActorApplication' en Hallo actor 'HelloWorldActor'.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="6b0bd-138">Hallo steigers na worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="6b0bd-139">Betrouwbare actoren bouwstenen</span><span class="sxs-lookup"><span data-stu-id="6b0bd-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="6b0bd-140">Hallo basisconcepten eerder beschreven vertalen naar bouwstenen Hallo van een betrouwbare Actor-service.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="6b0bd-141">Actor-interface</span><span class="sxs-lookup"><span data-stu-id="6b0bd-141">Actor interface</span></span>
<span data-ttu-id="6b0bd-142">Dit document bevat Hallo interfacedefinitie voor Hallo actor.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="6b0bd-143">Deze interface definieert Hallo actor contract dat wordt gedeeld door Hallo actor-implementatie en het aanroepen van Hallo acteur, dus is het meestal wel zinvol toodefine deze op een locatie die is gescheiden van Hallo actor-implementatie en kan worden gedeeld door meerdere andere Hallo-clients client-toepassingen of services.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="6b0bd-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="6b0bd-145">Actor-service</span><span class="sxs-lookup"><span data-stu-id="6b0bd-145">Actor service</span></span>
<span data-ttu-id="6b0bd-146">Dit document bevat uw actor-implementatie en actor registratiecode.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="6b0bd-147">Hallo actor-klasse Hallo actor-interface implementeert.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="6b0bd-148">Dit is waar uw actor zijn werk doet.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-148">This is where your actor does its work.</span></span>

<span data-ttu-id="6b0bd-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="6b0bd-150">Actor-registratie</span><span class="sxs-lookup"><span data-stu-id="6b0bd-150">Actor registration</span></span>
<span data-ttu-id="6b0bd-151">Hallo actor-service moet zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="6b0bd-152">In volgorde voor Hallo Actor Service toorun uw actor-exemplaren, uw actortype moet ook zijn geregistreerd bij Hallo Actor-Service.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="6b0bd-153">Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="6b0bd-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="6b0bd-155">Testclient</span><span class="sxs-lookup"><span data-stu-id="6b0bd-155">Test client</span></span>
<span data-ttu-id="6b0bd-156">Dit is een eenvoudige test clienttoepassing kunt u afzonderlijk uitvoeren van Hallo Service Fabric-toepassing tootest uw actor-service.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="6b0bd-157">Dit is een voorbeeld van waar Hallo ActorProxy worden gebruikte tooactivate en communiceren met actor-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="6b0bd-158">Deze wordt geïmplementeerd met uw service.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="6b0bd-159">Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="6b0bd-159">hello application</span></span>
<span data-ttu-id="6b0bd-160">Ten slotte Hallo Hallo toepassingspakketten actor-service en andere services die u wilt in Hallo toekomstige samen voor implementatie toevoegen mogelijk.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="6b0bd-161">Het Hallo bevat *ApplicationManifest.xml* en plaats houders voor Hallo actor servicepakket.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="6b0bd-162">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6b0bd-162">Run hello application</span></span>

<span data-ttu-id="6b0bd-163">Hallo Yeoman steigers bevat een gradle script toobuild Hallo toepassings- en bash-scripts toodeploy en verwijder de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="6b0bd-164">toodeploy hello toepassing eerste build Hallo-toepassing met gradle:</span><span class="sxs-lookup"><span data-stu-id="6b0bd-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="6b0bd-165">Het resultaat is een Service Fabric-toepassingspakket dat kan worden geïmplementeerd met behulp van Service Fabric CLI-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="6b0bd-166">Service Fabric CLI implementeren</span><span class="sxs-lookup"><span data-stu-id="6b0bd-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="6b0bd-167">Hallo install.sh script bevat Hallo benodigde Service Fabric CLI (sfctl) opdrachten toodeploy Hallo toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="6b0bd-168">Hallo install.sh script toodeploy Hallo toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6b0bd-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="6b0bd-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b0bd-169">Next steps</span></span>

* [<span data-ttu-id="6b0bd-170">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="6b0bd-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
