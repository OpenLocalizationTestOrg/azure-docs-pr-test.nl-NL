---
title: aaaCreate uw eerste Azure betrouwbare microservice in Java | Microsoft Docs
description: Inleiding toocreating een Microsoft Azure Service Fabric-toepassing met staatloze en stateful services.
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="732b0-103">Aan de slag met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="732b0-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="732b0-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="732b0-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="732b0-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="732b0-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="732b0-106">In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Services en leidt u door het maken en implementeren van een eenvoudige betrouwbare servicetoepassing geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="732b0-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="732b0-107">Deze Microsoft Virtual Academy video ook ziet u hoe toocreate een stateless betrouwbare service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="732b0-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="732b0-108">Installatie en configuratie</span><span class="sxs-lookup"><span data-stu-id="732b0-108">Installation and setup</span></span>
<span data-ttu-id="732b0-109">Voordat u begint, zorg er dan voor dat u hebt Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="732b0-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="732b0-110">Als u tooset moet deze, gaat u te[aan de slag op Mac](service-fabric-get-started-mac.md) of [aan de slag op Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="732b0-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="732b0-111">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="732b0-111">Basic concepts</span></span>
<span data-ttu-id="732b0-112">de slag met Reliable Services, u alleen tooget moet toounderstand enkele basisbeginselen:</span><span class="sxs-lookup"><span data-stu-id="732b0-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="732b0-113">**Servicetype**: dit is uw service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="732b0-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="732b0-114">Dit is gedefinieerd door u schrijft Hallo-klasse die uitgebreider is dan `StatelessService` en andere code of afhankelijkheden gebruikt, samen met een naam en een uniek versienummer.</span><span class="sxs-lookup"><span data-stu-id="732b0-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="732b0-115">**Service-exemplaar met de naam**: toorun uw service u maakt benoemde exemplaren van het servicetype veel zoals u instanties van objecten van het type van een klasse maken.</span><span class="sxs-lookup"><span data-stu-id="732b0-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="732b0-116">Service-exemplaren zijn in feite objectinstanties van uw serviceklasse die u schrijft.</span><span class="sxs-lookup"><span data-stu-id="732b0-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="732b0-117">**ServiceHost**: Hallo service-exemplaren maken van toorun moeten in een host met de naam.</span><span class="sxs-lookup"><span data-stu-id="732b0-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="732b0-118">Hallo ServiceHost is alleen een proces waarbij exemplaren van de service kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="732b0-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="732b0-119">**Service-registratie**: inschrijving brengt alles bij elkaar.</span><span class="sxs-lookup"><span data-stu-id="732b0-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="732b0-120">Hallo servicetype moet zijn geregistreerd met Hallo Service Fabric runtime in een service hosten tooallow Service Fabric toocreate exemplaren van deze toorun.</span><span class="sxs-lookup"><span data-stu-id="732b0-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="732b0-121">Een stateless service maken</span><span class="sxs-lookup"><span data-stu-id="732b0-121">Create a stateless service</span></span>
<span data-ttu-id="732b0-122">Begint met het maken van een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="732b0-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="732b0-123">Hallo Service Fabric SDK voor Linux bevat een Yeoman generator tooprovide Hallo steigers voor een Service Fabric-toepassing met een stateless service.</span><span class="sxs-lookup"><span data-stu-id="732b0-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="732b0-124">Start met Hallo na Yeoman opdracht:</span><span class="sxs-lookup"><span data-stu-id="732b0-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="732b0-125">Ga als volgt Hallo instructies toocreate een **betrouwbare staatloze Service**.</span><span class="sxs-lookup"><span data-stu-id="732b0-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="732b0-126">Voor deze zelfstudie naam Hallo application 'HelloWorldApplication' en Hallo "Hallowereld"-service.</span><span class="sxs-lookup"><span data-stu-id="732b0-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="732b0-127">Hallo resultaat omvat mappen voor Hallo `HelloWorldApplication` en `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="732b0-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="732b0-128">Hallo service implementeren</span><span class="sxs-lookup"><span data-stu-id="732b0-128">Implement hello service</span></span>
<span data-ttu-id="732b0-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="732b0-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="732b0-130">Deze klasse definieert Hallo servicetype en code kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="732b0-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="732b0-131">Hallo service API biedt twee toegangspunten voor uw code:</span><span class="sxs-lookup"><span data-stu-id="732b0-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="732b0-132">Een methode met een vermelding point, aangeroepen `runAsync()`, waar u kunt beginnen alle werkbelastingen, met inbegrip van langlopende compute-workloads uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="732b0-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="732b0-133">Een communicatie-ingangspunt waar u uw communicatiestack van keuze kunt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="732b0-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="732b0-134">Dit is waar u ontvangen van aanvragen van gebruikers en andere services kan starten.</span><span class="sxs-lookup"><span data-stu-id="732b0-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="732b0-135">In deze zelfstudie we richten op Hallo `runAsync()` entry point-methode.</span><span class="sxs-lookup"><span data-stu-id="732b0-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="732b0-136">Dit is waar u kunt onmiddellijk starten uitvoeren van uw code.</span><span class="sxs-lookup"><span data-stu-id="732b0-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="732b0-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="732b0-137">RunAsync</span></span>
<span data-ttu-id="732b0-138">Hallo platform roept deze methode wanneer u een exemplaar van een service wordt geplaatst en zijn ze klaar tooexecute.</span><span class="sxs-lookup"><span data-stu-id="732b0-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="732b0-139">Voor een stateless service betekent dat gewoon wanneer Hallo service-exemplaar wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="732b0-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="732b0-140">Een token annulering wordt toocoordinate opgegeven als uw service-exemplaar toobe gesloten moet.</span><span class="sxs-lookup"><span data-stu-id="732b0-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="732b0-141">Deze cyclus openen en sluiten van een service-exemplaar kan in Service Fabric vaak tijdens Hallo-levensduur van Hallo service optreden als geheel.</span><span class="sxs-lookup"><span data-stu-id="732b0-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="732b0-142">Dit kan gebeuren om verschillende redenen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="732b0-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="732b0-143">Hallo-systeem wordt uw service-exemplaren voor resourceverdeling verplaatst.</span><span class="sxs-lookup"><span data-stu-id="732b0-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="732b0-144">Fouten die voorkomen in uw code.</span><span class="sxs-lookup"><span data-stu-id="732b0-144">Faults occur in your code.</span></span>
* <span data-ttu-id="732b0-145">Hallo toepassings- of upgrade.</span><span class="sxs-lookup"><span data-stu-id="732b0-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="732b0-146">de onderliggende hardware Hallo optreedt een storing.</span><span class="sxs-lookup"><span data-stu-id="732b0-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="732b0-147">Deze indeling wordt beheerd door Service Fabric tookeep uw service maximaal beschikbaar is en goed taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="732b0-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="732b0-148">`runAsync()`moet niet synchroon blokkeren.</span><span class="sxs-lookup"><span data-stu-id="732b0-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="732b0-149">De implementatie van runAsync moet een CompletableFuture tooallow Hallo runtime toocontinue retourneren.</span><span class="sxs-lookup"><span data-stu-id="732b0-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="732b0-150">Als uw werkbelasting een langlopende taak die moet worden uitgevoerd moet binnen tooimplement Hallo CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="732b0-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="732b0-151">Annulering</span><span class="sxs-lookup"><span data-stu-id="732b0-151">Cancellation</span></span>
<span data-ttu-id="732b0-152">Annulering van uw werkbelasting is een gezamenlijke inspanning gedirigeerd door Hallo annulering token opgegeven.</span><span class="sxs-lookup"><span data-stu-id="732b0-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="732b0-153">Hallo-systeem wacht voor uw taak tooend (door met succes is voltooid, geannuleerd of fault) voordat het wordt verplaatst op.</span><span class="sxs-lookup"><span data-stu-id="732b0-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="732b0-154">Het is belangrijk toohonor Hallo annulering token, voltooien een werken en af te sluiten `runAsync()` zo snel mogelijk wanneer Hallo system annulering aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="732b0-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="732b0-155">Hallo volgende voorbeeld laat zien hoe een gebeurtenis annulering toohandle:</span><span class="sxs-lookup"><span data-stu-id="732b0-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="732b0-156">Registratie van service</span><span class="sxs-lookup"><span data-stu-id="732b0-156">Service registration</span></span>
<span data-ttu-id="732b0-157">Servicetypen moeten zijn geregistreerd met Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="732b0-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="732b0-158">Hallo servicetype is gedefinieerd in Hallo `ServiceManifest.xml` en uw serviceklasse die implementeert `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="732b0-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="732b0-159">Registratie van de service wordt uitgevoerd in Hallo proces Hoofdingangspunt is.</span><span class="sxs-lookup"><span data-stu-id="732b0-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="732b0-160">In dit voorbeeld Hallo proces Hoofdingangspunt is `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="732b0-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="732b0-161">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="732b0-161">Run hello application</span></span>

<span data-ttu-id="732b0-162">Hallo Yeoman steigers bevat een gradle script toobuild Hallo toepassings- en bash-scripts toodeploy en verwijder de toepassing.</span><span class="sxs-lookup"><span data-stu-id="732b0-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="732b0-163">toorun hello toepassing eerste build Hallo-toepassing met gradle:</span><span class="sxs-lookup"><span data-stu-id="732b0-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="732b0-164">Dit resulteert in een Service Fabric-toepassingspakket dat kan worden geïmplementeerd met behulp van Service Fabric CLI.</span><span class="sxs-lookup"><span data-stu-id="732b0-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="732b0-165">Met Service Fabric CLI implementeren</span><span class="sxs-lookup"><span data-stu-id="732b0-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="732b0-166">Hallo install.sh script bevat Hallo benodigde Service Fabric CLI-opdrachten toodeploy Hallo toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="732b0-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="732b0-167">Voer de install.sh script toodeploy Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="732b0-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="732b0-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="732b0-168">Next steps</span></span>

* [<span data-ttu-id="732b0-169">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="732b0-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
