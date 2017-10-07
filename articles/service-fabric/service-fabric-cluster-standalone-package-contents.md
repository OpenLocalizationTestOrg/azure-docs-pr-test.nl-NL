---
title: aaaAzure Service Fabric zelfstandige-pakket voor Windows Server | Microsoft Docs
description: Beschrijving en de inhoud van hello Azure Service Fabric Standalone-pakket voor Windows Server.
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Inhoud van de zelfstandige versie van Service Fabric-pakket voor Windows Server
In Hallo [gedownload](http://go.microsoft.com/fwlink/?LinkId=730690) zelfstandige voor Service Fabric-pakket, vindt u Hallo volgende bestanden:

| **Bestandsnaam** | **Korte beschrijving** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Een PowerShell-script waarmee het Hallo-cluster met Hallo-instellingen in ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Een PowerShell-script dat wordt verwijderd van een cluster met Hallo-instellingen in ClusterConfig.json. |
| AddNode.ps1 |Een PowerShell-script voor het toevoegen van een knooppunt tooan bestaande cluster op de huidige computer Hallo geïmplementeerd. |
| RemoveNode.ps1 |Een PowerShell-script voor het verwijderen van een knooppunt van een bestaand cluster met de huidige machine Hallo geïmplementeerd. |
| CleanFabric.ps1 |Een PowerShell-script voor het reinigen van een zelfstandige installatie van Service Fabric Hallo huidige machine uit. Vorige MSI-installaties moeten worden verwijderd met behulp van hun eigen uninstallers gekoppeld. |
| TestConfiguration.ps1 |Een PowerShell-script voor het analyseren van Hallo infrastructuur zoals opgegeven in Hallo Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Een PowerShell-script gebruikt voor het downloaden van het meest recente runtime-pakket Hallo buiten band zijn, voor scenario's waarin Hallo implementeren machine niet toohello verbonden internet. |
| DeploymentComponentsAutoextractor.exe |Zelfuitpakkende archief met van onderdelen voor implementatie gebruikt door Hallo zelfstandige pakket scripts. |
| EULA_ENU.txt |Hallo-licentievoorwaarden voor Hallo gebruik van Microsoft Azure Service Fabric zelfstandig pakket met Windows Server. U kunt [download een exemplaar van Hallo overeenkomst](http://go.microsoft.com/fwlink/?LinkID=733084) nu. |
| Leesmij |Een koppeling toohello releaseopmerkingen en eenvoudige installatie-instructies. Dit is een subset van Hallo-instructies in dit document. |
| ThirdPartyNotice.rtf |De aankondiging van de software van derden die in het Hallo-pakket. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe die wordt uitgevoerd op aanvraag toocollect en uploaden trace logboeken tooMicrosoft voor ondersteuning doel. |
| Tools\ServiceFabricUpdateService.zip |Een hulpprogramma gebruikt tooenable automatisch code-upgrade voor clusters waarvoor geen toegang tot internet. Meer informatie vindt u [hier](service-fabric-cluster-upgrade-windows-server.md)|

**Sjablonen** 
| **Bestandsnaam** | **Korte beschrijving** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Een cluster voorbeeld configuratiebestand dat Hallo-instellingen voor een onbeveiligde, drie-knooppunt, single-(of virtuele machine) ontwikkeling cluster, inclusief Hallo-informatie voor elk knooppunt in het Hallo-cluster bevat. |
| ClusterConfig.Unsecure.MultiMachine.json |Een cluster voorbeeld configuratiebestand dat Hallo-instellingen voor een niet-beveiligde, meerdere (of virtuele machine)-cluster, inclusief Hallo-informatie voor elke computer in Hallo cluster bevat. |
| ClusterConfig.Windows.DevCluster.json |Een cluster voorbeeld configuratiebestand met alle Hallo-instellingen voor een veilige, drie-knooppunt, single-(of virtuele machine) ontwikkelcluster, met inbegrip van Hallo-informatie voor elk knooppunt in het Hallo-cluster. Hallo-cluster is beveiligd met behulp van [Windows identiteiten](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Een cluster voorbeeld configuratiebestand dat alle Hallo-instellingen voor een veilige, meerdere (of virtuele machine)-cluster met behulp van Windows-beveiliging, met inbegrip van informatie voor elke machine die zich in de beveiligde cluster Hallo Hallo bevat. Hallo-cluster is beveiligd met behulp van [Windows identiteiten](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Een cluster voorbeeld configuratiebestand met alle Hallo-instellingen voor een veilige, drie knooppunten single-(of virtuele machine) ontwikkeling cluster, inclusief Hallo-informatie voor elk knooppunt in het Hallo-cluster. Hallo cluster is beveiligd met x509 certificaten. |
| ClusterConfig.x509.MultiMachine.json |Een cluster voorbeeld configuratiebestand dat alle Hallo-instellingen voor Hallo veilige, meerdere (of virtuele machine) cluster, inclusief Hallo-informatie voor elk knooppunt in Hallo beveiligde cluster bevat. Hallo cluster is beveiligd met x509 certificaten. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Een cluster voorbeeld configuratiebestand dat alle Hallo-instellingen voor Hallo veilige, meerdere (of virtuele machine) cluster, inclusief Hallo-informatie voor elk knooppunt in Hallo beveiligde cluster bevat. Hallo cluster is beveiligd met [Group Managed Service Accounts](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Voorbeelden van de cluster-configuratie
Meest recente versies van de configuratiesjablonen cluster kunnen worden gevonden op Hallo GitHub-pagina: [zelfstandige Cluster configuratie voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Onafhankelijke Runtime-pakket
Hallo nieuwste runtime-pakket wordt automatisch gedownload tijdens de implementatie van het cluster uit [- Service Fabric-Runtime - koppeling Download Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Verwant
* [Een zelfstandige Azure Service Fabric-cluster maken](service-fabric-cluster-creation-for-windows-server.md)
* [Scenario's voor beveiliging van service Fabric-cluster](service-fabric-windows-cluster-windows-security.md)
