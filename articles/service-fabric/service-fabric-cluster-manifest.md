---
title: aaaConfigure uw Azure Service Fabric zelfstandige cluster | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw zelfstandige of persoonlijke Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="3fd37-103">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="3fd37-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="3fd37-104">Dit artikel wordt beschreven hoe een zelfstandige Service Fabric cluster met tooconfigure Hallo ***ClusterConfig.JSON*** bestand.</span><span class="sxs-lookup"><span data-stu-id="3fd37-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="3fd37-105">U kunt dit bestand toospecify informatie zoals Hallo Service Fabric-knooppunten en hun IP-adressen, verschillende soorten knooppunten op Hallo-cluster, beveiligingsconfiguraties hello, evenals Hallo netwerktopologie in termen van fouttolerantie/upgrade-domeinen, gebruiken voor uw zelfstandige cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="3fd37-106">Wanneer u [Hallo zelfstandige Service Fabric-pakket te downloaden](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), een paar voorbeelden van Hallo ClusterConfig.JSON bestand gedownloade tooyour werk machine zijn.</span><span class="sxs-lookup"><span data-stu-id="3fd37-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="3fd37-107">Hallo-voorbeelden met *DevCluster* in hun naam helpt u bij het maken van een cluster met alle drie knooppunten op dezelfde computer, zoals logische knooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="3fd37-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="3fd37-108">Buiten deze, moet ten minste één knooppunt worden gemarkeerd als een primaire knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="3fd37-109">Dit cluster is handig voor een omgeving met ontwikkeling of tests en wordt niet ondersteund als een productiecluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="3fd37-110">Hallo-voorbeelden met *MultiMachine* in hun naam helpt u bij het maken van een productiecluster kwaliteit met elk knooppunt op een afzonderlijke computer.</span><span class="sxs-lookup"><span data-stu-id="3fd37-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="3fd37-111">*ClusterConfig.Unsecure.DevCluster.JSON* en *ClusterConfig.Unsecure.MultiMachine.JSON* laten zien hoe een onbeveiligde test toocreate productie van het cluster of respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="3fd37-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="3fd37-112">*ClusterConfig.Windows.DevCluster.JSON* en *ClusterConfig.Windows.MultiMachine.JSON* tonen hoe toocreate test- of -cluster beveiligd met [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="3fd37-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="3fd37-113">*ClusterConfig.X509.DevCluster.JSON* en *ClusterConfig.X509.MultiMachine.JSON* tonen hoe toocreate test- of -cluster beveiligd met [X509 beveiliging op basis van certificaat](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="3fd37-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="3fd37-114">Nu gaan we kijken Hallo verschillende secties van een ***ClusterConfig.JSON*** bestand zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="3fd37-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="3fd37-115">Algemene clusterconfiguraties</span><span class="sxs-lookup"><span data-stu-id="3fd37-115">General cluster configurations</span></span>
<span data-ttu-id="3fd37-116">Dit heeft betrekking op Hallo brede cluster specifieke configuraties, zoals weergegeven in onderstaande Hallo JSON-codefragment.</span><span class="sxs-lookup"><span data-stu-id="3fd37-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="3fd37-117">U kunt een beschrijvende naam tooyour Service Fabric-cluster geven door toe te wijzen toohello **naam** variabele.</span><span class="sxs-lookup"><span data-stu-id="3fd37-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="3fd37-118">Hallo **clusterConfigurationVersion** Hallo versienummer van het cluster, moet u deze verhogen telkens wanneer u een upgrade uitvoert van Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="3fd37-119">Laat u echter Hallo **apiVersion** toohello standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="3fd37-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="3fd37-120">Knooppunten op Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="3fd37-120">Nodes on hello cluster</span></span>
<span data-ttu-id="3fd37-121">U kunt Hallo knooppunten op uw Service Fabric-cluster configureren met behulp van Hallo **knooppunten** sectie als Hallo volgende codefragment bevat.</span><span class="sxs-lookup"><span data-stu-id="3fd37-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="3fd37-122">Een Service Fabric-cluster moet ten minste 3 knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="3fd37-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="3fd37-123">U kunt meer knooppunten toothis sectie toevoegen aan de hand van uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="3fd37-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="3fd37-124">Hallo volgende tabel wordt uitgelegd Hallo configuratie-instellingen voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="3fd37-125">**Knooppuntconfiguratie**</span><span class="sxs-lookup"><span data-stu-id="3fd37-125">**Node configuration**</span></span> | <span data-ttu-id="3fd37-126">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="3fd37-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3fd37-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="3fd37-127">nodeName</span></span> |<span data-ttu-id="3fd37-128">U kunt een beschrijvende naam toohello knooppunt op te geven.</span><span class="sxs-lookup"><span data-stu-id="3fd37-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="3fd37-129">IP-adres</span><span class="sxs-lookup"><span data-stu-id="3fd37-129">iPAddress</span></span> |<span data-ttu-id="3fd37-130">Hallo IP-adres van het knooppunt door een opdrachtpromptvenster te openen en te typen weten `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="3fd37-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="3fd37-131">Houd er rekening mee Hallo IPV4-adres en toe te wijzen toohello **iPAddress** variabele.</span><span class="sxs-lookup"><span data-stu-id="3fd37-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="3fd37-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="3fd37-132">nodeTypeRef</span></span> |<span data-ttu-id="3fd37-133">Elk knooppunt kan worden toegewezen als een ander knooppunt-type.</span><span class="sxs-lookup"><span data-stu-id="3fd37-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="3fd37-134">Hallo [knooppunttypen](#nodetypes) zijn gedefinieerd in de onderstaande Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="3fd37-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="3fd37-135">faultDomain</span></span> |<span data-ttu-id="3fd37-136">Fout met betrekking tot domeinen inschakelen beheerders toodefine Hallo fysieke clusterknooppunten die op Hallo mislukken dezelfde tijd vanwege tooshared fysieke afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="3fd37-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="3fd37-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="3fd37-137">upgradeDomain</span></span> |<span data-ttu-id="3fd37-138">Upgradedomeinen beschrijven sets met knooppunten die zijn uitgeschakeld voor Service Fabric wordt bijgewerkt op over Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="3fd37-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="3fd37-139">U kunt kiezen welke knooppunten tooassign toowhich upgradedomeinen, zoals ze niet door de fysieke vereisten beperkt worden.</span><span class="sxs-lookup"><span data-stu-id="3fd37-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="3fd37-140">Eigenschappen van cluster</span><span class="sxs-lookup"><span data-stu-id="3fd37-140">Cluster properties</span></span>
<span data-ttu-id="3fd37-141">Hallo **eigenschappen** sectie in Hallo ClusterConfig.JSON gebruikte tooconfigure Hallo cluster is als volgt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="3fd37-142">Betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="3fd37-142">Reliability</span></span>
<span data-ttu-id="3fd37-143">Hallo-concept van **reliabilityLevel** definieert Hallo aantal replica's of exemplaren van Hallo Service Fabric-systeemservices die kunnen worden uitgevoerd op de primaire knooppunten Hallo van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="3fd37-144">Het bepaalt Hallo betrouwbaarheid van deze services en daarom Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="3fd37-145">Hallo-waarde is berekende door Hallo systeem gelijktijdig cluster maken en de upgrade.</span><span class="sxs-lookup"><span data-stu-id="3fd37-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="3fd37-146">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="3fd37-146">Diagnostics</span></span>
<span data-ttu-id="3fd37-147">Hallo **diagnosticsStore** sectie kunt u tooconfigure parameters tooenable diagnostische gegevens en het oplossen van problemen knooppunt of cluster fouten, zoals wordt weergegeven in het volgende codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="3fd37-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="3fd37-148">Hallo **metagegevens** is een beschrijving van uw cluster diagnostische gegevens en conform de instelling voor de installatie kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3fd37-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="3fd37-149">Deze variabelen helpen bij het verzamelen van ETW traceerlogboeken, crashdumps, evenals prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="3fd37-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="3fd37-150">Lees [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) en [ETW-tracering](https://msdn.microsoft.com/library/ms751538.aspx) traceerlogboeken voor meer informatie over ETW.</span><span class="sxs-lookup"><span data-stu-id="3fd37-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="3fd37-151">Alle logboeken, met inbegrip van [dumpbestanden Crash](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) en [prestatiemeteritems](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) mag gerichte toohello **connectionString** map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3fd37-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="3fd37-152">U kunt ook *AzureStorage* voor het opslaan van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3fd37-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="3fd37-153">Hieronder vindt u een voorbeeld-fragment.</span><span class="sxs-lookup"><span data-stu-id="3fd37-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="3fd37-154">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="3fd37-154">Security</span></span>
<span data-ttu-id="3fd37-155">Hallo **beveiliging** sectie nodig is voor een veilige zelfstandige Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="3fd37-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="3fd37-156">Hallo volgende fragment toont een deel van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="3fd37-157">Hallo **metagegevens** is een beschrijving van uw beveiligde cluster en conform de instelling voor de installatie kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3fd37-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="3fd37-158">Hallo **ClusterCredentialType** en **ServerCredentialType** bepalen Hallo type beveiliging Hallo-cluster en Hallo knooppunten gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="3fd37-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="3fd37-159">Ze kunnen worden ingesteld tooeither *X509* voor een beveiliging op basis van certificaten of *Windows* voor een Azure Active Directory gebaseerde beveiliging.</span><span class="sxs-lookup"><span data-stu-id="3fd37-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="3fd37-160">Hallo rest Hallo **beveiliging** sectie wordt gebaseerd op Hallo type Hallo-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="3fd37-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="3fd37-161">Lees [beveiliging op basis van certificaten in een zelfstandige cluster](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging in een zelfstandige cluster](service-fabric-windows-cluster-windows-security.md) voor meer informatie over hoe toofill uit Hallo rest van de Hallo **beveiliging**sectie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="3fd37-162">Knooppunttypen</span><span class="sxs-lookup"><span data-stu-id="3fd37-162">Node Types</span></span>
<span data-ttu-id="3fd37-163">Hallo **nodeTypes** sectie wordt beschreven Hallo type Hallo knooppunten die fungeren als uw cluster heeft.</span><span class="sxs-lookup"><span data-stu-id="3fd37-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="3fd37-164">Ten minste één knooppunttype moet worden opgegeven voor een cluster, zoals wordt weergegeven in onderstaande Hallo stukje.</span><span class="sxs-lookup"><span data-stu-id="3fd37-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="3fd37-165">Hallo **naam** Hallo beschrijvende naam voor dit knooppunttype is.</span><span class="sxs-lookup"><span data-stu-id="3fd37-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="3fd37-166">een knooppunt van dit knooppunttype toocreate toewijzen de beschrijvende naam toohello **nodeTypeRef** variabele voor dat knooppunt, zoals vermeld [hierboven](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="3fd37-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="3fd37-167">Voor elk knooppunttype definiëren Hallo verbindingseindpunten die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="3fd37-168">U kunt een ander poortnummer op voor deze verbindingseindpunten, zolang ze niet met een andere eindpunten in dit cluster conflicteren.</span><span class="sxs-lookup"><span data-stu-id="3fd37-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="3fd37-169">In een cluster met meerdere knooppunten zal er een of meer primaire knooppunten (dat wil zeggen **isPrimary** instellen te*true*), afhankelijk van Hallo [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="3fd37-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="3fd37-170">Lees [Service Fabric-cluster overwegingen bij capaciteitsplanning](service-fabric-cluster-capacity.md) voor meer informatie over **nodeTypes** en **reliabilityLevel**, en tooknow wat zijn de primaire en Hallo typen van niet-primaire knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3fd37-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="3fd37-171">Eindpunten tooconfigure Hallo knooppunttypen gebruikt</span><span class="sxs-lookup"><span data-stu-id="3fd37-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="3fd37-172">*clientConnectionEndpointPort* Hallo poort gebruikt door Hallo client tooconnect toohello cluster als u Hallo client-API's.</span><span class="sxs-lookup"><span data-stu-id="3fd37-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="3fd37-173">*clusterConnectionEndpointPort* Hallo poort waarop Hallo knooppunten met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="3fd37-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="3fd37-174">*leaseDriverEndpointPort* Hallo poort wordt gebruikt door Hallo cluster lease stuurprogramma toofind uit als Hallo knooppunten nog steeds actief zijn is.</span><span class="sxs-lookup"><span data-stu-id="3fd37-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="3fd37-175">*serviceConnectionEndpointPort* Hallo-poort die wordt gebruikt door Hallo toepassingen en services die zijn geïmplementeerd op een knooppunt, toocommunicate met Hallo Service Fabric-client op dat bepaalde knooppunt is.</span><span class="sxs-lookup"><span data-stu-id="3fd37-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="3fd37-176">*httpGatewayEndpointPort* Hallo-poort die wordt gebruikt door Hallo Service Fabric Explorer tooconnect toohello cluster is.</span><span class="sxs-lookup"><span data-stu-id="3fd37-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="3fd37-177">*ephemeralPorts* overschrijven Hallo [dynamische poorten gebruikt door Hallo OS](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="3fd37-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="3fd37-178">Service Fabric gebruikt een deel van deze poorten als toepassing poorten en Hallo resterende beschikbaar zullen zijn voor Hallo OS.</span><span class="sxs-lookup"><span data-stu-id="3fd37-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="3fd37-179">Dit wordt ook deze bereik toohello bestaande bereik toegewezen aanwezig is in Hallo OS, zodat u Hallo bereiken opgegeven in de JSON voorbeeldbestanden Hallo voor alle doeleinden gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="3fd37-180">U moet toomake Hallo verschil tussen het Hallo-begin- en end-poorten Hallo moet ten minste 255.</span><span class="sxs-lookup"><span data-stu-id="3fd37-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="3fd37-181">U kunt uitvoeren in conflicten als dit verschil te laag, omdat dit bereik wordt gedeeld met Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3fd37-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="3fd37-182">Zie het dynamisch poortbereik Hallo geconfigureerd door te voeren `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="3fd37-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="3fd37-183">*applicationPorts* Hallo-poorten die worden gebruikt door Hallo Service Fabric-toepassingen zijn.</span><span class="sxs-lookup"><span data-stu-id="3fd37-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="3fd37-184">Hallo toepassingspoortbereik moet groot genoeg toocover Hallo eindpunt vereisten van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3fd37-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="3fd37-185">Dit bereik moet exclusieve van Hallo dynamisch poortbereik op Hallo machine, dat wil zeggen Hallo *ephemeralPorts* bereik zoals ingesteld in Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="3fd37-186">Service Fabric Gebruik deze wanneer nieuwe poorten zijn vereist, evenals behandelen Hallo firewall voor deze poorten te openen.</span><span class="sxs-lookup"><span data-stu-id="3fd37-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="3fd37-187">*reverseProxyEndpointPort* is een optionele reverse proxy-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="3fd37-188">Zie [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="3fd37-189">Logboekinstellingen</span><span class="sxs-lookup"><span data-stu-id="3fd37-189">Log Settings</span></span>
<span data-ttu-id="3fd37-190">Hallo **fabricSettings** sectie kunt u tooset Hallo hoofdmappen voor Hallo Service Fabric-gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="3fd37-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="3fd37-191">U kunt deze alleen tijdens het maken van het oorspronkelijke cluster Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3fd37-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="3fd37-192">Hieronder vindt u een voorbeeld-fragment van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3fd37-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="3fd37-193">Het is raadzaam om met behulp van een niet-OS-station als Hallo FabricDataRoot en FabricLogRoot, aangezien deze meer betrouwbaarheid tegen OS crashes biedt.</span><span class="sxs-lookup"><span data-stu-id="3fd37-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="3fd37-194">Houd er rekening mee dat als u alleen Hallo gegevenshoofdmap wilt aanpassen, klikt u vervolgens Hallo logboek hoofdmap worden geplaatst één niveau onder het Hallo-gegevenshoofdmap.</span><span class="sxs-lookup"><span data-stu-id="3fd37-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="3fd37-195">Stateful betrouwbare Service-instellingen</span><span class="sxs-lookup"><span data-stu-id="3fd37-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="3fd37-196">Hallo **KtlLogger** sectie kunt u tooset Hallo globale configuratie-instellingen voor Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="3fd37-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="3fd37-197">Lees voor meer informatie over deze instellingen [stateful betrouwbare services configureren](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="3fd37-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="3fd37-198">Hallo voorbeeld hieronder ziet u hoe toochange Hallo Hallo gedeelde transactielogboek die wordt gemaakt tooback worden betrouwbare verzamelingen voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="3fd37-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="3fd37-199">Extra functies</span><span class="sxs-lookup"><span data-stu-id="3fd37-199">Add-on features</span></span>
<span data-ttu-id="3fd37-200">Extra functies van tooconfigure hello apiVersion moet worden geconfigureerd als '-04-2017' of hoger en addonFeatures moet toobe geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="3fd37-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="3fd37-201">Container-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="3fd37-201">Container support</span></span>
<span data-ttu-id="3fd37-202">tooenable container ondersteuning voor windows server-container en hyper-v-container voor zelfstandige clusters, Hallo 'DnsService' invoegtoepassing functie moet toobe ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3fd37-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3fd37-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3fd37-203">Next steps</span></span>
<span data-ttu-id="3fd37-204">Zodra u een volledig ClusterConfig.JSON-bestand dat is geconfigureerd volgens de instellingen van uw zelfstandige cluster hebt, kunt u uw cluster door volgende Hallo artikel implementeren [maken van een zelfstandige Service Fabric-cluster](service-fabric-cluster-creation-for-windows-server.md) en ga vervolgens verder te[uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3fd37-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

