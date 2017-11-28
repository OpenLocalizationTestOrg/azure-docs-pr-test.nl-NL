---
title: een bestaand uitvoerbaar tooAzure Service Fabric aaaDeploy | Microsoft Docs
description: "Overzicht over hoe toopackage een bestaande toepassing als een gast uitvoerbaar bestand, zodat deze kan worden geïmplementeerd voor tooa Service Fabric-cluster"
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
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="8c625-103">Een gast uitvoerbare tooService Fabric implementeren</span><span class="sxs-lookup"><span data-stu-id="8c625-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="8c625-104">Als een service kunt u verschillende typen code, zoals Node.js, Java of C++ uitvoeren in Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c625-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="8c625-105">Service Fabric verwijst toothese soorten services als gast uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="8c625-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="8c625-106">Gast uitvoerbare bestanden worden behandeld door het Service Fabric zoals stateless services.</span><span class="sxs-lookup"><span data-stu-id="8c625-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="8c625-107">Als gevolg hiervan worden deze geplaatst op knooppunten in een cluster, op basis van beschikbaarheid en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8c625-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="8c625-108">Dit artikel wordt beschreven hoe toopackage en een gast uitvoerbare tooa Service Fabric-cluster implementeren met behulp van Visual Studio of een opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="8c625-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="8c625-109">In dit artikel, we hebben betrekking op Hallo stappen toopackage uitvoerbare Gast en implementeert u deze tooService Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c625-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="8c625-110">Voordelen van het uitvoeren van een gast uitvoerbare in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8c625-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="8c625-111">Er zijn enkele voordelen toorunning Gast uitvoerbare in een Service Fabric-cluster:</span><span class="sxs-lookup"><span data-stu-id="8c625-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="8c625-112">Hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="8c625-112">High availability.</span></span> <span data-ttu-id="8c625-113">Toepassingen die worden uitgevoerd in Service Fabric zijn maximaal beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c625-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="8c625-114">Service Fabric zorgt ervoor dat de exemplaren van een toepassing worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="8c625-115">Statuscontrole.</span><span class="sxs-lookup"><span data-stu-id="8c625-115">Health monitoring.</span></span> <span data-ttu-id="8c625-116">Service Fabric-statuscontrole detecteert als een toepassing wordt uitgevoerd, en bevat de diagnostische gegevens als er een storing optreedt.</span><span class="sxs-lookup"><span data-stu-id="8c625-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="8c625-117">Levenscyclus van Toepassingsbeheer.</span><span class="sxs-lookup"><span data-stu-id="8c625-117">Application lifecycle management.</span></span> <span data-ttu-id="8c625-118">Service Fabric bevat eerdere versie van automatisch herstel toohello naast het bieden van upgrades zonder uitvaltijd, als er een ongeldige statusgebeurtenis gerapporteerd tijdens een upgrade.</span><span class="sxs-lookup"><span data-stu-id="8c625-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="8c625-119">Dichtheid.</span><span class="sxs-lookup"><span data-stu-id="8c625-119">Density.</span></span> <span data-ttu-id="8c625-120">U kunt meerdere toepassingen uitvoeren in een cluster, zodat Hallo voor elke toepassing toorun op een eigen hardware.</span><span class="sxs-lookup"><span data-stu-id="8c625-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="8c625-121">Zichtbaarheid: REST kunt u aanroepen Hallo Service Fabric Naming service toofind andere services in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="8c625-122">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8c625-122">Samples</span></span>
* [<span data-ttu-id="8c625-123">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="8c625-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="8c625-124">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="8c625-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="8c625-125">Overzicht van de toepassing en service manifest-bestanden</span><span class="sxs-lookup"><span data-stu-id="8c625-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="8c625-126">Als onderdeel van de implementatie van een gast uitvoerbaar bestand, is het nuttig toounderstand Hallo Service Fabric-pakketten en -implementatiemodel zoals beschreven in [toepassingsmodel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c625-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="8c625-127">Hallo Service Fabric-pakket model is afhankelijk van de twee XML-bestanden: Hallo toepassing en service manifesten.</span><span class="sxs-lookup"><span data-stu-id="8c625-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="8c625-128">Hallo schemadefinitie voor hello is ApplicationManifest.xml en ServiceManifest.xml-bestanden geïnstalleerd met Hallo Service Fabric SDK in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="8c625-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="8c625-129">**Het toepassingsmanifest** Hallo-toepassingsmanifest gebruikte toodescribe Hallo toepassing is.</span><span class="sxs-lookup"><span data-stu-id="8c625-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="8c625-130">Geeft het Hallo-services waaruit deze en andere parameters die zijn gebruikt toodefine hoe een of meer services moeten worden geïmplementeerd, zoals het aantal exemplaren Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c625-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="8c625-131">Een toepassing is in Service Fabric eenheid van de implementatie en upgrade.</span><span class="sxs-lookup"><span data-stu-id="8c625-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="8c625-132">Een toepassing kan worden bijgewerkt als één eenheid waar de potentiële fouten en mogelijke Rollback worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="8c625-133">Service Fabric zorgt ervoor dat het upgradeproces Hallo ofwel is geslaagd, of als Hallo upgrade mislukt, laat Hallo-toepassing in een onbekende of onstabiele status heeft.</span><span class="sxs-lookup"><span data-stu-id="8c625-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="8c625-134">**Servicemanifest** Hallo servicemanifest beschrijving Hallo onderdelen van een service.</span><span class="sxs-lookup"><span data-stu-id="8c625-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="8c625-135">Dit omvat gegevens, zoals het Hallo-naam en type van de service, en de code en configuratie.</span><span class="sxs-lookup"><span data-stu-id="8c625-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="8c625-136">Hallo servicemanifest bevat ook een aantal extra parameters die kunnen worden gebruikt tooconfigure Hallo service nadat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="8c625-137">Bestandsstructuur voor Application-pakket</span><span class="sxs-lookup"><span data-stu-id="8c625-137">Application package file structure</span></span>
<span data-ttu-id="8c625-138">een toepassing tooService Fabric toodeploy, toepassing hello moet volgen op een vooraf gedefinieerde mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="8c625-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="8c625-139">Hallo Hier volgt een voorbeeld van die structuur.</span><span class="sxs-lookup"><span data-stu-id="8c625-139">hello following is an example of that structure.</span></span>

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

<span data-ttu-id="8c625-140">Hallo ApplicationPackageRoot bevat hello ApplicationManifest.xml-bestand waarin de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8c625-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="8c625-141">Een submap voor elke service die is opgenomen in de toepassing hello is gebruikte toocontain alle Hallo artefacten die Hallo service nodig.</span><span class="sxs-lookup"><span data-stu-id="8c625-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="8c625-142">Deze submappen zijn Hallo ServiceManifest.xml en normaal gesproken hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="8c625-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="8c625-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="8c625-143">*Code*.</span></span> <span data-ttu-id="8c625-144">Deze map bevat Hallo servicecode.</span><span class="sxs-lookup"><span data-stu-id="8c625-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="8c625-145">*Config*. Deze map bevat een Settings.xml-bestand (en andere bestanden indien nodig) dat Hallo-service toegang op runtime tooretrieve specifieke configuratie-instellingen tot.</span><span class="sxs-lookup"><span data-stu-id="8c625-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="8c625-146">*Gegevens*.</span><span class="sxs-lookup"><span data-stu-id="8c625-146">*Data*.</span></span> <span data-ttu-id="8c625-147">Dit is een extra map toostore aanvullende lokale gegevens die Hallo-service moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="8c625-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="8c625-148">Gegevens moeten alleen kortstondige gebruikte toostore-gegevens.</span><span class="sxs-lookup"><span data-stu-id="8c625-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="8c625-149">Service Fabric komt niet worden gekopieerd of repliceren wijzigingen toohello gegevensmap als Hallo-service toobe verplaatst (bijvoorbeeld tijdens de failover moet).</span><span class="sxs-lookup"><span data-stu-id="8c625-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="8c625-150">U hebt geen toocreate hello `config` en `data` mappen als u deze niet nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8c625-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="8c625-151">Een bestaand uitvoerbaar bestand van het pakket</span><span class="sxs-lookup"><span data-stu-id="8c625-151">Package an existing executable</span></span>
<span data-ttu-id="8c625-152">Wanneer een gast uitvoerbaar bestand verpakking, kunt u beide toouse een Visual Studio-projectsjabloon of te[handmatig maken van het toepassingspakket Hallo](#manually).</span><span class="sxs-lookup"><span data-stu-id="8c625-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="8c625-153">Pakketstructuur van toepassing met Visual Studio, Hallo en manifest-bestanden in het nieuwe projectsjabloon Hallo voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c625-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="8c625-154">Hallo gemakkelijkste manier toopackage een bestaande Windows uitvoerbare bij een service is toouse Visual Studio en op Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="8c625-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="8c625-155">Gebruik Visual Studio toopackage en de implementatie van een bestaand uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="8c625-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="8c625-156">Visual Studio biedt een Service Fabric service sjabloon toohelp implementeren van een gast uitvoerbare tooa Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="8c625-157">Kies **bestand** > **nieuw Project**, en maak een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c625-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="8c625-158">Kies **Gast uitvoerbaar bestand** als Hallo-servicesjabloon.</span><span class="sxs-lookup"><span data-stu-id="8c625-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="8c625-159">Klik op **Bladeren** tooselect Hallo map met de uitvoerbare bestand en vul Hallo rest van Hallo parameters toocreate Hallo service.</span><span class="sxs-lookup"><span data-stu-id="8c625-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="8c625-160">*Pakketgedrag code*.</span><span class="sxs-lookup"><span data-stu-id="8c625-160">*Code Package Behavior*.</span></span> <span data-ttu-id="8c625-161">Kan worden set toocopy alle Hallo inhoud van uw map toohello Visual Studio-Project, dit is handig als Hallo uitvoerbare wordt niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8c625-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="8c625-162">Als u Hallo uitvoerbare toochange verwacht en Hallo mogelijkheid toopick van nieuwe builds dynamisch wilt, kunt u in plaats daarvan toolink toohello map.</span><span class="sxs-lookup"><span data-stu-id="8c625-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="8c625-163">U kunt de gekoppelde mappen kunt gebruiken bij het Hallo-toepassingsproject maken in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c625-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="8c625-164">Toohello bronlocatie uit binnen Hallo-project, waardoor het mogelijk dat u tooupdate Hallo Gast uitvoerbare in de bron-doel wordt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8c625-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="8c625-165">Deze updates uitmaken deel van Hallo-toepassingspakket op build.</span><span class="sxs-lookup"><span data-stu-id="8c625-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="8c625-166">*Programma* Hallo uitvoerbaar bestand dat moet worden uitgevoerd toostart Hallo service bevat.</span><span class="sxs-lookup"><span data-stu-id="8c625-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="8c625-167">*Argumenten* Hallo argumenten die moeten worden doorgegeven toohello uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="8c625-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="8c625-168">Het kan zijn dat een lijst met parameters met argumenten.</span><span class="sxs-lookup"><span data-stu-id="8c625-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="8c625-169">*WorkingFolder* Hiermee geeft u de werkmap Hallo voor Hallo-proces dat wordt toobe gestart.</span><span class="sxs-lookup"><span data-stu-id="8c625-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="8c625-170">U kunt drie waarden opgeven:</span><span class="sxs-lookup"><span data-stu-id="8c625-170">You can specify three values:</span></span>
     * <span data-ttu-id="8c625-171">`CodeBase`Hiermee geeft u deze werkmap Hallo gaat toobe toohello code directory instellen in het toepassingspakket hello (`Code` directory die wordt weergegeven in de voorgaande bestandsstructuur Hallo).</span><span class="sxs-lookup"><span data-stu-id="8c625-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="8c625-172">`CodePackage`Hiermee geeft u deze werkmap Hallo gaat toobe toohello hoofdmap van het toepassingspakket Hallo ingesteld (`GuestService1Pkg` wordt weergegeven in de voorgaande bestandsstructuur Hallo).</span><span class="sxs-lookup"><span data-stu-id="8c625-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="8c625-173">`Work`Hiermee geeft u op dat Hallo-bestanden in de submap werk zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="8c625-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="8c625-174">Geef de service een naam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c625-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="8c625-175">Als uw service een eindpunt voor communicatie moet, kunt u nu Hallo-protocol en poort type toohello ServiceManifest.xml bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8c625-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="8c625-176">Bijvoorbeeld: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="8c625-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="8c625-177">U kunt nu Hallo pakket gebruiken en publiceren van actie tegen uw lokale cluster door foutopsporing Hallo-oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c625-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="8c625-178">Wanneer u klaar bent, kunt u Hallo toepassing tooa extern clusterbeheer publiceren of inchecken Hallo oplossing toosource besturingselement.</span><span class="sxs-lookup"><span data-stu-id="8c625-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="8c625-179">Hoe gaat u toohello einde van dit artikel toosee tooview uw gast uitvoerbare service wordt uitgevoerd op de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="8c625-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="8c625-180">Gebruik Yoeman toopackage en de implementatie van een bestaand uitvoerbaar bestand op Linux</span><span class="sxs-lookup"><span data-stu-id="8c625-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="8c625-181">Hallo-procedure voor het maken en implementeren van een uitvoerbaar zijn op Linux Gast is hetzelfde als het implementeren van een csharp of java-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8c625-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="8c625-182">Typ in een terminal `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="8c625-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="8c625-183">Geef uw toepassing een naam.</span><span class="sxs-lookup"><span data-stu-id="8c625-183">Name your application.</span></span>
3. <span data-ttu-id="8c625-184">Naam van uw service en Hallo details, zoals het pad van uitvoerbare Hallo en Hallo-parameters die moeten worden aangeroepen met bieden.</span><span class="sxs-lookup"><span data-stu-id="8c625-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="8c625-185">Yeoman maakt een toepassingspakket met de juiste toepassing hello en manifest-bestanden samen met het installeren en verwijderen van scripts.</span><span class="sxs-lookup"><span data-stu-id="8c625-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="8c625-186">Handmatig verpakken en distribueren van een bestaand uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="8c625-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="8c625-187">Hallo-proces verpakt handmatig een gast uitvoerbaar bestand is gebaseerd op Hallo algemene stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8c625-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="8c625-188">Mapstructuur Hallo-pakket maken.</span><span class="sxs-lookup"><span data-stu-id="8c625-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="8c625-189">De bestanden code en configuratie van de toepassing hello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8c625-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="8c625-190">Servicemanifest Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="8c625-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="8c625-191">Manifestbestand van de toepassing hello bewerken.</span><span class="sxs-lookup"><span data-stu-id="8c625-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="8c625-192">Mapstructuur Hallo-pakket maken</span><span class="sxs-lookup"><span data-stu-id="8c625-192">Create hello package directory structure</span></span>
<span data-ttu-id="8c625-193">U kunt starten door het maken van de mapstructuur Hallo, zoals beschreven in voorgaande sectie Hallo "Application-pakket bestandsstructuur."</span><span class="sxs-lookup"><span data-stu-id="8c625-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="8c625-194">De bestanden code en configuratie van de toepassing hello toevoegen</span><span class="sxs-lookup"><span data-stu-id="8c625-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="8c625-195">Nadat u de mapstructuur Hallo hebt gemaakt, kunt u Hallo van code en configuratie toepassingsbestanden onder Hallo code en config-mappen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8c625-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="8c625-196">U kunt ook extra mappen of submappen onder de code of configuratieversie mappen Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="8c625-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="8c625-197">Service Fabric biedt een `xcopy` van Hallo inhoud van Hallo hoofdmap van toepassing, zodat er geen toouse vooraf gedefinieerde structuur dan het maken van de twee bovenste mappen, code en instellingen.</span><span class="sxs-lookup"><span data-stu-id="8c625-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="8c625-198">(U kunt kiezen verschillende namen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="8c625-198">(You can pick different names if you want.</span></span> <span data-ttu-id="8c625-199">Meer informatie vindt u in de volgende sectie Hallo.)</span><span class="sxs-lookup"><span data-stu-id="8c625-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="8c625-200">Zorg ervoor dat u alle Hallo bestanden en afhankelijkheden die behoeften toepassing hello opneemt.</span><span class="sxs-lookup"><span data-stu-id="8c625-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="8c625-201">Service Fabric kopieert Hallo inhoud van het toepassingspakket Hallo op alle knooppunten in Hallo cluster waarbij Hallo toepassingsservices gaat toobe geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="8c625-202">Hallo-pakket moet alle Hallo code dat de toepassing hello toorun moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="8c625-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="8c625-203">Niet wordt ervan uitgegaan dat Hallo afhankelijkheden al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="8c625-204">Servicemanifest Hallo bewerken</span><span class="sxs-lookup"><span data-stu-id="8c625-204">Edit hello service manifest file</span></span>
<span data-ttu-id="8c625-205">de volgende stap Hallo is tooedit Hallo service manifestbestand tooinclude Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8c625-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="8c625-206">Hallo-naam van het servicetype Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c625-206">hello name of hello service type.</span></span> <span data-ttu-id="8c625-207">Dit is een ID dat gebruikmaakt van Service Fabric tooidentify een service.</span><span class="sxs-lookup"><span data-stu-id="8c625-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="8c625-208">Hallo opdracht toouse toolaunch Hallo toepassing (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="8c625-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="8c625-209">Elk script dat moet toobe tooset Hallo-toepassing (entrypoint) worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="8c625-210">Hallo Hieronder volgt een voorbeeld van een `ServiceManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="8c625-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="8c625-211">Hallo uit te voeren gaan via verschillende onderdelen van Hallo-bestand dat u nodig hebt tooupdate Hallo</span><span class="sxs-lookup"><span data-stu-id="8c625-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="8c625-212">ServiceTypes bijwerken</span><span class="sxs-lookup"><span data-stu-id="8c625-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="8c625-213">U kunt elke willekeurige naam die u wilt verzamelen `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="8c625-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="8c625-214">Hallo-waarde wordt gebruikt in Hallo `ApplicationManifest.xml` file tooidentify Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8c625-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="8c625-215">Geef `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="8c625-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="8c625-216">Dit kenmerk instrueert Service Fabric dat Hallo-service is gebaseerd op een zelfstandige app, zodat alle Service Fabric moet toodo toolaunch als een proces en de status controleren.</span><span class="sxs-lookup"><span data-stu-id="8c625-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="8c625-217">CodePackage bijwerken</span><span class="sxs-lookup"><span data-stu-id="8c625-217">Update CodePackage</span></span>
<span data-ttu-id="8c625-218">Hallo CodePackage element geeft Hallo locatie (en versie) van Hallo servicecode.</span><span class="sxs-lookup"><span data-stu-id="8c625-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="8c625-219">Hallo `Name` element is gebruikte toospecify Hallo naam van de map Hallo in Hallo-toepassingspakket met Hallo servicecode.</span><span class="sxs-lookup"><span data-stu-id="8c625-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="8c625-220">`CodePackage`heeft ook Hallo `version` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8c625-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="8c625-221">Deze versie van de gebruikte toospecify Hallo Hallo code en kan mogelijk ook tooupgrade Hallo service code gebruikt met behulp van Hallo toepassing lifecycle beheerinfrastructuur in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c625-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="8c625-222">Optioneel: Update entrypoint</span><span class="sxs-lookup"><span data-stu-id="8c625-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="8c625-223">Hallo entrypoint element gebruikte toospecify is een uitvoerbaar bestand of batch-bestand dat moet worden uitgevoerd voordat het Hallo servicecode wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8c625-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="8c625-224">Het is een optionele stap zodat deze niet toobe opgenomen hoeft als er geen initialisatie vereist.</span><span class="sxs-lookup"><span data-stu-id="8c625-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="8c625-225">Hallo entrypoint wordt uitgevoerd telkens wanneer het Hallo-service opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8c625-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="8c625-226">Er is slechts één entrypoint daarom installatiescripts toobe gegroepeerd in een enkel batchbestand als Hallo toepassingsinstellingen meerdere scripts vereist.</span><span class="sxs-lookup"><span data-stu-id="8c625-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="8c625-227">Hallo entrypoint elk type bestand kunt uitvoeren: uitvoerbare bestanden, batchbestanden en PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8c625-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="8c625-228">Zie voor meer informatie [entrypoint configureren](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="8c625-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="8c625-229">In Hallo voorgaande voorbeeld, Hallo entrypoint wordt uitgevoerd een batchbestand aangeroepen `LaunchConfig.cmd` dat zich bevindt in Hallo `scripts` submap van Hallo codemap (ervan uitgaande dat Hallo WorkingFolder element tooCodeBase is ingesteld).</span><span class="sxs-lookup"><span data-stu-id="8c625-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="8c625-230">EntryPoint bijwerken</span><span class="sxs-lookup"><span data-stu-id="8c625-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="8c625-231">Hallo `EntryPoint` -element in Hallo servicemanifestbestand is gebruikte toospecify hoe toolaunch Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8c625-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="8c625-232">Hallo `ExeHost` element geeft uitvoerbare hello (en argumenten) die moet worden gebruikt toolaunch Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8c625-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="8c625-233">`Program`Geeft de naam Hallo van Hallo uitvoerbaar bestand dat Hallo-service moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="8c625-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="8c625-234">`Arguments`Hiermee geeft u Hallo argumenten die moeten worden doorgegeven toohello uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="8c625-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="8c625-235">Het kan zijn dat een lijst met parameters met argumenten.</span><span class="sxs-lookup"><span data-stu-id="8c625-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="8c625-236">`WorkingFolder`Hiermee geeft u de werkmap Hallo voor Hallo-proces dat wordt toobe gestart.</span><span class="sxs-lookup"><span data-stu-id="8c625-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="8c625-237">U kunt drie waarden opgeven:</span><span class="sxs-lookup"><span data-stu-id="8c625-237">You can specify three values:</span></span>
  * <span data-ttu-id="8c625-238">`CodeBase`Hiermee geeft u deze werkmap Hallo gaat toobe toohello code directory instellen in het toepassingspakket hello (`Code` map in de voorgaande bestandsstructuur Hallo).</span><span class="sxs-lookup"><span data-stu-id="8c625-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="8c625-239">`CodePackage`Hiermee geeft u deze werkmap Hallo gaat toobe toohello hoofdmap van het toepassingspakket Hallo ingesteld (`GuestService1Pkg` in de voorgaande bestandsstructuur Hallo).</span><span class="sxs-lookup"><span data-stu-id="8c625-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="8c625-240">`Work`Hiermee geeft u op dat Hallo-bestanden in de submap werk zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="8c625-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="8c625-241">Hallo WorkingFolder is nuttig tooset Hallo juiste werkmap zodat relatieve paden kunnen worden gebruikt door beide Hallo toepassings- of initialisatie-scripts.</span><span class="sxs-lookup"><span data-stu-id="8c625-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="8c625-242">Bijwerken van eindpunten en registreren met Naming Service voor communicatie</span><span class="sxs-lookup"><span data-stu-id="8c625-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="8c625-243">Hallo in Hallo voorgaande voorbeeld, `Endpoint` element geeft Hallo-eindpunten die toepassing hello kunt luisteren op.</span><span class="sxs-lookup"><span data-stu-id="8c625-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="8c625-244">In dit voorbeeld luistert Hallo Node.js-toepassing naar http op 3000-poort.</span><span class="sxs-lookup"><span data-stu-id="8c625-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="8c625-245">Bovendien kunt u vragen Service Fabric toopublish dit eindpunt toohello Naming Service zodat andere services Hallo eindpunt adres toothis service kunnen detecteren.</span><span class="sxs-lookup"><span data-stu-id="8c625-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="8c625-246">Hiermee kunt u toobe kunnen toocommunicate tussen services die gast uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="8c625-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="8c625-247">Hallo gepubliceerde eindpuntadres heeft Hallo vorm `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="8c625-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="8c625-248">`UriScheme`en `PathSuffix` optionele kenmerken zijn.</span><span class="sxs-lookup"><span data-stu-id="8c625-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="8c625-249">`IPAddressOrFQDN`Hallo IP-adres of FQDN-naam van dit uitvoerbare bestand wordt geplaatst op Hallo-knooppunt en wordt berekend voor u is.</span><span class="sxs-lookup"><span data-stu-id="8c625-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="8c625-250">In hello volgende voorbeeld wordt één keer Hallo-service is geïmplementeerd, in Service Fabric Explorer ziet u een eindpunt die vergelijkbaar te`http://10.1.4.92:3000/myapp/` gepubliceerd voor Hallo service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8c625-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="8c625-251">Of als dit een lokale computer is, ziet u `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="8c625-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="8c625-252">U kunt deze adressen met [omgekeerde proxy](service-fabric-reverseproxy.md) toocommunicate tussen services.</span><span class="sxs-lookup"><span data-stu-id="8c625-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="8c625-253">Manifestbestand van de toepassing hello bewerken</span><span class="sxs-lookup"><span data-stu-id="8c625-253">Edit hello application manifest file</span></span>
<span data-ttu-id="8c625-254">Nadat u hebt geconfigureerd Hallo `Servicemanifest.xml` bestand, moet u toomake na enkele wijzigingen toohello `ApplicationManifest.xml` bestand tooensure die Hallo juiste servicetype en de naam worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8c625-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="8c625-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="8c625-255">ServiceManifestImport</span></span>
<span data-ttu-id="8c625-256">In Hallo `ServiceManifestImport` element, kunt u een of meer services die u wilt dat tooinclude in Hallo-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="8c625-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="8c625-257">Services wordt verwezen met `ServiceManifestName`, waarmee Hallo-naam van Hallo map waar hello `ServiceManifest.xml` bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="8c625-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="8c625-258">Logboekregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="8c625-258">Set up logging</span></span>
<span data-ttu-id="8c625-259">Voor uitvoerbare bestanden Gast is het nuttig toobe kunnen toosee console logboeken toofind uit als het Hallo-toepassing en configuratie-scripts tonen eventuele fouten.</span><span class="sxs-lookup"><span data-stu-id="8c625-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="8c625-260">Console-omleiding kan worden geconfigureerd in Hallo `ServiceManifest.xml` -bestand met de Hallo `ConsoleRedirection` element.</span><span class="sxs-lookup"><span data-stu-id="8c625-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="8c625-261">Gebruik nooit Omleidingsbeleid Hallo-console in een toepassing die is geïmplementeerd in productie, omdat dit Hallo toepassing failover kan beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="8c625-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="8c625-262">*Alleen* Gebruik deze optie voor lokale ontwikkeling en foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="8c625-262">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="8c625-263">`ConsoleRedirection`kan worden gebruikt tooredirect console-uitvoer (stdout en stderr) tooa-werkmap.</span><span class="sxs-lookup"><span data-stu-id="8c625-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="8c625-264">Dit biedt Hallo mogelijkheid tooverify dat er geen fouten zijn opgetreden tijdens het Hallo-setup of uitvoering van de toepassing hello in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="8c625-265">`FileRetentionCount`Hiermee wordt bepaald hoeveel bestanden worden opgeslagen in de werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c625-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="8c625-266">Een waarde van 5, betekent bijvoorbeeld dat Hallo-logboekbestanden voor de vorige vijf uitvoeringen Hallo zijn opgeslagen in de werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c625-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="8c625-267">`FileMaxSizeInKb`Geeft de maximumomvang Hallo Hallo-logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="8c625-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="8c625-268">Logboekbestanden worden opgeslagen in een van de service Hallo werkende mappen.</span><span class="sxs-lookup"><span data-stu-id="8c625-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="8c625-269">toodetermine waar Hallo bestanden zich bevinden, gebruik Service Fabric Explorer toodetermine welk knooppunt Hallo-service wordt uitgevoerd op, en welke werkmap wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8c625-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="8c625-270">Dit proces wordt verderop in dit artikel beschreven.</span><span class="sxs-lookup"><span data-stu-id="8c625-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="8c625-271">Implementatie</span><span class="sxs-lookup"><span data-stu-id="8c625-271">Deployment</span></span>
<span data-ttu-id="8c625-272">Hallo laatste stap is te[implementeren van uw toepassing](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="8c625-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="8c625-273">Hallo volgende PowerShell-script toont hoe toodeploy uw toepassing toohello lokaal ontwikkelcluster en start een nieuwe Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="8c625-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="8c625-274">[Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert als Hallo-pakket grote is of veel bestanden.</span><span class="sxs-lookup"><span data-stu-id="8c625-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="8c625-275">Lees meer [hier](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="8c625-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="8c625-276">Een Service Fabric-service kan worden geïmplementeerd in verschillende 'configuraties."</span><span class="sxs-lookup"><span data-stu-id="8c625-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="8c625-277">Bijvoorbeeld, het kan worden geïmplementeerd als één of meerdere exemplaren of deze zodanig dat er een exemplaar van de service op elk knooppunt van de Service Fabric-cluster Hallo Hallo wordt kan worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="8c625-278">Hallo `InstanceCount` parameter Hallo `New-ServiceFabricService` cmdlet gebruikte toospecify hoeveel exemplaren van Hallo-service moeten worden gestart in Hallo Service Fabric-cluster is.</span><span class="sxs-lookup"><span data-stu-id="8c625-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="8c625-279">U kunt instellen Hallo `InstanceCount` waarde, afhankelijk van het Hallo-type van de toepassing die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="8c625-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="8c625-280">Hallo twee meest voorkomende scenario's:</span><span class="sxs-lookup"><span data-stu-id="8c625-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="8c625-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="8c625-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="8c625-282">In dit geval wordt is slechts één exemplaar van het Hallo-service geïmplementeerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="8c625-283">Service-Fabric scheduler bepaalt welke knooppunt Hallo-service gaat toobe geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="8c625-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="8c625-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="8c625-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="8c625-285">In dit geval wordt wordt één exemplaar van Hallo-service geïmplementeerd op elk knooppunt in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="8c625-286">Hallo resultaat heeft één (en slechts één) exemplaar van Hallo-service voor elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8c625-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="8c625-287">Dit is een nuttig configuratie voor de front-end-toepassingen (bijvoorbeeld een REST-eindpunt), omdat clienttoepassingen nodig te "verbinding maken met' tooany van Hallo knooppunten in Hallo cluster toouse Hallo eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8c625-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="8c625-288">Deze configuratie kan ook worden gebruikt als alle knooppunten van het Service Fabric-cluster Hallo bijvoorbeeld verbonden tooa load balancer zijn.</span><span class="sxs-lookup"><span data-stu-id="8c625-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="8c625-289">Clientverkeer kan vervolgens worden gedistribueerd over Hallo-service die wordt uitgevoerd op alle knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="8c625-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="8c625-290">Controleer de actieve toepassing</span><span class="sxs-lookup"><span data-stu-id="8c625-290">Check your running application</span></span>
<span data-ttu-id="8c625-291">In Service Fabric Explorer geïdentificeerd Hallo knooppunt waarop Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8c625-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="8c625-292">In dit voorbeeld op wordt uitgevoerd knooppunt1:</span><span class="sxs-lookup"><span data-stu-id="8c625-292">In this example, it runs on Node1:</span></span>

![Knooppunt waarop de service wordt uitgevoerd](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="8c625-294">Als u toohello knooppunt navigeren en toohello toepassing bladeren, ziet u Hallo knooppunt essentiële informatie, waaronder de locatie op schijf.</span><span class="sxs-lookup"><span data-stu-id="8c625-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Locatie op schijf](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="8c625-296">Als u toohello directory bladert met behulp van de Server Explorer, vindt u Hallo-werkmap en logboekmap Hallo-service, zoals wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="8c625-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Locatie van logboek](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="8c625-298">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c625-298">Next steps</span></span>
<span data-ttu-id="8c625-299">In dit artikel hebt u geleerd hoe een gast uitvoerbaar bestand toopackage en tooService Fabric implementeert.</span><span class="sxs-lookup"><span data-stu-id="8c625-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="8c625-300">Zie Hallo artikelen voor meer informatie en taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="8c625-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="8c625-301">[Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), met inbegrip van een koppeling toohello voorlopige versie van hulpprogramma voor hello-pakketten</span><span class="sxs-lookup"><span data-stu-id="8c625-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="8c625-302">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="8c625-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="8c625-303">Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="8c625-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="8c625-304">Uw eerste Service Fabric-toepassing met Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="8c625-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
