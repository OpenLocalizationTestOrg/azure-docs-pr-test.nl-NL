---
title: aaaCreate uw eerste app in Azure microservices op Linux met C# | Microsoft Docs
description: Een Service Fabric-toepassing maken en implementeren met behulp van C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="5deb0-103">Uw eerste Azure Service Fabric-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5deb0-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5deb0-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="5deb0-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="5deb0-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="5deb0-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="5deb0-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="5deb0-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="5deb0-107">Service Fabric biedt SDK's voor het bouwen van services in Linux in zowel .NET Core als Java.</span><span class="sxs-lookup"><span data-stu-id="5deb0-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="5deb0-108">In deze zelfstudie kijken we hoe toocreate een toepassing voor Linux en build een service met C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="5deb0-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5deb0-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5deb0-109">Prerequisites</span></span>
<span data-ttu-id="5deb0-110">Zorg voordat u begint ervoor dat u [uw Linux-ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5deb0-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="5deb0-111">Als u Mac OS X gebruikt, kunt u [een Linux one-box omgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="5deb0-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="5deb0-112">Wilt u ook tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5deb0-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="5deb0-113">Installeren en Hallo genereren voor CSharp instellen</span><span class="sxs-lookup"><span data-stu-id="5deb0-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="5deb0-114">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric CSharp-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="5deb0-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="5deb0-115">Volg de stappen Hallo hieronder tooensure er Hallo Service Fabric yeoman sjabloon generator voor CSharp werkt op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5deb0-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="5deb0-116">nodejs en NPM installeren op uw computer</span><span class="sxs-lookup"><span data-stu-id="5deb0-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="5deb0-117">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="5deb0-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="5deb0-118">Hallo Service Fabric Yeo Java-toepassing generator installeren via NPM</span><span class="sxs-lookup"><span data-stu-id="5deb0-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="5deb0-119">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5deb0-119">Create hello application</span></span>
<span data-ttu-id="5deb0-120">Een Service Fabric-toepassing kan een of meer services, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing hello bevatten.</span><span class="sxs-lookup"><span data-stu-id="5deb0-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="5deb0-121">Hallo Service Fabric [Yeoman](http://yeoman.io/) generator voor CSharp die u in de laatste stap hebt geïnstalleerd, maakt het eenvoudig toocreate uw eerste service en later tooadd.</span><span class="sxs-lookup"><span data-stu-id="5deb0-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="5deb0-122">Laten we Yeoman toocreate een toepassing met een enkele service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5deb0-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="5deb0-123">Typ in een terminal Hallo opdracht toostart bouwen Hallo steigers te volgen:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="5deb0-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="5deb0-124">Geef uw toepassing een naam.</span><span class="sxs-lookup"><span data-stu-id="5deb0-124">Name your application.</span></span>
3. <span data-ttu-id="5deb0-125">Hallo-type van uw eerste service kiezen en noem deze.</span><span class="sxs-lookup"><span data-stu-id="5deb0-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="5deb0-126">Voor Hallo doel van deze zelfstudie kiest u een betrouwbare Actor-Service.</span><span class="sxs-lookup"><span data-stu-id="5deb0-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Service Fabric Yeoman-generator voor C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="5deb0-128">Zie voor meer informatie over opties voor Hallo [Service Fabric programming model overzicht](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="5deb0-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="5deb0-129">Hallo-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="5deb0-129">Build hello application</span></span>
<span data-ttu-id="5deb0-130">Hallo Service Fabric Yeoman sjablonen bevatten een build-script dat u toobuild Hallo-app uit Hallo terminal gebruiken kunt (na de toepassingsmap toohello navigeren).</span><span class="sxs-lookup"><span data-stu-id="5deb0-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="5deb0-131">Hallo-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="5deb0-131">Deploy hello application</span></span>

<span data-ttu-id="5deb0-132">Als de toepassing hello is gebouwd, kunt u het lokale cluster toohello implementeren.</span><span class="sxs-lookup"><span data-stu-id="5deb0-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="5deb0-133">Verbinding maken met toohello lokale Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="5deb0-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="5deb0-134">Voer Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype hello, en maken van een exemplaar van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="5deb0-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="5deb0-135">Implementatie Hallo gebouwd toepassing is dezelfde als een andere Service Fabric-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="5deb0-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="5deb0-136">Raadpleeg de documentatie Hallo op [het beheren van een Service Fabric-toepassing Hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="5deb0-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="5deb0-137">Parameters toothese opdrachten vindt u in de manifesten in programmapakket Hallo Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5deb0-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="5deb0-138">Zodra het Hallo-toepassing is geïmplementeerd, open een browser en Ga naar [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) op [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="5deb0-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="5deb0-139">Vouw vervolgens Hallo **toepassingen** knooppunt en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type opmerking.</span><span class="sxs-lookup"><span data-stu-id="5deb0-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="5deb0-140">Hallo testclient Start en een failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5deb0-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="5deb0-141">Actorprojecten doen niets uit zichzelf.</span><span class="sxs-lookup"><span data-stu-id="5deb0-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="5deb0-142">Vereist een andere service of client toosend ze berichten.</span><span class="sxs-lookup"><span data-stu-id="5deb0-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="5deb0-143">Hallo actor-sjabloon bevat een eenvoudige test-script dat u toointeract met Hallo actor-service gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="5deb0-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="5deb0-144">Met behulp van Hallo controle hulpprogramma toosee Hallo uitvoer van Hallo actor service Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5deb0-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="5deb0-145">Zoek knooppunt Hallo primaire replica voor Hallo actor service gehost in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="5deb0-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="5deb0-146">In onderstaande Hallo schermafbeelding is het knooppunt 3.</span><span class="sxs-lookup"><span data-stu-id="5deb0-146">In hello screenshot below, it is node 3.</span></span>

    ![Zoeken naar de primaire replica Hallo in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="5deb0-148">Klik op Hallo knooppunt u gevonden in de vorige stap Hallo en selecteer vervolgens **uitschakelen (opnieuw opstarten)** van menu Hallo-acties.</span><span class="sxs-lookup"><span data-stu-id="5deb0-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="5deb0-149">Deze actie wordt één knooppunt in het lokale cluster een failover-tooa secundaire replica uitgevoerd op een ander knooppunt geforceerd opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="5deb0-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="5deb0-150">Als u deze actie uitvoert, betaalt u aandacht toohello uitvoer van Hallo testclient en opmerking dat Hallo item blijft tooincrement ondanks Hallo failover.</span><span class="sxs-lookup"><span data-stu-id="5deb0-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="5deb0-151">Meer services tooan bestaande toepassing toe te voegen</span><span class="sxs-lookup"><span data-stu-id="5deb0-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="5deb0-152">tooadd een andere service tooan toepassing al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5deb0-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="5deb0-153">Toohello hoofdmap van de bestaande toepassing hello wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5deb0-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="5deb0-154">Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5deb0-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="5deb0-155">Voer `yo azuresfcsharp:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="5deb0-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="5deb0-156">Migreren van project.json too.csproj</span><span class="sxs-lookup"><span data-stu-id="5deb0-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="5deb0-157">Uitgevoerd 'dotnet migreren' in de hoofdmap project worden alle Hallo project.json toocsproj indeling worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="5deb0-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="5deb0-158">Update Hallo project verwijst naar dienovereenkomstig toocsproj bestanden in de project-bestanden.</span><span class="sxs-lookup"><span data-stu-id="5deb0-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="5deb0-159">Hallo bestand namen toocsproj projectbestanden in build.sh bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5deb0-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5deb0-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5deb0-160">Next steps</span></span>

* [<span data-ttu-id="5deb0-161">Meer informatie over Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5deb0-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="5deb0-162">Interactie met Service Fabric-clusters met Hallo Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="5deb0-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="5deb0-163">Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="5deb0-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="5deb0-164">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="5deb0-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
