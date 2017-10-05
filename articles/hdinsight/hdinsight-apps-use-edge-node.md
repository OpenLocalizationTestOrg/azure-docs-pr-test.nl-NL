---
title: Lege edge-knooppunten op Hadoop-clusters in HDInsight - Azure gebruiken | Microsoft Docs
description: Hoe een leeg edge-knooppunt toevoegen aan een HDInsight-cluster die kan worden gebruikt als een client en vervolgens test/host uw HDInsight-toepassingen.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="24fde-103">Lege edge-knooppunten op Hadoop-clusters in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="24fde-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="24fde-104">Informatie over het toevoegen van een leeg edge-knooppunt aan een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="24fde-105">Een leeg edge-knooppunt is een virtuele Linux-machine met de dezelfde clienthulpprogramma's geïnstalleerd en geconfigureerd zoals in de headnodes, maar met geen Hadoop-services die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="24fde-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="24fde-106">U kunt het edge-knooppunt gebruiken voor toegang tot het cluster, testen van uw clienttoepassingen en die als host fungeert voor uw clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="24fde-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="24fde-107">U kunt een lege edge-knooppunt toevoegen aan een bestaand HDInsight-cluster naar een nieuw cluster bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="24fde-108">Toevoegen van een leeg edge-knooppunt wordt uitgevoerd met behulp van Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="24fde-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="24fde-109">Het volgende voorbeeld laat zien hoe deze wordt uitgevoerd met behulp van een sjabloon:</span><span class="sxs-lookup"><span data-stu-id="24fde-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="24fde-110">Zoals u in het voorbeeld, kunt u eventueel aanroepen een [script actie](hdinsight-hadoop-customize-cluster-linux.md) om uit te voeren aanvullende configuratiestappen, zoals het installeren van [Apache Hue](hdinsight-hadoop-hue-linux.md) in het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="24fde-111">Het script actiescript moet openbaar toegankelijk is op het web.</span><span class="sxs-lookup"><span data-stu-id="24fde-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="24fde-112">Bijvoorbeeld, als het script is opgeslagen in Azure-opslag, gebruiken openbare containers of openbare blobs.</span><span class="sxs-lookup"><span data-stu-id="24fde-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="24fde-113">De virtuele machinegrootte van het edge-knooppunt moet voldoen aan de vereiste grootte van HDInsight-cluster worker knooppunt vm.</span><span class="sxs-lookup"><span data-stu-id="24fde-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="24fde-114">Zie voor de aanbevolen worker knooppunt vm-grootten [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="24fde-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="24fde-115">Nadat u een edge-knooppunt hebt gemaakt, kunt u verbinding maken met het edge-knooppunt met behulp van SSH en clienthulpprogramma's voor toegang tot het Hadoop-cluster in HDInsight worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="24fde-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="24fde-116">Gebruik een lege edge-knooppunt met HDInsight is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="24fde-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="24fde-117">Aangepaste onderdelen die zijn geïnstalleerd op de edge-knooppunt ontvangt binnen commercieel redelijke ondersteuning van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="24fde-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="24fde-118">Dit kan leiden bij het oplossen van problemen die kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="24fde-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="24fde-119">Of u kan worden verwezen naar community-bronnen voor verdere ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="24fde-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="24fde-120">Hier volgen enkele van de meest actieve sites voor het ophalen van de help van de community:</span><span class="sxs-lookup"><span data-stu-id="24fde-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="24fde-121">MSDN-forum voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="24fde-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="24fde-122">[http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="24fde-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="24fde-123">Als u een Apache-technologie gebruikt, u kunt mogelijk hulp via de Apache projectsites zoeken op [http://apache.org](http://apache.org), zoals de [Hadoop](http://hadoop.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="24fde-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="24fde-124">Een edge-knooppunt toevoegen aan een bestaand cluster</span><span class="sxs-lookup"><span data-stu-id="24fde-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="24fde-125">In deze sectie kunt u een Resource Manager-sjabloon gebruiken een edge-knooppunt toevoegen aan een bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="24fde-126">De Resource Manager-sjabloon kunt u vinden in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="24fde-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="24fde-127">De Resource Manager-sjabloon roept een scriptactie zich bevindt op https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. Het script heeft geen acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="24fde-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="24fde-128">Het is voor het demonstreren van aanroepen scriptactie van Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="24fde-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="24fde-129">**Een leeg edge-knooppunt toevoegen aan een bestaand cluster**</span><span class="sxs-lookup"><span data-stu-id="24fde-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="24fde-130">Een HDInsight-cluster maken als u nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="24fde-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="24fde-131">Zie [Hadoop-zelfstudie: aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24fde-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="24fde-132">Klik op de volgende afbeelding om te melden bij Azure en open de Azure Resource Manager-sjabloon in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="24fde-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="24fde-133">Configureer de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="24fde-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="24fde-134">**Abonnement**: Selecteer een Azure-abonnement gebruikt voor het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="24fde-135">**Resourcegroep**: Selecteer de resourcegroep die wordt gebruikt voor het bestaande HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="24fde-136">**Locatie**: Selecteer de locatie van het bestaande HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="24fde-137">**Clusternaam**: Voer de naam van een bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="24fde-138">**Edge-Knooppuntgrootte**: Selecteer een van de VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="24fde-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="24fde-139">De vm-grootte moet voldoen aan de vereiste worker knooppunt vm-grootte.</span><span class="sxs-lookup"><span data-stu-id="24fde-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="24fde-140">Zie voor de aanbevolen worker knooppunt vm-grootten [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="24fde-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="24fde-141">**Edge-knooppunt voorvoegsel**: de standaardwaarde is **nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="24fde-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="24fde-142">De naam van de edge-knooppunt is de standaardwaarde wordt gebruikt, **nieuwe edgenode**.</span><span class="sxs-lookup"><span data-stu-id="24fde-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="24fde-143">U kunt het voorvoegsel van de portal kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="24fde-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="24fde-144">U kunt ook de volledige naam van de sjabloon aanpassen.</span><span class="sxs-lookup"><span data-stu-id="24fde-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="24fde-145">Controleer **ik ga akkoord met de voorwaarden en bepalingen hierboven**, en klik vervolgens op **aankoop** voor het maken van het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="24fde-146">Zorg ervoor dat u selecteert de Azure-resourcegroep voor de bestaande HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="24fde-147">Anders wordt de ophalen van het foutbericht 'kan aangevraagde bewerking op geneste resource niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="24fde-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="24fde-148">Bovenliggende resource '&lt;ClusterName >' niet gevonden. "</span><span class="sxs-lookup"><span data-stu-id="24fde-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="24fde-149">Een edge-knooppunt toevoegen bij het maken van een cluster</span><span class="sxs-lookup"><span data-stu-id="24fde-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="24fde-150">In deze sectie kunt u een Resource Manager-sjabloon maken van HDInsight-cluster met een edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="24fde-151">De Resource Manager-sjabloon kunt u vinden in de [galerie van Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="24fde-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="24fde-152">De Resource Manager-sjabloon roept een scriptactie zich bevindt op https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. Het script heeft geen acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="24fde-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="24fde-153">Het is voor het demonstreren van aanroepen scriptactie van Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="24fde-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="24fde-154">**Een leeg edge-knooppunt toevoegen aan een bestaand cluster**</span><span class="sxs-lookup"><span data-stu-id="24fde-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="24fde-155">Een HDInsight-cluster maken als u nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="24fde-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="24fde-156">Zie [aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24fde-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="24fde-157">Klik op de volgende afbeelding om te melden bij Azure en open de Azure Resource Manager-sjabloon in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="24fde-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="24fde-158">Configureer de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="24fde-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="24fde-159">**Abonnement**: Selecteer een Azure-abonnement gebruikt voor het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="24fde-160">**Resourcegroep**: Maak een nieuwe resourcegroep gebruikt voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="24fde-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="24fde-161">**Locatie**: selecteer een locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="24fde-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="24fde-162">**Clusternaam**: Voer een naam voor het nieuwe cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="24fde-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="24fde-163">**Aanmeldingsnaam van gebruiker cluster**: Geef de gebruikersnaam van Hadoop HTTP.</span><span class="sxs-lookup"><span data-stu-id="24fde-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="24fde-164">De standaardnaam is **admin**.</span><span class="sxs-lookup"><span data-stu-id="24fde-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="24fde-165">**Aanmeldingswachtwoord cluster**: Geef het wachtwoord van de Hadoop-HTTP-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="24fde-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="24fde-166">**SSH gebruikersnaam**: Voer de SSH-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="24fde-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="24fde-167">De standaardnaam is **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="24fde-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="24fde-168">**SSH wachtwoord**: Geef het wachtwoord van de SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="24fde-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="24fde-169">**Installeren van de scriptactie**: de standaardwaarde voor het doorlopen van deze zelfstudie houden.</span><span class="sxs-lookup"><span data-stu-id="24fde-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="24fde-170">Sommige eigenschappen zijn vastgelegd in de sjabloon: clustertype, aantal Cluster worker-knooppunten, de grootte van de Edge-knooppunt en de naam van de Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="24fde-171">Controleer **ik ga akkoord met de voorwaarden en bepalingen hierboven**, en klik vervolgens op **aankoop** het cluster maken met het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="24fde-172">Toegang tot een edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="24fde-172">Access an edge node</span></span>
<span data-ttu-id="24fde-173">Het edge-knooppunt ssh-eindpunt is &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="24fde-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="24fde-174">Bijvoorbeeld, nieuwe-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="24fde-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="24fde-175">Het edge-knooppunt wordt weergegeven als een toepassing op de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="24fde-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="24fde-176">De portal biedt u de informatie voor toegang tot het gebruik van SSH edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="24fde-177">**Om te controleren of het edge-knooppunt SSH-eindpunt**</span><span class="sxs-lookup"><span data-stu-id="24fde-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="24fde-178">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24fde-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="24fde-179">Open het HDInsight-cluster met een edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="24fde-180">Klik op **toepassingen** uit de cluster-blade.</span><span class="sxs-lookup"><span data-stu-id="24fde-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="24fde-181">U ziet het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-181">You shall see the edge node.</span></span>  <span data-ttu-id="24fde-182">De standaardnaam is **nieuwe edgenode**.</span><span class="sxs-lookup"><span data-stu-id="24fde-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="24fde-183">Klik op de edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-183">Click the edge node.</span></span> <span data-ttu-id="24fde-184">U ziet het SSH-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="24fde-185">**Hive gebruiken op de edge-knooppunt**</span><span class="sxs-lookup"><span data-stu-id="24fde-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="24fde-186">SSH gebruiken voor verbinding met het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="24fde-187">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="24fde-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="24fde-188">Nadat u hebt verbonden met het edge-knooppunt via SSH, gebruikt u de volgende opdracht om de Hive-console te openen:</span><span class="sxs-lookup"><span data-stu-id="24fde-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="24fde-189">Voer de volgende opdracht om Hive-tabellen in het cluster weer te geven:</span><span class="sxs-lookup"><span data-stu-id="24fde-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="24fde-190">Verwijderen van een edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="24fde-190">Delete an edge node</span></span>
<span data-ttu-id="24fde-191">U kunt een edge-knooppunt verwijderen uit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="24fde-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="24fde-192">**Voor toegang tot een edge-knooppunt**</span><span class="sxs-lookup"><span data-stu-id="24fde-192">**To access an edge node**</span></span>

1. <span data-ttu-id="24fde-193">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24fde-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="24fde-194">Open het HDInsight-cluster met een edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="24fde-195">Klik op **toepassingen** uit de cluster-blade.</span><span class="sxs-lookup"><span data-stu-id="24fde-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="24fde-196">U ziet een lijst met knooppunten van de rand.</span><span class="sxs-lookup"><span data-stu-id="24fde-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="24fde-197">Met de rechtermuisknop op de edge-knooppunt dat u wilt verwijderen en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="24fde-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="24fde-198">Klik op **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="24fde-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24fde-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24fde-199">Next steps</span></span>
<span data-ttu-id="24fde-200">In dit artikel hebt u geleerd hoe een edge-knooppunt toevoegen en over het openen van het edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="24fde-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="24fde-201">Zie voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="24fde-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="24fde-202">[HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): informatie over het installeren van een HDInsight-toepassing op uw clusters.</span><span class="sxs-lookup"><span data-stu-id="24fde-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="24fde-203">[Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): informatie over het implementeren van een niet-gepubliceerde HDInsight-toepassing op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="24fde-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="24fde-204">[HDInsight-toepassingen publiceren](hdinsight-apps-publish-applications.md): informatie over het publiceren van aangepaste HDInsight-toepassingen in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="24fde-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="24fde-205">[MSDN: een HDInsight-toepassing installeren](https://msdn.microsoft.com/library/mt706515.aspx): informatie over het definiëren van HDInsight-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="24fde-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="24fde-206">[Op Linux gebaseerde HDInsight-clusters aanpassen met behulp van een scriptactie](hdinsight-hadoop-customize-cluster-linux.md): informatie over het gebruik van een scriptactie om extra toepassingen te installeren.</span><span class="sxs-lookup"><span data-stu-id="24fde-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="24fde-207">[Op Linux gebaseerde Hadoop-clusters maken in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md): informatie over het aanroepen van Resource Manager-sjablonen om HDInsight-clusters te maken.</span><span class="sxs-lookup"><span data-stu-id="24fde-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

