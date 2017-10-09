---
title: een Azure Service Fabric betrouwbare actoren Java-toepassing op Linux aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van een toepassing Java Service Fabric betrouwbare actoren in vijf minuten.
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="642f4-103">Uw eerste betrouwbare Service Fabric Java-actortoepassing maken in Linux</span><span class="sxs-lookup"><span data-stu-id="642f4-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="642f4-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="642f4-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="642f4-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="642f4-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="642f4-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="642f4-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="642f4-107">Met deze Quick Start kunt u in een paar minuten uw eerste Azure Service Fabric Java-toepassing maken in een Linux-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="642f4-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="642f4-108">Wanneer u klaar bent, hebt u een eenvoudige Java één service-toepassing uitgevoerd op Hallo lokaal ontwikkelcluster.</span><span class="sxs-lookup"><span data-stu-id="642f4-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="642f4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="642f4-109">Prerequisites</span></span>
<span data-ttu-id="642f4-110">Voordat u begint, Hallo Service Fabric SDK installeren, Service Fabric CLI Hallo en instellen van een cluster ontwikkeling in uw [Linux ontwikkelomgeving](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="642f4-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="642f4-111">Als u Mac OS X gebruikt, kunt u [een Linux-ontwikkelomgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="642f4-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="642f4-112">Wilt u ook tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="642f4-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="642f4-113">Installeren en instellen Hallo genereren voor Java</span><span class="sxs-lookup"><span data-stu-id="642f4-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="642f4-114">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric Java-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="642f4-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="642f4-115">Volg de stappen Hallo hieronder tooensure die u Hallo Service Fabric-generator voor yeoman sjabloon voor Java hebt op uw computer werkt.</span><span class="sxs-lookup"><span data-stu-id="642f4-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="642f4-116">nodejs en NPM installeren op uw computer</span><span class="sxs-lookup"><span data-stu-id="642f4-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="642f4-117">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="642f4-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="642f4-118">Hallo Service Fabric Yeo Java-toepassing generator installeren via NPM</span><span class="sxs-lookup"><span data-stu-id="642f4-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="642f4-119">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="642f4-119">Create hello application</span></span>
<span data-ttu-id="642f4-120">Een Service Fabric-toepassing bevat een of meer services, elk met een specifieke rol in de functionaliteit van de toepassing hello leveren.</span><span class="sxs-lookup"><span data-stu-id="642f4-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="642f4-121">Hallo-generator u geïnstalleerd in de laatste sectie hello, maakt het eenvoudig toocreate uw eerste service en later tooadd.</span><span class="sxs-lookup"><span data-stu-id="642f4-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="642f4-122">U kunt ook Service Fabric-Java-toepassingen maken, ontwikkelen en implementeren met behulp van een invoegtoepassing voor Eclipse.</span><span class="sxs-lookup"><span data-stu-id="642f4-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="642f4-123">Zie [Uw eerste Java-toepassing maken en implementeren met behulp van Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="642f4-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="642f4-124">Gebruik Yeoman toocreate een toepassing met een enkele service die worden opgeslagen en opgehaald van een waarde van het prestatiemeteritem voor deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="642f4-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="642f4-125">Typ in een terminal ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="642f4-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="642f4-126">Geef uw toepassing een naam.</span><span class="sxs-lookup"><span data-stu-id="642f4-126">Name your application.</span></span>
3. <span data-ttu-id="642f4-127">Hallo-type van uw eerste service kiezen en noem deze.</span><span class="sxs-lookup"><span data-stu-id="642f4-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="642f4-128">In deze zelfstudie kiest u voor een Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="642f4-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="642f4-129">Zie voor meer informatie over Hallo andere soorten services, [Service Fabric programming model overzicht](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="642f4-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="642f4-130">![Service Fabric Yeoman-generator voor Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="642f4-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="642f4-131">Hallo-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="642f4-131">Build hello application</span></span>
<span data-ttu-id="642f4-132">Hallo Service Fabric Yeoman sjablonen bevatten een build script voor [Gradle](https://gradle.org/), waardoor u toobuild Hallo toepassing hello terminal kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="642f4-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="642f4-133">Java-afhankelijkheden in Service Fabric worden opgehaald uit Maven.</span><span class="sxs-lookup"><span data-stu-id="642f4-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="642f4-134">toobuild en werk op Hallo Service Fabric-Java-toepassingen, moet u tooensure dat u JDK hebt en Gradle geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="642f4-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="642f4-135">Als nog niet is geïnstalleerd, kunt u Hallo uitvoeren na de tooinstall JDK(openjdk-8-jdk) en Gradle -</span><span class="sxs-lookup"><span data-stu-id="642f4-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="642f4-136">toobuild en pakket Hallo-toepassing hello volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="642f4-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="642f4-137">Hallo-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="642f4-137">Deploy hello application</span></span>
<span data-ttu-id="642f4-138">Als de toepassing hello is gebouwd, kunt u het lokale cluster toohello implementeren.</span><span class="sxs-lookup"><span data-stu-id="642f4-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="642f4-139">Verbinding maken met toohello lokale Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="642f4-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="642f4-140">Voer Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype hello, en maken van een exemplaar van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="642f4-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="642f4-141">Implementatie Hallo gebouwd toepassing is dezelfde als een andere Service Fabric-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="642f4-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="642f4-142">Raadpleeg de documentatie Hallo op [het beheren van een Service Fabric-toepassing Hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="642f4-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="642f4-143">Parameters toothese opdrachten vindt u in de manifesten in programmapakket Hallo Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="642f4-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="642f4-144">Zodra het Hallo-toepassing is geïmplementeerd, open een browser en Ga naar [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) op [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="642f4-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="642f4-145">Vouw vervolgens Hallo **toepassingen** knooppunt en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type opmerking.</span><span class="sxs-lookup"><span data-stu-id="642f4-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="642f4-146">Hallo testclient Start en een failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="642f4-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="642f4-147">Actoren iets op hun eigen niet doet, ze een andere service of client toosend vereisen ze berichten.</span><span class="sxs-lookup"><span data-stu-id="642f4-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="642f4-148">Hallo actor-sjabloon bevat een eenvoudige test-script dat u toointeract met Hallo actor-service gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="642f4-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="642f4-149">Met behulp van Hallo controle hulpprogramma toosee Hallo uitvoer van Hallo actor service Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="642f4-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="642f4-150">Hallo testscript roept Hallo `setCountAsync()` methodeaanroepen op Hallo actor tooincrement een teller Hallo `getCountAsync()` methode op Hallo actor tooget Hallo nieuwe itemwaarde en geeft die waarde toohello-console.</span><span class="sxs-lookup"><span data-stu-id="642f4-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="642f4-151">Zoek in Service Fabric Explorer Hallo knooppunt hosting Hallo primaire replica voor Hallo actor-service.</span><span class="sxs-lookup"><span data-stu-id="642f4-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="642f4-152">In onderstaande Hallo schermafbeelding is het knooppunt 3.</span><span class="sxs-lookup"><span data-stu-id="642f4-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="642f4-153">Hallo primaire service replica ingangen lees- en schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="642f4-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="642f4-154">Wijzigingen in de status van service vervolgens uit toohello secundaire replica's uitgevoerd op knooppunten 0 en 1 in de onderstaande schermafdruk Hallo worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="642f4-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Zoeken naar de primaire replica Hallo in Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="642f4-156">In **knooppunten**, klikt u op Hallo knooppunt u gevonden in de vorige stap Hallo en selecteer vervolgens **uitschakelen (opnieuw opstarten)** van menu Hallo-acties.</span><span class="sxs-lookup"><span data-stu-id="642f4-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="642f4-157">Deze actie Hallo knooppunt uitgevoerd Hallo service primaire replica opnieuw is opgestart en zorgt ervoor dat een failover-tooone van Hallo secundaire replica's uitgevoerd op een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="642f4-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="642f4-158">Die secundaire replica is gepromoveerde tooprimary, een andere secundaire replica is gemaakt op een ander knooppunt en de primaire replica Hallo begint tootake lees-en schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="642f4-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="642f4-159">Omdat hello knooppunt opnieuw wordt opgestart, wordt controle Hallo uitvoer van Hallo client testen en houd er rekening mee dat teller Hallo blijft tooincrement ondanks Hallo failover.</span><span class="sxs-lookup"><span data-stu-id="642f4-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="642f4-160">Hallo-toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="642f4-160">Remove hello application</span></span>
<span data-ttu-id="642f4-161">Hallo uninstall-script is opgegeven in Hallo toodelete Hallo toepassing sjabloonexemplaar gebruiken, hef de registratie van het toepassingspakket Hallo en Hallo toepassingspakket verwijderen uit de installatiekopieopslag Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="642f4-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="642f4-162">In Service Fabric explorer ziet u dat Hallo-toepassing en toepassingstype niet meer in Hallo weergegeven **toepassingen** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="642f4-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="642f4-163">Service Fabric-Java-bibliotheken op Maven</span><span class="sxs-lookup"><span data-stu-id="642f4-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="642f4-164">Service Fabric Java-bibliotheken worden gehost in Maven.</span><span class="sxs-lookup"><span data-stu-id="642f4-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="642f4-165">U kunt op Hallo Hallo afhankelijkheden toevoegen ``pom.xml`` of ``build.gradle`` van uw projecten toouse Service Fabric-Java-bibliotheken van **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="642f4-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="642f4-166">Actoren</span><span class="sxs-lookup"><span data-stu-id="642f4-166">Actors</span></span>

<span data-ttu-id="642f4-167">Ondersteuning voor betrouwbare actoren in Service Fabric voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="642f4-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="642f4-168">Services</span><span class="sxs-lookup"><span data-stu-id="642f4-168">Services</span></span>

<span data-ttu-id="642f4-169">Betrouwbare ondersteuning voor stateless services in Service Fabric voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="642f4-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="642f4-170">Andere</span><span class="sxs-lookup"><span data-stu-id="642f4-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="642f4-171">Transport</span><span class="sxs-lookup"><span data-stu-id="642f4-171">Transport</span></span>

<span data-ttu-id="642f4-172">Ondersteuning van transportlaag voor Service Fabric Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="642f4-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="642f4-173">U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen, toevoegen, tenzij u programmeren op Hallo transportlaag.</span><span class="sxs-lookup"><span data-stu-id="642f4-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="642f4-174">Fabric-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="642f4-174">Fabric support</span></span>

<span data-ttu-id="642f4-175">Niveau ondersteuning voor Service Fabric, die wordt gesproken toonative Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="642f4-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="642f4-176">U hoeft geen tooexplicitly deze afhankelijkheid tooyour betrouwbare Actor of servicetoepassingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="642f4-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="642f4-177">Dit wordt automatisch opgehaald uit de Maven, wanneer u opneemt Hallo andere bovenstaande afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="642f4-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="642f4-178">Oude Service Fabric-Java-toepassingen toobe gebruikt met Maven migreren</span><span class="sxs-lookup"><span data-stu-id="642f4-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="642f4-179">We hebben onlangs Service Fabric-Java-bibliotheken verplaatst vanuit Service Fabric Java SDK tooMaven opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="642f4-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="642f4-180">Tijdens het Hallo nieuwe toepassingen die u met Yeoman of Eclipse genereren genereert de meest recente bijgewerkte projecten (die worden kunnen toowork met Maven), kunt u uw bestaande Service Fabric staatloze of actor Java-toepassingen, wat Hallo Service gebruikten bijwerken Fabric Java SDK eerder toouse Hallo Service Fabric Java afhankelijkheden van Maven.</span><span class="sxs-lookup"><span data-stu-id="642f4-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="642f4-181">Stappen Hallo vermeld [hier](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure de oudere toepassing met Maven werkt.</span><span class="sxs-lookup"><span data-stu-id="642f4-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="642f4-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="642f4-182">Next steps</span></span>

* [<span data-ttu-id="642f4-183">Uw eerste Service Fabric Java-toepassing maken op Linux met Eclipse</span><span class="sxs-lookup"><span data-stu-id="642f4-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="642f4-184">Meer informatie over Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="642f4-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="642f4-185">Interactie met Service Fabric-clusters met Hallo Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="642f4-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="642f4-186">Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="642f4-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="642f4-187">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="642f4-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
