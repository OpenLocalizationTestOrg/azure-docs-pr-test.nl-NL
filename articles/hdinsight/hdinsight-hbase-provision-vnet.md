---
title: aaaCreate HBase-clusters in een virtueel netwerk - Azure | Microsoft Docs
description: Aan de slag met HBase in Azure HDInsight. Meer informatie over hoe toocreate HDInsight HBase-clusters op Azure Virtual Network.
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="63ed9-104">HBase-clusters maken in HDInsight in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="63ed9-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="63ed9-105">Meer informatie over hoe toocreate Azure HDInsight HBase-clusters in een [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="63ed9-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="63ed9-106">Aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden toepassingen rechtstreeks met HBase kunnen communiceren.</span><span class="sxs-lookup"><span data-stu-id="63ed9-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="63ed9-107">Hallo voordelen zijn:</span><span class="sxs-lookup"><span data-stu-id="63ed9-107">hello benefits include:</span></span>

* <span data-ttu-id="63ed9-108">Directe verbinding Hallo web application toohello knooppunten van de HBase-cluster hello, waarmee communicatie via externe procedureaanroepen HBase Java call (RPC) API's.</span><span class="sxs-lookup"><span data-stu-id="63ed9-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="63ed9-109">Verbeterde prestaties omdat u niet hoeft uw verkeer Ga via meerdere gateways en load balancers.</span><span class="sxs-lookup"><span data-stu-id="63ed9-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="63ed9-110">Hallo mogelijkheid tooprocess gevoelige informatie op een veiliger manier zonder een openbaar eindpunt bloot te stellen.</span><span class="sxs-lookup"><span data-stu-id="63ed9-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="63ed9-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63ed9-111">Prerequisites</span></span>
<span data-ttu-id="63ed9-112">Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="63ed9-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="63ed9-113">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-113">**An Azure subscription**.</span></span> <span data-ttu-id="63ed9-114">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="63ed9-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="63ed9-115">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="63ed9-116">Zie [installeren en gebruiken Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="63ed9-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="63ed9-117">HBase-cluster in virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="63ed9-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="63ed9-118">In deze sectie maakt u een Linux-gebaseerde HBase-cluster maken met Hallo afhankelijke Azure Storage-account aan een virtuele Azure-netwerk met een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="63ed9-119">Voor andere methoden voor het maken van cluster en inzicht Hallo-instellingen, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="63ed9-120">Zie voor meer informatie over het gebruik van een sjabloon toocreate Hadoop-clusters in HDInsight, [maken Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="63ed9-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="63ed9-121">Sommige eigenschappen zijn hardgecodeerd in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="63ed9-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="63ed9-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63ed9-122">For example:</span></span>
>
> * <span data-ttu-id="63ed9-123">**Locatie**: VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="63ed9-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="63ed9-124">**Clusterversie**: 3.5</span><span class="sxs-lookup"><span data-stu-id="63ed9-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="63ed9-125">**Aantal worker-knooppunten cluster**: 2</span><span class="sxs-lookup"><span data-stu-id="63ed9-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="63ed9-126">**Storage-account standaard**: een unieke tekenreeks</span><span class="sxs-lookup"><span data-stu-id="63ed9-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="63ed9-127">**Virtuele-netwerknaam**: &lt;Clusternaam >-vnet</span><span class="sxs-lookup"><span data-stu-id="63ed9-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="63ed9-128">**Adresruimte voor virtueel netwerk**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="63ed9-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="63ed9-129">**De subnetnaam van het**: subnet1</span><span class="sxs-lookup"><span data-stu-id="63ed9-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="63ed9-130">**Adresbereik van**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="63ed9-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="63ed9-131">&lt;Clusternaam > is vervangen door de clusternaam Hallo u opgeven wanneer Hallo-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63ed9-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="63ed9-132">Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="63ed9-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="63ed9-133">Hallo-sjabloon bevindt zich in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="63ed9-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="63ed9-134">Van Hallo **aangepaste implementatie** blade Voer Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="63ed9-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="63ed9-135">**Abonnement**: Selecteer een Azure-abonnement gebruikt toocreate hello HDInsight-cluster, Hallo afhankelijke opslagaccount en Hallo virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="63ed9-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="63ed9-136">**Resourcegroep**: Selecteer **nieuw**, en geef een nieuwe Resourcegroepnaam.</span><span class="sxs-lookup"><span data-stu-id="63ed9-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="63ed9-137">**Locatie**: Selecteer een locatie voor resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="63ed9-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="63ed9-138">**Clusternaam**: Voer een naam voor Hallo Hadoop-cluster toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="63ed9-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="63ed9-139">**Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="63ed9-140">**SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="63ed9-141">U kunt de naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="63ed9-141">You can rename it.</span></span>
   * <span data-ttu-id="63ed9-142">**Ik ga akkoord toohello voorwaarden Hallo hierboven**: (selecteren)</span><span class="sxs-lookup"><span data-stu-id="63ed9-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="63ed9-143">Klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-143">Click **Purchase**.</span></span> <span data-ttu-id="63ed9-144">Het duurt ongeveer 20 minuten toocreate een cluster.</span><span class="sxs-lookup"><span data-stu-id="63ed9-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="63ed9-145">Zodra het Hallo-cluster is gemaakt, klikt u op Hallo cluster-blade in de portal tooopen Hallo deze.</span><span class="sxs-lookup"><span data-stu-id="63ed9-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="63ed9-146">Nadat u Hallo-zelfstudie hebt voltooid, kunt u toodelete Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="63ed9-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="63ed9-147">Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63ed9-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="63ed9-148">Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63ed9-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="63ed9-149">Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="63ed9-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="63ed9-150">Zie voor instructies van het verwijderen van een cluster Hallo [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="63ed9-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="63ed9-151">toobegin werken met uw nieuwe HBase-cluster, kunt u Hallo procedures gevonden in [aan de slag met HBase met Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="63ed9-152">Verbinding maken met toohello HBase-cluster met HBase Java RPC-API 's</span><span class="sxs-lookup"><span data-stu-id="63ed9-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="63ed9-153">Maken van een infrastructuur als een dienst (IaaS) virtuele machine in hetzelfde virtuele Azure-netwerk Hallo en Hallo hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="63ed9-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="63ed9-154">Zie voor instructies over het maken van een nieuwe virtuele machine voor IaaS [maken van een virtuele Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="63ed9-155">Wanneer Hallo stappen in dit document uitvoert, moet u de volgende waarden voor de netwerkconfiguratie Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63ed9-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="63ed9-156">**Virtueel netwerk**: &lt;Clusternaam >-vnet</span><span class="sxs-lookup"><span data-stu-id="63ed9-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="63ed9-157">**Subnet**: subnet1</span><span class="sxs-lookup"><span data-stu-id="63ed9-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="63ed9-158">Vervang &lt;Clusternaam > met Hallo-naam die u hebt gebruikt bij het maken van Hallo HDInsight-cluster in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="63ed9-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="63ed9-159">Met deze waarden, Hallo virtuele machine wordt geplaatst in Hallo hetzelfde virtuele netwerk en subnet als Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="63ed9-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="63ed9-160">Deze configuratie kan ze toodirectly met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="63ed9-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="63ed9-161">Er is een toocreate manier een HDInsight-cluster met een leeg edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="63ed9-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="63ed9-162">Hallo edge-knooppunt kan worden gebruikt toomanage Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="63ed9-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="63ed9-163">Zie voor meer informatie [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="63ed9-164">Wanneer u een Java-toepassing tooconnect tooHBase op afstand gebruikt, moet u Hallo volledig gekwalificeerde domeinnaam (FQDN).</span><span class="sxs-lookup"><span data-stu-id="63ed9-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="63ed9-165">toodetermine, moet u Hallo verbindingsspecifieke DNS-achtervoegsel van de HBase-cluster Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="63ed9-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="63ed9-166">toodo, kunt u een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63ed9-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="63ed9-167">Een Web browser toomake een oproep Ambari gebruiken:</span><span class="sxs-lookup"><span data-stu-id="63ed9-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="63ed9-168">Blader toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / als host fungeert voor? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="63ed9-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="63ed9-169">Hiermee schakelt u een JSON-bestand met Hallo DNS-achtervoegsels.</span><span class="sxs-lookup"><span data-stu-id="63ed9-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="63ed9-170">Gebruik Hallo Ambari-website:</span><span class="sxs-lookup"><span data-stu-id="63ed9-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="63ed9-171">Te bladeren https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="63ed9-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="63ed9-172">Klik op **Hosts** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="63ed9-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="63ed9-173">Gebruik Curl toomake REST-aanroepen:</span><span class="sxs-lookup"><span data-stu-id="63ed9-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="63ed9-174">Hallo JSON JavaScript Object Notation ()-gegevens geretourneerd, Hallo 'hostnaam' vermelding te vinden.</span><span class="sxs-lookup"><span data-stu-id="63ed9-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="63ed9-175">Het bevat Hallo FQDN voor Hallo knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="63ed9-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="63ed9-176">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63ed9-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="63ed9-177">Hallo-gedeelte van Hallo domein naam die begint met de naam van de cluster Hallo is Hallo DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="63ed9-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="63ed9-178">Bijvoorbeeld: mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="63ed9-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="63ed9-179">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="63ed9-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="63ed9-180">Gebruik hello Azure PowerShell-script tooregister Hallo na **Get-ClusterDetail** functie, die gebruikt tooreturn Hallo DNS-achtervoegsel worden kan:</span><span class="sxs-lookup"><span data-stu-id="63ed9-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="63ed9-181">Na het actieve hello Azure PowerShell-script gebruik Hallo volgende tooreturn Hallo DNS-achtervoegsel opdracht met behulp van Hallo **Get-ClusterDetail** functie.</span><span class="sxs-lookup"><span data-stu-id="63ed9-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="63ed9-182">Geef uw naam van HDInsight HBase-cluster, naam van de serverbeheerder en beheerderswachtwoord wanneer u deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="63ed9-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="63ed9-183">Deze opdracht retourneert Hallo DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="63ed9-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="63ed9-184">Bijvoorbeeld: **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="63ed9-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="63ed9-185">tooverify die virtuele machine Hallo kan communiceren met de Hallo HBase-cluster, gebruikt u Hallo opdracht `ping headnode0.<dns suffix>` van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="63ed9-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="63ed9-186">Bijvoorbeeld: ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="63ed9-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="63ed9-187">toouse deze informatie in een Java-toepassing en u kunt stappen Hallo in [Maven gebruiken toobuild Java-toepassingen die gebruikmaken van HBase met HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate een toepassing.</span><span class="sxs-lookup"><span data-stu-id="63ed9-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="63ed9-188">toohave hello toepassing tooa externe HBase-server verbinding kan maken, wijzigen Hallo **hbase-site.xml** bestand in dit voorbeeld toouse Hallo FQDN voor Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="63ed9-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="63ed9-189">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="63ed9-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="63ed9-190">Voor meer informatie over naamomzetting in virtuele netwerken in Azure, met inbegrip van hoe toouse uw eigen DNS-server, Zie [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="63ed9-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="63ed9-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63ed9-191">Next steps</span></span>
<span data-ttu-id="63ed9-192">In deze zelfstudie hebt u geleerd hoe toocreate een HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="63ed9-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="63ed9-193">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="63ed9-193">toolearn more, see:</span></span>

* [<span data-ttu-id="63ed9-194">Aan de slag met HDInsight</span><span class="sxs-lookup"><span data-stu-id="63ed9-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="63ed9-195">Lege edge-knooppunten in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="63ed9-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="63ed9-196">HBase-replicatie in HDInsight configureren</span><span class="sxs-lookup"><span data-stu-id="63ed9-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="63ed9-197">Hadoop-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63ed9-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="63ed9-198">Aan de slag met HBase met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63ed9-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="63ed9-199">Twitter-gevoel met HBase in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="63ed9-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="63ed9-200">[Overzicht van Virtual Network][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="63ed9-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Details voor de nieuwe HBase-cluster Hallo inrichten"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Scriptactie toocustomize een HBase-cluster gebruiken"

[azure-preview-portal]: https://portal.azure.com
