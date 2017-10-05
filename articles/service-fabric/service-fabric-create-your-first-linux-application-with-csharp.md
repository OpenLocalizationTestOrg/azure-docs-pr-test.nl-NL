---
title: Uw eerste Azure-microservices-app in Linux maken met behulp van C# | Microsoft Docs
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
ms.openlocfilehash: adcafaa5522fcddc0a01eb1dc8deba04ebfc38f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="0dd6f-103">Uw eerste Azure Service Fabric-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0dd6f-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dd6f-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="0dd6f-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="0dd6f-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="0dd6f-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="0dd6f-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="0dd6f-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="0dd6f-107">Service Fabric biedt SDK's voor het bouwen van services in Linux in zowel .NET Core als Java.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="0dd6f-108">In deze zelfstudie wordt behandeld hoe u een toepassing maakt voor Linux en een service bouwt met behulp van C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="0dd6f-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd6f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0dd6f-109">Prerequisites</span></span>
<span data-ttu-id="0dd6f-110">Zorg voordat u begint ervoor dat u [uw Linux-ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0dd6f-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="0dd6f-111">Als u Mac OS X gebruikt, kunt u [een Linux one-box omgeving instellen op een virtuele machine met behulp van Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="0dd6f-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="0dd6f-112">Het is dan ook een goed idee om de [Service Fabric-CLI](service-fabric-cli.md) te installeren.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-csharp"></a><span data-ttu-id="0dd6f-113">Generatoren voor CSharp installeren en instellen</span><span class="sxs-lookup"><span data-stu-id="0dd6f-113">Install and set up the generators for CSharp</span></span>
<span data-ttu-id="0dd6f-114">Service Fabric biedt hulpprogramma's waarmee u vanuit de terminal een Service Fabric CSharp-toepassing kunt maken met behulp van de Yeoman-sjabloongenerator.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="0dd6f-115">Volg de stappen hieronder om te controleren of de Yeoman-sjabloongenerator voor CSharp werkt op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="0dd6f-116">nodejs en NPM installeren op uw computer</span><span class="sxs-lookup"><span data-stu-id="0dd6f-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="0dd6f-117">[Yeoman](http://yeoman.io/)-sjabloongenerator installeren op uw computer vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="0dd6f-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="0dd6f-118">Generator voor Service Fabric Yeoman Java-toepassingen installeren vanuit NPM</span><span class="sxs-lookup"><span data-stu-id="0dd6f-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="0dd6f-119">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0dd6f-119">Create the application</span></span>
<span data-ttu-id="0dd6f-120">Een Service Fabric-toepassing kan een of meer services bevatten, elk met een specifieke functie met betrekking tot het leveren van de functionaliteit van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="0dd6f-121">De Service Fabric [Yeoman](http://yeoman.io/)-generator voor CSharp, die u in de laatste stap hebt geïnstalleerd, zorgt ervoor dat u gemakkelijk uw eerste service kunt maken en er later meer kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="0dd6f-122">We gebruiken Yeoman om een toepassing te maken met één service.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="0dd6f-123">Typ in een terminal de volgende opdracht om te beginnen met de opbouw van de sjabloon: `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="0dd6f-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="0dd6f-124">Geef uw toepassing een naam.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-124">Name your application.</span></span>
3. <span data-ttu-id="0dd6f-125">Kies het type van uw eerste service en geef de service een naam.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="0dd6f-126">In deze zelfstudie kiezen we voor een Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Service Fabric Yeoman-generator voor C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="0dd6f-128">Zie [Service Fabric programming model overview](service-fabric-choose-framework.md) (Overzicht van het Service Fabric-programmeermodel) voor meer informatie over de opties.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-128">For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="0dd6f-129">De toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="0dd6f-129">Build the application</span></span>
<span data-ttu-id="0dd6f-130">De Service Fabric Yeoman-sjablonen bevatten een bouwscript dat u kunt gebruiken om de app via de terminal te maken (na het navigeren naar de toepassingsmap).</span><span class="sxs-lookup"><span data-stu-id="0dd6f-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="0dd6f-131">De toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="0dd6f-131">Deploy the application</span></span>

<span data-ttu-id="0dd6f-132">Nadat de toepassing is gemaakt, kunt u deze implementeren in het lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="0dd6f-133">Maak verbinding met het lokale cluster van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="0dd6f-134">Voer het installatiescript uit dat is opgegeven in de sjabloon om het toepassingspakket te kopiëren naar de installatiekopieopslag van het cluster, het toepassingstype te registreren en een exemplaar van de toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="0dd6f-135">De implementatie van de gemaakte toepassing werkt hetzelfde als van andere Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="0dd6f-136">Zie de documentatie over het [beheren van een Service Fabric-toepassing met de Service Fabric-CLI](service-fabric-application-lifecycle-sfctl.md) voor gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="0dd6f-137">Parameters voor deze opdrachten vindt u in de gegenereerde manifesten binnen het toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="0dd6f-138">Nadat de toepassing is geïmplementeerd, opent u een browser en gaat u naar [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) op [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="0dd6f-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="0dd6f-139">Vouw vervolgens het knooppunt **Toepassingen** uit. U ziet dat er nu een vermelding is voor uw toepassingstype en nog een voor het eerste exemplaar van dat type.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="0dd6f-140">De testclient starten en een failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0dd6f-140">Start the test client and perform a failover</span></span>
<span data-ttu-id="0dd6f-141">Actorprojecten doen niets uit zichzelf.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="0dd6f-142">Ze hebben een andere service of client nodig die hen berichten stuurt.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-142">They require another service or client to send them messages.</span></span> <span data-ttu-id="0dd6f-143">De actorsjabloon bevat een eenvoudig testscript dat u kunt gebruiken om te communiceren met de actorservice.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-143">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="0dd6f-144">Voer het script uit met behulp van het controleprogramma om de uitvoer van de actorservice te bekijken.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-144">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="0dd6f-145">Zoek in Service Fabric Explorer het knooppunt op dat als host fungeert voor de primaire replica voor de actorservice.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-145">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="0dd6f-146">In de onderstaande schermafbeelding is dit knooppunt 3.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-146">In the screenshot below, it is node 3.</span></span>

    ![Zoeken naar de primaire replica in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="0dd6f-148">Klik op het knooppunt dat u hebt gevonden in de vorige stap en selecteer vervolgens **Deactiveren (opnieuw starten)** in het menu Acties.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-148">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="0dd6f-149">Deze actie start één knooppunt in het lokale cluster opnieuw op om een failover af te dwingen naar een secundaire replica die wordt uitgevoerd op een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-149">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="0dd6f-150">Let terwijl u deze actie uitvoert op de uitvoer van de testclient en houd er rekening mee dat de teller blijft toenemen ondanks de failover.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-150">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="0dd6f-151">Meer services toevoegen aan een bestaande toepassing</span><span class="sxs-lookup"><span data-stu-id="0dd6f-151">Adding more services to an existing application</span></span>

<span data-ttu-id="0dd6f-152">Voer de volgende stappen uit als u nog een service wilt toevoegen aan een toepassing die al is gemaakt met `yo`:</span><span class="sxs-lookup"><span data-stu-id="0dd6f-152">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="0dd6f-153">Stel de directory in op de hoofdmap van de bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-153">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="0dd6f-154">Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="0dd6f-155">Voer `yo azuresfcsharp:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-to-csproj"></a><span data-ttu-id="0dd6f-156">Migreren van project.json naar .csproj</span><span class="sxs-lookup"><span data-stu-id="0dd6f-156">Migrating from project.json to .csproj</span></span>
1. <span data-ttu-id="0dd6f-157">Als u dotnet migrate uitvoert in de hoofdmap van het project, worden alle project.json gemigreerd naar de indeling csproj.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-157">Running 'dotnet migrate' in project root directory will migrate all the project.json to csproj format.</span></span>
2. <span data-ttu-id="0dd6f-158">Werk de projectverwijzingen in de projectbestanden op basis hiervan bij naar csproj-bestanden.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-158">Update the project references accordingly to csproj files in project files.</span></span>
3. <span data-ttu-id="0dd6f-159">Werk de projectbestandsnamen bij naar csproj-bestanden in build.sh.</span><span class="sxs-lookup"><span data-stu-id="0dd6f-159">Update the project file names to csproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dd6f-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0dd6f-160">Next steps</span></span>

* [<span data-ttu-id="0dd6f-161">Meer informatie over Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="0dd6f-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="0dd6f-162">Werken met Service Fabric-clusters via de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="0dd6f-162">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="0dd6f-163">Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="0dd6f-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="0dd6f-164">Aan de slag met de Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="0dd6f-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
