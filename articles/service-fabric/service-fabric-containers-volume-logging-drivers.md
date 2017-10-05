---
title: Azure Service Fabric Docker Compose Preview | Microsoft Docs
description: Azure Service Fabric accepteert Docker Compose indeling u indeelt exsiting containers met behulp van Service Fabric te vereenvoudigen. Deze ondersteuning is momenteel in preview.
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
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="0342b-104">Geven volume invoegtoepassingen en stuurprogramma's voor de container logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="0342b-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="0342b-105">Service Fabric ondersteunt het opgeven van [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) en [Docker-logboekregistratie stuurprogramma's](https://docs.docker.com/engine/admin/logging/overview/) voor uw containerservice.</span><span class="sxs-lookup"><span data-stu-id="0342b-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="0342b-106">De invoegtoepassingen zijn opgegeven in het toepassingsmanifest, zoals wordt weergegeven in het manifest van de volgende:</span><span class="sxs-lookup"><span data-stu-id="0342b-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


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

<span data-ttu-id="0342b-107">In het voorgaande voorbeeld de `Source` tag voor de `Volume` verwijst naar de bronmap.</span><span class="sxs-lookup"><span data-stu-id="0342b-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="0342b-108">De bronmap wordt mogelijk een map in de virtuele machine die als host fungeert voor de containers of een permanente externe opslag.</span><span class="sxs-lookup"><span data-stu-id="0342b-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="0342b-109">De `Destination` label is de locatie die het `Source` is toegewezen aan in de actieve container.</span><span class="sxs-lookup"><span data-stu-id="0342b-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="0342b-110">Wanneer u een invoegtoepassing volume opgeeft, maakt Service Fabric automatisch het volume met de opgegeven parameters.</span><span class="sxs-lookup"><span data-stu-id="0342b-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="0342b-111">De `Source` label is de naam van het volume en de `Driver` tag geeft de stuurprogramma-invoegtoepassing voor volume.</span><span class="sxs-lookup"><span data-stu-id="0342b-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="0342b-112">Opties kunnen worden opgegeven met behulp van de `DriverOption` tag zoals weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="0342b-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="0342b-113">Als een stuurprogramma Docker-logboek is opgegeven, is het voor het implementeren van agents (of containers) voor het afhandelen van de logboeken in het cluster.</span><span class="sxs-lookup"><span data-stu-id="0342b-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="0342b-114">De `DriverOption` label kan worden gebruikt om op te geven, evenals stuurprogramma-opties in logboek.</span><span class="sxs-lookup"><span data-stu-id="0342b-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="0342b-115">Raadpleeg de volgende artikelen voor het implementeren van containers naar een Service Fabric-cluster:</span><span class="sxs-lookup"><span data-stu-id="0342b-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="0342b-116">Een Service Fabric-container implementeren</span><span class="sxs-lookup"><span data-stu-id="0342b-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

