---
title: aaaHigh beschikbaarheid voor Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe HDInsight-clusters betrouwbaarheid en beschikbaarheid verbeteren met behulp van een extra hoofdknooppunt. Meer informatie over hoe dit heeft gevolgen voor Hadoop-services zoals Ambari en Hive, evenals hoe tooindividually tooeach hoofdknooppunt via SSH verbinding.
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="2870a-105">Beschikbaarheid en betrouwbaarheid van Hadoop-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2870a-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="2870a-106">HDInsight-clusters bieden twee hoofdknooppunten tooincrease Hallo beschikbaarheid en betrouwbaarheid van Hadoop-services en taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2870a-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="2870a-107">Hadoop bereikt door het repliceren van services en gegevens op meerdere knooppunten in een cluster toe te hoge beschikbaarheid en betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2870a-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="2870a-108">Standaard distributies van Hadoop hebben echter meestal alleen voor slechts één hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="2870a-109">Een storing optreedt van één hoofdknooppunt Hallo kan leiden tot Hallo cluster toostop werken.</span><span class="sxs-lookup"><span data-stu-id="2870a-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="2870a-110">HDInsight biedt twee headnodes tooimprove Hadoop beschikbaarheid en betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2870a-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2870a-111">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2870a-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2870a-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2870a-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="2870a-113">Beschikbaarheid en betrouwbaarheid van knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="2870a-114">Knooppunten in een HDInsight-cluster worden geïmplementeerd met behulp van Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="2870a-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="2870a-115">Hallo volgende secties worden besproken Hallo afzonderlijke knooppunten die worden gebruikt met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2870a-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="2870a-116">Niet alle knooppunttypen worden gebruikt voor het type van een cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="2870a-117">Een Hadoop-clustertype heeft bijvoorbeeld geen eventuele Nimbus-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="2870a-118">Zie voor meer informatie over knooppunten die wordt gebruikt door HDInsight-clustertypen Hallo Cluster typen sectie Hallo [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="2870a-119">HEAD-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-119">Head nodes</span></span>

<span data-ttu-id="2870a-120">tooensure hoge beschikbaarheid van Hadoop-services, HDInsight biedt twee hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="2870a-121">Beide hoofdknooppunten zijn tegelijkertijd actief en wordt uitgevoerd binnen Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="2870a-122">Sommige services, zoals HDFS of YARN, zijn alleen op elk moment 'active' op één hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="2870a-123">Andere services zoals HiveServer2 of Hive-MetaStore actief zijn op beide hoofdknooppunten op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="2870a-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="2870a-124">HEAD-knooppunten (en andere knooppunten in HDInsight) hebben een numerieke waarde als onderdeel van het Hallo-hostnaam van Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="2870a-125">Bijvoorbeeld: `hn0-CLUSTERNAME` of `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="2870a-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2870a-126">Koppel geen Hallo numerieke waarde aan of een knooppunt primair of secundair wordt.</span><span class="sxs-lookup"><span data-stu-id="2870a-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="2870a-127">Hallo numerieke waarde is alleen aanwezig tooprovide een unieke naam voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="2870a-128">Nimbus-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-128">Nimbus Nodes</span></span>

<span data-ttu-id="2870a-129">Nimbus-knooppunten zijn beschikbaar met Storm-clusters.</span><span class="sxs-lookup"><span data-stu-id="2870a-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="2870a-130">Hallo Nimbus-knooppunten bieden vergelijkbare functionaliteit toohello Hadoop JobTracker met distributie en verwerking bewaking over worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="2870a-131">HDInsight biedt twee Nimbus-knooppunten voor Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="2870a-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="2870a-132">Zookeeper-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-132">Zookeeper nodes</span></span>

<span data-ttu-id="2870a-133">[ZooKeeper](http://zookeeper.apache.org/) knooppunten worden gebruikt voor de keuze opvulteken master services op hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="2870a-134">Ze zijn ook gebruikte tooinsure dat services, gegevensknooppunten (worker) en gateways weten welke hoofd-service actief is op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="2870a-135">HDInsight biedt standaard drie ZooKeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="2870a-136">Worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-136">Worker nodes</span></span>

<span data-ttu-id="2870a-137">Worker-knooppunten niet Hallo werkelijke data-analyse uitvoeren als een taak verzonden toohello cluster wordt.</span><span class="sxs-lookup"><span data-stu-id="2870a-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="2870a-138">Als een werkrolknooppunt is mislukt, wordt in het Hallo-taak die bezig was ingediende tooanother werkrolknooppunt is.</span><span class="sxs-lookup"><span data-stu-id="2870a-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="2870a-139">HDInsight maakt standaard vier worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="2870a-140">U kunt dit nummer toosuit uw behoeften wijzigen tijdens en na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="2870a-141">Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="2870a-141">Edge node</span></span>

<span data-ttu-id="2870a-142">Een edge-knooppunt deelneemt niet actief aan gegevensanalyse binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="2870a-143">Deze wordt gebruikt door ontwikkelaars of gegevenswetenschappers bij het werken met Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2870a-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="2870a-144">Hallo edge-knooppunt leven in hetzelfde virtuele Azure-netwerk als Hallo andere knooppunten in cluster Hallo Hallo en rechtstreeks toegang tot alle andere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="2870a-145">Hallo edge-knooppunt kan worden gebruikt zonder resources verlaten kritieke Hadoop-services of analyse taken.</span><span class="sxs-lookup"><span data-stu-id="2870a-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="2870a-146">Op HDInsight R Server is momenteel het enige clustertype hello, waarmee een edge-knooppunt standaard.</span><span class="sxs-lookup"><span data-stu-id="2870a-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="2870a-147">Voor op HDInsight R Server, Hallo edge-knooppunt wordt gebruikt test R code lokaal op Hallo knooppunt voordat het wordt ingediend toohello cluster voor gedistribueerde verwerking.</span><span class="sxs-lookup"><span data-stu-id="2870a-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="2870a-148">Zie voor informatie over het gebruik van een edge-knooppunt met clustertypen dan R Server Hallo [edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="2870a-149">Toegang tot Hallo knooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-149">Accessing hello nodes</span></span>

<span data-ttu-id="2870a-150">RAS-cluster toohello via Hallo internet is beschikbaar via een openbare-gateway.</span><span class="sxs-lookup"><span data-stu-id="2870a-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="2870a-151">Hallo edge-knooppunt toegang is beperkt tooconnecting toohello hoofdknooppunten en (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="2870a-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="2870a-152">Toegang tooservices uitgevoerd op Hallo hoofdknooppunten niet wordt toegepast wanneer er meerdere hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="2870a-153">Hallo openbare gateway routes aanvragen toohello head-knooppunt dat als host fungeert voor Hallo aangevraagde service.</span><span class="sxs-lookup"><span data-stu-id="2870a-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="2870a-154">Als de Ambari is momenteel gehost op een secundair hoofdknooppunt hello, routeert Hallo gateway binnenkomende aanvragen voor Ambari toothat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="2870a-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="2870a-155">Toegang via openbare Hallo-gateway is beperkt tooport 443 (HTTPS), 22 en 23.</span><span class="sxs-lookup"><span data-stu-id="2870a-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="2870a-156">Poort __443__ gebruikte tooaccess is Ambari en andere web-gebruikersinterface of REST-API's die worden gehost op Hallo hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="2870a-157">Poort __22__ gebruikte tooaccess Hallo primaire hoofdknooppunt of edge-knooppunt met SSH.</span><span class="sxs-lookup"><span data-stu-id="2870a-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="2870a-158">Poort __23__ gebruikte tooaccess Hallo secundair hoofdknooppunt met SSH is.</span><span class="sxs-lookup"><span data-stu-id="2870a-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="2870a-159">Bijvoorbeeld: `ssh username@mycluster-ssh.azurehdinsight.net` toohello primaire hoofdknooppunt van het Hallo-cluster met de naam verbindt **mijncluster**.</span><span class="sxs-lookup"><span data-stu-id="2870a-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="2870a-160">Zie voor meer informatie over het gebruik van SSH Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="2870a-161">Interne volledig gekwalificeerde domeinnamen (FQDN)</span><span class="sxs-lookup"><span data-stu-id="2870a-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="2870a-162">Knooppunten in een HDInsight-cluster hebben een interne IP-adres en de FQDN-naam die alleen toegankelijk zijn vanuit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="2870a-163">Bij het openen van services op Hallo-cluster met behulp van de interne FQDN of IP-adres hello, moet u Ambari tooverify Hallo IP of FQDN toouse gebruiken bij het openen van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="2870a-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="2870a-164">Bijvoorbeeld Hallo Oozie-service kan alleen worden uitgevoerd op één hoofdknooppunt en met behulp van Hallo `oozie` opdracht van een SSH-sessie Hallo URL toohello service is vereist.</span><span class="sxs-lookup"><span data-stu-id="2870a-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="2870a-165">Deze URL kan uit de Ambari worden opgehaald met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2870a-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="2870a-166">Met deze opdracht retourneert een waarde van een vergelijkbare toohello na de opdracht Hallo interne URL toouse Hello bevat `oozie` opdracht:</span><span class="sxs-lookup"><span data-stu-id="2870a-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="2870a-167">Zie voor meer informatie over het werken met Hallo Ambari REST-API [bewaken en beheren van HDInsight met behulp van Hallo Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="2870a-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="2870a-168">Toegang tot andere knooppunttypen</span><span class="sxs-lookup"><span data-stu-id="2870a-168">Accessing other node types</span></span>

<span data-ttu-id="2870a-169">U kunt verbinding maken toonodes die niet rechtstreeks toegankelijk via internet met behulp van de volgende methoden Hallo Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="2870a-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="2870a-170">**SSH**: eenmaal zijn verbonden tooa hoofdknooppunt via SSH, kunt u vervolgens SSH uit Hallo hoofdknooppunt tooconnect tooother knooppunten in cluster hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2870a-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="2870a-171">Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="2870a-172">**SSH-Tunnel**: als u een webservice die worden gehost op tooaccess moet een van Hallo knooppunten die niet beschikbaar gesteld toohello internet, moet u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="2870a-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="2870a-173">Zie voor meer informatie, Hallo [een SSH-tunnel gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="2870a-174">**Azure Virtual Network**: als uw cluster maakt deel uit van een virtueel netwerk in Azure een resource in HDInsight Hallo hetzelfde virtuele netwerk rechtstreeks toegang tot alle knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="2870a-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="2870a-175">Zie voor meer informatie, Hallo [uitbreiden HDInsight met behulp van Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="2870a-176">Hoe toocheck op de status van een service</span><span class="sxs-lookup"><span data-stu-id="2870a-176">How toocheck on a service status</span></span>

<span data-ttu-id="2870a-177">toocheck hello status van services die worden uitgevoerd op hoofdknooppunten Hallo Hallo Ambari-Webgebruikersinterface gebruiken of Hallo Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="2870a-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="2870a-178">Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="2870a-178">Ambari Web UI</span></span>

<span data-ttu-id="2870a-179">Hallo Ambari-Webgebruikersinterface is op https://CLUSTERNAME.azurehdinsight.net zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="2870a-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="2870a-180">Vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="2870a-181">Als u wordt gevraagd, voert u Hallo HTTP gebruikersreferenties voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="2870a-182">Hallo HTTP standaardgebruikersnaam is **admin** en Hallo wachtwoord is opgegeven bij het maken van de cluster Hallo Hallo-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="2870a-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="2870a-183">Wanneer u op Hallo Ambari pagina aankomt, vindt u op Hallo links van de pagina Hallo Hallo geïnstalleerd services.</span><span class="sxs-lookup"><span data-stu-id="2870a-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Geïnstalleerde services](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="2870a-185">Er zijn een reeks pictogrammen die kunnen worden weergegeven de volgende tooa tooindicate servicestatus.</span><span class="sxs-lookup"><span data-stu-id="2870a-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="2870a-186">Alle waarschuwingen gerelateerde tooa-service kan worden bekeken met Hallo **waarschuwingen** koppeling bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="2870a-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="2870a-187">U kunt elke service tooview meer informatie over het selecteren.</span><span class="sxs-lookup"><span data-stu-id="2870a-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="2870a-188">Tijdens het Hallo-servicepagina bevat informatie over het Hallo-status en configuratie van elke service, biedt het geen informatie waarop hoofdknooppunt Hallo-service wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="2870a-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="2870a-189">tooview deze informatie, gebruik Hallo **Hosts** koppeling bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="2870a-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="2870a-190">Deze pagina bevat hosts binnen het Hallo-cluster, inclusief Hallo hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2870a-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![lijst met hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="2870a-192">Selecteren Hallo-koppeling voor een van de hoofdknooppunten Hallo weergegeven Hallo services en onderdelen die op dat knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2870a-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Onderdeelstatus](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="2870a-194">Zie voor meer informatie over het gebruik van Ambari [bewaken en beheren van HDInsight met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="2870a-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="2870a-195">Ambari REST-API</span><span class="sxs-lookup"><span data-stu-id="2870a-195">Ambari REST API</span></span>

<span data-ttu-id="2870a-196">Hallo Ambari REST-API beschikbaar is via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="2870a-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="2870a-197">Hallo HDInsight openbare gateway verwerkt routering aanvragen toohello hoofdknooppunt waarop Hallo REST-API wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="2870a-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="2870a-198">U kunt Hallo opdracht toocheck Hallo status van een service via Hallo Ambari REST-API te volgen:</span><span class="sxs-lookup"><span data-stu-id="2870a-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="2870a-199">Vervang **wachtwoord** met het wachtwoord voor gebruikersaccount (admin) Hallo HTTP.</span><span class="sxs-lookup"><span data-stu-id="2870a-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="2870a-200">Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2870a-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="2870a-201">Vervang **SERVICENAME** met de naam van service Hallo Hallo gewenste toocheck Hallo status.</span><span class="sxs-lookup"><span data-stu-id="2870a-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="2870a-202">Bijvoorbeeld, toocheck Hallo status Hallo **HDFS** service op een cluster met de naam **mijncluster**, met een wachtwoord van **wachtwoord**, zou u Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2870a-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="2870a-203">Hallo-antwoord is vergelijkbaar toohello JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="2870a-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="2870a-204">Hallo URL geeft aan dat Hallo service momenteel wordt uitgevoerd op een hoofdknooppunt met de naam **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="2870a-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="2870a-205">Hallo status geeft aan dat de Hallo service momenteel wordt uitgevoerd, of **gestart**.</span><span class="sxs-lookup"><span data-stu-id="2870a-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="2870a-206">Als u niet welke services zijn geïnstalleerd op het Hallo-cluster weet, kunt u Hallo opdracht tooretrieve een lijst te volgen:</span><span class="sxs-lookup"><span data-stu-id="2870a-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="2870a-207">Zie voor meer informatie over het werken met Hallo Ambari REST-API [bewaken en beheren van HDInsight met behulp van Hallo Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="2870a-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="2870a-208">Serviceonderdelen</span><span class="sxs-lookup"><span data-stu-id="2870a-208">Service components</span></span>

<span data-ttu-id="2870a-209">Services kunnen de onderdelen die u wenst dat toocheck Hallo status van afzonderlijk bevatten.</span><span class="sxs-lookup"><span data-stu-id="2870a-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="2870a-210">HDFS bevat bijvoorbeeld Hallo NameNode onderdeel.</span><span class="sxs-lookup"><span data-stu-id="2870a-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="2870a-211">informatie over een onderdeel tooview Hallo opdracht zou zijn:</span><span class="sxs-lookup"><span data-stu-id="2870a-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="2870a-212">Als u niet welke onderdelen worden geleverd door een service weet, kunt u Hallo opdracht tooretrieve een lijst te volgen:</span><span class="sxs-lookup"><span data-stu-id="2870a-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="2870a-213">Hoe tooaccess logboekbestanden op Hallo hoofdknooppunten</span><span class="sxs-lookup"><span data-stu-id="2870a-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="2870a-214">SSH</span><span class="sxs-lookup"><span data-stu-id="2870a-214">SSH</span></span>

<span data-ttu-id="2870a-215">Tijdens het hoofdknooppunt verbonden tooa via SSH logboekbestanden kunnen worden gevonden in het **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="2870a-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="2870a-216">Bijvoorbeeld: **/var/log/hadoop-yarn/yarn** bevatten de logboeken voor YARN.</span><span class="sxs-lookup"><span data-stu-id="2870a-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="2870a-217">Elke hoofdknooppunt kan unieke logboekvermeldingen, hebben, dus moet u controleren Hallo van beide aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="2870a-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="2870a-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="2870a-218">SFTP</span></span>

<span data-ttu-id="2870a-219">U kunt ook verbinding maken met hoofdknooppunt toohello met Hallo SSH File Transfer Protocol of Secure File Transfer Protocol (SFTP) en logboekbestanden Hallo rechtstreeks downloaden.</span><span class="sxs-lookup"><span data-stu-id="2870a-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="2870a-220">Vergelijkbare toousing een SSH-client, wanneer u verbinding maakt toohello cluster moet u opgeven Hallo SSH gebruiker account naam en het Hallo SSH-adres van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="2870a-221">Bijvoorbeeld `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="2870a-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="2870a-222">Hallo wachtwoord opgeven voor Hallo account wanneer u wordt gevraagd, of geef een openbare sleutel met behulp van Hallo `-i` parameter.</span><span class="sxs-lookup"><span data-stu-id="2870a-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="2870a-223">Eenmaal zijn verbonden, krijgt u een `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="2870a-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="2870a-224">Vanaf deze prompt kunt u mappen, uploaden en downloaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="2870a-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="2870a-225">Bijvoorbeeld Hallo opdrachten na toohello mappen wijzigen **/var/log/hadoop/hdfs** directory en vervolgens alle bestanden in de directory hello te downloaden.</span><span class="sxs-lookup"><span data-stu-id="2870a-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="2870a-226">Voer voor een lijst met beschikbare opdrachten `help` op Hallo `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="2870a-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="2870a-227">Er zijn ook grafische interfaces waarmee u toovisualize Hallo bestandssysteem wanneer verbinding met SFTP.</span><span class="sxs-lookup"><span data-stu-id="2870a-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="2870a-228">Bijvoorbeeld: [MobaXTerm](http://mobaxterm.mobatek.net/) kunt u met behulp van een interface vergelijkbare tooWindows Explorer Hallo-bestandssysteem voor toobrowse.</span><span class="sxs-lookup"><span data-stu-id="2870a-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="2870a-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="2870a-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="2870a-230">tooaccess logboekbestanden met Ambari, moet u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="2870a-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="2870a-231">Hallo webinterfaces voor afzonderlijke services Hallo niet openbaar op Hallo Internet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2870a-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="2870a-232">Zie voor informatie over het gebruik van een SSH-tunnel Hallo [SSH-Tunneling gebruiken](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="2870a-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="2870a-233">Selecteer in de Hallo Ambari-Webgebruikersinterface, Hallo-service die u wenst dat tooview logboeken voor (bijvoorbeeld YARN).</span><span class="sxs-lookup"><span data-stu-id="2870a-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="2870a-234">Gebruik vervolgens **snelkoppelingen** tooselect welke hoofdknooppunt tooview Hallo logboeken voor.</span><span class="sxs-lookup"><span data-stu-id="2870a-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Met behulp van snelle koppelingen tooview Logboeken](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="2870a-236">Hoe tooconfigure knooppuntgrootte Hallo</span><span class="sxs-lookup"><span data-stu-id="2870a-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="2870a-237">Hallo-grootte van een knooppunt kan alleen worden ingeschakeld tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="2870a-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="2870a-238">U vindt een lijst met Hallo andere VM-grootten beschikbaar voor HDInsight op Hallo [HDInsight pagina met prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2870a-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="2870a-239">Wanneer u een cluster maakt, kunt u de grootte Hallo Hallo-knooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="2870a-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="2870a-240">Hallo volgende informatie bevat richtlijnen voor het gebruik van toospecify Hallo grootte Hallo [Azure-portal][preview-portal], [Azure PowerShell][azure-powershell], en Hallo [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="2870a-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="2870a-241">**Azure-portal**: wanneer u een cluster maakt, kunt u Hallo grootte van Hallo knooppunten gebruikt door Hallo cluster instellen:</span><span class="sxs-lookup"><span data-stu-id="2870a-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Afbeelding van het maken van clusterwizard met knooppunt grootte selectie](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="2870a-243">**Azure CLI**: bij gebruik van Hallo `azure hdinsight cluster create` uitvoert, en u kunt de grootte Hallo Hallo hoofd, worker en ZooKeeper-knooppunten instellen met behulp van Hallo `--headNodeSize`, `--workerNodeSize`, en `--zookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="2870a-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="2870a-244">**Azure PowerShell**: bij gebruik van Hallo `New-AzureRmHDInsightCluster` cmdlet, u kunt de grootte Hallo Hallo hoofd, worker en ZooKeeper-knooppunten instellen met behulp van Hallo `-HeadNodeVMSize`, `-WorkerNodeSize`, en `-ZookeeperNodeSize` parameters.</span><span class="sxs-lookup"><span data-stu-id="2870a-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2870a-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2870a-245">Next steps</span></span>

<span data-ttu-id="2870a-246">Gebruik Hallo koppelingen toolearn meer over elementen die worden vermeld in dit document te volgen.</span><span class="sxs-lookup"><span data-stu-id="2870a-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="2870a-247">Ambari REST-verwijzing</span><span class="sxs-lookup"><span data-stu-id="2870a-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="2870a-248">Installeer en configureer hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2870a-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="2870a-249">Azure PowerShell installeren en configureren </span><span class="sxs-lookup"><span data-stu-id="2870a-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2870a-250">HDInsight met Ambari beheren</span><span class="sxs-lookup"><span data-stu-id="2870a-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="2870a-251">Linux gebaseerde HDInsight-clusters inrichten</span><span class="sxs-lookup"><span data-stu-id="2870a-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
