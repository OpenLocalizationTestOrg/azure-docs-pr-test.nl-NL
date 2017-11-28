---
title: Hoge beschikbaarheid voor Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe HDInsight-clusters betrouwbaarheid en beschikbaarheid verbeteren met behulp van een extra hoofdknooppunt. Meer informatie over hoe dit heeft gevolgen voor Hadoop-services zoals Ambari en Hive, en hoe afzonderlijk verbinding maken met elke hoofdknooppunt via SSH.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: hoge beschikbaarheid voor hadoop
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="1d47a-105">Beschikbaarheid en betrouwbaarheid van Hadoop-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d47a-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="1d47a-106">HDInsight-clusters bieden twee hoofdknooppunten voor een verhoging van de beschikbaarheid en betrouwbaarheid van Hadoop-services en taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1d47a-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="1d47a-107">Hadoop bereikt door het repliceren van services en gegevens op meerdere knooppunten in een cluster toe te hoge beschikbaarheid en betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="1d47a-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="1d47a-108">Standaard distributies van Hadoop hebben echter meestal alleen voor slechts één hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="1d47a-109">Een onderbreking van de één hoofdknooppunt kan leiden tot het cluster niet meer werkt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="1d47a-110">HDInsight biedt twee headnodes ter verbetering van de beschikbaarheid en betrouwbaarheid van Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1d47a-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d47a-111">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1d47a-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1d47a-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1d47a-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="1d47a-113">Beschikbaarheid en betrouwbaarheid van knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="1d47a-114">Knooppunten in een HDInsight-cluster worden geïmplementeerd met behulp van Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="1d47a-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="1d47a-115">De volgende secties worden de afzonderlijke knooppunttypen gebruikt met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d47a-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="1d47a-116">Niet alle knooppunttypen worden gebruikt voor het type van een cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="1d47a-117">Een Hadoop-clustertype heeft bijvoorbeeld geen eventuele Nimbus-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="1d47a-118">Voor meer informatie over de knooppunten die door HDInsight-clustertypen gebruikt, Zie de sectie van de typen Cluster van de [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="1d47a-119">HEAD-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-119">Head nodes</span></span>

<span data-ttu-id="1d47a-120">HDInsight biedt hoge beschikbaarheid van Hadoop-services, zodat twee hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="1d47a-121">Beide hoofdknooppunten zijn tegelijkertijd actief en wordt uitgevoerd binnen het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="1d47a-122">Sommige services, zoals HDFS of YARN, zijn alleen op elk moment 'active' op één hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="1d47a-123">Andere services zoals HiveServer2 of Hive-MetaStore zijn actief op beide head knooppunten op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="1d47a-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="1d47a-124">HEAD-knooppunten (en andere knooppunten in HDInsight) hebben een numerieke waarde als onderdeel van de hostnaam van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="1d47a-125">Bijvoorbeeld: `hn0-CLUSTERNAME` of `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="1d47a-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d47a-126">De numerieke waarde geen koppelt aan of een knooppunt primair of secundair wordt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="1d47a-127">De numerieke waarde is alleen aanwezig is een unieke naam voor elk knooppunt op te geven.</span><span class="sxs-lookup"><span data-stu-id="1d47a-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="1d47a-128">Nimbus-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-128">Nimbus Nodes</span></span>

<span data-ttu-id="1d47a-129">Nimbus-knooppunten zijn beschikbaar met Storm-clusters.</span><span class="sxs-lookup"><span data-stu-id="1d47a-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="1d47a-130">De Nimbus-knooppunten bieden vergelijkbare functionaliteit aan de Hadoop JobTracker met distributie en verwerking bewaking over worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="1d47a-131">HDInsight biedt twee Nimbus-knooppunten voor Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="1d47a-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="1d47a-132">Zookeeper-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-132">Zookeeper nodes</span></span>

<span data-ttu-id="1d47a-133">[ZooKeeper](http://zookeeper.apache.org/) knooppunten worden gebruikt voor de keuze opvulteken master services op hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="1d47a-134">Ze worden ook gebruikt om ervoor te zorgen dat services, gegevensknooppunten (worker) en gateways weten welke hoofdknooppunt een master-service actief is op.</span><span class="sxs-lookup"><span data-stu-id="1d47a-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="1d47a-135">HDInsight biedt standaard drie ZooKeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="1d47a-136">Worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-136">Worker nodes</span></span>

<span data-ttu-id="1d47a-137">Worker-knooppunten analyse van de werkelijke gegevens als een taak wordt verzonden naar het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="1d47a-138">Als een werkrolknooppunt is mislukt, wordt de taak die bezig was met een andere werkrolknooppunt verzonden.</span><span class="sxs-lookup"><span data-stu-id="1d47a-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="1d47a-139">HDInsight maakt standaard vier worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="1d47a-140">U kunt dit nummer voor de behoeften van uw zowel tijdens als na het maken van het cluster wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1d47a-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="1d47a-141">Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="1d47a-141">Edge node</span></span>

<span data-ttu-id="1d47a-142">Een edge-knooppunt deelneemt niet actief aan analyse van gegevens binnen het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="1d47a-143">Deze wordt gebruikt door ontwikkelaars of gegevenswetenschappers bij het werken met Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1d47a-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="1d47a-144">Het edge-knooppunt woont in het hetzelfde virtuele Azure-netwerk als de andere knooppunten in het cluster en rechtstreeks toegang tot alle andere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="1d47a-145">Het edge-knooppunt kan worden gebruikt zonder resources verlaten kritieke Hadoop-services of analyse taken.</span><span class="sxs-lookup"><span data-stu-id="1d47a-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="1d47a-146">Op HDInsight R Server is momenteel het enige clustertype dat een edge-knooppunt standaard biedt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="1d47a-147">Voor op HDInsight R Server, het edge-knooppunt wordt gebruikt test R code lokaal op het knooppunt alvorens deze aan het cluster voor gedistribueerde verwerking.</span><span class="sxs-lookup"><span data-stu-id="1d47a-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="1d47a-148">Zie voor meer informatie over het gebruik van een edge-knooppunt met clustertypen dan R Server de [edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="1d47a-149">Toegang tot de knooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-149">Accessing the nodes</span></span>

<span data-ttu-id="1d47a-150">Toegang tot het cluster via internet is beschikbaar via een openbare-gateway.</span><span class="sxs-lookup"><span data-stu-id="1d47a-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="1d47a-151">De toegang is beperkt tot de verbinding met de hoofdknooppunten en (indien aanwezig) de edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="1d47a-152">Toegang tot de services worden uitgevoerd op de hoofdknooppunten niet wordt toegepast wanneer er meerdere hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="1d47a-153">De openbare-gateway routeert aanvragen met het hoofdknooppunt die als host fungeert voor de aangevraagde service.</span><span class="sxs-lookup"><span data-stu-id="1d47a-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="1d47a-154">Bijvoorbeeld, als Ambari momenteel op de secundaire hoofdknooppunt gehost is, routeert de gateway binnenkomende aanvragen voor Ambari naar dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="1d47a-155">Toegang via de openbare gateway is beperkt tot poort 443 (HTTPS), 22 en 23.</span><span class="sxs-lookup"><span data-stu-id="1d47a-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="1d47a-156">Poort __443__ wordt gebruikt voor toegang tot de Ambari en andere web-gebruikersinterface of REST-API's die worden gehost op de hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="1d47a-157">Poort __22__ voor toegang tot de primaire hoofdknooppunt of edge-knooppunt met SSH wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="1d47a-158">Poort __23__ voor toegang tot de secundair hoofdknooppunt met SSH wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="1d47a-159">Bijvoorbeeld: `ssh username@mycluster-ssh.azurehdinsight.net` maakt verbinding met het primaire hoofdknooppunt van het cluster met de naam **mijncluster**.</span><span class="sxs-lookup"><span data-stu-id="1d47a-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="1d47a-160">Zie voor meer informatie over het gebruik van SSH, het [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="1d47a-161">Interne volledig gekwalificeerde domeinnamen (FQDN)</span><span class="sxs-lookup"><span data-stu-id="1d47a-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="1d47a-162">Knooppunten in een HDInsight-cluster hebben een interne IP-adres en de FQDN-naam die alleen toegankelijk is vanaf het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="1d47a-163">Als u toegang tot services op het cluster met behulp van de interne FQDN of IP-adres, moet u Ambari gebruiken om te controleren of het IP of FQDN-naam moet worden gebruikt bij het openen van de service.</span><span class="sxs-lookup"><span data-stu-id="1d47a-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="1d47a-164">De service Oozie kan bijvoorbeeld alleen uitgevoerd op één hoofdknooppunt en het gebruik van de `oozie` opdracht van een SSH-sessie is de URL van de service vereist.</span><span class="sxs-lookup"><span data-stu-id="1d47a-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="1d47a-165">Deze URL kan uit de Ambari worden opgehaald met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1d47a-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="1d47a-166">Met deze opdracht retourneert een waarde vergelijkbaar met de volgende opdracht, waarin de interne URL voor gebruik met de `oozie` opdracht:</span><span class="sxs-lookup"><span data-stu-id="1d47a-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="1d47a-167">Zie voor meer informatie over het werken met de Ambari REST-API [bewaken en beheren van HDInsight met de Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1d47a-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="1d47a-168">Toegang tot andere knooppunttypen</span><span class="sxs-lookup"><span data-stu-id="1d47a-168">Accessing other node types</span></span>

<span data-ttu-id="1d47a-169">U kunt verbinding maken met knooppunten die niet rechtstreeks toegankelijk zijn via internet met behulp van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="1d47a-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="1d47a-170">**SSH**: eenmaal zijn verbonden met een hoofdknooppunt via SSH, u kunt vervolgens SSH gebruiken vanaf het hoofdknooppunt van verbinding maken met de andere knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="1d47a-171">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1d47a-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="1d47a-172">**SSH-Tunnel**: als u nodig hebt voor toegang tot een webservice die wordt gehost op een van de knooppunten die geen toegang heeft tot internet, moet u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="1d47a-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="1d47a-173">Zie voor meer informatie de [een SSH-tunnel gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="1d47a-174">**Azure Virtual Network**: als uw HDInsight-cluster deel uit van een Azure-netwerk maakt, een resource in hetzelfde virtuele netwerk rechtstreeks toegang tot alle knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="1d47a-175">Zie voor meer informatie de [uitbreiden HDInsight met behulp van Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="1d47a-176">Het controleren van de servicestatus van een</span><span class="sxs-lookup"><span data-stu-id="1d47a-176">How to check on a service status</span></span>

<span data-ttu-id="1d47a-177">Gebruik de Ambari-Webgebruikersinterface of de Ambari REST-API te controleren van de status van services die worden uitgevoerd op de hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="1d47a-178">Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1d47a-178">Ambari Web UI</span></span>

<span data-ttu-id="1d47a-179">De Ambari-Webgebruikersinterface is op https://CLUSTERNAME.azurehdinsight.net zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="1d47a-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1d47a-180">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="1d47a-181">Als u wordt gevraagd, voert u de referenties van de HTTP-gebruiker voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="1d47a-182">De standaardnaam van de HTTP-gebruiker is **admin** en het wachtwoord het wachtwoord die u hebt ingevoerd bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="1d47a-183">Wanneer u op de pagina Ambari binnenkomen, worden de geïnstalleerde services aan de linkerkant van de pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d47a-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Geïnstalleerde services](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="1d47a-185">Er zijn een reeks pictogrammen die kunnen worden weergegeven naast een service om status te geven.</span><span class="sxs-lookup"><span data-stu-id="1d47a-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="1d47a-186">Waarschuwingen met betrekking tot een service kunnen worden weergegeven met de **waarschuwingen** koppeling aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="1d47a-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="1d47a-187">U kunt elke service voor meer informatie over het selecteren.</span><span class="sxs-lookup"><span data-stu-id="1d47a-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="1d47a-188">Terwijl de pagina informatie over de status en configuratie van elke service bevat, biedt het geen informatie welke hoofdknooppunt van de service wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="1d47a-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="1d47a-189">U kunt deze informatie weergeven, met de **Hosts** koppeling aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="1d47a-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="1d47a-190">Deze pagina bevat hosts binnen het cluster, inclusief de hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![lijst met hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="1d47a-192">Als u de koppeling voor een van de hoofdknooppunten wordt weergegeven, de services en onderdelen die op dat knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1d47a-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Onderdeelstatus](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="1d47a-194">Zie voor meer informatie over het gebruik van Ambari [bewaken en beheren van HDInsight met behulp van de Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="1d47a-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="1d47a-195">Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="1d47a-195">Ambari REST API</span></span>

<span data-ttu-id="1d47a-196">De Ambari REST-API is beschikbaar via het internet.</span><span class="sxs-lookup"><span data-stu-id="1d47a-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="1d47a-197">De openbare HDInsight-gateway routering aanvragen met het hoofdknooppunt waarop de REST-API wordt gehost worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="1d47a-198">De volgende opdracht kunt u de status van een service met de Ambari REST-API niet controleren:</span><span class="sxs-lookup"><span data-stu-id="1d47a-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="1d47a-199">Vervang **wachtwoord** met wachtwoord voor het HTTP-gebruikersaccount (admin).</span><span class="sxs-lookup"><span data-stu-id="1d47a-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="1d47a-200">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="1d47a-201">Vervang **SERVICENAME** met de naam van de service die u wilt controleren, de status van.</span><span class="sxs-lookup"><span data-stu-id="1d47a-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="1d47a-202">Bijvoorbeeld, om te controleren van de status van de **HDFS** service op een cluster met de naam **mijncluster**, met een wachtwoord van **wachtwoord**, kunt u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1d47a-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="1d47a-203">Het antwoord is vergelijkbaar met de volgende JSON:</span><span class="sxs-lookup"><span data-stu-id="1d47a-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="1d47a-204">De URL geeft aan of de service momenteel wordt uitgevoerd op een hoofdknooppunt met de naam **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="1d47a-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="1d47a-205">De status geeft aan dat de service momenteel actief is, of **gestart**.</span><span class="sxs-lookup"><span data-stu-id="1d47a-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="1d47a-206">Als u niet welke services zijn geïnstalleerd op het cluster weet, kunt u de volgende opdracht om een lijst te halen:</span><span class="sxs-lookup"><span data-stu-id="1d47a-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="1d47a-207">Zie voor meer informatie over het werken met de Ambari REST-API [bewaken en beheren van HDInsight met de Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="1d47a-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="1d47a-208">Serviceonderdelen</span><span class="sxs-lookup"><span data-stu-id="1d47a-208">Service components</span></span>

<span data-ttu-id="1d47a-209">Services mogen onderdelen die u wilt de status van afzonderlijk te controleren.</span><span class="sxs-lookup"><span data-stu-id="1d47a-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="1d47a-210">HDFS bevat bijvoorbeeld het onderdeel NameNode.</span><span class="sxs-lookup"><span data-stu-id="1d47a-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="1d47a-211">Als u informatie op een onderdeel, zou de opdracht zijn:</span><span class="sxs-lookup"><span data-stu-id="1d47a-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="1d47a-212">Als u niet welke onderdelen worden geleverd door een service weet, kunt u de volgende opdracht om een lijst te halen:</span><span class="sxs-lookup"><span data-stu-id="1d47a-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="1d47a-213">Over het openen van de logboekbestanden op de hoofdknooppunten</span><span class="sxs-lookup"><span data-stu-id="1d47a-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="1d47a-214">SSH</span><span class="sxs-lookup"><span data-stu-id="1d47a-214">SSH</span></span>

<span data-ttu-id="1d47a-215">Verbinding gemaakt met een hoofdknooppunt via SSH en logboekbestanden kunnen u vinden onder **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="1d47a-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="1d47a-216">Bijvoorbeeld: **/var/log/hadoop-yarn/yarn** bevatten de logboeken voor YARN.</span><span class="sxs-lookup"><span data-stu-id="1d47a-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="1d47a-217">Elke hoofdknooppunt kan unieke logboekvermeldingen, hebben, dus moet u de logboeken op beide controleren.</span><span class="sxs-lookup"><span data-stu-id="1d47a-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="1d47a-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="1d47a-218">SFTP</span></span>

<span data-ttu-id="1d47a-219">U kunt ook verbinding maken met het hoofdknooppunt met de SSH File Transfer Protocol of Secure File Transfer Protocol (SFTP) en de logboekbestanden rechtstreeks downloaden.</span><span class="sxs-lookup"><span data-stu-id="1d47a-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="1d47a-220">Vergelijkbaar met een SSH-client, wanneer de verbinding met het cluster dat u het hulpprogramma voor het account van de SSH-gebruikersnaam en het SSH-adres van het cluster moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="1d47a-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="1d47a-221">Bijvoorbeeld `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="1d47a-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="1d47a-222">Geef het wachtwoord voor het account wanneer u wordt gevraagd, of geef een openbare sleutel met de `-i` parameter.</span><span class="sxs-lookup"><span data-stu-id="1d47a-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="1d47a-223">Eenmaal zijn verbonden, krijgt u een `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="1d47a-224">Vanaf deze prompt kunt u mappen, uploaden en downloaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="1d47a-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="1d47a-225">Bijvoorbeeld de volgende opdrachten Wijzig de mappen op de **/var/log/hadoop/hdfs** directory en vervolgens alle bestanden in de map te downloaden.</span><span class="sxs-lookup"><span data-stu-id="1d47a-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="1d47a-226">Voer voor een lijst met beschikbare opdrachten `help` op de `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="1d47a-227">Er zijn ook grafische interfaces waarmee u kunt het visualiseren van het bestandssysteem wanneer verbinding met SFTP.</span><span class="sxs-lookup"><span data-stu-id="1d47a-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="1d47a-228">Bijvoorbeeld: [MobaXTerm](http://mobaxterm.mobatek.net/) kunt u bladeren naar het bestandssysteem een interface die vergelijkbaar is met Windows Verkenner gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1d47a-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="1d47a-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="1d47a-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="1d47a-230">Voor toegang tot de logboekbestanden met Ambari, moet u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="1d47a-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="1d47a-231">De webinterfaces voor de afzonderlijke services worden niet openbaar weergegeven op het Internet.</span><span class="sxs-lookup"><span data-stu-id="1d47a-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="1d47a-232">Zie voor meer informatie over het gebruik van een SSH-tunnel de [SSH-Tunneling gebruiken](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="1d47a-233">Selecteer de service die u wilt weergeven van Logboeken voor (bijvoorbeeld YARN) in de Ambari-Webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="1d47a-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="1d47a-234">Gebruik vervolgens **snelkoppelingen** te selecteren welke hoofdknooppunt om de logboeken voor weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1d47a-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Met behulp van snelle koppelingen om logboeken weer te geven](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="1d47a-236">Het configureren van de grootte van het knooppunt</span><span class="sxs-lookup"><span data-stu-id="1d47a-236">How to configure the node size</span></span>

<span data-ttu-id="1d47a-237">De grootte van een knooppunt kan alleen worden ingeschakeld tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="1d47a-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="1d47a-238">U vindt een lijst met de andere VM-grootten voor HDInsight in de [HDInsight pagina met prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1d47a-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="1d47a-239">Wanneer u een cluster maakt, kunt u de grootte van de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1d47a-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="1d47a-240">De volgende informatie biedt richtlijnen voor het opgeven van de grootte met behulp van de [Azure-portal][preview-portal], [Azure PowerShell][azure-powershell], en de [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="1d47a-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="1d47a-241">**Azure-portal**: wanneer u een cluster maakt, kunt u de grootte van de knooppunten die wordt gebruikt door het cluster instellen:</span><span class="sxs-lookup"><span data-stu-id="1d47a-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Afbeelding van het maken van clusterwizard met knooppunt grootte selectie](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="1d47a-243">**Azure CLI**: bij gebruik van de `azure hdinsight cluster create` opdracht, kunt u de grootte van de kop, worker en ZooKeeper-knooppunten instellen met behulp van de `--headNodeSize`, `--workerNodeSize`, en `--zookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="1d47a-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="1d47a-244">**Azure PowerShell**: bij gebruik van de `New-AzureRmHDInsightCluster` cmdlet, kunt u de grootte van de kop, worker en ZooKeeper-knooppunten instellen met behulp van de `-HeadNodeVMSize`, `-WorkerNodeSize`, en `-ZookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="1d47a-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d47a-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d47a-245">Next steps</span></span>

<span data-ttu-id="1d47a-246">Gebruik de volgende koppelingen voor meer informatie over zaken die worden vermeld in dit document.</span><span class="sxs-lookup"><span data-stu-id="1d47a-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="1d47a-247">Ambari REST-verwijzing</span><span class="sxs-lookup"><span data-stu-id="1d47a-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="1d47a-248">De Azure CLI installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="1d47a-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="1d47a-249">Azure PowerShell installeren en configureren </span><span class="sxs-lookup"><span data-stu-id="1d47a-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="1d47a-250">HDInsight met Ambari beheren</span><span class="sxs-lookup"><span data-stu-id="1d47a-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="1d47a-251">Linux gebaseerde HDInsight-clusters inrichten</span><span class="sxs-lookup"><span data-stu-id="1d47a-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
