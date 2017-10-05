---
title: Implementeren van een bestaand uitvoerbaar bestand op Azure Service Fabric | Microsoft Docs
description: "Overzicht over het inpakken van een bestaande toepassing als gast uitvoerbare, zodat het kan worden geïmplementeerd naar een Service Fabric-cluster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="05780-103">Uitvoerbare Gast implementeren op Service Fabric</span><span class="sxs-lookup"><span data-stu-id="05780-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="05780-104">Als een service kunt u verschillende typen code, zoals Node.js, Java of C++ uitvoeren in Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="05780-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="05780-105">Service Fabric verwijst naar deze soorten services als gast uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="05780-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="05780-106">Gast uitvoerbare bestanden worden behandeld door het Service Fabric zoals stateless services.</span><span class="sxs-lookup"><span data-stu-id="05780-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="05780-107">Als gevolg hiervan worden deze geplaatst op knooppunten in een cluster, op basis van beschikbaarheid en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="05780-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="05780-108">In dit artikel wordt beschreven hoe het pakket en een gast uitvoerbare aan een Service Fabric-cluster implementeren met behulp van Visual Studio of een opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="05780-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="05780-109">In dit artikel komen we de stappen voor het pakket uitvoerbare Gast en deze implementeren in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="05780-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="05780-110">Voordelen van het uitvoeren van een gast uitvoerbare in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="05780-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="05780-111">Er zijn enkele voordelen voor het uitvoeren van een gast uitvoerbare in een Service Fabric-cluster:</span><span class="sxs-lookup"><span data-stu-id="05780-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="05780-112">Hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="05780-112">High availability.</span></span> <span data-ttu-id="05780-113">Toepassingen die worden uitgevoerd in Service Fabric zijn maximaal beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05780-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="05780-114">Service Fabric zorgt ervoor dat de exemplaren van een toepassing worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05780-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="05780-115">Statuscontrole.</span><span class="sxs-lookup"><span data-stu-id="05780-115">Health monitoring.</span></span> <span data-ttu-id="05780-116">Service Fabric-statuscontrole detecteert als een toepassing wordt uitgevoerd, en bevat de diagnostische gegevens als er een storing optreedt.</span><span class="sxs-lookup"><span data-stu-id="05780-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="05780-117">Levenscyclus van Toepassingsbeheer.</span><span class="sxs-lookup"><span data-stu-id="05780-117">Application lifecycle management.</span></span> <span data-ttu-id="05780-118">Service Fabric biedt automatisch herstel naar de vorige versie naast het bieden van upgrades zonder uitvaltijd, als er een ongeldige statusgebeurtenis gerapporteerd tijdens een upgrade.</span><span class="sxs-lookup"><span data-stu-id="05780-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="05780-119">Dichtheid.</span><span class="sxs-lookup"><span data-stu-id="05780-119">Density.</span></span> <span data-ttu-id="05780-120">U kunt meerdere toepassingen uitvoeren in een cluster die niet meer nodig voor elke toepassing uitvoeren op een eigen hardware.</span><span class="sxs-lookup"><span data-stu-id="05780-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="05780-121">U kunt de naamgeving van Service Fabric-service om andere services in het cluster zichtbaarheid: Met behulp van REST aanroepen.</span><span class="sxs-lookup"><span data-stu-id="05780-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="05780-122">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="05780-122">Samples</span></span>
* [<span data-ttu-id="05780-123">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="05780-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="05780-124">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceren via de Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="05780-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="05780-125">Overzicht van de toepassing en service manifest-bestanden</span><span class="sxs-lookup"><span data-stu-id="05780-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="05780-126">Als onderdeel van de implementatie van een gast uitvoerbaar bestand is het nuttig om het Service Fabric-model voor pakketten en implementatie begrijpen, zoals beschreven in [toepassingsmodel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="05780-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="05780-127">Het model van Service Fabric-pakket is afhankelijk van de twee XML-bestanden: de toepassing en service manifesten.</span><span class="sxs-lookup"><span data-stu-id="05780-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="05780-128">De schemadefinitie voor de bestanden ApplicationManifest.xml en ServiceManifest.xml is geïnstalleerd met de Service Fabric SDK in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="05780-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="05780-129">**Het toepassingsmanifest** het toepassingsmanifest wordt gebruikt om de toepassing te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="05780-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="05780-130">Geeft een lijst van de services die het opstellen en andere parameters die worden gebruikt om te definiëren hoe een of meer services moeten worden geïmplementeerd, zoals het aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="05780-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="05780-131">Een toepassing is in Service Fabric eenheid van de implementatie en upgrade.</span><span class="sxs-lookup"><span data-stu-id="05780-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="05780-132">Een toepassing kan worden bijgewerkt als één eenheid waar de potentiële fouten en mogelijke Rollback worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="05780-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="05780-133">Service Fabric zorgt ervoor dat het upgradeproces een is geslaagd, of als de upgrade mislukt, laat de toepassing in een onbekende of onstabiele status heeft.</span><span class="sxs-lookup"><span data-stu-id="05780-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="05780-134">**Servicemanifest** de servicemanifest beschrijving van de onderdelen van een service.</span><span class="sxs-lookup"><span data-stu-id="05780-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="05780-135">Dit omvat gegevens, zoals de naam en type van service, en de code en configuratie.</span><span class="sxs-lookup"><span data-stu-id="05780-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="05780-136">Het servicemanifest bevat ook een aantal extra parameters die kunnen worden gebruikt voor het configureren van de service nadat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="05780-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="05780-137">Bestandsstructuur voor Application-pakket</span><span class="sxs-lookup"><span data-stu-id="05780-137">Application package file structure</span></span>
<span data-ttu-id="05780-138">De toepassing moet een vooraf gedefinieerde mapstructuur Volg voor het implementeren van een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="05780-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="05780-139">Hier volgt een voorbeeld van die structuur.</span><span class="sxs-lookup"><span data-stu-id="05780-139">The following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="05780-140">De ApplicationPackageRoot bevat de ApplicationManifest.xml-bestand waarin de toepassing.</span><span class="sxs-lookup"><span data-stu-id="05780-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="05780-141">Een submap voor elke service die is opgenomen in de toepassing wordt gebruikt voor het bevatten van alle artefacten die de service vereist.</span><span class="sxs-lookup"><span data-stu-id="05780-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="05780-142">Deze submappen zijn de ServiceManifest.xml en gewoonlijk het volgende:</span><span class="sxs-lookup"><span data-stu-id="05780-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="05780-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="05780-143">*Code*.</span></span> <span data-ttu-id="05780-144">Deze map bevat de servicecode.</span><span class="sxs-lookup"><span data-stu-id="05780-144">This directory contains the service code.</span></span>
* <span data-ttu-id="05780-145">*Config*.</span><span class="sxs-lookup"><span data-stu-id="05780-145">*Config*.</span></span> <span data-ttu-id="05780-146">Deze map bevat een Settings.xml-bestand (en andere bestanden indien nodig) dat de service toegang heeft tot tijdens runtime specifieke configuratie-instellingen op te halen.</span><span class="sxs-lookup"><span data-stu-id="05780-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="05780-147">*Gegevens*.</span><span class="sxs-lookup"><span data-stu-id="05780-147">*Data*.</span></span> <span data-ttu-id="05780-148">Dit is een extra map voor het opslaan van aanvullende lokale gegevens die de service moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="05780-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="05780-149">Gegevens moet worden gebruikt voor het opslaan van alleen kortstondige gegevens.</span><span class="sxs-lookup"><span data-stu-id="05780-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="05780-150">Service Fabric niet gekopieerd of wijzigingen repliceren naar de map data als de service moet worden verplaatst (bijvoorbeeld tijdens failover).</span><span class="sxs-lookup"><span data-stu-id="05780-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="05780-151">U hoeft te maken van de `config` en `data` mappen als u deze niet nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="05780-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="05780-152">Een bestaand uitvoerbaar bestand van het pakket</span><span class="sxs-lookup"><span data-stu-id="05780-152">Package an existing executable</span></span>
<span data-ttu-id="05780-153">Wanneer een gast uitvoerbaar bestand verpakking, kunt u ofwel een Visual Studio-projectsjabloon gebruiken of [handmatig maken van het toepassingspakket](#manually).</span><span class="sxs-lookup"><span data-stu-id="05780-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="05780-154">Met Visual Studio, worden de toepassing pakketstructuur en manifest-bestanden door het nieuwe projectsjabloon voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05780-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="05780-155">De eenvoudigste manier om een bestaande Windows uitvoerbare bij een service van het pakket is met Visual Studio en op Linux Yeoman gebruiken</span><span class="sxs-lookup"><span data-stu-id="05780-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="05780-156">Visual Studio gebruiken om te verpakken en distribueren van een bestaand uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="05780-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="05780-157">Visual Studio biedt een Service Fabric-servicesjabloon om te helpen bij het implementeren van een gast uitvoerbare naar een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="05780-158">Kies **bestand** > **nieuw Project**, en maak een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="05780-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="05780-159">Kies **Gast uitvoerbaar bestand** als de servicesjabloon.</span><span class="sxs-lookup"><span data-stu-id="05780-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="05780-160">Klik op **Bladeren** om te selecteren van de map met het uitvoerbare bestand en voer de rest van de parameters voor het maken van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="05780-161">*Pakketgedrag code*.</span><span class="sxs-lookup"><span data-stu-id="05780-161">*Code Package Behavior*.</span></span> <span data-ttu-id="05780-162">De inhoud van de map naar de Visual Studio-Project kopiëren dit is handig als het uitvoerbare bestand wordt niet gewijzigd kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="05780-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="05780-163">Als u verwacht het uitvoerbare bestand dat te wijzigen en de mogelijkheid om op te halen nieuwe builds dynamisch wilt, kunt u de koppeling naar de map maken in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="05780-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="05780-164">U kunt de gekoppelde mappen kunt gebruiken bij het maken van het project voor een toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05780-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="05780-165">Deze koppelingen naar de bronlocatie van binnen het project, waardoor het mogelijk dat u wilt bijwerken van de Gast uitvoerbare in de doel-bron.</span><span class="sxs-lookup"><span data-stu-id="05780-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="05780-166">Deze updates uitmaken deel van het toepassingspakket met build.</span><span class="sxs-lookup"><span data-stu-id="05780-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="05780-167">*Programma* het uitvoerbare bestand dat moet worden uitgevoerd om de service te starten.</span><span class="sxs-lookup"><span data-stu-id="05780-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="05780-168">*Argumenten* Hiermee geeft u de argumenten die moeten worden doorgegeven aan het uitvoerbare bestand.</span><span class="sxs-lookup"><span data-stu-id="05780-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="05780-169">Het kan zijn dat een lijst met parameters met argumenten.</span><span class="sxs-lookup"><span data-stu-id="05780-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="05780-170">*WorkingFolder* Hiermee geeft u de werkmap voor het proces dat zal worden gestart.</span><span class="sxs-lookup"><span data-stu-id="05780-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="05780-171">U kunt drie waarden opgeven:</span><span class="sxs-lookup"><span data-stu-id="05780-171">You can specify three values:</span></span>
     * <span data-ttu-id="05780-172">`CodeBase`Hiermee geeft u aan dat de werkmap moet worden ingesteld op de codemap in het toepassingspakket gaat (`Code` directory die wordt weergegeven in de voorgaande bestandsstructuur).</span><span class="sxs-lookup"><span data-stu-id="05780-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="05780-173">`CodePackage`Hiermee geeft u aan dat de werkmap moet worden ingesteld op de hoofdmap van het toepassingspakket gaat (`GuestService1Pkg` weergegeven in de voorgaande bestandsstructuur).</span><span class="sxs-lookup"><span data-stu-id="05780-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="05780-174">`Work`Hiermee geeft u op dat de bestanden in de submap werk zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="05780-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="05780-175">Geef de service een naam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="05780-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="05780-176">Als uw service een eindpunt voor communicatie moet, kunt u nu de protocol, de poort en het type toevoegen aan het bestand ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="05780-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="05780-177">Bijvoorbeeld: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="05780-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="05780-178">U kunt nu gebruik van het pakket en publiceren van actie tegen uw lokale cluster door de oplossing in Visual Studio-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="05780-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="05780-179">Wanneer u klaar bent, kunt u de toepassing publiceren in een cluster met externe of Controleer in de oplossing met resourcebeheer.</span><span class="sxs-lookup"><span data-stu-id="05780-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="05780-180">Ga naar het einde van dit artikel voor informatie over het weergeven van de Gast uitvoerbare service wordt uitgevoerd op de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="05780-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="05780-181">Yoeman gebruiken voor het pakket en implementeren van een bestaand uitvoerbaar bestand op Linux</span><span class="sxs-lookup"><span data-stu-id="05780-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="05780-182">De procedure voor het maken en implementeren van een uitvoerbaar zijn op Linux Gast is hetzelfde als het implementeren van een csharp of java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="05780-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="05780-183">Typ in een terminal `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="05780-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="05780-184">Geef uw toepassing een naam.</span><span class="sxs-lookup"><span data-stu-id="05780-184">Name your application.</span></span>
3. <span data-ttu-id="05780-185">Naam van uw service en geef de details, zoals het pad van het uitvoerbare bestand en de parameters die moeten worden aangeroepen met.</span><span class="sxs-lookup"><span data-stu-id="05780-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="05780-186">Yeoman een toepassingspakket met de juiste toepassing maakt en manifest-bestanden samen met het installeren en verwijderen van scripts.</span><span class="sxs-lookup"><span data-stu-id="05780-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="05780-187">Handmatig verpakken en distribueren van een bestaand uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="05780-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="05780-188">Het proces van het verpakken van handmatig een gast uitvoerbaar bestand is gebaseerd op de volgende algemene stappen:</span><span class="sxs-lookup"><span data-stu-id="05780-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="05780-189">De mapstructuur pakket maken.</span><span class="sxs-lookup"><span data-stu-id="05780-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="05780-190">De bestanden en de configuratie van de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="05780-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="05780-191">Bewerk het manifestbestand van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="05780-192">Bewerk het manifestbestand van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="05780-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="05780-193">De mapstructuur pakket maken</span><span class="sxs-lookup"><span data-stu-id="05780-193">Create the package directory structure</span></span>
<span data-ttu-id="05780-194">U kunt starten door het maken van de mapstructuur zoals beschreven in de vorige sectie, "Toepassing pakket bestandsstructuur."</span><span class="sxs-lookup"><span data-stu-id="05780-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="05780-195">De bestanden code en configuratie van de toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="05780-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="05780-196">Nadat u de mapstructuur hebt gemaakt, kunt u de toepassingscode en configuratiebestanden onder de code en config-mappen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="05780-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="05780-197">U kunt ook extra mappen of submappen onder de code of configuratieversie mappen maken.</span><span class="sxs-lookup"><span data-stu-id="05780-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="05780-198">Service Fabric biedt een `xcopy` van de inhoud van de hoofdmap van toepassing, zodat er geen vooraf gedefinieerde structuur dan het maken van de twee bovenste mappen, code en instellingen.</span><span class="sxs-lookup"><span data-stu-id="05780-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="05780-199">(U kunt kiezen verschillende namen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="05780-199">(You can pick different names if you want.</span></span> <span data-ttu-id="05780-200">Meer informatie vindt u in de volgende sectie.)</span><span class="sxs-lookup"><span data-stu-id="05780-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="05780-201">Zorg ervoor dat u alle bestanden en afhankelijkheden die behoeften van de toepassing opneemt.</span><span class="sxs-lookup"><span data-stu-id="05780-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="05780-202">Service Fabric kopieert de inhoud van het toepassingspakket op alle knooppunten in het cluster waar de toepassing services gaat worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="05780-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="05780-203">Het pakket bevat de code die de toepassing moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05780-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="05780-204">Niet wordt ervan uitgegaan dat de afhankelijkheden al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="05780-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="05780-205">Het manifestbestand van de service bewerken</span><span class="sxs-lookup"><span data-stu-id="05780-205">Edit the service manifest file</span></span>
<span data-ttu-id="05780-206">De volgende stap is het bewerken van het manifestbestand van de service met de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="05780-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="05780-207">De naam van het type van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-207">The name of the service type.</span></span> <span data-ttu-id="05780-208">Dit is een ID die Service Fabric gebruikt om een service te identificeren.</span><span class="sxs-lookup"><span data-stu-id="05780-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="05780-209">De opdracht die moet worden gebruikt om de toepassing (ExeHost) te starten.</span><span class="sxs-lookup"><span data-stu-id="05780-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="05780-210">Elk script dat moet worden uitgevoerd om de toepassing (entrypoint) in te stellen.</span><span class="sxs-lookup"><span data-stu-id="05780-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="05780-211">Hieronder volgt een voorbeeld van een `ServiceManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="05780-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="05780-212">De volgende secties gaat over de verschillende onderdelen van het bestand dat u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="05780-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="05780-213">ServiceTypes bijwerken</span><span class="sxs-lookup"><span data-stu-id="05780-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="05780-214">U kunt elke willekeurige naam die u wilt verzamelen `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="05780-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="05780-215">De waarde wordt gebruikt in de `ApplicationManifest.xml` bestand om de service te identificeren.</span><span class="sxs-lookup"><span data-stu-id="05780-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="05780-216">Geef `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="05780-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="05780-217">Dit kenmerk instrueert Service Fabric dat de service is gebaseerd op een zelfstandige app, zodat alle Service Fabric-behoeften te doen als een proces te starten en de status controleren.</span><span class="sxs-lookup"><span data-stu-id="05780-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="05780-218">CodePackage bijwerken</span><span class="sxs-lookup"><span data-stu-id="05780-218">Update CodePackage</span></span>
<span data-ttu-id="05780-219">Het element CodePackage geeft de locatie (en versie) van de code van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="05780-220">De `Name` element wordt gebruikt om op te geven van de naam van de map in het toepassingspakket met de code van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="05780-221">`CodePackage`heeft ook de `version` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="05780-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="05780-222">Dit kan worden gebruikt om op te geven van de versie van de code en mogelijk ook van de service om code te upgraden met behulp van de beheerinfrastructuur van de toepassing lifecycle in Service Fabric kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05780-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="05780-223">Optioneel: Update entrypoint</span><span class="sxs-lookup"><span data-stu-id="05780-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="05780-224">Het element entrypoint wordt gebruikt om op te geven van een uitvoerbaar bestand of batch-bestand dat moet worden uitgevoerd voordat de code van de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="05780-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="05780-225">Het is een optionele stap zodat deze niet hoeft te worden opgenomen als er geen initialisatie vereist.</span><span class="sxs-lookup"><span data-stu-id="05780-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="05780-226">De entrypoint wordt uitgevoerd telkens wanneer de service is gestart.</span><span class="sxs-lookup"><span data-stu-id="05780-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="05780-227">Er is slechts één entrypoint zodat setup-scripts worden gegroepeerd in een enkel batchbestand moeten als de toepassing setup meerdere scripts vereist.</span><span class="sxs-lookup"><span data-stu-id="05780-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="05780-228">Elk type bestand kan worden uitgevoerd door de entrypoint: uitvoerbare bestanden, batchbestanden en PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05780-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="05780-229">Zie voor meer informatie [entrypoint configureren](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="05780-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="05780-230">In het voorgaande voorbeeld de entrypoint wordt uitgevoerd een batchbestand aangeroepen `LaunchConfig.cmd` die zich bevindt de `scripts` submap van de codemap (uitgaande van het element WorkingFolder is ingesteld op CodeBase).</span><span class="sxs-lookup"><span data-stu-id="05780-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="05780-231">EntryPoint bijwerken</span><span class="sxs-lookup"><span data-stu-id="05780-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="05780-232">De `EntryPoint` element in het manifestbestand van de service wordt gebruikt om op te geven hoe u kunt de service te starten.</span><span class="sxs-lookup"><span data-stu-id="05780-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="05780-233">De `ExeHost` element geeft de uitvoerbare bestand (en de argumenten) die moet worden gebruikt voor het starten van de service.</span><span class="sxs-lookup"><span data-stu-id="05780-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="05780-234">`Program`Hiermee geeft u de naam van het uitvoerbare bestand dat de service moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="05780-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="05780-235">`Arguments`Hiermee geeft u de argumenten die moeten worden doorgegeven aan het uitvoerbare bestand.</span><span class="sxs-lookup"><span data-stu-id="05780-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="05780-236">Het kan zijn dat een lijst met parameters met argumenten.</span><span class="sxs-lookup"><span data-stu-id="05780-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="05780-237">`WorkingFolder`Hiermee geeft u de werkmap voor het proces dat zal worden gestart.</span><span class="sxs-lookup"><span data-stu-id="05780-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="05780-238">U kunt drie waarden opgeven:</span><span class="sxs-lookup"><span data-stu-id="05780-238">You can specify three values:</span></span>
  * <span data-ttu-id="05780-239">`CodeBase`Hiermee geeft u aan dat de werkmap moet worden ingesteld op de codemap in het toepassingspakket gaat (`Code` map in de voorgaande bestandsstructuur).</span><span class="sxs-lookup"><span data-stu-id="05780-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="05780-240">`CodePackage`Hiermee geeft u aan dat de werkmap moet worden ingesteld op de hoofdmap van het toepassingspakket gaat (`GuestService1Pkg` in de voorgaande bestandsstructuur).</span><span class="sxs-lookup"><span data-stu-id="05780-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="05780-241">`Work`Hiermee geeft u op dat de bestanden in de submap werk zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="05780-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="05780-242">De WorkingFolder is handig voor het instellen van de juiste werkmap zodat relatieve paden kunnen worden gebruikt door de toepassing of de initialisatie van de scripts.</span><span class="sxs-lookup"><span data-stu-id="05780-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="05780-243">Bijwerken van eindpunten en registreren met Naming Service voor communicatie</span><span class="sxs-lookup"><span data-stu-id="05780-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="05780-244">In het voorgaande voorbeeld de `Endpoint` element geeft de eindpunten die de toepassing kunt luisteren op.</span><span class="sxs-lookup"><span data-stu-id="05780-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="05780-245">In dit voorbeeld wordt de Node.js-toepassing luistert naar http op 3000-poort.</span><span class="sxs-lookup"><span data-stu-id="05780-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="05780-246">Bovendien kunt u vragen over Service Fabric dit eindpunt publiceren naar de Naming Service, zodat het adres van het eindpunt naar deze service kunnen worden gedetecteerd door andere services.</span><span class="sxs-lookup"><span data-stu-id="05780-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="05780-247">Hiermee kunt u communiceren tussen services die gast uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="05780-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="05780-248">Adres van het gepubliceerde eindpunt heeft de vorm `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="05780-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="05780-249">`UriScheme`en `PathSuffix` optionele kenmerken zijn.</span><span class="sxs-lookup"><span data-stu-id="05780-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="05780-250">`IPAddressOrFQDN`de IP-adres of FQDN-naam van het knooppunt op dit uitvoerbare bestand wordt geplaatst en wordt automatisch voor u.</span><span class="sxs-lookup"><span data-stu-id="05780-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="05780-251">In het volgende voorbeeld zodra de service is geïmplementeerd, in Service Fabric Explorer ziet u een eindpunt die vergelijkbaar is met `http://10.1.4.92:3000/myapp/` gepubliceerd voor service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="05780-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="05780-252">Of als dit een lokale computer is, ziet u `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="05780-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="05780-253">U kunt deze adressen met [omgekeerde proxy](service-fabric-reverseproxy.md) voor de communicatie tussen services.</span><span class="sxs-lookup"><span data-stu-id="05780-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="05780-254">Het manifestbestand van de toepassing bewerken</span><span class="sxs-lookup"><span data-stu-id="05780-254">Edit the application manifest file</span></span>
<span data-ttu-id="05780-255">Nadat u hebt geconfigureerd de `Servicemanifest.xml` -bestand, moet u enkele wijzigingen in de `ApplicationManifest.xml` bestand om ervoor te zorgen dat de juiste servicetype en de naam worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05780-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="05780-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="05780-256">ServiceManifestImport</span></span>
<span data-ttu-id="05780-257">In de `ServiceManifestImport` element, kunt u een of meer services die u wilt opnemen in de app opgeven.</span><span class="sxs-lookup"><span data-stu-id="05780-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="05780-258">Services wordt verwezen met `ServiceManifestName`, die aangeeft dat de naam van de map waar de `ServiceManifest.xml` bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="05780-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="05780-259">Logboekregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="05780-259">Set up logging</span></span>
<span data-ttu-id="05780-260">Voor uitvoerbare bestanden Gast is het handig om te kunnen zien van de logboeken van de console om erachter te komen als de toepassing en configuratie-scripts eventuele fouten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="05780-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="05780-261">Console-omleiding kan worden geconfigureerd in de `ServiceManifest.xml` bestand met de `ConsoleRedirection` element.</span><span class="sxs-lookup"><span data-stu-id="05780-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="05780-262">Gebruik het beleid voor omleiding console nooit in een toepassing die wordt geïmplementeerd in productie, omdat dit de failover van de toepassing kan beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="05780-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="05780-263">*Alleen* Gebruik deze optie voor lokale ontwikkeling en foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="05780-263">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="05780-264">`ConsoleRedirection`kan worden gebruikt voor het omleiden van de console-uitvoer (stdout en stderr) in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="05780-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="05780-265">Dit biedt de mogelijkheid om te controleren of er zijn geen fouten tijdens de installatie of de uitvoering van de toepassing in de Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="05780-266">`FileRetentionCount`Hiermee wordt bepaald hoeveel bestanden worden opgeslagen in de werkmap.</span><span class="sxs-lookup"><span data-stu-id="05780-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="05780-267">Een waarde van 5, betekent bijvoorbeeld dat de logboekbestanden voor de vorige vijf uitvoeringen zijn opgeslagen in de werkmap.</span><span class="sxs-lookup"><span data-stu-id="05780-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="05780-268">`FileMaxSizeInKb`Hiermee geeft u de maximale grootte van de logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="05780-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="05780-269">Logboekbestanden worden opgeslagen in een van de service werken mappen.</span><span class="sxs-lookup"><span data-stu-id="05780-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="05780-270">Service Fabric Explorer om te bepalen welk knooppunt de service gebruiken om te bepalen waar de bestanden zich bevinden op wordt uitgevoerd en welke werkmap wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05780-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="05780-271">Dit proces wordt verderop in dit artikel beschreven.</span><span class="sxs-lookup"><span data-stu-id="05780-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="05780-272">Implementatie</span><span class="sxs-lookup"><span data-stu-id="05780-272">Deployment</span></span>
<span data-ttu-id="05780-273">De laatste stap is het [implementeren van uw toepassing](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="05780-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="05780-274">De volgende PowerShell-script laat zien hoe uw toepassing implementeert op de lokaal ontwikkelcluster, en een nieuwe Service Fabric-service starten.</span><span class="sxs-lookup"><span data-stu-id="05780-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="05780-275">[Comprimeren van het pakket](service-fabric-package-apps.md#compress-a-package) vóór het kopiëren van de image store als het pakket grote is of veel bestanden.</span><span class="sxs-lookup"><span data-stu-id="05780-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="05780-276">Lees meer [hier](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="05780-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="05780-277">Een Service Fabric-service kan worden geïmplementeerd in verschillende 'configuraties."</span><span class="sxs-lookup"><span data-stu-id="05780-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="05780-278">Bijvoorbeeld, het kan worden geïmplementeerd als één of meerdere exemplaren of deze zodanig dat er een exemplaar van de service op elk knooppunt van het Service Fabric-cluster wordt kan worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="05780-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="05780-279">De `InstanceCount` parameter van de `New-ServiceFabricService` cmdlet wordt gebruikt om op te geven hoeveel exemplaren van de service moeten worden gestart in de Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="05780-280">U kunt instellen de `InstanceCount` waarde, afhankelijk van het type van de toepassing die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="05780-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="05780-281">De twee meest voorkomende scenario's:</span><span class="sxs-lookup"><span data-stu-id="05780-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="05780-282">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="05780-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="05780-283">In dit geval wordt wordt slechts één exemplaar van de service geïmplementeerd in het cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="05780-284">Service-Fabric scheduler bepaalt welk knooppunt de service gaat wordt geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="05780-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="05780-285">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="05780-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="05780-286">In dit geval wordt wordt één exemplaar van de service geïmplementeerd op elk knooppunt in het Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="05780-287">Het resultaat heeft één (en slechts één) exemplaar van de service voor elk knooppunt in het cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="05780-288">Dit is een nuttig configuratie voor de front-end-toepassingen (bijvoorbeeld een REST-eindpunt), omdat clienttoepassingen verbinding moeten maken "" een van de knooppunten in het cluster het eindpunt te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05780-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="05780-289">Deze configuratie kan ook worden gebruikt wanneer u bijvoorbeeld alle knooppunten van het Service Fabric-cluster zijn verbonden met een load balancer.</span><span class="sxs-lookup"><span data-stu-id="05780-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="05780-290">Clientverkeer kan vervolgens worden gedistribueerd via de service die wordt uitgevoerd op alle knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="05780-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="05780-291">Controleer de actieve toepassing</span><span class="sxs-lookup"><span data-stu-id="05780-291">Check your running application</span></span>
<span data-ttu-id="05780-292">Identificeer in Service Fabric Explorer het knooppunt waar de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05780-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="05780-293">In dit voorbeeld op wordt uitgevoerd knooppunt1:</span><span class="sxs-lookup"><span data-stu-id="05780-293">In this example, it runs on Node1:</span></span>

![Knooppunt waarop de service wordt uitgevoerd](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="05780-295">Als u naar het knooppunt navigeren en blader naar de toepassing, ziet u de essentiële knooppunt informatie, waaronder de locatie op schijf.</span><span class="sxs-lookup"><span data-stu-id="05780-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![Locatie op schijf](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="05780-297">Als u naar de map bladeren met behulp van de Server Explorer, vindt u de werkmap en de logboekmap voor de service, zoals wordt weergegeven in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="05780-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![Locatie van logboek](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="05780-299">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05780-299">Next steps</span></span>
<span data-ttu-id="05780-300">In dit artikel hebt u geleerd hoe een gast uitvoerbaar bestand van het pakket en deze implementeren in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="05780-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="05780-301">Zie de volgende artikelen voor meer informatie en taken.</span><span class="sxs-lookup"><span data-stu-id="05780-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="05780-302">[Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), inclusief een koppeling naar de voorlopige versie van het hulpprogramma verpakking</span><span class="sxs-lookup"><span data-stu-id="05780-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="05780-303">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceren via de Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="05780-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="05780-304">Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="05780-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="05780-305">Uw eerste Service Fabric-toepassing met Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="05780-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
