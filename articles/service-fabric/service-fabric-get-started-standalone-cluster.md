---
title: aaaSet een zelfstandige Azure Service Fabric-cluster | Microsoft Docs
description: Maken van een zelfstandige ontwikkelcluster met drie knooppunten uitgevoerd op Hallo dezelfde computer. Na het voltooien van deze installatie, kunt u zich gereed toocreate cluster met meerdere machines.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Uw eerste zelfstandige Service Fabric-cluster maken
U kunt een zelfstandige Service Fabric-cluster maken op elke virtuele machines of computers waarop Windows Server 2012 R2 of Windows Server 2016, lokaal of in Hallo cloud. Deze snelstartgids kunt u een zelfstandige ontwikkelcluster toocreate in slechts enkele minuten.  Wanneer u klaar bent, hebt u een cluster met drie knooppunten die worden uitgevoerd op één computer. Hierop kunt u vervolgens apps implementeren.

## <a name="before-you-begin"></a>Voordat u begint
Service Fabric bevat een setup-pakket toocreate Service Fabric zelfstandige clusters.  [Hallo-installatiepakket downloaden](http://go.microsoft.com/fwlink/?LinkId=730690).  Pak Hallo setup tooa pakketmap op Hallo computer of virtuele machine waar u Hallo ontwikkelcluster instelt.  Hallo-inhoud van het Hallo-installatiepakket worden gedetailleerd beschreven [hier](service-fabric-cluster-standalone-package-contents.md).

Hallo Clusterbeheer implementeren en configureren van Hallo cluster moet administrator-bevoegdheden hebben op Hallo-computer. U kunt Service Fabric niet installeren op een domeincontroller.

## <a name="validate-hello-environment"></a>Hallo-omgeving valideren
Hallo *TestConfiguration.ps1* script in Hallo zelfstandige pakket wordt gebruikt als een best practices analyzer toovalidate of een cluster kan worden geïmplementeerd op een bepaalde omgeving. [Implementatie voorbereiden](service-fabric-cluster-standalone-deployment-preparation.md) lijsten Hallo vereisten en vereisten. Hallo script tooverify uitvoeren als u Hallo ontwikkelcluster kunt maken:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Hallo-cluster maken
Verschillende cluster configuratie voorbeeldbestanden worden geïnstalleerd met Hallo-installatiepakket. *ClusterConfig.Unsecure.DevCluster.json* is de eenvoudigste clusterconfiguratie Hallo: een onbeveiligde, drie-node cluster uitgevoerd op een enkele computer.  Andere configuratiebestanden beschrijven clusters voor één of meerdere machines die zijn beveiligd met een x.509-certificaat of met Windows-beveiliging.  U niet toomodify Hallo standaard configuratie-instellingen nodig voor deze zelfstudie, maar bekijkt hello configuratiebestand en raken met het Hallo-instellingen.  Hallo **knooppunten** sectie wordt beschreven Hallo drie knooppunten in cluster Hallo: naam, IP-adres, [knooppunttype foutdomein en upgradedomein](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Hallo **eigenschappen** sectie definieert Hallo [beveiliging, niveau van betrouwbaarheid, de verzameling diagnostische gegevens en soorten knooppunten](service-fabric-cluster-manifest.md#cluster-properties) voor Hallo-cluster.

Dit cluster is onveilig.  Iedereen kan anoniem verbinding maken en beheerbewerkingen uitvoeren. Productieclusters moeten dus altijd worden beveiligd met X.509-certificaten of Windows-beveiliging.  Beveiliging alleen tijdens het maken van een cluster is geconfigureerd en is niet mogelijk tooenable beveiliging nadat Hallo-cluster is gemaakt.  Lees [beveiligen van een cluster](service-fabric-cluster-security.md) toolearn meer over de beveiliging van de Service Fabric-cluster.  

toocreate hello drie knooppunten ontwikkelcluster, Voer Hallo *CreateServiceFabricCluster.ps1* script van een beheerder PowerShell-sessie:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Hallo Service Fabric-runtime-pakket wordt automatisch gedownload en geïnstalleerd tijdens het maken van het cluster.

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello
Het ontwikkelingscluster met drie knooppunten wordt nu uitgevoerd. Hallo runtime is Hallo ServiceFabric PowerShell-module geïnstalleerd.  U kunt controleren dat Hallo-cluster wordt uitgevoerd op Hallo dezelfde computer of vanaf een externe computer met Hallo Service Fabric-runtime.  Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stelt een verbinding toohello-cluster.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor andere voorbeelden van verbindende tooa cluster. Na het maken van verbinding toohello-cluster gebruiken Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet een lijst met knooppunten in het Hallo-cluster en de status van informatie voor elk knooppunt. **HealthState** moet *OK* zijn voor elk knooppunt.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Hallo-cluster met Service Fabric explorer visualiseren
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een goed hulpmiddel om een cluster te visualiseren en toepassingen te beheren.  Service Fabric Explorer is een service die wordt uitgevoerd in Hallo-cluster dat u via een browser openen door te navigeren[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). 

Hallo cluster-dashboard biedt een overzicht van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status. Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster. Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Hallo-cluster verwijderen
tooremove een cluster uitvoert Hallo *RemoveServiceFabricCluster.ps1* PowerShell-script van de pakketmap Hallo en geeft u Hallo pad toohello JSON-configuratiebestand. U kunt optioneel een locatie voor Hallo logboek van Hallo verwijdering opgeven.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove hello Service Fabric-runtime vanaf Hallo-computer, Hallo volgende PowerShell-script uit Hallo pakketmap worden uitgevoerd.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Volgende stappen
Nu u een zelfstandige ontwikkelcluster hebt ingesteld, proberen Hallo artikelen te volgen:
* [Een zelfstandig cluster met meerdere machines instellen](service-fabric-cluster-creation-for-windows-server.md) en beveiliging inschakelen.
* [Apps implementeren met behulp van Powershell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
