---
title: HDInsight-Clusters met behulp van de bootstrap - Azure aaaCustomize | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-clusters met behulp van de bootstrap.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="06433-103">HDInsight-clusters met behulp van de Bootstrap aanpassen</span><span class="sxs-lookup"><span data-stu-id="06433-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="06433-104">Soms wilt u tooconfigure Hallo configuratiebestanden, waaronder:</span><span class="sxs-lookup"><span data-stu-id="06433-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="06433-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="06433-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="06433-106">Core-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-106">core-site.xml</span></span>
* <span data-ttu-id="06433-107">gateway.XML</span><span class="sxs-lookup"><span data-stu-id="06433-107">gateway.xml</span></span>
* <span data-ttu-id="06433-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="06433-108">hbase-env.xml</span></span>
* <span data-ttu-id="06433-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-109">hbase-site.xml</span></span>
* <span data-ttu-id="06433-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-110">hdfs-site.xml</span></span>
* <span data-ttu-id="06433-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="06433-111">hive-env.xml</span></span>
* <span data-ttu-id="06433-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-112">hive-site.xml</span></span>
* <span data-ttu-id="06433-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="06433-113">mapred-site</span></span>
* <span data-ttu-id="06433-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-114">oozie-site.xml</span></span>
* <span data-ttu-id="06433-115">oozie env.xml</span><span class="sxs-lookup"><span data-stu-id="06433-115">oozie-env.xml</span></span>
* <span data-ttu-id="06433-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-116">storm-site.xml</span></span>
* <span data-ttu-id="06433-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-117">tez-site.xml</span></span>
* <span data-ttu-id="06433-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-118">webhcat-site.xml</span></span>
* <span data-ttu-id="06433-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="06433-119">yarn-site.xml</span></span>

<span data-ttu-id="06433-120">Er zijn drie methoden toouse bootstrap:</span><span class="sxs-lookup"><span data-stu-id="06433-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="06433-121">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="06433-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="06433-122">.NET SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="06433-122">Use .NET SDK</span></span>
* <span data-ttu-id="06433-123">Azure Resource Manager-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="06433-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="06433-124">Zie voor informatie over het installeren van extra onderdelen in HDInsight-cluster tijdens de aanmaakfase Hallo:</span><span class="sxs-lookup"><span data-stu-id="06433-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="06433-125">Aanpassen van HDInsight-clusters met behulp van de scriptactie (Linux)</span><span class="sxs-lookup"><span data-stu-id="06433-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="06433-126">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="06433-126">Use Azure PowerShell</span></span>
<span data-ttu-id="06433-127">Hallo volgende PowerShell-code aanpassen een Hive-configuratie:</span><span class="sxs-lookup"><span data-stu-id="06433-127">hello following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="06433-128">Een volledig werkend PowerShell-script kan worden gevonden in [bijlage A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="06433-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="06433-129">**tooverify hello wijzigen:**</span><span class="sxs-lookup"><span data-stu-id="06433-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="06433-130">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06433-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="06433-131">In het linkermenu hello, klikt u op **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="06433-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="06433-132">Als u deze niet ziet, klikt u op **meer services** eerste.</span><span class="sxs-lookup"><span data-stu-id="06433-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="06433-133">Klik op Hallo cluster die u zojuist hebt gemaakt met Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="06433-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="06433-134">Klik op **Dashboard** vanaf de bovenkant Hallo van Hallo blade tooopen Hallo Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="06433-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="06433-135">Klik op **Hive** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="06433-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="06433-136">Klik op **HiveServer2** van **samenvatting**.</span><span class="sxs-lookup"><span data-stu-id="06433-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="06433-137">Klik op Hallo **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="06433-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="06433-138">Klik op **Hive** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="06433-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="06433-139">Klik op Hallo **Geavanceerd** tabblad.</span><span class="sxs-lookup"><span data-stu-id="06433-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="06433-140">Schuif naar beneden en vouw vervolgens **geavanceerde hive-site**.</span><span class="sxs-lookup"><span data-stu-id="06433-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="06433-141">Zoek naar **hive.metastore.client.socket.timeout** in Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="06433-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="06433-142">Enkele voorbeelden van meer over het aanpassen van andere configuratiebestanden:</span><span class="sxs-lookup"><span data-stu-id="06433-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="06433-143">Zie voor meer informatie, met de titel van Azim Uddin-blog [maken van HDInsight-clusters aanpassen](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="06433-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="06433-144">.NET SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="06433-144">Use .NET SDK</span></span>
<span data-ttu-id="06433-145">Zie [maken Linux gebaseerde clusters in HDInsight met behulp Hallo .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="06433-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="06433-146">Gebruik Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="06433-146">Use Resource Manager template</span></span>
<span data-ttu-id="06433-147">U kunt bootstrap in Resource Manager-sjabloon gebruiken:</span><span class="sxs-lookup"><span data-stu-id="06433-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop aanpassen cluster bootstrap Azure Resource Manager-sjabloon](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="06433-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="06433-149">See also</span></span>
* <span data-ttu-id="06433-150">[Hadoop-clusters maken in HDInsight] [ hdinsight-provision-cluster] vindt u instructies voor hoe toocreate een HDInsight-cluster met behulp van andere aangepaste opties.</span><span class="sxs-lookup"><span data-stu-id="06433-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="06433-151">[Scriptactie-scripts ontwikkelen voor HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="06433-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="06433-152">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="06433-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="06433-153">[Installeren en gebruiken van R op HDInsight-clusters][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="06433-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="06433-154">[Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="06433-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="06433-155">[Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="06433-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="06433-157">Appx-a PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="06433-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="06433-158">Deze PowerShell-script maakt een HDInsight-cluster en aanpassen van een Hive-instelling:</span><span class="sxs-lookup"><span data-stu-id="06433-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
