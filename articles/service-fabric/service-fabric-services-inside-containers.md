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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Hoe toocontainerize uw Service Fabric-betrouwbaar Services en Reliable Actors (Preview)

Service Fabric ondersteunt containerizing Service Fabric-microservices (Reliable Services en betrouwbare op basis van actorservices). Zie voor meer informatie [service fabric-containers](service-fabric-containers-overview.md).


 Deze functie is een Preview-versie en dit artikel bevat verschillende stappen tooget Hallo uw uitgevoerd binnen een container service.  

> [!NOTE]
> Deze functie is Preview-versie en wordt niet ondersteund in productie. Deze functie werkt momenteel alleen voor Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Stappen toocontainerize uw Service Fabric-toepassing

1. Open uw Service Fabric-toepassing in Visual Studio.

2. Klasse toevoegen [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project. Hallo-code in deze klasse is een helper toocorrectly load Hallo Service Fabric-runtime binaire bestanden in uw toepassing bij uitvoering binnen een container.

3. U wilt voor elk codepakket toocontainerize, initialiseren Hallo loader op Hallo programma toegangspunt. Hallo statische constructor weergegeven in het volgende codefragment tooyour programma vermelding punt codebestand Hallo toevoegen.

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

4. Opbouwen en [pakket](service-fabric-package-apps.md#Package-App) uw project. toobuild en maak een pakket, met de rechtermuisknop op Hallo application-project in Solution Explorer en kiest u Hallo **pakket** opdracht.

5. Voor elke codepakket moet u toocontainerize, Voer Hallo PowerShell-script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). Hallo-gebruik is als volgt:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  Hallo script maakt een map met Docker-artefacten op $dockerPackageOutputDirectoryPath. Hallo gegenereerd Dockerfile tooexpose alle poorten, setup scripts op basis van de behoeften van uw enzovoort uitvoeren wijzigen.

6. Vervolgens dient u te[bouwen](service-fabric-get-started-containers.md#Build-Containers) en [push](service-fabric-get-started-containers.md#Push-Containers) uw Docker-container pakket tooyour opslagplaats.

7. Hallo ApplicationManifest.xml en ServiceManifest.xml tooadd wijzigen uw installatiekopie van de container, opslagplaats informatie, register-verificatie en toewijzing van de poort-naar-host. Zie voor het wijzigen van de manifesten Hallo [maken van een toepassing Azure Service Fabric-container](service-fabric-get-started-containers.md). Hallo code pakketdefinitie in Hallo service manifest behoeften toobe vervangen door de bijbehorende container installatiekopie. Zorg ervoor dat toochange Hallo EntryPoint tooa ContainerHost type.

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

8. Hallo-poort-naar-host-toewijzing voor de replicator en service-eindpunt toevoegen. Omdat beide deze poorten worden toegewezen tijdens runtime door Service Fabric, kan Hallo ContainerPort toozero toouse Hallo toegewezen poort voor de toewijzing is ingesteld.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest deze toepassing, moet u toodeploy het tooa-cluster dat versie 5.7 of hoger wordt uitgevoerd. Bovendien moet tooedit en bijwerken Hallo cluster instellingen tooenable deze preview-functie. Hallo stappen in dit [artikel](service-fabric-cluster-fabric-settings.md) tooadd Hallo instelling volgende weergegeven.
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
10. Volgende [implementeren](service-fabric-deploy-remove-applications.md) Hallo toepassing pakket toothis cluster bewerkt.

U hebt nu een beperkte Service Fabric-toepassing die het cluster wordt uitgevoerd.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-get-started-containers.md).
* Meer informatie over Service Fabric Hallo [toepassing levenscyclus](service-fabric-application-lifecycle.md).
