---
title: aaaCreate Hadoop-clusters met behulp van sjablonen - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate clusters voor HDInsight met behulp van Resource Manager-sjablonen
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="d236a-103">Hadoop-clusters maken in HDInsight met behulp van Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="d236a-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="d236a-104">In dit artikel leert u op verschillende manieren toocreate Azure HDInsight-clusters met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="d236a-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="d236a-105">Zie voor meer informatie [Implementeer een toepassing met Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="d236a-106">toolearn over andere hulpmiddelen voor het cluster maken en de functies, klikt u op de tabselector Hallo op Hallo boven aan deze pagina of Zie [methoden voor het maken van Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="d236a-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d236a-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d236a-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d236a-108">toofollow Hallo-instructies in dit artikel hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="d236a-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="d236a-109">Een [Azure-abonnement](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d236a-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d236a-110">Azure PowerShell en/of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d236a-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="d236a-111">Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="d236a-111">Resource Manager templates</span></span>
<span data-ttu-id="d236a-112">Resource Manager-sjabloon maakt het eenvoudig toocreate Hallo voor uw toepassing in een enkele, gecoördineerde bewerking te volgen:</span><span class="sxs-lookup"><span data-stu-id="d236a-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="d236a-113">HDInsight-clusters en hun afhankelijke bronnen (zoals Hallo standaardopslagaccount)</span><span class="sxs-lookup"><span data-stu-id="d236a-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="d236a-114">Andere bronnen (zoals Azure SQL Database toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="d236a-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="d236a-115">In de sjabloon hello definieert u Hallo-resources die nodig zijn voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d236a-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="d236a-116">U wordt ook implementatie parameters tooinput waarden voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="d236a-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="d236a-117">Hallo sjabloon bestaat uit JSON en uitdrukkingen tooconstruct waarden te gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="d236a-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="d236a-118">Vindt u voorbeelden van HDInsight-sjabloon op [Azure-Snelstartsjablonen](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="d236a-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="d236a-119">Cross-platform gebruiken [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) Hello [Resource Manager-extensie](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) of een tekst-editor toosave Hallo sjabloon naar een bestand op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="d236a-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="d236a-120">U leert hoe toocall sjabloon Hallo via andere methoden.</span><span class="sxs-lookup"><span data-stu-id="d236a-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="d236a-121">Zie voor meer informatie over de Resource Manager-sjablonen, Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d236a-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="d236a-122">De auteur van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="d236a-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="d236a-123">Implementeer een toepassing met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="d236a-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="d236a-124">Genereren van sjablonen</span><span class="sxs-lookup"><span data-stu-id="d236a-124">Generate templates</span></span>

<span data-ttu-id="d236a-125">U kunt met behulp van hello Azure-portal alle Hallo-eigenschappen van een cluster configureren en vervolgens Hallo sjabloon opslaan voordat u deze implementeert.</span><span class="sxs-lookup"><span data-stu-id="d236a-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="d236a-126">Vervolgens kunt u de sjabloon Hallo hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="d236a-126">You can then reuse hello template.</span></span>

<span data-ttu-id="d236a-127">**toogenerate een sjabloon met hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="d236a-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="d236a-128">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d236a-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d236a-129">Klik op **nieuw** op Hallo menu links, klikt u op **Intelligence en analyse**, en klik vervolgens op **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d236a-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="d236a-130">Ga als volgt Hallo instructies tooenter eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d236a-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="d236a-131">U kunt beide Hallo **snelle invoer** of Hallo **aangepaste** optie.</span><span class="sxs-lookup"><span data-stu-id="d236a-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="d236a-132">Op Hallo **samenvatting** tabblad **sjabloon en parameters downloaden**:</span><span class="sxs-lookup"><span data-stu-id="d236a-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Maken van HDInsight Hadoop cluster Resource Manager-sjabloon downloaden](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="d236a-134">U ziet een lijst met sjabloonbestand hello, parameterbestand en de code steekproeven toodeploy Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="d236a-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop maken-cluster Downloadinstellingen voor Resource Manager-sjabloon](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="d236a-136">Hier kunt kunt u Hallo sjabloon downloaden, tooyour sjabloonbibliotheek opslaan of Hallo sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="d236a-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="d236a-137">tooaccess een sjabloon in de bibliotheek, klikt u op **meer services** van Hallo menu aan de linkerkant en klik vervolgens op **sjablonen** (onder Hallo **andere** categorie).</span><span class="sxs-lookup"><span data-stu-id="d236a-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="d236a-138">Hallo-sjabloon en de parameters-bestand moet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d236a-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="d236a-139">Anders krijgt u mogelijk onverwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="d236a-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="d236a-140">Bijvoorbeeld, Hallo standaard **clusterKind** is altijd de waarde van de eigenschap **hadoop**, ondanks wat u opgeven voordat u Hallo sjabloon downloaden.</span><span class="sxs-lookup"><span data-stu-id="d236a-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="d236a-141">Implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="d236a-141">Deploy with PowerShell</span></span>

<span data-ttu-id="d236a-142">Deze procedure maakt u een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d236a-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="d236a-143">Hallo JSON-bestand opslaan in Hallo [bijlage](#appx-a-arm-template) tooyour werkstation.</span><span class="sxs-lookup"><span data-stu-id="d236a-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="d236a-144">In Hallo PowerShell-script, is het Hallo-bestandsnaam `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="d236a-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="d236a-145">Hallo-parameters en variabelen instellen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d236a-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="d236a-146">Hallo sjabloon uitvoeren met behulp van PowerShell-script volgen Hallo:</span><span class="sxs-lookup"><span data-stu-id="d236a-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="d236a-147">Hallo PowerShell-script configureert alleen Hallo clusternaam.</span><span class="sxs-lookup"><span data-stu-id="d236a-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="d236a-148">Hallo opslagaccountnaam is vastgelegd in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d236a-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="d236a-149">U bent na vragen aan gebruiker tooenter Hallo cluster gebruikerswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d236a-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="d236a-150">(de standaardgebruikersnaam Hallo **admin**.) Bent u ook na vragen aan gebruiker tooenter Hallo SSH gebruiker-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d236a-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="d236a-151">(de standaardgebruikersnaam SSH Hallo **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="d236a-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="d236a-152">Zie voor meer informatie [implementeren met PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="d236a-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="d236a-153">Implementeren met CLI</span><span class="sxs-lookup"><span data-stu-id="d236a-153">Deploy with CLI</span></span>
<span data-ttu-id="d236a-154">Hallo volgende voorbeeld maakt gebruik van Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="d236a-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="d236a-155">Er wordt een cluster en het afhankelijke opslagaccount en container gemaakt door het aanroepen van Resource Manager-sjabloon:</span><span class="sxs-lookup"><span data-stu-id="d236a-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="d236a-156">U bent tooenter na vragen aan gebruiker:</span><span class="sxs-lookup"><span data-stu-id="d236a-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="d236a-157">Hallo clusternaam.</span><span class="sxs-lookup"><span data-stu-id="d236a-157">hello cluster name.</span></span>
* <span data-ttu-id="d236a-158">Hallo cluster gebruikerswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d236a-158">hello cluster user password.</span></span> <span data-ttu-id="d236a-159">(de standaardgebruikersnaam Hallo **admin**.)</span><span class="sxs-lookup"><span data-stu-id="d236a-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="d236a-160">Hallo SSH gebruiker-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d236a-160">hello SSH user password.</span></span> <span data-ttu-id="d236a-161">(de standaardgebruikersnaam SSH Hallo **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="d236a-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="d236a-162">Hallo na code levert inline-parameters:</span><span class="sxs-lookup"><span data-stu-id="d236a-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="d236a-163">Met de Hallo REST-API implementeren</span><span class="sxs-lookup"><span data-stu-id="d236a-163">Deploy with hello REST API</span></span>
<span data-ttu-id="d236a-164">Zie [implementeren met Hallo REST-API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="d236a-165">Implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d236a-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="d236a-166">Gebruik Visual Studio toocreate een resourcegroepproject en tooAzure via de gebruikersinterface Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="d236a-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="d236a-167">U selecteren Hallo type resources tooinclude in uw project.</span><span class="sxs-lookup"><span data-stu-id="d236a-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="d236a-168">Deze resources worden automatisch toegevoegd aan toohello Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d236a-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="d236a-169">Hallo-project bevat ook een PowerShell-script toodeploy Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d236a-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="d236a-170">Zie voor een inleiding toousing Visual Studio aan resourcegroepen, [maken en implementeren van Azure-resourcegroepen met Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="d236a-171">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d236a-171">Troubleshoot</span></span>

<span data-ttu-id="d236a-172">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d236a-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d236a-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d236a-173">Next steps</span></span>
<span data-ttu-id="d236a-174">In dit artikel hebt u geleerd toocreate met verschillende manieren een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d236a-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="d236a-175">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d236a-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="d236a-176">Zie voor een voorbeeld van het implementeren van resources via de .NET-clientbibliotheek Hallo [resources implementeren met behulp van .NET-bibliotheken en een sjabloon](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d236a-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d236a-177">Zie voor een gedetailleerd voorbeeld van een toepassing implementeren, [inrichten en implementeren van microservices zoals verwacht in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="d236a-178">Zie voor instructies over het implementeren van uw oplossing toodifferent omgevingen [ontwikkel- en testomgevingen in Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="d236a-179">toolearn hello secties van hello Azure Resource Manager-sjabloon, Zie [sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d236a-180">Zie voor een lijst met Hallo-functies kunt u in een Azure Resource Manager-sjabloon, [sjabloonfuncties](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="d236a-181">Bijlage: Resource Manager sjabloon toocreate een Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="d236a-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="d236a-182">Hallo maakt volgende Azure Resource Manager-sjabloon een Linux gebaseerde Hadoop-cluster met Hallo afhankelijke Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="d236a-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="d236a-183">Dit voorbeeld bevat configuratie-informatie voor Hive-metastore en Oozie-metastore.</span><span class="sxs-lookup"><span data-stu-id="d236a-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="d236a-184">Hallo sectie verwijderen of Hallo sectie configureren voordat u Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d236a-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="d236a-185">Bijlage: Resource Manager sjabloon toocreate een Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="d236a-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="d236a-186">Deze sectie vindt u een Resource Manager-sjabloon waarmee u toocreate een HDInsight Spark-cluster kunt.</span><span class="sxs-lookup"><span data-stu-id="d236a-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="d236a-187">Deze sjabloon bevat configuraties voor `spark-defaults` en `spark-thrift-sparkconf` (voor Spark 1.6-clusters) en `spark2-defaults` en `spark2-thrift-sparkconf` (voor 2 Spark-clusters).</span><span class="sxs-lookup"><span data-stu-id="d236a-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="d236a-188">Bovendien toothis, HDInsight berekend en ingesteld configuraties, zoals `spark.executor.instances`, `spark.executor.memory`, en `spark.executor.cores` op basis van Hallo clustergrootte.</span><span class="sxs-lookup"><span data-stu-id="d236a-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="d236a-189">Als u een één parameter ingesteld in een sectie als onderdeel van het Hallo-sjabloon zelf, HDInsight niet berekenen en andere parameters Hallo Hallo instellen hetzelfde gedeelte.</span><span class="sxs-lookup"><span data-stu-id="d236a-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="d236a-190">Bijvoorbeeld: parameter `spark.executor.instances` bevindt zich in Hallo `spark-defaults` configuratie.</span><span class="sxs-lookup"><span data-stu-id="d236a-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="d236a-191">Als u een andere parameter ingesteld (bijvoorbeeld `spark.yarn.exector.memoryOverhead`) in Hallo `spark-defaults` configuratie, HDInsight niet berekenen en stel de Hallo `spark.executor.instances` ook de parameter.</span><span class="sxs-lookup"><span data-stu-id="d236a-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
