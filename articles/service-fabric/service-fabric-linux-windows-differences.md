---
title: Service Fabric aaaAzure verschillen tussen de Linux- en Windows | Microsoft Docs
description: Verschillen tussen hello Azure Service Fabric Preview op Linux- en Azure Service Fabric in Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a>Verschillen tussen Service Fabric in Linux (preview) en Service Fabric in Windows (algemeen beschikbaar)

Omdat Service Fabric in Linux een preview-versie is, zijn er enkele functies die wel worden ondersteund in Windows, maar nog niet in Linux. Uiteindelijk zich Hallo functiesets aan pariteit zodra het Service Fabric op Linux in het algemeen beschikbaar. In toekomstige versies worden de verschillen in functies steeds kleiner. Hallo volgende verschillen bestaan tussen Hallo meest recente beschikbare versies (dat wil zeggen, tussen versie 5.6 voor Windows en versie 5.5 op Linux): 

* Betrouwbare verzamelingen (en betrouwbare stateful services) 
* ReverseProxy 
* Zelfstandig installatieprogramma 
* XML-schemavalidatie voor manifestbestanden 
* Consoleomleiding 
* Hallo veroorzaakt Analysis Service (door)
* Docker Compose-volume en logboekregistratiestuurprogramma's voor containers 
* Resourcebeheer voor containers en services 
* DNS-service
* Ondersteuning van Azure Active Directory
* CLI-opdrachtequivalenten van bepaalde Powershell-opdrachten 
* Alleen een subset van de Powershell-opdrachten kan worden uitgevoerd op een Linux-cluster (zoals uitgevouwen in de volgende sectie Hallo).

>[!NOTE]
>Console-omleiding wordt niet ondersteund in productieclusters, ook niet in Windows.

De hulpmiddelen voor ontwikkelaars verschillen ook tussen Windows en Linux. VisualStudio, Powershell VSTS en ETW worden gebruikt op Windows terwijl Yeoman, Eclipse, Jenkins en LTTng op Linux worden gebruikt.

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>PowerShell-cmdlets die niet werken voor een Service Fabric-cluster in Linux

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Cmd
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>Volgende stappen
* [Uw ontwikkelomgeving voorbereiden in Linux](service-fabric-get-started-linux.md)
* [Uw ontwikkelomgeving voorbereiden in OSX](service-fabric-get-started-mac.md)
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Uw eerste Service Fabric Java-toepassing in Linux maken en implementeren met behulp van de Service Fabric-invoegtoepassing voor Eclipse](service-fabric-get-started-eclipse.md)
* [Uw eerste CSharp-toepassing in Linux maken](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Hallo Service Fabric CLI toomanage uw toepassingen gebruiken](service-fabric-application-lifecycle-sfctl.md)
