---
title: Service Fabric Docker Compose Preview aaaAzure | Microsoft Docs
description: Azure Service Fabric-indeling toomake Docker Compose accepteert deze eenvoudiger tooorchestrate exsiting containers met behulp van Service Fabric. Deze ondersteuning is momenteel in preview.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="d8f27-104">Geven volume invoegtoepassingen en stuurprogramma's voor de container logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="d8f27-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="d8f27-105">Service Fabric ondersteunt het opgeven van [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) en [Docker-logboekregistratie stuurprogramma's](https://docs.docker.com/engine/admin/logging/overview/) voor uw containerservice.</span><span class="sxs-lookup"><span data-stu-id="d8f27-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="d8f27-106">Hallo invoegtoepassingen zijn opgegeven in Hallo toepassingsmanifest zoals weergegeven in de volgende manifest Hallo:</span><span class="sxs-lookup"><span data-stu-id="d8f27-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="d8f27-107">Hallo in Hallo voorgaande voorbeeld, `Source` tag voor Hallo `Volume` toohello bronmap verwijst.</span><span class="sxs-lookup"><span data-stu-id="d8f27-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="d8f27-108">Hallo bronmap mogelijk een map in Hallo VM die als host fungeert voor Hallo containers of een permanente externe opslag.</span><span class="sxs-lookup"><span data-stu-id="d8f27-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="d8f27-109">Hallo `Destination` tag is Hallo-locatie waar Hallo `Source` wordt toegewezen toowithin Hallo container uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d8f27-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="d8f27-110">Wanneer u een invoegtoepassing volume opgeeft, maakt Service Fabric automatisch Hallo volume met behulp van Hallo parameters opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d8f27-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="d8f27-111">Hallo `Source` tag heet Hallo Hallo volume en Hallo `Driver` code geeft Hallo volume stuurprogramma-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d8f27-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="d8f27-112">Opties kunnen worden opgegeven met behulp van Hallo `DriverOption` zoals weergegeven in het volgende codefragment Hallo tag:</span><span class="sxs-lookup"><span data-stu-id="d8f27-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="d8f27-113">Als een stuurprogramma Docker-logboek is opgegeven, is het nodig toodeploy agents (of containers) toohandle Hallo Hallo cluster zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="d8f27-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="d8f27-114">Hallo `DriverOption` tag gebruikte toospecify logboek stuurprogrammaopties ook kan worden.</span><span class="sxs-lookup"><span data-stu-id="d8f27-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="d8f27-115">Raadpleeg toohello artikelen toodeploy containers tooa Service Fabric-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="d8f27-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="d8f27-116">Een Service Fabric-container implementeren</span><span class="sxs-lookup"><span data-stu-id="d8f27-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

