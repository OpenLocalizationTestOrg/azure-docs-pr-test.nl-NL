---
title: Hoe containerize van uw Azure Service Fabric-microservices (preview)
description: Azure Service Fabric is nieuwe functionaliteit om uw Service Fabric-microservices containerize toegevoegd. Deze functie is momenteel beschikbaar als preview-product.
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6f8ad0bad8d1ae861e6b72f7e1a32ab0675813c2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-containerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="f2560-104">Hoe containerize uw Service Fabric Reliable Services en Reliable Actors (Preview)</span><span class="sxs-lookup"><span data-stu-id="f2560-104">How to containerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="f2560-105">Service Fabric ondersteunt containerizing Service Fabric-microservices (Reliable Services en betrouwbare op basis van actorservices).</span><span class="sxs-lookup"><span data-stu-id="f2560-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="f2560-106">Zie voor meer informatie [service fabric-containers](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2560-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="f2560-107">Deze functie is een Preview-versie en dit artikel bevat de verschillende stappen om uw service uitgevoerd binnen een container.</span><span class="sxs-lookup"><span data-stu-id="f2560-107">This feature is in preview and this article provides the various steps to get your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="f2560-108">Deze functie is Preview-versie en wordt niet ondersteund in productie.</span><span class="sxs-lookup"><span data-stu-id="f2560-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="f2560-109">Deze functie werkt momenteel alleen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="f2560-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-to-containerize-your-service-fabric-application"></a><span data-ttu-id="f2560-110">Stappen voor uw Service Fabric-toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="f2560-110">Steps to containerize your Service Fabric Application</span></span>

1. <span data-ttu-id="f2560-111">Open uw Service Fabric-toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2560-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="f2560-112">Klasse toevoegen [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) aan uw project.</span><span class="sxs-lookup"><span data-stu-id="f2560-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) to your project.</span></span> <span data-ttu-id="f2560-113">De code in deze klasse is een helper correct laden van de Service Fabric-runtime binaire bestanden in uw toepassing bij uitvoering binnen een container.</span><span class="sxs-lookup"><span data-stu-id="f2560-113">The code in this class is a helper to correctly load the Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="f2560-114">Voor elk codepakket dat u wilt containerize, initialiseren het laadprogramma op de programmavermelding verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f2560-114">For each code package you would like to containerize, initialize the loader at the program entry point.</span></span> <span data-ttu-id="f2560-115">De statische constructor weergegeven in het volgende codefragment aan het programma vermelding punt bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2560-115">Add the static constructor shown in the following code snippet to your program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is the entry point of the service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="f2560-116">Opbouwen en [pakket](service-fabric-package-apps.md#Package-App) uw project.</span><span class="sxs-lookup"><span data-stu-id="f2560-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="f2560-117">Voor het bouwen en maak een pakket, met de rechtermuisknop op de application-project in Solution Explorer en kiest u de **pakket** opdracht.</span><span class="sxs-lookup"><span data-stu-id="f2560-117">To build and create a package, right-click the application project in Solution Explorer and choose the **Package** command.</span></span>

5. <span data-ttu-id="f2560-118">Voor elke codepakket moet u containerize, voer de PowerShell-script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="f2560-118">For every code package you need to containerize, run the PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="f2560-119">Het gebruik is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f2560-119">The usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path to the code package to containerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for the generated docker folder.'
    $applicationExeName = 'Name of the ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="f2560-120">Het script maakt een map met Docker-artefacten op $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="f2560-120">The script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="f2560-121">Wijzig de gegenereerde Dockerfile naar eventuele poorten beschikbaar, voert u setup-scripts op basis van de behoeften van uw enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f2560-121">Modify the generated Dockerfile to expose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="f2560-122">Vervolgens moet u [bouwen](service-fabric-get-started-containers.md#Build-Containers) en [push](service-fabric-get-started-containers.md#Push-Containers) uw Docker-container-pakket naar uw opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f2560-122">Next you need to [build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package to your repository.</span></span>

7. <span data-ttu-id="f2560-123">Wijzig de ApplicationManifest.xml en ServiceManifest.xml als uw installatiekopie van de container, opslagplaats informatie, register-verificatie en toewijzing van de poort-naar-host wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2560-123">Modify the ApplicationManifest.xml and ServiceManifest.xml to add your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="f2560-124">Zie voor het wijzigen van de manifesten [maken van een toepassing Azure Service Fabric-container](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="f2560-124">For modifying the manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="f2560-125">De pakketdefinitie code in het servicemanifest moet worden vervangen door de bijbehorende container installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f2560-125">The code package definition in the service manifest needs to be replaced with corresponding container image.</span></span> <span data-ttu-id="f2560-126">Zorg ervoor dat het ingangspunt wijzigen in een ContainerHost-type.</span><span class="sxs-lookup"><span data-stu-id="f2560-126">Make sure to change the EntryPoint to a ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables to your container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="f2560-127">De toewijzing van de poort-naar-host voor de replicator en service-eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2560-127">Add the port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="f2560-128">Omdat beide deze poorten worden toegewezen tijdens runtime door Service Fabric, worden de ContainerPort is ingesteld op nul wordt op de toegewezen poort gebruiken voor de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="f2560-128">Since both these ports are assigned at runtime by Service Fabric, the ContainerPort is set to zero to use the assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="f2560-129">Testen van deze toepassing, moet u deze implementeren naar een cluster dat versie 5.7 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2560-129">To test this application, you need to deploy it to a cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="f2560-130">Bovendien hoeft te bewerken en bijwerken van de clusterinstellingen voor deze preview-functie.</span><span class="sxs-lookup"><span data-stu-id="f2560-130">In addition, you need to edit and update the cluster settings to enable this preview feature.</span></span> <span data-ttu-id="f2560-131">Volg de stappen in dit [artikel](service-fabric-cluster-fabric-settings.md) om toe te voegen van de instelling van de volgende weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2560-131">Follow the steps in this [article](service-fabric-cluster-fabric-settings.md) to add the setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="f2560-132">Volgende [implementeren](service-fabric-deploy-remove-applications.md) het bewerkte toepassingspakket aan dit cluster.</span><span class="sxs-lookup"><span data-stu-id="f2560-132">Next [deploy](service-fabric-deploy-remove-applications.md) the edited application package to this cluster.</span></span>

<span data-ttu-id="f2560-133">U hebt nu een beperkte Service Fabric-toepassing die het cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2560-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2560-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2560-134">Next steps</span></span>
* <span data-ttu-id="f2560-135">Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="f2560-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="f2560-136">Meer informatie over de [levenscyclus](service-fabric-application-lifecycle.md) van de Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2560-136">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
