---
title: aaaConfigure HBase-cluster-replicatie in virtuele netwerken - Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure HBase-replicatie voor de load balancer, hoge beschikbaarheid, nul uitvaltijd migratie/bijwerken van een HDInsight versie tooanother en herstel na noodgevallen.
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="d9ff9-103">HBase-cluster-replicatie in virtuele netwerken configureren</span><span class="sxs-lookup"><span data-stu-id="d9ff9-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="d9ff9-104">Meer informatie over hoe tooconfigure HBase-replicatie binnen één virtueel netwerk (VNet) of tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="d9ff9-105">Replicatie in een cluster maakt gebruik van een bron-push-methode.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="d9ff9-106">Een HBase-cluster kan een bron of bestemming, of beide functies tegelijk kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="d9ff9-107">Replicatie is asynchroon en Hallo doel van de replicatie is uiteindelijke consistentie.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="d9ff9-108">Wanneer een familie bewerken tooa kolom Hallo bron met de replicatie is ingeschakeld ontvangt, is dat de bewerkingsactie doorgegeven tooall doelclusters.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="d9ff9-109">Wanneer gegevens worden gerepliceerd van één cluster tooanother, zijn broncluster hello en alle clusters al verbruikt Hallo gegevens bijgehouden tooprevent replicatie lussen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="d9ff9-110">In deze zelfstudie configureert u de replicatie van een bron-doel.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="d9ff9-111">Zie voor andere clustertopologieën [Naslaggids voor Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="d9ff9-112">HBase-replicatie gebruik gevallen voor één virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="d9ff9-113">Taakverdeling--bijvoorbeeld scans of MapReduce-taken uitgevoerd op de doelcluster Hallo en ophalen van gegevens in de broncluster Hallo</span><span class="sxs-lookup"><span data-stu-id="d9ff9-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="d9ff9-114">Hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="d9ff9-114">High availability</span></span>
* <span data-ttu-id="d9ff9-115">Gegevens migreren van een HBase-cluster tooanother</span><span class="sxs-lookup"><span data-stu-id="d9ff9-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="d9ff9-116">Een Azure HDInsight-cluster upgraden van één versie tooanother</span><span class="sxs-lookup"><span data-stu-id="d9ff9-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="d9ff9-117">HBase-replicatie gebruik gevallen voor twee virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="d9ff9-118">Herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="d9ff9-118">Disaster recovery</span></span>
* <span data-ttu-id="d9ff9-119">Taakverdeling en toepassing hello partitioneren</span><span class="sxs-lookup"><span data-stu-id="d9ff9-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="d9ff9-120">Hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="d9ff9-120">High availability</span></span>

<span data-ttu-id="d9ff9-121">Replicatie van clusters met behulp van [script actie](hdinsight-hadoop-customize-cluster-linux.md) scripts zich bevindt op [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9ff9-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9ff9-122">Prerequisites</span></span>
<span data-ttu-id="d9ff9-123">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="d9ff9-124">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="d9ff9-125">Hallo-omgevingen configureren</span><span class="sxs-lookup"><span data-stu-id="d9ff9-125">Configure hello environments</span></span>

<span data-ttu-id="d9ff9-126">Er zijn drie mogelijke configuraties:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-126">There are three possible configurations:</span></span>

- <span data-ttu-id="d9ff9-127">Twee HBase-clusters in een virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="d9ff9-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="d9ff9-128">Twee HBase-clusters in twee verschillende virtuele netwerken in dezelfde regio Hallo</span><span class="sxs-lookup"><span data-stu-id="d9ff9-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="d9ff9-129">Twee HBase-clusters in twee verschillende virtuele netwerken in twee verschillende regio's (geo-replicatie)</span><span class="sxs-lookup"><span data-stu-id="d9ff9-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="d9ff9-130">toomake deze eenvoudiger tooconfigure Hallo-omgevingen, hebben wij enkele [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d9ff9-131">Als u liever tooconfigure Hallo omgevingen via andere methoden, Zie:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="d9ff9-132">Hadoop op basis van Linux-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9ff9-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="d9ff9-133">HBase-clusters maken in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d9ff9-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="d9ff9-134">Een virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="d9ff9-134">Configure one virtual network</span></span>

<span data-ttu-id="d9ff9-135">Klik op volgende installatiekopie toocreate twee HBase-clusters in Hallo Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="d9ff9-136">Hallo-sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="d9ff9-137">Twee virtuele netwerken configureren in Hallo dezelfde regio</span><span class="sxs-lookup"><span data-stu-id="d9ff9-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="d9ff9-138">Klik op volgende installatiekopie toocreate twee virtuele netwerken met VNet-peering en twee HBase-clusters in Hallo Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="d9ff9-139">Hallo-sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="d9ff9-140">In dit scenario moeten [VNet-peering](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="d9ff9-141">Hallo-sjabloon kunt VNet-peering.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="d9ff9-142">HBase-replicatie maakt gebruik van IP-adressen van Hallo ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="d9ff9-143">U kunt statische IP-adressen voor Hallo bestemming HBase ZooKeeper-knooppunten moet configureren.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="d9ff9-144">**tooconfigure statische IP-adressen**</span><span class="sxs-lookup"><span data-stu-id="d9ff9-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="d9ff9-145">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d9ff9-146">In het linkermenu hello, klikt u op **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="d9ff9-147">Klik op de resourcegroep die Hallo bestemming HBase-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="d9ff9-148">Dit is Hallo resourcegroep die u hebt opgegeven tijdens het gebruik van Hallo Resource Manager-sjabloon toocreate Hallo omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="d9ff9-149">U kunt Hallo filter toonarrow omlaag in de lijst hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="d9ff9-150">Hier ziet u een lijst met bronnen die twee virtuele netwerken Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="d9ff9-151">Klik op Hallo virtueel netwerk met Hallo bestemming HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="d9ff9-152">Bijvoorbeeld, klik op **xxxx vnet2**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="d9ff9-153">Ziet u drie apparaten met namen die met beginnen **nic-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="d9ff9-154">Deze apparaten zijn Hallo drie ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="d9ff9-155">Klik op een Hallo ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="d9ff9-156">Klik op **IP-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="d9ff9-157">Klik op **ipConfig1** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="d9ff9-158">Klik op **statische**, en noteer Hallo werkelijke IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="d9ff9-159">U moet Hallo IP-adres tijdens het uitvoeren van Hallo script actie tooenable replicatie.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![HDInsight HBase replicatie ZooKeeper vaste IP-adres](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="d9ff9-161">Herhaal stap 6 tooset Hallo statisch IP-adres voor Hallo andere twee ZooKeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="d9ff9-162">Hallo cross-VNet-scenario, moet u Hallo **- IP-** switch bij het aanroepen van Hallo **hdi_enable_replication.sh** script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="d9ff9-163">Twee virtuele netwerken configureren in twee verschillende regio 's</span><span class="sxs-lookup"><span data-stu-id="d9ff9-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="d9ff9-164">Klik op Hallo installatiekopie toocreate twee virtuele netwerken in twee verschillende regio's te volgen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="d9ff9-165">Hallo-sjabloon wordt opgeslagen in een openbare Azure Blob-container.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="d9ff9-166">Een VPN-gateway tussen Hallo twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="d9ff9-167">Zie voor instructies [een VNet maken met een site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="d9ff9-168">HBase-replicatie maakt gebruik van IP-adressen van Hallo ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="d9ff9-169">U kunt statische IP-adressen voor Hallo bestemming HBase ZooKeeper-knooppunten moet configureren.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="d9ff9-170">tooconfigure vaste IP-adres, raadpleegt u "configureren twee virtuele netwerken in hello dezelfde regio" Hallo-sectie in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="d9ff9-171">Hallo cross-VNet-scenario, moet u Hallo **- IP-** switch bij het aanroepen van Hallo **hdi_enable_replication.sh** script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="d9ff9-172">Testgegevens laden</span><span class="sxs-lookup"><span data-stu-id="d9ff9-172">Load test data</span></span>

<span data-ttu-id="d9ff9-173">Wanneer u een cluster repliceert, moet u Hallo tabellen tooreplicate opgeven.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="d9ff9-174">In deze sectie wordt u sommige gegevens in de broncluster Hallo geladen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="d9ff9-175">In de volgende sectie hello schakelt u replicatie tussen twee clusters met Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="d9ff9-176">Volg de instructies in Hallo [HBase-zelfstudie: aan de slag met Apache HBase met Hadoop op basis van Linux in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate een **contactpersonen** tabel en sommige gegevens in Hallo tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="d9ff9-177">Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="d9ff9-177">Enable replication</span></span>

<span data-ttu-id="d9ff9-178">Hallo stappen te volgen laten zien hoe toocall Hallo script actiescript vanaf hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="d9ff9-179">Zie voor het uitvoeren van een scriptactie met behulp van Azure PowerShell en hello Azure-opdrachtregelinterface (CLI), [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="d9ff9-180">**tooenable HBase-replicatie van hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="d9ff9-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="d9ff9-181">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d9ff9-182">Open Hallo bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="d9ff9-183">Klik op Hallo cluster menu **scriptacties**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="d9ff9-184">Klik op **nieuwe indienen** vanaf de bovenkant Hallo van Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="d9ff9-185">Selecteer of typ de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="d9ff9-186">**Naam**: Voer **replicatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="d9ff9-187">**Script-URL Bash**: Voer **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="d9ff9-188">**HEAD**: geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-188">**Head**: Selected.</span></span> <span data-ttu-id="d9ff9-189">Hallo Schakel andere knooppunttypen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="d9ff9-190">**Parameters**: Hallo volgende steekproef replicatie van de parameters inschakelen voor alle bestaande Hallo-tabellen en alle Hallo gegevens kopiëren van toohello doelcluster voor Hallo bron cluster:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="d9ff9-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-191">Click **Create**.</span></span> <span data-ttu-id="d9ff9-192">Hallo-script kan enige tijd duren, vooral wanneer Hallo - copydata argument wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="d9ff9-193">Vereiste argumenten:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-193">Required arguments:</span></span>

|<span data-ttu-id="d9ff9-194">Naam</span><span class="sxs-lookup"><span data-stu-id="d9ff9-194">Name</span></span>|<span data-ttu-id="d9ff9-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d9ff9-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="d9ff9-196">-s,--src-cluster</span><span class="sxs-lookup"><span data-stu-id="d9ff9-196">-s, --src-cluster</span></span> | <span data-ttu-id="d9ff9-197">Hallo DNS-naam opgeven van Hallo bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="d9ff9-198">Bijvoorbeeld: -s hbsrccluster,--src-cluster hbsrccluster =</span><span class="sxs-lookup"><span data-stu-id="d9ff9-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="d9ff9-199">-d,--zomertijd-cluster</span><span class="sxs-lookup"><span data-stu-id="d9ff9-199">-d, --dst-cluster</span></span> | <span data-ttu-id="d9ff9-200">Hallo DNS-naam opgeven van Hallo bestemming (replica) HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="d9ff9-201">Bijvoorbeeld: -s dsthbcluster,--src-cluster dsthbcluster =</span><span class="sxs-lookup"><span data-stu-id="d9ff9-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="d9ff9-202">-sp,--src-ambari-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d9ff9-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="d9ff9-203">Hallo beheerderswachtwoord opgeven voor Ambari op Hallo bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="d9ff9-204">-dp,--zomertijd-ambari-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d9ff9-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="d9ff9-205">Hallo beheerderswachtwoord opgeven voor Ambari op Hallo bestemming HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="d9ff9-206">Optionele argumenten:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-206">Optional arguments:</span></span>

|<span data-ttu-id="d9ff9-207">Naam</span><span class="sxs-lookup"><span data-stu-id="d9ff9-207">Name</span></span>|<span data-ttu-id="d9ff9-208">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d9ff9-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="d9ff9-209">-su,--src-ambari-gebruiker</span><span class="sxs-lookup"><span data-stu-id="d9ff9-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="d9ff9-210">Hallo beheerdersgebruikersnaam voor Ambari op Hallo bron HBase-cluster opgeven.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="d9ff9-211">de standaardwaarde Hallo is **admin**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="d9ff9-212">-du,--zomertijd-ambari-gebruiker</span><span class="sxs-lookup"><span data-stu-id="d9ff9-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="d9ff9-213">Hallo beheerdersgebruikersnaam voor Ambari op Hallo bestemming HBase-cluster opgeven.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="d9ff9-214">de standaardwaarde Hallo is **admin**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="d9ff9-215">-t,--lijst van de tabel</span><span class="sxs-lookup"><span data-stu-id="d9ff9-215">-t, --table-list</span></span> | <span data-ttu-id="d9ff9-216">Geef Hallo tabellen toobe gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="d9ff9-217">Bijvoorbeeld:--tabel lijst = 'Tabel1; tabel2; Tabel3'.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="d9ff9-218">Als u geen tabellen opgeeft, worden alle bestaande HBase-tabellen gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="d9ff9-219">-m,--machine</span><span class="sxs-lookup"><span data-stu-id="d9ff9-219">-m, --machine</span></span> | <span data-ttu-id="d9ff9-220">Geef Hallo hoofdknooppunt waar Hallo scriptactie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="d9ff9-221">Hallo-waarde is hn1 of hn0.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="d9ff9-222">Omdat hn0 meestal veelgebruikte is, wordt u aangeraden hn1.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="d9ff9-223">U kunt deze optie gebruiken bij waarvan u Hallo $0 script als een scriptactie hello HDInsight portal of Azure PowerShell uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="d9ff9-224">-ip</span><span class="sxs-lookup"><span data-stu-id="d9ff9-224">-ip</span></span> | <span data-ttu-id="d9ff9-225">Dit argument is vereist als u bij het inschakelen van replicatie tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="d9ff9-226">Dit argument fungeert als een switch toouse Hallo statische IP-adressen van ZooKeeper-knooppunten van replica-clusters in plaats van FQDN-namen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="d9ff9-227">Hallo statisch IP-adressen moet toobe vooraf geconfigureerd voordat u replicatie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="d9ff9-228">-cp - copydata</span><span class="sxs-lookup"><span data-stu-id="d9ff9-228">-cp, -copydata</span></span> | <span data-ttu-id="d9ff9-229">Schakel Hallo migratie van bestaande gegevens op Hallo tabellen waarvoor replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="d9ff9-230">-rpm, -repliceren-phoenix-metagegevens</span><span class="sxs-lookup"><span data-stu-id="d9ff9-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="d9ff9-231">Replicatie inschakelen voor Phoenix systeemtabellen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="d9ff9-232">*Gebruik deze optie voorzichtig.*</span><span class="sxs-lookup"><span data-stu-id="d9ff9-232">*Use this option with caution.*</span></span> <span data-ttu-id="d9ff9-233">U wordt aangeraden Phoenix tabellen op de replica-clusters opnieuw te maken voordat u dit script gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="d9ff9-234">-h,--help</span><span class="sxs-lookup"><span data-stu-id="d9ff9-234">-h, --help</span></span> | <span data-ttu-id="d9ff9-235">Gebruiksgegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-235">Display usage information.</span></span> |

<span data-ttu-id="d9ff9-236">Hallo print_usage() sectie Hallo [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) wordt een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="d9ff9-237">Nadat Hallo scriptactie met succes is kunt geïmplementeerd, u gebruiken SSH tooconnect toohello bestemming HBase-cluster, en controleer of Hallo gegevens zijn gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="d9ff9-238">Replicatie-scenario 's</span><span class="sxs-lookup"><span data-stu-id="d9ff9-238">Replication scenarios</span></span>

<span data-ttu-id="d9ff9-239">Hello volgende lijst ziet u enkele gevallen algemeen gebruik en de bijbehorende parameterinstellingen:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="d9ff9-240">**Replicatie inschakelen voor alle tabellen tussen clusters met twee Hallo**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="d9ff9-241">Dit scenario vereist geen Hallo kopie/migratie van bestaande gegevens op Hallo tabellen en gebruikt geen Phoenix tabellen.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="d9ff9-242">Hallo volgende parameters gebruikt:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="d9ff9-243">**Replicatie inschakelen voor specifieke tabellen**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="d9ff9-244">Volgende parameters tooenable replicatie op table1 en table2 Tabel3 hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="d9ff9-245">**Replicatie inschakelen voor specifieke tabellen en kopieer de bestaande gegevens Hallo**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="d9ff9-246">Volgende parameters tooenable replicatie op table1 en table2 Tabel3 hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="d9ff9-247">**Replicatie inschakelen voor alle tabellen met phoenix metagegevens van de bron toodestination repliceren**.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="d9ff9-248">Phoenix metagegevens replicatie is niet perfect en wees voorzichtig met moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="d9ff9-249">Kopiëren en gegevens migreren</span><span class="sxs-lookup"><span data-stu-id="d9ff9-249">Copy and migrate data</span></span>

<span data-ttu-id="d9ff9-250">Er zijn twee afzonderlijke script actie scripts voor het kopiëren van/migreren van gegevens na de replicatie is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="d9ff9-251">[Script voor kleine tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (enkele gigabytes in grootte en de algehele kopie is verwachte toofinish in minder dan één uur)</span><span class="sxs-lookup"><span data-stu-id="d9ff9-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="d9ff9-252">[Script voor grote tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (meer dan één uur toocopy tootake verwacht)</span><span class="sxs-lookup"><span data-stu-id="d9ff9-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="d9ff9-253">Kunt u dezelfde procedure in Hallo [replicatie inschakelen](#enable-replication) toocall hello scriptactie Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="d9ff9-254">Hallo print_usage() sectie Hallo [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) bevat een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="d9ff9-255">Scenario's</span><span class="sxs-lookup"><span data-stu-id="d9ff9-255">Scenarios</span></span>

- <span data-ttu-id="d9ff9-256">**Kopiëren van specifieke tabellen (test1, test2 en test3) voor alle rijen bewerkt tot nu toe (huidige tijdstempel)**:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="d9ff9-257">of</span><span class="sxs-lookup"><span data-stu-id="d9ff9-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="d9ff9-258">**Kopiëren van specifieke tabellen met een opgegeven tijdperiode**:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="d9ff9-259">Schakel replicatie uit</span><span class="sxs-lookup"><span data-stu-id="d9ff9-259">Disable replication</span></span>

<span data-ttu-id="d9ff9-260">toodisable replicatie, gebruikt u een ander script actiescript zich bevindt op [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="d9ff9-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="d9ff9-261">Kunt u dezelfde procedure in Hallo [replicatie inschakelen](#enable-replication) toocall hello scriptactie Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="d9ff9-262">Hallo print_usage() sectie Hallo [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) wordt een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="d9ff9-263">Scenario's</span><span class="sxs-lookup"><span data-stu-id="d9ff9-263">Scenarios</span></span>

- <span data-ttu-id="d9ff9-264">**Schakel replicatie op alle tabellen**:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="d9ff9-265">of</span><span class="sxs-lookup"><span data-stu-id="d9ff9-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="d9ff9-266">**Schakel replicatie op de opgegeven tabellen (Tabel1, tabel2 en Tabel3)**:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="d9ff9-267">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9ff9-267">Next steps</span></span>

<span data-ttu-id="d9ff9-268">In deze zelfstudie hebt u geleerd hoe tooconfigure HBase-replicatie tussen twee datacentra.</span><span class="sxs-lookup"><span data-stu-id="d9ff9-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="d9ff9-269">toolearn meer informatie over HDInsight en HBase, Zie:</span><span class="sxs-lookup"><span data-stu-id="d9ff9-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="d9ff9-270">[Aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="d9ff9-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="d9ff9-271">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="d9ff9-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="d9ff9-272">[HBase-clusters maken in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="d9ff9-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="d9ff9-273">[Realtime Twitter-gevoel met HBase analyseren][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="d9ff9-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="d9ff9-274">[Analyseren van sensorgegevens met Storm en HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="d9ff9-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
