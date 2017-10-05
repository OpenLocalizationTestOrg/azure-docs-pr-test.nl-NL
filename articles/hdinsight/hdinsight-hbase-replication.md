---
title: HBase-cluster-replicatie in virtuele netwerken - Azure configureren | Microsoft Docs
description: Informatie over het configureren van HBase-replicatie voor taakverdeling, hoge beschikbaarheid, nul uitvaltijd migratie/bijwerken van een HDInsight versie naar een andere en herstel na noodgevallen.
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="5ce2b-103">HBase-cluster-replicatie in virtuele netwerken configureren</span><span class="sxs-lookup"><span data-stu-id="5ce2b-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="5ce2b-104">Informatie over het configureren van HBase-replicatie binnen één virtueel netwerk (VNet) of tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="5ce2b-105">Replicatie in een cluster maakt gebruik van een bron-push-methode.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="5ce2b-106">Een HBase-cluster kan een bron of bestemming, of beide functies tegelijk kunnen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="5ce2b-107">Replicatie is asynchroon en het doel van de replicatie is uiteindelijke consistentie.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="5ce2b-108">Als de bron een bewerking naar de kolomfamilie voor een met de replicatie is ingeschakeld ontvangt, wordt die bewerken doorgegeven aan alle doelclusters.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="5ce2b-109">Wanneer gegevens worden gerepliceerd van de ene cluster naar een andere, worden de broncluster en alle clusters die de gegevens al hebt gebruikt om te voorkomen dat replicatie lussen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="5ce2b-110">In deze zelfstudie configureert u de replicatie van een bron-doel.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="5ce2b-111">Zie voor andere clustertopologieën [Naslaggids voor Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="5ce2b-112">HBase-replicatie gebruik gevallen voor één virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="5ce2b-113">Taakverdeling--bijvoorbeeld scans of MapReduce-taken uitgevoerd op het doelcluster en ophalen van gegevens in de broncluster</span><span class="sxs-lookup"><span data-stu-id="5ce2b-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="5ce2b-114">Hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="5ce2b-114">High availability</span></span>
* <span data-ttu-id="5ce2b-115">Migreren van gegevens van een HBase-cluster naar een andere</span><span class="sxs-lookup"><span data-stu-id="5ce2b-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="5ce2b-116">Een Azure HDInsight-cluster upgraden met één versie naar een andere</span><span class="sxs-lookup"><span data-stu-id="5ce2b-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="5ce2b-117">HBase-replicatie gebruik gevallen voor twee virtuele netwerken:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="5ce2b-118">Herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="5ce2b-118">Disaster recovery</span></span>
* <span data-ttu-id="5ce2b-119">Taakverdeling en partitioneren van de toepassing</span><span class="sxs-lookup"><span data-stu-id="5ce2b-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="5ce2b-120">Hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="5ce2b-120">High availability</span></span>

<span data-ttu-id="5ce2b-121">Replicatie van clusters met behulp van [script actie](hdinsight-hadoop-customize-cluster-linux.md) scripts zich bevindt op [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ce2b-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5ce2b-122">Prerequisites</span></span>
<span data-ttu-id="5ce2b-123">Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5ce2b-124">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="5ce2b-125">De omgevingen configureren</span><span class="sxs-lookup"><span data-stu-id="5ce2b-125">Configure the environments</span></span>

<span data-ttu-id="5ce2b-126">Er zijn drie mogelijke configuraties:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-126">There are three possible configurations:</span></span>

- <span data-ttu-id="5ce2b-127">Twee HBase-clusters in een virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="5ce2b-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="5ce2b-128">Twee HBase-clusters in twee verschillende virtuele netwerken in dezelfde regio</span><span class="sxs-lookup"><span data-stu-id="5ce2b-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="5ce2b-129">Twee HBase-clusters in twee verschillende virtuele netwerken in twee verschillende regio's (geo-replicatie)</span><span class="sxs-lookup"><span data-stu-id="5ce2b-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="5ce2b-130">Voor het configureren van de omgevingen te vereenvoudigen hebben wij enkele [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5ce2b-131">Als u liever de omgevingen met behulp van andere methoden configureren, Zie:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="5ce2b-132">Hadoop op basis van Linux-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ce2b-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="5ce2b-133">HBase-clusters maken in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5ce2b-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="5ce2b-134">Een virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="5ce2b-134">Configure one virtual network</span></span>

<span data-ttu-id="5ce2b-135">Klik op de volgende afbeelding om twee HBase-clusters maken in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="5ce2b-136">De sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="5ce2b-137">Twee virtuele netwerken configureren in dezelfde regio</span><span class="sxs-lookup"><span data-stu-id="5ce2b-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="5ce2b-138">Klik op de volgende afbeelding om twee virtuele netwerken met VNet-peering en twee HBase-clusters maken in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="5ce2b-139">De sjabloon wordt opgeslagen in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="5ce2b-140">In dit scenario moeten [VNet-peering](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="5ce2b-141">De sjabloon kunt VNet-peering.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="5ce2b-142">HBase-replicatie maakt gebruik van IP-adressen van de ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="5ce2b-143">U kunt statische IP-adressen voor de bestemming HBase ZooKeeper-knooppunten moet configureren.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="5ce2b-144">**Statische IP-adressen configureren**</span><span class="sxs-lookup"><span data-stu-id="5ce2b-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="5ce2b-145">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5ce2b-146">Klik in het menu links op **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="5ce2b-147">Klik op de resourcegroep die het doel HBase-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="5ce2b-148">Dit is de resourcegroep die u hebt opgegeven wanneer u de Resource Manager-sjabloon gebruikt om de omgeving te maken.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="5ce2b-149">Beperken van de lijst kunt u het filter.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="5ce2b-150">Hier ziet u een lijst met bronnen die de twee virtuele netwerken bevat.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="5ce2b-151">Klik op het virtuele netwerk waarin het doel HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="5ce2b-152">Bijvoorbeeld, klik op **xxxx vnet2**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="5ce2b-153">Ziet u drie apparaten met namen die met beginnen **nic-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="5ce2b-154">Deze apparaten zijn de drie ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="5ce2b-155">Klik op een van de ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="5ce2b-156">Klik op **IP-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="5ce2b-157">Klik op **ipConfig1** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="5ce2b-158">Klik op **statische**, en noteer de IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="5ce2b-159">U moet het IP-adres tijdens het uitvoeren van de scriptactie replicatie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![HDInsight HBase replicatie ZooKeeper vaste IP-adres](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="5ce2b-161">Herhaal stap 6 instellen van het statische IP-adres voor de andere twee ZooKeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="5ce2b-162">Voor het scenario voor cross-VNet, moet u de **- IP-** switch bij het aanroepen van de **hdi_enable_replication.sh** script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="5ce2b-163">Twee virtuele netwerken configureren in twee verschillende regio 's</span><span class="sxs-lookup"><span data-stu-id="5ce2b-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="5ce2b-164">Klik op de volgende afbeelding om twee virtuele netwerken maken in twee verschillende regio's.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="5ce2b-165">De sjabloon wordt opgeslagen in een openbare Azure Blob-container.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="5ce2b-166">Een VPN-gateway tussen de twee virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="5ce2b-167">Zie voor instructies [een VNet maken met een site-naar-site-verbinding](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="5ce2b-168">HBase-replicatie maakt gebruik van IP-adressen van de ZooKeeper virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="5ce2b-169">U kunt statische IP-adressen voor de bestemming HBase ZooKeeper-knooppunten moet configureren.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="5ce2b-170">Zie de sectie 'Twee virtuele netwerken configureren in dezelfde regio' in dit artikel voor het configureren van vaste IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="5ce2b-171">Voor het scenario voor cross-VNet, moet u de **- IP-** switch bij het aanroepen van de **hdi_enable_replication.sh** script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="5ce2b-172">Testgegevens laden</span><span class="sxs-lookup"><span data-stu-id="5ce2b-172">Load test data</span></span>

<span data-ttu-id="5ce2b-173">Wanneer u een cluster repliceert, moet u de tabellen te repliceren.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="5ce2b-174">In deze sectie wordt u sommige gegevens in de broncluster geladen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="5ce2b-175">In de volgende sectie schakelt u replicatie tussen de twee clusters.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="5ce2b-176">Volg de instructies in [HBase-zelfstudie: aan de slag met Apache HBase met Hadoop op basis van Linux in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) maken een **contactpersonen** tabel en sommige gegevens in de tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="5ce2b-177">Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="5ce2b-177">Enable replication</span></span>

<span data-ttu-id="5ce2b-178">De volgende stappen laten zien hoe het script actiescript aanroepen vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="5ce2b-179">Zie voor het uitvoeren van een scriptactie met behulp van Azure PowerShell en de Azure-opdrachtregelinterface (CLI), [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="5ce2b-180">**HBase-replicatie van de Azure-portal in te schakelen**</span><span class="sxs-lookup"><span data-stu-id="5ce2b-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="5ce2b-181">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5ce2b-182">Open de bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="5ce2b-183">Klik op het menu cluster **scriptacties**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="5ce2b-184">Klik op **nieuwe indienen** vanaf de bovenkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="5ce2b-185">Selecteer of Voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="5ce2b-186">**Naam**: Voer **replicatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="5ce2b-187">**Script-URL Bash**: Voer **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="5ce2b-188">**HEAD**: geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-188">**Head**: Selected.</span></span> <span data-ttu-id="5ce2b-189">De knooppunttypen wissen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-189">Clear the other node types.</span></span>
  - <span data-ttu-id="5ce2b-190">**Parameters**: het volgende voorbeeld parameters replicatie inschakelen voor de bestaande tabellen en kopieer alle gegevens van de bron-cluster naar het doelcluster:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="5ce2b-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-191">Click **Create**.</span></span> <span data-ttu-id="5ce2b-192">Het script kan enige tijd duren, vooral wanneer het argument - copydata wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="5ce2b-193">Vereiste argumenten:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-193">Required arguments:</span></span>

|<span data-ttu-id="5ce2b-194">Naam</span><span class="sxs-lookup"><span data-stu-id="5ce2b-194">Name</span></span>|<span data-ttu-id="5ce2b-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5ce2b-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="5ce2b-196">-s,--src-cluster</span><span class="sxs-lookup"><span data-stu-id="5ce2b-196">-s, --src-cluster</span></span> | <span data-ttu-id="5ce2b-197">Geef de DNS-naam van de bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="5ce2b-198">Bijvoorbeeld: -s hbsrccluster,--src-cluster hbsrccluster =</span><span class="sxs-lookup"><span data-stu-id="5ce2b-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="5ce2b-199">-d,--zomertijd-cluster</span><span class="sxs-lookup"><span data-stu-id="5ce2b-199">-d, --dst-cluster</span></span> | <span data-ttu-id="5ce2b-200">Geef de DNS-naam van het doel (replica) HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="5ce2b-201">Bijvoorbeeld: -s dsthbcluster,--src-cluster dsthbcluster =</span><span class="sxs-lookup"><span data-stu-id="5ce2b-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="5ce2b-202">-sp,--src-ambari-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="5ce2b-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="5ce2b-203">Geef het beheerderswachtwoord voor Ambari op de bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="5ce2b-204">-dp,--zomertijd-ambari-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="5ce2b-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="5ce2b-205">Geef het beheerderswachtwoord voor Ambari op de doelcluster HBase.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="5ce2b-206">Optionele argumenten:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-206">Optional arguments:</span></span>

|<span data-ttu-id="5ce2b-207">Naam</span><span class="sxs-lookup"><span data-stu-id="5ce2b-207">Name</span></span>|<span data-ttu-id="5ce2b-208">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5ce2b-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="5ce2b-209">-su,--src-ambari-gebruiker</span><span class="sxs-lookup"><span data-stu-id="5ce2b-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="5ce2b-210">Geef de gebruikersnaam van de beheerder voor Ambari op de bron HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="5ce2b-211">De standaardwaarde is **admin**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="5ce2b-212">-du,--zomertijd-ambari-gebruiker</span><span class="sxs-lookup"><span data-stu-id="5ce2b-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="5ce2b-213">Geef de gebruikersnaam van de beheerder voor Ambari op de doelcluster HBase.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="5ce2b-214">De standaardwaarde is **admin**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="5ce2b-215">-t,--lijst van de tabel</span><span class="sxs-lookup"><span data-stu-id="5ce2b-215">-t, --table-list</span></span> | <span data-ttu-id="5ce2b-216">Geef de tabellen worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="5ce2b-217">Bijvoorbeeld:--tabel lijst = 'Tabel1; tabel2; Tabel3'.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="5ce2b-218">Als u geen tabellen opgeeft, worden alle bestaande HBase-tabellen gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="5ce2b-219">-m,--machine</span><span class="sxs-lookup"><span data-stu-id="5ce2b-219">-m, --machine</span></span> | <span data-ttu-id="5ce2b-220">Geef het hoofdknooppunt waar de scriptactie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="5ce2b-221">De waarde is hn1 of hn0.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="5ce2b-222">Omdat hn0 meestal veelgebruikte is, wordt u aangeraden hn1.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="5ce2b-223">U kunt deze optie gebruiken als u het script $0 als de scriptactie van een van de HDInsight-portal of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="5ce2b-224">-ip</span><span class="sxs-lookup"><span data-stu-id="5ce2b-224">-ip</span></span> | <span data-ttu-id="5ce2b-225">Dit argument is vereist als u bij het inschakelen van replicatie tussen twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="5ce2b-226">Dit argument fungeert als een overschakelen naar de statische IP-adressen van ZooKeeper-knooppunten uit replica clusters gebruiken in plaats van FQDN-namen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="5ce2b-227">De statische IP-adressen moeten vooraf geconfigureerde voordat u replicatie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="5ce2b-228">-cp - copydata</span><span class="sxs-lookup"><span data-stu-id="5ce2b-228">-cp, -copydata</span></span> | <span data-ttu-id="5ce2b-229">Schakel de migratie van bestaande gegevens op de tabellen waarvoor replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="5ce2b-230">-rpm, -repliceren-phoenix-metagegevens</span><span class="sxs-lookup"><span data-stu-id="5ce2b-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="5ce2b-231">Replicatie inschakelen voor Phoenix systeemtabellen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="5ce2b-232">*Gebruik deze optie voorzichtig.*</span><span class="sxs-lookup"><span data-stu-id="5ce2b-232">*Use this option with caution.*</span></span> <span data-ttu-id="5ce2b-233">U wordt aangeraden Phoenix tabellen op de replica-clusters opnieuw te maken voordat u dit script gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="5ce2b-234">-h,--help</span><span class="sxs-lookup"><span data-stu-id="5ce2b-234">-h, --help</span></span> | <span data-ttu-id="5ce2b-235">Gebruiksgegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-235">Display usage information.</span></span> |

<span data-ttu-id="5ce2b-236">De sectie print_usage() van de [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) wordt een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="5ce2b-237">Nadat de scriptactie is geïmplementeerd, kunt u SSH verbinding maken met het doelcluster HBase en controleer of dat de gegevens zijn gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="5ce2b-238">Replicatie-scenario 's</span><span class="sxs-lookup"><span data-stu-id="5ce2b-238">Replication scenarios</span></span>

<span data-ttu-id="5ce2b-239">De volgende lijst ziet u enkele gevallen algemeen gebruik en de bijbehorende parameterinstellingen:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="5ce2b-240">**Replicatie inschakelen voor alle tabellen tussen twee clusters**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="5ce2b-241">Dit scenario is niet vereist voor de kopie/migratie van bestaande gegevens op de tabellen en gebruikt geen Phoenix tabellen.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="5ce2b-242">Gebruik de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="5ce2b-243">**Replicatie inschakelen voor specifieke tabellen**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="5ce2b-244">De volgende parameters gebruiken om replicatie van table1 en table2 Tabel3 in te schakelen:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="5ce2b-245">**Replicatie inschakelen voor specifieke tabellen en kopieer de bestaande gegevens**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="5ce2b-246">De volgende parameters gebruiken om replicatie van table1 en table2 Tabel3 in te schakelen:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="5ce2b-247">**Replicatie inschakelen voor alle tabellen met het repliceren van phoenix metagegevens van bron naar doel**.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="5ce2b-248">Phoenix metagegevens replicatie is niet perfect en wees voorzichtig met moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="5ce2b-249">Kopiëren en gegevens migreren</span><span class="sxs-lookup"><span data-stu-id="5ce2b-249">Copy and migrate data</span></span>

<span data-ttu-id="5ce2b-250">Er zijn twee afzonderlijke script actie scripts voor het kopiëren van/migreren van gegevens na de replicatie is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="5ce2b-251">[Script voor kleine tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (enkele gigabytes in grootte en de algehele kopie is voltooid in minder dan een uur verwacht)</span><span class="sxs-lookup"><span data-stu-id="5ce2b-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="5ce2b-252">[Script voor grote tabellen](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (verwachte langer duurt dan een uur kopiëren)</span><span class="sxs-lookup"><span data-stu-id="5ce2b-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="5ce2b-253">Kunt u dezelfde procedure in [replicatie inschakelen](#enable-replication) aanroepen van de scriptactie met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="5ce2b-254">De sectie print_usage() van de [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) bevat een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="5ce2b-255">Scenario's</span><span class="sxs-lookup"><span data-stu-id="5ce2b-255">Scenarios</span></span>

- <span data-ttu-id="5ce2b-256">**Kopiëren van specifieke tabellen (test1, test2 en test3) voor alle rijen bewerkt tot nu toe (huidige tijdstempel)**:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="5ce2b-257">of</span><span class="sxs-lookup"><span data-stu-id="5ce2b-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="5ce2b-258">**Kopiëren van specifieke tabellen met een opgegeven tijdperiode**:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="5ce2b-259">Schakel replicatie uit</span><span class="sxs-lookup"><span data-stu-id="5ce2b-259">Disable replication</span></span>

<span data-ttu-id="5ce2b-260">Als replicatie wilt uitschakelen, gebruikt u een ander script actiescript zich bevindt op [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="5ce2b-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="5ce2b-261">Kunt u dezelfde procedure in [replicatie inschakelen](#enable-replication) aanroepen van de scriptactie met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="5ce2b-262">De sectie print_usage() van de [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) wordt een gedetailleerde beschrijving van parameters.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="5ce2b-263">Scenario's</span><span class="sxs-lookup"><span data-stu-id="5ce2b-263">Scenarios</span></span>

- <span data-ttu-id="5ce2b-264">**Schakel replicatie op alle tabellen**:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="5ce2b-265">of</span><span class="sxs-lookup"><span data-stu-id="5ce2b-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="5ce2b-266">**Schakel replicatie op de opgegeven tabellen (Tabel1, tabel2 en Tabel3)**:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="5ce2b-267">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ce2b-267">Next steps</span></span>

<span data-ttu-id="5ce2b-268">In deze zelfstudie hebt u geleerd hoe het configureren van HBase-replicatie tussen twee datacentra.</span><span class="sxs-lookup"><span data-stu-id="5ce2b-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="5ce2b-269">Zie voor meer informatie over HDInsight en HBase:</span><span class="sxs-lookup"><span data-stu-id="5ce2b-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="5ce2b-270">[Aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="5ce2b-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="5ce2b-271">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="5ce2b-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="5ce2b-272">[HBase-clusters maken in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="5ce2b-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="5ce2b-273">[Realtime Twitter-gevoel met HBase analyseren][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="5ce2b-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="5ce2b-274">[Analyseren van sensorgegevens met Storm en HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="5ce2b-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
