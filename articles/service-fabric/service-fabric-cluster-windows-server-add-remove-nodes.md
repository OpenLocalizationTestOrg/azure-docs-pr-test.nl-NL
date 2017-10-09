---
title: aaaAdd of verwijder knooppunten tooa zelfstandige Service Fabric-cluster | Microsoft Docs
description: Meer informatie over hoe tooadd of verwijder knooppunten tooan Azure Service Fabric-cluster op een fysieke of virtuele machine met Windows Server, kan nu on-premises of in een cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster met Windows Server
Nadat u hebt [uw zelfstandige Service Fabric-cluster gemaakt op Windows Server-machines](service-fabric-cluster-creation-for-windows-server.md), behoeften van uw bedrijf kunnen worden gewijzigd en of u kunt mogelijk tooadd knooppunten tooyour cluster verwijderen. Dit artikel vindt gedetailleerde stappen tooachieve dit. Houd er rekening mee toevoegen of verwijderen knooppunt functionaliteit wordt niet ondersteund in lokale ontwikkeling clusters.

## <a name="add-nodes-tooyour-cluster"></a>Knooppunten tooyour cluster toevoegen
1. Prepare Hallo VM/machine tooadd tooyour cluster gewenste door Hallo stappen uit te voeren die worden vermeld in Hallo [voorbereiden Hallo machines toomeet Hallo vereisten voor de implementatie van het cluster](service-fabric-cluster-creation-for-windows-server.md) sectie
2. Identificeren welke foutdomein en u momenteel tooadd deze VM/machine bent upgradedomein
3. Extern bureaublad (RDP) naar Hallo VM/machine die u wilt dat tooadd toohello cluster
4. Kopieer of [Hallo zelfstandige pakket downloaden voor Service Fabric voor Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine en pak Hallo-pakket
5. Powershell uitvoeren met verhoogde bevoegdheden en navigeer toohello locatie van de uitgepakte Hallo-pakket
6. Voer Hallo *AddNode.ps1* script met met een beschrijving van het nieuwe knooppunt tooadd Hallo Hallo-parameters. Hallo voorbeeld hieronder wordt een nieuw knooppunt VM5 aangeroepen, met het type NodeType0 en IP-adres 182.17.34.52, in UD1 en fd: / dc1/r0. Hallo *ExistingClusterConnectionEndPoint* nog een eindpunt voor de verbinding voor een knooppunt bestaand cluster hello, wat kan zijn Hallo IP-adres van *eventuele* knooppunt in Hallo cluster.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Zodra het Hallo-script is voltooid, kunt u controleren of Hallo nieuw knooppunt is toegevoegd door het uitvoeren van Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.

7. tooensure consistentie op verschillende knooppunten in cluster hello, moet u een configuratie-upgrade initiëren. Uitvoeren [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget nieuwste configuratiebestand Hallo en toe te voegen toegevoegde knooppunt te Hallo 'Knooppunten'-sectie. Ook wordt u aangeraden tooalways Hallo recentste clusterconfiguratie beschikbaar in Hallo geval moet u een cluster met Hallo tooredploy hebben dezelfde configuratie.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer. U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Toevoegen van knooppunten tooclusters geconfigureerd met behulp van gMSA Windows-beveiliging
Clusters die zijn geconfigureerd met een groep beheerde Service Account(gMSA) (https://technet.microsoft.com/library/hh831782.aspx), worden een nieuw knooppunt toegevoegd met behulp van een upgrade van een configuratie:
1. Voer [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) op een van de bestaande knooppunten Hallo tooget nieuwste configuratiebestand Hallo en details toevoegen over een nieuw knooppunt Hallo gewenste tooadd in de sectie Hallo 'knooppunten'. Zorg ervoor dat het nieuwe knooppunt Hallo deel uitmaakt van Hallo dezelfde beheerd account groep. Deze account moet een beheerder zijn op alle machines.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer. U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Knooppunt typen tooyour cluster toevoegen
In volgorde tooadd een nieuw knooppunttype, de configuratie tooinclude Hallo nieuwe knooppunttype in de sectie 'NodeTypes' onder 'Eigenschappen' wijzigen en beginnen met een configuratie met behulp van upgrade [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Zodra het Hallo-upgrade is voltooid, kunt u nieuwe knooppunten tooyour cluster toevoegen aan dit knooppunttype.

## <a name="remove-nodes-from-your-cluster"></a>Knooppunten van het cluster verwijderen
Een knooppunt kan worden verwijderd uit een cluster met behulp van de upgrade van een configuratie in Hallo manier te volgen:

1. Uitvoeren [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Hallo nieuwste configuratiebestand en *verwijderen* Hallo knooppunt uit de sectie 'Knooppunten'.
Hallo 'NodesToBeRemoved' toevoegen parameter te 'instellingen' sectie in de sectie 'FabricSettings'. Hallo '' waarde '' moet een door komma's gescheiden lijst met knooppuntnamen van knooppunten die toobe verwijderd moeten.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer. U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> Verwijderen van knooppunten mogelijk meerdere upgrades initiëren. Sommige knooppunten zijn gemarkeerd met `IsSeedNode=”true”` labelen en kan worden geïdentificeerd door het uitvoeren van query's Hallo cluster manifest met `Get-ServiceFabricClusterManifest`. Verwijderen van deze knooppunten kan het langer duren dan andere omdat Hallo seed-knooppunten toobe verplaatst in dergelijke scenario's. Hallo-cluster moet minimaal 3 primaire knooppunt type knooppunten onderhouden.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Knooppunttypen verwijderen uit het cluster
Voordat u een knooppunttype verwijdert, Controleer als er knooppunten verwijzen naar Hallo knooppunttype. Verwijder deze knooppunten voordat u de bijbehorende knooppunttype Hallo verwijdert. Zodra alle bijbehorende knooppunten zijn verwijderd, kunt u Hallo NodeType verwijderen uit de clusterconfiguratie Hallo en beginnen met een configuratie met behulp van upgrade [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Vervang primaire knooppunten van het cluster
Hallo vervanging van primaire knooppunten moet één knooppunt uitgevoerd na de andere in plaats van te verwijderen en vervolgens toe te voegen in batches.


## <a name="next-steps"></a>Volgende stappen
* [Configuratie-instellingen voor zelfstandige Windows-cluster](service-fabric-cluster-manifest.md)
* [Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten](service-fabric-windows-cluster-x509-security.md)
* [Een zelfstandige Service Fabric-cluster maken met Azure Virtual machines waarop Windows wordt uitgevoerd](service-fabric-cluster-creation-with-windows-azure-vms.md)

