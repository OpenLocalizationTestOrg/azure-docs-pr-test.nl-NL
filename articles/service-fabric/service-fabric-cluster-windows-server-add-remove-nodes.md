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
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="4422f-103">Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster met Windows Server</span><span class="sxs-lookup"><span data-stu-id="4422f-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="4422f-104">Nadat u hebt [uw zelfstandige Service Fabric-cluster gemaakt op Windows Server-machines](service-fabric-cluster-creation-for-windows-server.md), behoeften van uw bedrijf kunnen worden gewijzigd en of u kunt mogelijk tooadd knooppunten tooyour cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4422f-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="4422f-105">Dit artikel vindt gedetailleerde stappen tooachieve dit.</span><span class="sxs-lookup"><span data-stu-id="4422f-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="4422f-106">Houd er rekening mee toevoegen of verwijderen knooppunt functionaliteit wordt niet ondersteund in lokale ontwikkeling clusters.</span><span class="sxs-lookup"><span data-stu-id="4422f-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="4422f-107">Knooppunten tooyour cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="4422f-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="4422f-108">Prepare Hallo VM/machine tooadd tooyour cluster gewenste door Hallo stappen uit te voeren die worden vermeld in Hallo [voorbereiden Hallo machines toomeet Hallo vereisten voor de implementatie van het cluster](service-fabric-cluster-creation-for-windows-server.md) sectie</span><span class="sxs-lookup"><span data-stu-id="4422f-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="4422f-109">Identificeren welke foutdomein en u momenteel tooadd deze VM/machine bent upgradedomein</span><span class="sxs-lookup"><span data-stu-id="4422f-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="4422f-110">Extern bureaublad (RDP) naar Hallo VM/machine die u wilt dat tooadd toohello cluster</span><span class="sxs-lookup"><span data-stu-id="4422f-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="4422f-111">Kopieer of [Hallo zelfstandige pakket downloaden voor Service Fabric voor Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine en pak Hallo-pakket</span><span class="sxs-lookup"><span data-stu-id="4422f-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="4422f-112">Powershell uitvoeren met verhoogde bevoegdheden en navigeer toohello locatie van de uitgepakte Hallo-pakket</span><span class="sxs-lookup"><span data-stu-id="4422f-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="4422f-113">Voer Hallo *AddNode.ps1* script met met een beschrijving van het nieuwe knooppunt tooadd Hallo Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="4422f-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="4422f-114">Hallo voorbeeld hieronder wordt een nieuw knooppunt VM5 aangeroepen, met het type NodeType0 en IP-adres 182.17.34.52, in UD1 en fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="4422f-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="4422f-115">Hallo *ExistingClusterConnectionEndPoint* nog een eindpunt voor de verbinding voor een knooppunt bestaand cluster hello, wat kan zijn Hallo IP-adres van *eventuele* knooppunt in Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="4422f-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="4422f-116">Zodra het Hallo-script is voltooid, kunt u controleren of Hallo nieuw knooppunt is toegevoegd door het uitvoeren van Hallo [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4422f-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="4422f-117">tooensure consistentie op verschillende knooppunten in cluster hello, moet u een configuratie-upgrade initiëren.</span><span class="sxs-lookup"><span data-stu-id="4422f-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="4422f-118">Uitvoeren [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget nieuwste configuratiebestand Hallo en toe te voegen toegevoegde knooppunt te Hallo 'Knooppunten'-sectie.</span><span class="sxs-lookup"><span data-stu-id="4422f-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="4422f-119">Ook wordt u aangeraden tooalways Hallo recentste clusterconfiguratie beschikbaar in Hallo geval moet u een cluster met Hallo tooredploy hebben dezelfde configuratie.</span><span class="sxs-lookup"><span data-stu-id="4422f-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="4422f-120">Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.</span><span class="sxs-lookup"><span data-stu-id="4422f-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="4422f-121">U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4422f-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4422f-122">U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4422f-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="4422f-123">Toevoegen van knooppunten tooclusters geconfigureerd met behulp van gMSA Windows-beveiliging</span><span class="sxs-lookup"><span data-stu-id="4422f-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="4422f-124">Clusters die zijn geconfigureerd met een groep beheerde Service Account(gMSA) (https://technet.microsoft.com/library/hh831782.aspx), worden een nieuw knooppunt toegevoegd met behulp van een upgrade van een configuratie:</span><span class="sxs-lookup"><span data-stu-id="4422f-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="4422f-125">Voer [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) op een van de bestaande knooppunten Hallo tooget nieuwste configuratiebestand Hallo en details toevoegen over een nieuw knooppunt Hallo gewenste tooadd in de sectie Hallo 'knooppunten'.</span><span class="sxs-lookup"><span data-stu-id="4422f-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="4422f-126">Zorg ervoor dat het nieuwe knooppunt Hallo deel uitmaakt van Hallo dezelfde beheerd account groep.</span><span class="sxs-lookup"><span data-stu-id="4422f-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="4422f-127">Deze account moet een beheerder zijn op alle machines.</span><span class="sxs-lookup"><span data-stu-id="4422f-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="4422f-128">Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.</span><span class="sxs-lookup"><span data-stu-id="4422f-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="4422f-129">U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4422f-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4422f-130">U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4422f-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="4422f-131">Knooppunt typen tooyour cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="4422f-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="4422f-132">In volgorde tooadd een nieuw knooppunttype, de configuratie tooinclude Hallo nieuwe knooppunttype in de sectie 'NodeTypes' onder 'Eigenschappen' wijzigen en beginnen met een configuratie met behulp van upgrade [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4422f-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="4422f-133">Zodra het Hallo-upgrade is voltooid, kunt u nieuwe knooppunten tooyour cluster toevoegen aan dit knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="4422f-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="4422f-134">Knooppunten van het cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="4422f-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="4422f-135">Een knooppunt kan worden verwijderd uit een cluster met behulp van de upgrade van een configuratie in Hallo manier te volgen:</span><span class="sxs-lookup"><span data-stu-id="4422f-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="4422f-136">Uitvoeren [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Hallo nieuwste configuratiebestand en *verwijderen* Hallo knooppunt uit de sectie 'Knooppunten'.</span><span class="sxs-lookup"><span data-stu-id="4422f-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="4422f-137">Hallo 'NodesToBeRemoved' toevoegen parameter te 'instellingen' sectie in de sectie 'FabricSettings'.</span><span class="sxs-lookup"><span data-stu-id="4422f-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="4422f-138">Hallo '' waarde '' moet een door komma's gescheiden lijst met knooppuntnamen van knooppunten die toobe verwijderd moeten.</span><span class="sxs-lookup"><span data-stu-id="4422f-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

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
2. <span data-ttu-id="4422f-139">Voer [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin Hallo upgrade.</span><span class="sxs-lookup"><span data-stu-id="4422f-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="4422f-140">U kunt voortgang Hallo van Hallo upgrade in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4422f-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="4422f-141">U kunt ook uitvoeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4422f-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="4422f-142">Verwijderen van knooppunten mogelijk meerdere upgrades initiëren.</span><span class="sxs-lookup"><span data-stu-id="4422f-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="4422f-143">Sommige knooppunten zijn gemarkeerd met `IsSeedNode=”true”` labelen en kan worden geïdentificeerd door het uitvoeren van query's Hallo cluster manifest met `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="4422f-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="4422f-144">Verwijderen van deze knooppunten kan het langer duren dan andere omdat Hallo seed-knooppunten toobe verplaatst in dergelijke scenario's.</span><span class="sxs-lookup"><span data-stu-id="4422f-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="4422f-145">Hallo-cluster moet minimaal 3 primaire knooppunt type knooppunten onderhouden.</span><span class="sxs-lookup"><span data-stu-id="4422f-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="4422f-146">Knooppunttypen verwijderen uit het cluster</span><span class="sxs-lookup"><span data-stu-id="4422f-146">Remove node types from your cluster</span></span>
<span data-ttu-id="4422f-147">Voordat u een knooppunttype verwijdert, Controleer als er knooppunten verwijzen naar Hallo knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="4422f-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="4422f-148">Verwijder deze knooppunten voordat u de bijbehorende knooppunttype Hallo verwijdert.</span><span class="sxs-lookup"><span data-stu-id="4422f-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="4422f-149">Zodra alle bijbehorende knooppunten zijn verwijderd, kunt u Hallo NodeType verwijderen uit de clusterconfiguratie Hallo en beginnen met een configuratie met behulp van upgrade [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4422f-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="4422f-150">Vervang primaire knooppunten van het cluster</span><span class="sxs-lookup"><span data-stu-id="4422f-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="4422f-151">Hallo vervanging van primaire knooppunten moet één knooppunt uitgevoerd na de andere in plaats van te verwijderen en vervolgens toe te voegen in batches.</span><span class="sxs-lookup"><span data-stu-id="4422f-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4422f-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4422f-152">Next steps</span></span>
* [<span data-ttu-id="4422f-153">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="4422f-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="4422f-154">Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten</span><span class="sxs-lookup"><span data-stu-id="4422f-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="4422f-155">Een zelfstandige Service Fabric-cluster maken met Azure Virtual machines waarop Windows wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4422f-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

