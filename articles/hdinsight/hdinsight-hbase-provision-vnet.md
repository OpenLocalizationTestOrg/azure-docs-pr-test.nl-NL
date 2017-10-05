---
title: HBase-clusters maken in een virtueel netwerk - Azure | Microsoft Docs
description: Aan de slag met HBase in Azure HDInsight. Informatie over hoe HDInsight HBase-clusters maken op Azure Virtual Network.
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
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="e9411-104">HBase-clusters maken in HDInsight in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="e9411-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="e9411-105">Informatie over het maken van Azure HDInsight HBase-clusters in een [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="e9411-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="e9411-106">Met integratie van virtueel netwerk, kunnen HBase-clusters worden geïmplementeerd op hetzelfde virtuele netwerk als uw toepassingen zodat toepassingen rechtstreeks met HBase communiceren kunnen.</span><span class="sxs-lookup"><span data-stu-id="e9411-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="e9411-107">De voordelen zijn:</span><span class="sxs-lookup"><span data-stu-id="e9411-107">The benefits include:</span></span>

* <span data-ttu-id="e9411-108">Directe verbinding van de webtoepassing aan de knooppunten van het HBase-cluster, waarmee communicatie via HBase Java externe procedureaanroepen (RPC) API's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e9411-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="e9411-109">Verbeterde prestaties omdat u niet hoeft uw verkeer Ga via meerdere gateways en load balancers.</span><span class="sxs-lookup"><span data-stu-id="e9411-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="e9411-110">De mogelijkheid om gevoelige informatie op een veiliger manier verwerken zonder een openbaar eindpunt bloot te stellen.</span><span class="sxs-lookup"><span data-stu-id="e9411-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e9411-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e9411-111">Prerequisites</span></span>
<span data-ttu-id="e9411-112">Voordat u met deze zelfstudie begint, moet u beschikken over de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e9411-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="e9411-113">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e9411-113">**An Azure subscription**.</span></span> <span data-ttu-id="e9411-114">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e9411-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e9411-115">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e9411-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="e9411-116">Zie [installeren en gebruiken Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="e9411-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="e9411-117">HBase-cluster in virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="e9411-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="e9411-118">In deze sectie maakt u een Linux-gebaseerde HBase-cluster maken met het afhankelijke Azure Storage-account aan een virtuele Azure-netwerk met een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="e9411-119">Voor andere methoden voor het maken van cluster en kennis van de instellingen, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="e9411-120">Zie voor meer informatie over het gebruik van een sjabloon voor het maken van Hadoop-clusters in HDInsight [maken Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="e9411-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="e9411-121">Sommige eigenschappen zijn hardgecodeerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e9411-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="e9411-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9411-122">For example:</span></span>
>
> * <span data-ttu-id="e9411-123">**Locatie**: VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="e9411-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="e9411-124">**Clusterversie**: 3.5</span><span class="sxs-lookup"><span data-stu-id="e9411-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="e9411-125">**Aantal worker-knooppunten cluster**: 2</span><span class="sxs-lookup"><span data-stu-id="e9411-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="e9411-126">**Storage-account standaard**: een unieke tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e9411-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="e9411-127">**Virtuele-netwerknaam**: &lt;Clusternaam >-vnet</span><span class="sxs-lookup"><span data-stu-id="e9411-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="e9411-128">**Adresruimte voor virtueel netwerk**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e9411-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="e9411-129">**De subnetnaam van het**: subnet1</span><span class="sxs-lookup"><span data-stu-id="e9411-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="e9411-130">**Adresbereik van**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e9411-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="e9411-131">&lt;Clusternaam > is vervangen door de clusternaam die u opgeeft wanneer u de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e9411-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="e9411-132">Klik op de volgende afbeelding om de sjabloon in Azure Portal te openen.</span><span class="sxs-lookup"><span data-stu-id="e9411-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="e9411-133">De sjabloon bevindt zich in [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="e9411-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="e9411-134">Van de **aangepaste implementatie** blade, voer de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e9411-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="e9411-135">**Abonnement**: Selecteer een Azure-abonnement gebruikt voor het maken van het HDInsight-cluster, het afhankelijke opslagaccount en de virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9411-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="e9411-136">**Resourcegroep**: Selecteer **nieuw**, en geef een nieuwe Resourcegroepnaam.</span><span class="sxs-lookup"><span data-stu-id="e9411-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="e9411-137">**Locatie**: selecteer een locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9411-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="e9411-138">**Clusternaam**: Voer een naam voor het Hadoop-cluster moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e9411-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="e9411-139">**Aanmeldgegevens voor het cluster**: de standaardaanmeldnaam is **admin**.</span><span class="sxs-lookup"><span data-stu-id="e9411-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="e9411-140">**SSH-gebruikersnaam en -wachtwoord**: de standaardgebruikersnaam is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="e9411-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="e9411-141">U kunt de naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e9411-141">You can rename it.</span></span>
   * <span data-ttu-id="e9411-142">**Ik ga akkoord met de voorwaarden de hierboven vermelde**: (selecteren)</span><span class="sxs-lookup"><span data-stu-id="e9411-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="e9411-143">Klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="e9411-143">Click **Purchase**.</span></span> <span data-ttu-id="e9411-144">Het duurt ongeveer 20 minuten om een cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="e9411-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="e9411-145">Zodra het cluster is gemaakt, kunt u de cluster-blade in de portal om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="e9411-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="e9411-146">Nadat u de zelfstudie hebt voltooid, kunt u het cluster verwijdert.</span><span class="sxs-lookup"><span data-stu-id="e9411-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="e9411-147">Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9411-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="e9411-148">Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9411-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="e9411-149">Aangezien de kosten voor het cluster vaak zoveel hoger zijn dan de kosten voor opslag, is het financieel gezien logischer clusters te verwijderen wanneer ze niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9411-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="e9411-150">Zie voor de instructies van het verwijderen van een cluster [beheren Hadoop-clusters in HDInsight met behulp van de Azure-portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="e9411-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="e9411-151">Als u wilt werken met uw nieuwe HBase-cluster, kunt u de procedures die zijn gevonden in [aan de slag met HBase met Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="e9411-152">Verbinding maken met de HBase-cluster met HBase Java RPC-API 's</span><span class="sxs-lookup"><span data-stu-id="e9411-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="e9411-153">Maak een infrastructuur als een dienst (IaaS) virtuele machine in hetzelfde virtuele netwerk van Azure en hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="e9411-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="e9411-154">Zie voor instructies over het maken van een nieuwe virtuele machine voor IaaS [maken van een virtuele Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="e9411-155">Wanneer u de stappen in dit document, moet u de volgende waarden gebruiken voor de netwerkconfiguratie:</span><span class="sxs-lookup"><span data-stu-id="e9411-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="e9411-156">**Virtueel netwerk**: &lt;Clusternaam >-vnet</span><span class="sxs-lookup"><span data-stu-id="e9411-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="e9411-157">**Subnet**: subnet1</span><span class="sxs-lookup"><span data-stu-id="e9411-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e9411-158">Vervang &lt;Clusternaam > met de naam die u hebt gebruikt bij het maken van het HDInsight-cluster in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="e9411-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="e9411-159">De virtuele machine wordt met behulp van deze waarden geplaatst in het hetzelfde virtuele netwerk en subnet als het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e9411-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="e9411-160">Deze configuratie kan ze rechtstreeks met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="e9411-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="e9411-161">Er is een manier om een HDInsight-cluster maken met een leeg edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e9411-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="e9411-162">Het edge-knooppunt kan worden gebruikt voor het beheren van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e9411-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="e9411-163">Zie voor meer informatie [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="e9411-164">Wanneer u een Java-toepassing op afstand verbinding maken met HBase, moet u de volledig gekwalificeerde domeinnaam (FQDN).</span><span class="sxs-lookup"><span data-stu-id="e9411-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="e9411-165">Als u wilt bepalen, moet u het verbindingsspecifieke DNS-achtervoegsel van de HBase-cluster ophalen.</span><span class="sxs-lookup"><span data-stu-id="e9411-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="e9411-166">Hiervoor kunt u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e9411-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="e9411-167">Een webbrowser gebruiken om een oproep Ambari te doen:</span><span class="sxs-lookup"><span data-stu-id="e9411-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="e9411-168">Blader naar https://&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / als host fungeert voor? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="e9411-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="e9411-169">Hiermee schakelt u een JSON-bestand met de DNS-achtervoegsels.</span><span class="sxs-lookup"><span data-stu-id="e9411-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="e9411-170">Gebruik de Ambari-website:</span><span class="sxs-lookup"><span data-stu-id="e9411-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="e9411-171">Blader naar https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e9411-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="e9411-172">Klik op **Hosts** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e9411-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="e9411-173">Gebruik Curl REST-aanroepen:</span><span class="sxs-lookup"><span data-stu-id="e9411-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="e9411-174">In de notatie JSON (JavaScript Object)-gegevens geretourneerd, de vermelding 'hostnaam' niet vinden.</span><span class="sxs-lookup"><span data-stu-id="e9411-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="e9411-175">Het bevat de FQDN-naam voor de knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="e9411-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="e9411-176">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9411-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="e9411-177">Het gedeelte van het domein naam die begint met de naam van het cluster is het DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="e9411-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="e9411-178">Bijvoorbeeld: mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e9411-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="e9411-179">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="e9411-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="e9411-180">De volgende Azure PowerShell-script gebruiken om te registreren de **Get-ClusterDetail** functie, die kan worden gebruikt voor het retourneren van de DNS-achtervoegsel:</span><span class="sxs-lookup"><span data-stu-id="e9411-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

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
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
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

     <span data-ttu-id="e9411-181">Nadat de Azure PowerShell-script is uitgevoerd, kunt u de volgende opdracht gebruiken om te retourneren van de DNS-achtervoegsel met behulp van de **Get-ClusterDetail** functie.</span><span class="sxs-lookup"><span data-stu-id="e9411-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="e9411-182">Geef uw naam van HDInsight HBase-cluster, naam van de serverbeheerder en beheerderswachtwoord wanneer u deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="e9411-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="e9411-183">Deze opdracht retourneert de DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="e9411-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="e9411-184">Bijvoorbeeld: **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="e9411-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="e9411-185">Gebruik de opdracht om te controleren of de virtuele machine met de HBase-cluster communiceren kan, `ping headnode0.<dns suffix>` van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9411-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="e9411-186">Bijvoorbeeld: ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e9411-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="e9411-187">Als u deze informatie in een Java-toepassing, kunt u de stappen in [Maven gebruiken voor het ontwikkelen van Java-toepassingen die gebruikmaken van HBase met HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) een toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="e9411-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="e9411-188">Als u de toepassing verbinding maken met een externe HBase-server wilt weergeven, wijzigen de **hbase-site.xml** bestand in dit voorbeeld met de FQDN-naam voor Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="e9411-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="e9411-189">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9411-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="e9411-190">Zie voor meer informatie over naamomzetting in Azure virtuele netwerken, inclusief het gebruik van uw eigen DNS-server, [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e9411-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9411-191">Next steps</span></span>
<span data-ttu-id="e9411-192">In deze zelfstudie hebt u geleerd hoe een HBase-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="e9411-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="e9411-193">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="e9411-193">To learn more, see:</span></span>

* [<span data-ttu-id="e9411-194">Aan de slag met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9411-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="e9411-195">Lege edge-knooppunten in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="e9411-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="e9411-196">HBase-replicatie in HDInsight configureren</span><span class="sxs-lookup"><span data-stu-id="e9411-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="e9411-197">Hadoop-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9411-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="e9411-198">Aan de slag met HBase met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9411-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="e9411-199">Twitter-gevoel met HBase in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="e9411-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="e9411-200">[Overzicht van Virtual Network][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="e9411-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Details voor het nieuwe HBase-cluster inrichten"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Scriptactie gebruiken voor het aanpassen van een HBase-cluster"

[azure-preview-portal]: https://portal.azure.com
