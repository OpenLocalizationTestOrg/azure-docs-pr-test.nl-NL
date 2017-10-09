---
title: aaaHow toocontainerize uw Azure Service Fabric-microservices (preview)
description: Azure Service Fabric is nieuwe functionaliteit toocontainerize uw Service Fabric-microservices toegevoegd. Deze functie is momenteel beschikbaar als preview-product.
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
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="15baf-104">Hoe toocontainerize uw Service Fabric-betrouwbaar Services en Reliable Actors (Preview)</span><span class="sxs-lookup"><span data-stu-id="15baf-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="15baf-105">Service Fabric ondersteunt containerizing Service Fabric-microservices (Reliable Services en betrouwbare op basis van actorservices).</span><span class="sxs-lookup"><span data-stu-id="15baf-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="15baf-106">Zie voor meer informatie [service fabric-containers](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15baf-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="15baf-107">Deze functie is een Preview-versie en dit artikel bevat verschillende stappen tooget Hallo uw uitgevoerd binnen een container service.</span><span class="sxs-lookup"><span data-stu-id="15baf-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="15baf-108">Deze functie is Preview-versie en wordt niet ondersteund in productie.</span><span class="sxs-lookup"><span data-stu-id="15baf-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="15baf-109">Deze functie werkt momenteel alleen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="15baf-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="15baf-110">Stappen toocontainerize uw Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="15baf-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="15baf-111">Open uw Service Fabric-toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15baf-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="15baf-112">Klasse toevoegen [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span><span class="sxs-lookup"><span data-stu-id="15baf-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="15baf-113">Hallo-code in deze klasse is een helper toocorrectly load Hallo Service Fabric-runtime binaire bestanden in uw toepassing bij uitvoering binnen een container.</span><span class="sxs-lookup"><span data-stu-id="15baf-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="15baf-114">U wilt voor elk codepakket toocontainerize, initialiseren Hallo loader op Hallo programma toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="15baf-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="15baf-115">Hallo statische constructor weergegeven in het volgende codefragment tooyour programma vermelding punt codebestand Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15baf-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

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
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="15baf-116">Opbouwen en [pakket](service-fabric-package-apps.md#Package-App) uw project.</span><span class="sxs-lookup"><span data-stu-id="15baf-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="15baf-117">toobuild en maak een pakket, met de rechtermuisknop op Hallo application-project in Solution Explorer en kiest u Hallo **pakket** opdracht.</span><span class="sxs-lookup"><span data-stu-id="15baf-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="15baf-118">Voor elke codepakket moet u toocontainerize, Voer Hallo PowerShell-script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="15baf-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="15baf-119">Hallo-gebruik is als volgt:</span><span class="sxs-lookup"><span data-stu-id="15baf-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="15baf-120">Hallo script maakt een map met Docker-artefacten op $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="15baf-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="15baf-121">Hallo gegenereerd Dockerfile tooexpose alle poorten, setup scripts op basis van de behoeften van uw enzovoort uitvoeren wijzigen.</span><span class="sxs-lookup"><span data-stu-id="15baf-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="15baf-122">Vervolgens dient u te[bouwen](service-fabric-get-started-containers.md#Build-Containers) en [push](service-fabric-get-started-containers.md#Push-Containers) uw Docker-container pakket tooyour opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="15baf-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="15baf-123">Hallo ApplicationManifest.xml en ServiceManifest.xml tooadd wijzigen uw installatiekopie van de container, opslagplaats informatie, register-verificatie en toewijzing van de poort-naar-host.</span><span class="sxs-lookup"><span data-stu-id="15baf-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="15baf-124">Zie voor het wijzigen van de manifesten Hallo [maken van een toepassing Azure Service Fabric-container](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="15baf-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="15baf-125">Hallo code pakketdefinitie in Hallo service manifest behoeften toobe vervangen door de bijbehorende container installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="15baf-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="15baf-126">Zorg ervoor dat toochange Hallo EntryPoint tooa ContainerHost type.</span><span class="sxs-lookup"><span data-stu-id="15baf-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="15baf-127">Hallo-poort-naar-host-toewijzing voor de replicator en service-eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15baf-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="15baf-128">Omdat beide deze poorten worden toegewezen tijdens runtime door Service Fabric, kan Hallo ContainerPort toozero toouse Hallo toegewezen poort voor de toewijzing is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="15baf-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="15baf-129">tootest deze toepassing, moet u toodeploy het tooa-cluster dat versie 5.7 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="15baf-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="15baf-130">Bovendien moet tooedit en bijwerken Hallo cluster instellingen tooenable deze preview-functie.</span><span class="sxs-lookup"><span data-stu-id="15baf-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="15baf-131">Hallo stappen in dit [artikel](service-fabric-cluster-fabric-settings.md) tooadd Hallo instelling volgende weergegeven.</span><span class="sxs-lookup"><span data-stu-id="15baf-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
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
10. <span data-ttu-id="15baf-132">Volgende [implementeren](service-fabric-deploy-remove-applications.md) Hallo toepassing pakket toothis cluster bewerkt.</span><span class="sxs-lookup"><span data-stu-id="15baf-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="15baf-133">U hebt nu een beperkte Service Fabric-toepassing die het cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="15baf-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15baf-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15baf-134">Next steps</span></span>
* <span data-ttu-id="15baf-135">Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="15baf-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="15baf-136">Meer informatie over Service Fabric Hallo [toepassing levenscyclus](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="15baf-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
