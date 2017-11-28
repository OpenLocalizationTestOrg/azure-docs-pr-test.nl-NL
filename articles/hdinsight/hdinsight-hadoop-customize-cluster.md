---
title: acties - Azure HDInsight-Clusters met behulp van aaaCustomize script | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-clusters met behulp van de scriptactie.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="d527c-103">HDInsight op basis van Windows-clusters met behulp van de scriptactie aanpassen</span><span class="sxs-lookup"><span data-stu-id="d527c-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="d527c-104">**Actie script** mag gebruikte tooinvoke [aangepaste scripts](hdinsight-hadoop-script-actions.md) tijdens het Hallo-cluster maken voor het installeren van extra software op een cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="d527c-105">Hallo-informatie in dit artikel is een specifieke tooWindows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d527c-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="d527c-106">Zie voor Linux gebaseerde clusters [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527c-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d527c-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d527c-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d527c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d527c-109">HDInsight-clusters kunnen worden aangepast op tal van andere manieren zoals inclusief extra Azure Storage-accounts, Hallo Hadoop wijzigen configuratiebestanden (core site.xml, hive-site.xml, enz.) of toe te voegen gedeeld bibliotheken (bijvoorbeeld Hive, Oozie) algemene locaties in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="d527c-110">Deze aanpassingen kunnen doen via Azure PowerShell hello Azure HDInsight .NET SDK of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d527c-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="d527c-111">Zie voor meer informatie [maken Hadoop-clusters in HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="d527c-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="d527c-112">Scriptactie in het proces voor het Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="d527c-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="d527c-113">Scriptactie wordt alleen gebruikt terwijl een cluster wordt Hallo proces wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d527c-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="d527c-114">Hallo volgende diagram wordt weergegeven wanneer het Script wordt uitgevoerd tijdens het maken van een Hallo:</span><span class="sxs-lookup"><span data-stu-id="d527c-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="d527c-115">![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="d527c-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="d527c-116">Wanneer het Hallo-script wordt uitgevoerd, Hallo cluster Hallo ingevoerd **ClusterCustomization** fase.</span><span class="sxs-lookup"><span data-stu-id="d527c-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="d527c-117">Opgegeven parallel op Hallo van alle knooppunten in cluster Hallo en biedt volledige beheerdersbevoegdheden op Hallo knooppunten in dit stadium Hallo script met Hallo beheerder systeemaccount wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d527c-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="d527c-118">Hebt u beheerdersbevoegdheden op de clusterknooppunten Hallo tijdens de **ClusterCustomization** fase, kunt u Hallo script tooperform bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services.</span><span class="sxs-lookup"><span data-stu-id="d527c-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="d527c-119">Dus als onderdeel van het Hallo-script, moet u ervoor zorgen zijn dat Hallo Ambari-services en andere Hadoop-gerelateerde services actief voordat het Hallo-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d527c-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="d527c-120">Deze services zijn vereist toosuccessfully vast Hallo gezondheid en status van de cluster Hallo terwijl deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d527c-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="d527c-121">Als u een willekeurige configuratie op het cluster dat betrekking heeft op deze services wijzigt, moet u Hallo hulpfuncties die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="d527c-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="d527c-122">Zie voor meer informatie over hulpfuncties [scriptactie ontwikkelen scripts voor HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="d527c-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="d527c-123">Hallo-uitvoer en Hallo foutenlogboeken voor Hallo script worden opgeslagen in Hallo standaardopslagaccount die u hebt opgegeven voor het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="d527c-124">Hallo logboeken worden opgeslagen in een tabel met naam Hallo **u < \cluster-name-fragment >< \time-stamp > bestand**.</span><span class="sxs-lookup"><span data-stu-id="d527c-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="d527c-125">Dit zijn de cumulatieve logboeken van Hallo-script uitvoeren op alle Hallo knooppunten (hoofdknooppunt en worker-knooppunten) in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="d527c-126">Elk cluster kan accepteren meerdere scriptacties die worden aangeroepen in Hallo volgorde waarin ze worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d527c-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="d527c-127">Een script kan worden uitgevoerd op het hoofdknooppunt hello, Hallo worker-knooppunten of beide.</span><span class="sxs-lookup"><span data-stu-id="d527c-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="d527c-128">HDInsight biedt verschillende scripts tooinstall Hallo onderdelen op HDInsight-clusters te volgen:</span><span class="sxs-lookup"><span data-stu-id="d527c-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="d527c-129">Naam</span><span class="sxs-lookup"><span data-stu-id="d527c-129">Name</span></span> | <span data-ttu-id="d527c-130">Script</span><span class="sxs-lookup"><span data-stu-id="d527c-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="d527c-131">**Spark installeren**</span><span class="sxs-lookup"><span data-stu-id="d527c-131">**Install Spark**</span></span> |<span data-ttu-id="d527c-132">https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="d527c-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="d527c-133">Zie [installeert en gebruikt Spark in HDInsight-clusters][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="d527c-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="d527c-134">**R installeren**</span><span class="sxs-lookup"><span data-stu-id="d527c-134">**Install R**</span></span> |<span data-ttu-id="d527c-135">https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="d527c-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="d527c-136">Zie [installeert en gebruikt R op HDInsight-clusters][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="d527c-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="d527c-137">**Solr installeren**</span><span class="sxs-lookup"><span data-stu-id="d527c-137">**Install Solr**</span></span> |<span data-ttu-id="d527c-138">https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d527c-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="d527c-139">Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="d527c-140">- **Giraph installeren**</span><span class="sxs-lookup"><span data-stu-id="d527c-140">- **Install Giraph**</span></span> |<span data-ttu-id="d527c-141">https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d527c-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="d527c-142">Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="d527c-143">**Vooraf laden Hive-bibliotheken**</span><span class="sxs-lookup"><span data-stu-id="d527c-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="d527c-144">https://hdiconfigactions.BLOB.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="d527c-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="d527c-145">Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d527c-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="d527c-146">Aanroepen van scripts met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d527c-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="d527c-147">**Van hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="d527c-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="d527c-148">Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="d527c-149">Onder optionele configuratie voor Hallo **scriptacties** blade, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d527c-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="d527c-150">![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize scriptactie gebruik een cluster")</span><span class="sxs-lookup"><span data-stu-id="d527c-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d527c-151">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d527c-151">Property</span></span></th><th><span data-ttu-id="d527c-152">Waarde</span><span class="sxs-lookup"><span data-stu-id="d527c-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d527c-153">Naam</span><span class="sxs-lookup"><span data-stu-id="d527c-153">Name</span></span></td>
            <td><span data-ttu-id="d527c-154">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d527c-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="d527c-155">Script-URI</span><span class="sxs-lookup"><span data-stu-id="d527c-155">Script URI</span></span></td>
            <td><span data-ttu-id="d527c-156">Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="d527c-157">s</span><span class="sxs-lookup"><span data-stu-id="d527c-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="d527c-158">HEAD/Worker</span><span class="sxs-lookup"><span data-stu-id="d527c-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="d527c-159">Hallo-knooppunten opgeven (**Head** of **Worker**) op waarin aanpassing Hallo script wordt uitgevoerd.</b>.</span><span class="sxs-lookup"><span data-stu-id="d527c-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="d527c-160">Parameters</span><span class="sxs-lookup"><span data-stu-id="d527c-160">Parameters</span></span></td>
            <td><span data-ttu-id="d527c-161">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d527c-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="d527c-162">Druk op ENTER tooadd meer dan één script actie tooinstall meerdere onderdelen op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="d527c-163">Klik op **Selecteer** toosave Hallo script actie configuratie en doorgaan met het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="d527c-164">Aanroep scripts met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d527c-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="d527c-165">Deze volgende PowerShell-script laat zien hoe tooinstall Spark op Windows gebaseerd HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="d527c-166">tooinstall andere software, moet u het Hallo-scriptbestand tooreplace in Hallo script:</span><span class="sxs-lookup"><span data-stu-id="d527c-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="d527c-167">Wanneer u wordt gevraagd, voert u Hallo referenties voor Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="d527c-168">Het kan enkele minuten duren voordat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d527c-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="d527c-169">Aanroepen van scripts die met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d527c-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="d527c-170">Hallo volgende voorbeeld laat zien hoe tooinstall Spark op Windows gebaseerd HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="d527c-171">tooinstall andere software, moet u het Hallo-scriptbestand tooreplace in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="d527c-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="d527c-172">**een HDInsight-cluster met Spark toocreate**</span><span class="sxs-lookup"><span data-stu-id="d527c-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="d527c-173">Maak een C#-consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d527c-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d527c-174">Voer Hallo volgende opdracht uit op Hallo Nuget Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="d527c-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="d527c-175">Gebruik Hallo using-instructies in het bestand Program.cs hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="d527c-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="d527c-176">Hallo code in de klasse met de volgende Hallo Hallo plaatsen:</span><span class="sxs-lookup"><span data-stu-id="d527c-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="d527c-177">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d527c-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="d527c-178">Ondersteuning voor open-source software gebruikt op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="d527c-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="d527c-179">Hallo Microsoft Azure HDInsight-service is een flexibel platform waarmee u toobuild big data-toepassingen in Hallo cloud met behulp van een ecosysteem van open-source technologieën gevormd rond Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d527c-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="d527c-180">Microsoft Azure biedt een algemeen niveau van ondersteuning voor open-source technologieën, zoals beschreven in Hallo **ondersteunen bereik** sectie Hallo <a href="http://azure.microsoft.com/support/faq/" target="_blank">ondersteunen Veelgestelde vragen over Azure-website</a>.</span><span class="sxs-lookup"><span data-stu-id="d527c-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="d527c-181">Hallo HDInsight-service biedt een extra verificatieniveau van ondersteuning voor een aantal Hallo-onderdelen, zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d527c-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="d527c-182">Er zijn twee soorten open source-onderdelen die beschikbaar in Hallo HDInsight-service zijn:</span><span class="sxs-lookup"><span data-stu-id="d527c-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="d527c-183">**Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="d527c-184">YARN ResourceManager Hallo Hive query language (HiveQL) en Hallo Mahout bibliotheek bijvoorbeeld behoren toothis categorie.</span><span class="sxs-lookup"><span data-stu-id="d527c-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="d527c-185">Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="d527c-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="d527c-186">**Aangepaste onderdelen** -u, als een gebruiker van het Hallo-cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in Hallo community of door u gemaakte.</span><span class="sxs-lookup"><span data-stu-id="d527c-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="d527c-187">Ingebouwde-onderdelen worden volledig ondersteund en Microsoft Support wordt tooisolate help en oplossen van problemen met gerelateerde toothese onderdelen.</span><span class="sxs-lookup"><span data-stu-id="d527c-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="d527c-188">Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support zal helpen tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.</span><span class="sxs-lookup"><span data-stu-id="d527c-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="d527c-189">Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="d527c-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="d527c-190">Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="d527c-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="d527c-191">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d527c-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="d527c-192">Hallo HDInsight-service biedt verschillende manieren toouse aangepaste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="d527c-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="d527c-193">Ongeacht hoe een onderdeel gebruikt of geïnstalleerd op Hallo-cluster, hello hetzelfde niveau van de ondersteuning van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="d527c-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="d527c-194">Hieronder volgt een lijst van de meest voorkomende manieren Hallo dat aangepaste onderdelen op HDInsight-clusters kunnen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="d527c-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="d527c-195">Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d527c-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="d527c-196">Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die worden geïnstalleerd op de clusterknooppunten Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="d527c-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="d527c-197">Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op Hallo HDInsight-clusters bieden.</span><span class="sxs-lookup"><span data-stu-id="d527c-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="d527c-198">Deze voorbeelden worden geleverd zonder ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d527c-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="d527c-199">Scriptactie-scripts ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="d527c-199">Develop Script Action scripts</span></span>
<span data-ttu-id="d527c-200">Zie [scriptactie ontwikkelen scripts voor HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="d527c-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="d527c-201">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d527c-201">See also</span></span>
* <span data-ttu-id="d527c-202">[Hadoop-clusters maken in HDInsight] [ hdinsight-provision-cluster] vindt u instructies voor hoe toocreate een HDInsight-cluster met behulp van andere aangepaste opties.</span><span class="sxs-lookup"><span data-stu-id="d527c-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="d527c-203">[Scriptactie-scripts ontwikkelen voor HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="d527c-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="d527c-204">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="d527c-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="d527c-205">[Installeren en gebruiken van R op HDInsight-clusters][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="d527c-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="d527c-206">[Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="d527c-207">[Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="d527c-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"
