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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Geven volume invoegtoepassingen en stuurprogramma's voor de container logboekregistratie

Service Fabric ondersteunt het opgeven van [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) en [Docker-logboekregistratie stuurprogramma's](https://docs.docker.com/engine/admin/logging/overview/) voor uw containerservice. Hallo invoegtoepassingen zijn opgegeven in Hallo toepassingsmanifest zoals weergegeven in de volgende manifest Hallo:


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

Hallo in Hallo voorgaande voorbeeld, `Source` tag voor Hallo `Volume` toohello bronmap verwijst. Hallo bronmap mogelijk een map in Hallo VM die als host fungeert voor Hallo containers of een permanente externe opslag. Hallo `Destination` tag is Hallo-locatie waar Hallo `Source` wordt toegewezen toowithin Hallo container uitgevoerd. 

Wanneer u een invoegtoepassing volume opgeeft, maakt Service Fabric automatisch Hallo volume met behulp van Hallo parameters opgegeven. Hallo `Source` tag heet Hallo Hallo volume en Hallo `Driver` code geeft Hallo volume stuurprogramma-invoegtoepassing. Opties kunnen worden opgegeven met behulp van Hallo `DriverOption` zoals weergegeven in het volgende codefragment Hallo tag:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Als een stuurprogramma Docker-logboek is opgegeven, is het nodig toodeploy agents (of containers) toohandle Hallo Hallo cluster zich aanmeldt.  Hallo `DriverOption` tag gebruikte toospecify logboek stuurprogrammaopties ook kan worden.

Raadpleeg toohello artikelen toodeploy containers tooa Service Fabric-cluster te volgen:


[Een Service Fabric-container implementeren](service-fabric-deploy-container.md)

