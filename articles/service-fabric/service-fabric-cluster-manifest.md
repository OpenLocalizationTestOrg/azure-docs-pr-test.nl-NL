---
title: Configureren van uw Azure Service Fabric-cluster zelfstandige | Microsoft Docs
description: Informatie over het configureren van uw zelfstandige of persoonlijke Service Fabric-cluster.
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="12048-103">Configuratie-instellingen voor zelfstandige Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="12048-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="12048-104">In dit artikel wordt beschreven hoe u een zelfstandige Service Fabric cluster met de ***ClusterConfig.JSON*** bestand.</span><span class="sxs-lookup"><span data-stu-id="12048-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="12048-105">U kunt dit bestand informatie zoals de Service Fabric-knooppunten en de IP-adressen, de verschillende soorten knooppunten op het cluster, de beveiligingsconfiguraties, evenals de netwerktopologie in termen van fouttolerantie/upgrade-domeinen voor uw zelfstandige cluster opgeven.</span><span class="sxs-lookup"><span data-stu-id="12048-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="12048-106">Wanneer u [download het zelfstandige Service Fabric-pakket](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), een paar voorbeelden van het bestand ClusterConfig.JSON worden gedownload met uw werk-machine.</span><span class="sxs-lookup"><span data-stu-id="12048-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="12048-107">De voorbeelden die *DevCluster* in hun naam helpt u bij het maken van een cluster met alle drie knooppunten op dezelfde computer, zoals logische knooppunten.</span><span class="sxs-lookup"><span data-stu-id="12048-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="12048-108">Buiten deze, moet ten minste één knooppunt worden gemarkeerd als een primaire knooppunt.</span><span class="sxs-lookup"><span data-stu-id="12048-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="12048-109">Dit cluster is handig voor een omgeving met ontwikkeling of tests en wordt niet ondersteund als een productiecluster.</span><span class="sxs-lookup"><span data-stu-id="12048-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="12048-110">De voorbeelden die *MultiMachine* in hun naam helpt u bij het maken van een productiecluster kwaliteit met elk knooppunt op een afzonderlijke computer.</span><span class="sxs-lookup"><span data-stu-id="12048-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="12048-111">*ClusterConfig.Unsecure.DevCluster.JSON* en *ClusterConfig.Unsecure.MultiMachine.JSON* laten zien hoe u respectievelijk een onbeveiligde test- of -cluster maken.</span><span class="sxs-lookup"><span data-stu-id="12048-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="12048-112">*ClusterConfig.Windows.DevCluster.JSON* en *ClusterConfig.Windows.MultiMachine.JSON* weergeven van het maken van de test- of -cluster beveiligd met [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="12048-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="12048-113">*ClusterConfig.X509.DevCluster.JSON* en *ClusterConfig.X509.MultiMachine.JSON* weergeven van het maken van de test- of -cluster beveiligd met [X509 beveiliging op basis van certificaat](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="12048-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="12048-114">Nu gaan we de verschillende secties van kijken een ***ClusterConfig.JSON*** bestand zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="12048-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="12048-115">Algemene clusterconfiguraties</span><span class="sxs-lookup"><span data-stu-id="12048-115">General cluster configurations</span></span>
<span data-ttu-id="12048-116">Dit betreft brede cluster specifieke configuraties, zoals wordt weergegeven in het onderstaande JSON-codefragment.</span><span class="sxs-lookup"><span data-stu-id="12048-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="12048-117">U kunt een beschrijvende naam geven tot uw Service Fabric-cluster door toe te wijzen aan de **naam** variabele.</span><span class="sxs-lookup"><span data-stu-id="12048-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="12048-118">De **clusterConfigurationVersion** is het versienummer van het cluster, moet u deze verhogen telkens wanneer u een upgrade uitvoert van Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="12048-119">Laat u echter de **apiVersion** op de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="12048-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="12048-120">Knooppunten op het cluster</span><span class="sxs-lookup"><span data-stu-id="12048-120">Nodes on the cluster</span></span>
<span data-ttu-id="12048-121">U kunt de knooppunten configureren op uw Service Fabric-cluster met behulp van de **knooppunten** sectie als het volgende codefragment bevat.</span><span class="sxs-lookup"><span data-stu-id="12048-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

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

<span data-ttu-id="12048-122">Een Service Fabric-cluster moet ten minste 3 knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="12048-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="12048-123">In deze sectie kunt u meer knooppunten toevoegen aan de hand van uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="12048-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="12048-124">De volgende tabel beschrijft de configuratie-instellingen voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="12048-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="12048-125">**Knooppuntconfiguratie**</span><span class="sxs-lookup"><span data-stu-id="12048-125">**Node configuration**</span></span> | <span data-ttu-id="12048-126">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="12048-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="12048-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="12048-127">nodeName</span></span> |<span data-ttu-id="12048-128">U kunt een beschrijvende naam geven tot het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="12048-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="12048-129">IP-adres</span><span class="sxs-lookup"><span data-stu-id="12048-129">iPAddress</span></span> |<span data-ttu-id="12048-130">Het IP-adres van uw knooppunt vinden door een opdrachtpromptvenster te openen en te typen `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="12048-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="12048-131">Let op het IPV4-adres en wijst deze toe aan de **iPAddress** variabele.</span><span class="sxs-lookup"><span data-stu-id="12048-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="12048-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="12048-132">nodeTypeRef</span></span> |<span data-ttu-id="12048-133">Elk knooppunt kan worden toegewezen als een ander knooppunt-type.</span><span class="sxs-lookup"><span data-stu-id="12048-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="12048-134">De [knooppunttypen](#nodetypes) zijn gedefinieerd in de onderstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="12048-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="12048-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="12048-135">faultDomain</span></span> |<span data-ttu-id="12048-136">Domeinen met fouten inschakelen clusterbeheerders voor het definiëren van fysieke knooppunten die op hetzelfde moment als gevolg van gedeelde fysieke afhankelijkheden kunnen mislukken.</span><span class="sxs-lookup"><span data-stu-id="12048-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="12048-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="12048-137">upgradeDomain</span></span> |<span data-ttu-id="12048-138">Upgradedomeinen beschrijven sets met knooppunten die Service Fabric-upgrades op rond dezelfde tijd worden afgesloten.</span><span class="sxs-lookup"><span data-stu-id="12048-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="12048-139">U kunt welke knooppunten toewijzen aan welke upgradedomeinen als ze niet door de fysieke vereisten beperkt worden.</span><span class="sxs-lookup"><span data-stu-id="12048-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="12048-140">Eigenschappen van cluster</span><span class="sxs-lookup"><span data-stu-id="12048-140">Cluster properties</span></span>
<span data-ttu-id="12048-141">De **eigenschappen** sectie in het ClusterConfig.JSON wordt gebruikt voor het configureren van het cluster als volgt.</span><span class="sxs-lookup"><span data-stu-id="12048-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="12048-142">Betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="12048-142">Reliability</span></span>
<span data-ttu-id="12048-143">Het concept van **reliabilityLevel** definieert het aantal replica's of exemplaren van de Service Fabric-systeemservices die kunnen worden uitgevoerd op de primaire knooppunten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="12048-144">Het bepalen van de betrouwbaarheid van deze services en is daarom het cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="12048-145">De waarde is berekende door het systeem tijdens het cluster maken en de upgrade.</span><span class="sxs-lookup"><span data-stu-id="12048-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="12048-146">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="12048-146">Diagnostics</span></span>
<span data-ttu-id="12048-147">De **diagnosticsStore** sectie kunt u parameters wilt configureren om in te schakelen van diagnostische gegevens en het oplossen van problemen knooppunt of cluster fouten, zoals wordt weergegeven in het volgende fragment.</span><span class="sxs-lookup"><span data-stu-id="12048-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="12048-148">De **metagegevens** is een beschrijving van uw cluster diagnostische gegevens en conform de instelling voor de installatie kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="12048-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="12048-149">Deze variabelen helpen bij het verzamelen van ETW traceerlogboeken, crashdumps, evenals prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="12048-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="12048-150">Lees [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) en [ETW-tracering](https://msdn.microsoft.com/library/ms751538.aspx) traceerlogboeken voor meer informatie over ETW.</span><span class="sxs-lookup"><span data-stu-id="12048-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="12048-151">Alle logboeken, met inbegrip van [dumpbestanden Crash](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) en [prestatiemeteritems](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) kunnen worden omgeleid naar de **connectionString** map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="12048-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="12048-152">U kunt ook *AzureStorage* voor het opslaan van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="12048-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="12048-153">Hieronder vindt u een voorbeeld-fragment.</span><span class="sxs-lookup"><span data-stu-id="12048-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="12048-154">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="12048-154">Security</span></span>
<span data-ttu-id="12048-155">De **beveiliging** sectie nodig is voor een veilige zelfstandige Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="12048-156">Het volgende fragment toont een deel van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="12048-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="12048-157">De **metagegevens** is een beschrijving van uw beveiligde cluster en conform de instelling voor de installatie kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="12048-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="12048-158">De **ClusterCredentialType** en **ServerCredentialType** , bepalen het type dat door het cluster en de knooppunten gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="12048-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="12048-159">Ze kunnen worden ingesteld op *X509* voor een beveiliging op basis van certificaten of *Windows* voor een Azure Active Directory gebaseerde beveiliging.</span><span class="sxs-lookup"><span data-stu-id="12048-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="12048-160">De rest van de **beveiliging** sectie wordt gebaseerd op het type van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="12048-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="12048-161">Lees [beveiliging op basis van certificaten in een zelfstandige cluster](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging in een zelfstandige cluster](service-fabric-windows-cluster-windows-security.md) voor informatie over het invullen van de rest van de **beveiliging** sectie.</span><span class="sxs-lookup"><span data-stu-id="12048-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="12048-162">Knooppunttypen</span><span class="sxs-lookup"><span data-stu-id="12048-162">Node Types</span></span>
<span data-ttu-id="12048-163">De **nodeTypes** sectie worden beschreven van het type van de knooppunten met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="12048-164">Ten minste één knooppunttype moet worden opgegeven voor een cluster, zoals wordt weergegeven in het onderstaande codefragment.</span><span class="sxs-lookup"><span data-stu-id="12048-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

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

<span data-ttu-id="12048-165">De **naam** is de beschrijvende naam voor dit knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="12048-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="12048-166">Wijs de beschrijvende naam op voor het maken van een knooppunt van dit knooppunttype de **nodeTypeRef** variabele voor dat knooppunt, zoals vermeld [hierboven](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="12048-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="12048-167">Definieer de eindpunten van de verbinding die wordt gebruikt voor elk knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="12048-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="12048-168">U kunt een ander poortnummer op voor deze verbindingseindpunten, zolang ze niet met een andere eindpunten in dit cluster conflicteren.</span><span class="sxs-lookup"><span data-stu-id="12048-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="12048-169">In een cluster met meerdere knooppunten zal er een of meer primaire knooppunten (dat wil zeggen **isPrimary** ingesteld op *true*), afhankelijk van de [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="12048-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="12048-170">Lees [Service Fabric-cluster overwegingen bij capaciteitsplanning](service-fabric-cluster-capacity.md) voor meer informatie over **nodeTypes** en **reliabilityLevel**, en om te weten wat zijn primaire en de typen van niet-primaire knooppunten.</span><span class="sxs-lookup"><span data-stu-id="12048-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="12048-171">Eindpunten die worden gebruikt voor het configureren van de knooppunttypen</span><span class="sxs-lookup"><span data-stu-id="12048-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="12048-172">*clientConnectionEndpointPort* is de poort die wordt gebruikt door de client verbinding maken met het cluster bij gebruik van de client-API.</span><span class="sxs-lookup"><span data-stu-id="12048-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="12048-173">*clusterConnectionEndpointPort* is de poort die de knooppunten met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="12048-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="12048-174">*leaseDriverEndpointPort* is de poort die wordt gebruikt door het stuurprogramma van de lease cluster om te controleren of de knooppunten nog steeds actief zijn.</span><span class="sxs-lookup"><span data-stu-id="12048-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="12048-175">*serviceConnectionEndpointPort* is de poort die wordt gebruikt door de toepassingen en services die zijn geïmplementeerd op een knooppunt, om te communiceren met de Service Fabric-client op dat specifieke knooppunt.</span><span class="sxs-lookup"><span data-stu-id="12048-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="12048-176">*httpGatewayEndpointPort* is de poort die wordt gebruikt door de Service Fabric Explorer verbinding maken met het cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="12048-177">*ephemeralPorts* overschrijven de [dynamische poorten gebruikt door het besturingssysteem](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="12048-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="12048-178">Service Fabric gebruikt een deel van deze poorten als toepassing poorten en de resterende beschikbaar zullen zijn voor het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="12048-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="12048-179">Dit wordt ook dit bereik toewijzen aan het bestaande bereik aanwezig is in het besturingssysteem, zodat u de adresbereiken die zijn opgegeven in de JSON-voorbeeldbestanden voor alle doeleinden gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="12048-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="12048-180">U moet ervoor zorgen dat het verschil tussen de begin- en end-poorten ten minste 255 is.</span><span class="sxs-lookup"><span data-stu-id="12048-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="12048-181">U kunt uitvoeren in conflicten als dit verschil te laag, omdat dit bereik wordt gedeeld met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="12048-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="12048-182">Zie het geconfigureerde dynamisch poortbereik door het uitvoeren van `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="12048-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="12048-183">*applicationPorts* zijn de poorten die worden gebruikt door de Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="12048-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="12048-184">Het poortbereik van toepassing moet groot genoeg is voor het eindpunt behoefte van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="12048-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="12048-185">Dit bereik moet exclusieve uit het bereik van de dynamische poort op de machine, dat wil zeggen de *ephemeralPorts* bereik zoals ingesteld in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="12048-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="12048-186">Service Fabric Gebruik deze wanneer nieuwe poorten zijn vereist, evenals zorgt voor het openen van de firewall voor deze poorten.</span><span class="sxs-lookup"><span data-stu-id="12048-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="12048-187">*reverseProxyEndpointPort* is een optionele reverse proxy-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="12048-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="12048-188">Zie [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="12048-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="12048-189">Logboekinstellingen</span><span class="sxs-lookup"><span data-stu-id="12048-189">Log Settings</span></span>
<span data-ttu-id="12048-190">De **fabricSettings** sectie kunt u de hoofdmappen voor de Service Fabric-gegevens en logboekbestanden instellen.</span><span class="sxs-lookup"><span data-stu-id="12048-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="12048-191">U kunt deze alleen tijdens het maken van het oorspronkelijke cluster.</span><span class="sxs-lookup"><span data-stu-id="12048-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="12048-192">Hieronder vindt u een voorbeeld-fragment van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="12048-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="12048-193">Het is raadzaam om een niet-OS-station gebruiken als de FabricDataRoot en FabricLogRoot aangezien deze biedt dat meer betrouwbaarheid tegen OS is vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="12048-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="12048-194">Houd er rekening mee dat als u alleen de gegevenshoofdmap wilt aanpassen, klikt u vervolgens de hoofdmap van het logboek wordt geplaatst één niveau onder de gegevenshoofdmap.</span><span class="sxs-lookup"><span data-stu-id="12048-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="12048-195">Stateful betrouwbare Service-instellingen</span><span class="sxs-lookup"><span data-stu-id="12048-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="12048-196">De **KtlLogger** sectie kunt u de globale configuratie-instellingen voor Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="12048-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="12048-197">Lees voor meer informatie over deze instellingen [stateful betrouwbare services configureren](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="12048-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="12048-198">Het volgende voorbeeld ziet u het wijzigen van de het gedeelde transactielogboek die wilt maken van een betrouwbare verzamelingen voor stateful services wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12048-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="12048-199">Extra functies</span><span class="sxs-lookup"><span data-stu-id="12048-199">Add-on features</span></span>
<span data-ttu-id="12048-200">Voor het configureren van extra functies van de apiVersion moet worden geconfigureerd als '-04-2017' of hoger en addonFeatures moet worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="12048-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="12048-201">Container-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="12048-201">Container support</span></span>
<span data-ttu-id="12048-202">De functie van de invoegtoepassing 'DnsService' moet worden ingeschakeld zodat de container-ondersteuning voor windows server-container en hyper-v-container voor zelfstandige clusters.</span><span class="sxs-lookup"><span data-stu-id="12048-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="12048-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12048-203">Next steps</span></span>
<span data-ttu-id="12048-204">Zodra u een volledig ClusterConfig.JSON-bestand dat is geconfigureerd volgens de instellingen van uw zelfstandige cluster hebt, kunt u uw cluster implementeren door het artikel [maken van een zelfstandige Service Fabric-cluster](service-fabric-cluster-creation-for-windows-server.md) en ga verder met [ uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="12048-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

