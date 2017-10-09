---
title: aaaAnalyze vluchtgegevens vertraging met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over hoe de Sqoop taak voor het uitvoeren van toouse een Windows PowerShell-script toocreate een HDInsight-cluster een Hive-taak uitvoert en Hallo cluster verwijderen.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="6642e-103">Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6642e-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="6642e-104">Hive biedt een methode voor Hadoop MapReduce-taken uitgevoerd via een SQL-achtige scripttaal genaamd  *[HiveQL][hadoop-hiveql]*, die naar samenvatten, opvragen en analyseren van grote hoeveelheden gegevens kunnen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="6642e-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6642e-105">Hallo moet stappen in dit document een HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="6642e-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="6642e-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6642e-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6642e-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6642e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6642e-108">Zie voor stappen die met een cluster op basis van Linux werken [vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6642e-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="6642e-109">Een van de belangrijkste voordelen van Azure HDInsight Hallo is Hallo scheiding van opslag van gegevens en rekencapaciteit.</span><span class="sxs-lookup"><span data-stu-id="6642e-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="6642e-110">HDInsight gebruikt Azure Blob-opslag voor gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="6642e-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="6642e-111">Een typische taak bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="6642e-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="6642e-112">**Gegevens opslaan in Azure Blob-opslag.**</span><span class="sxs-lookup"><span data-stu-id="6642e-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="6642e-113">Bijvoorbeeld, weerbericht gegevens, sensorgegevens, weblogboeken en in dit geval vertraging vluchtgegevens worden opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6642e-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="6642e-114">**Taken worden uitgevoerd.**</span><span class="sxs-lookup"><span data-stu-id="6642e-114">**Run jobs.**</span></span> <span data-ttu-id="6642e-115">Wanneer gegevens Hallo tooprocess is, voert u een Windows PowerShell-script (of een clienttoepassing) toocreate een HDInsight-cluster, taken uitvoeren en Hallo cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6642e-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="6642e-116">Hallo taken opslaan uitvoer gegevens tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6642e-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="6642e-117">Hallo uitvoergegevens wordt bewaard, zelfs nadat het Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6642e-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="6642e-118">Op deze manier u betaalt alleen wat u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6642e-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="6642e-119">**Hallo uitvoer ophalen uit Azure Blob storage**, of in deze zelfstudie Hallo gegevens tooan Azure SQL database te exporteren.</span><span class="sxs-lookup"><span data-stu-id="6642e-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="6642e-120">Hallo volgende diagram illustreert Hallo scenario en de structuur van deze zelfstudie Hallo:</span><span class="sxs-lookup"><span data-stu-id="6642e-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="6642e-122">Houd er rekening mee dat Hallo getallen in Hallo diagram toohello Sectietitels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="6642e-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="6642e-123">**M** staat voor Hallo hoofdproces.</span><span class="sxs-lookup"><span data-stu-id="6642e-123">**M** stands for hello main process.</span></span> <span data-ttu-id="6642e-124">**Een** staat voor de inhoud in de bijlage Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6642e-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="6642e-125">Hallo belangrijkste deel van Hallo zelfstudie ziet u hoe toouse een Windows PowerShell-script tooperform Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="6642e-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="6642e-126">Maak een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6642e-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="6642e-127">Een Hive-taak uitvoeren op Hallo cluster toocalculate gemiddelde vertragingen op luchthavens.</span><span class="sxs-lookup"><span data-stu-id="6642e-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="6642e-128">Hallo vertraging vluchtgegevens wordt opgeslagen in een Azure Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="6642e-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="6642e-129">Voer een Sqoop taak tooexport Hallo Hive-taak uitvoer tooan Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="6642e-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="6642e-130">Hallo HDInsight-cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6642e-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="6642e-131">In de bijlagen hello, kunt u Hallo-instructies vinden voor de vertraging vluchtgegevens uploaden, maken/uploaden van een queryreeks Hive en hello Azure SQL database voorbereiden voor Hallo Sqoop taak.</span><span class="sxs-lookup"><span data-stu-id="6642e-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="6642e-132">Hallo stappen in dit document zijn specifieke tooWindows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6642e-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="6642e-133">Zie voor stappen die met een cluster op basis van Linux werken [gegevens te analyseren vlucht vertraging met Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="6642e-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6642e-134">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6642e-134">Prerequisites</span></span>
<span data-ttu-id="6642e-135">Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="6642e-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="6642e-136">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="6642e-136">**An Azure subscription**.</span></span> <span data-ttu-id="6642e-137">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6642e-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6642e-138">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6642e-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6642e-139">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="6642e-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="6642e-140">Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="6642e-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="6642e-141">Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6642e-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="6642e-142">Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6642e-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="6642e-143">**Bestanden die in deze zelfstudie worden gebruikt**</span><span class="sxs-lookup"><span data-stu-id="6642e-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="6642e-144">Deze zelfstudie wordt gebruikgemaakt van Hallo tijdige prestaties van luchtvaartmaatschappij vluchtgegevens van [onderzoek en innovatieve technologie-beheer, Bureau vervoer statistieken of RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="6642e-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="6642e-145">Een kopie van Hallo gegevens zijn geüpload tooan Azure Blob storage-container met Hallo openbare Blob-machtiging.</span><span class="sxs-lookup"><span data-stu-id="6642e-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="6642e-146">Een gedeelte van het PowerShell-script kopieert Hallo gegevens van Hallo openbare blob-container toohello standaard blob-container van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6642e-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="6642e-147">Hallo HiveQL-script ook wordt gekopieerd toohello dezelfde Blob-container.</span><span class="sxs-lookup"><span data-stu-id="6642e-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="6642e-148">Als u wilt dat toolearn hoe tooget of uploadt Hallo gegevens tooyour eigenaar Storage-account en hoe toocreate of uploadt Hallo HiveQL script bestand, Zie [bijlage A](#appendix-a) en [bijlage B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="6642e-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="6642e-149">Hallo bevat volgende tabel Hallo-bestanden in deze zelfstudie gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6642e-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="6642e-150">Bestanden</span><span class="sxs-lookup"><span data-stu-id="6642e-150">Files</span></span></th><th><span data-ttu-id="6642e-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6642e-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="6642e-152">Hallo HiveQL-scriptbestand gebruikt door Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="6642e-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="6642e-153">Dit script is geüploade tooan Azure Blob storage-account met Hallo openbare toegang.</span><span class="sxs-lookup"><span data-stu-id="6642e-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="6642e-154"><a href="#appendix-b">Bijlage B</a> instructies over het voorbereiden en het uploaden van dit bestand tooyour eigen Azure Blob storage-account heeft.</span><span class="sxs-lookup"><span data-stu-id="6642e-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="6642e-155">De invoergegevens voor Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="6642e-155">Input data for hello Hive job.</span></span> <span data-ttu-id="6642e-156">Hallo-gegevens zijn geüpload tooan Azure Blob storage-account met Hallo openbare toegang.</span><span class="sxs-lookup"><span data-stu-id="6642e-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="6642e-157"><a href="#appendix-a">Bijlage A</a> bevat de instructies op Hallo-gegevens ophalen en uploadt Hallo gegevens tooyour eigen Azure Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="6642e-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="6642e-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="6642e-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="6642e-159">uitvoerpad Hallo voor Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="6642e-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="6642e-160">Hallo standaardcontainer wordt gebruikt voor het opslaan van Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="6642e-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="6642e-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="6642e-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="6642e-162">Hallo Hive-taak status map op de standaardcontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="6642e-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="6642e-163">Cluster maken en Hive/Sqoop taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6642e-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="6642e-164">Hadoop-MapReduce is batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="6642e-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="6642e-165">Hallo meeste rendabele manier toorun een Hive-taak is toocreate een cluster voor Hallo taak en Hallo taak verwijderen nadat het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6642e-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="6642e-166">Hallo volgende script bevat informatie over het hele proces Hallo.</span><span class="sxs-lookup"><span data-stu-id="6642e-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="6642e-167">Zie voor meer informatie over het maken van een HDInsight-cluster en het uitvoeren van Hive-taken [maken Hadoop-clusters in HDInsight] [ hdinsight-provision] en [Hive gebruiken met HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="6642e-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="6642e-168">**toorun hello Hive-query's met Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6642e-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="6642e-169">Een Azure SQL database en Hallo tabel voor Hallo Sqoop taakuitvoer maken met behulp van instructies Hallo in [bijlage C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="6642e-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="6642e-170">Open Windows PowerShell ISE en Hallo na script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6642e-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="6642e-171">Verbinding maken met tooyour SQL database en gemiddelde vertragingen per plaats in Hallo AvgDelays tabel zien:</span><span class="sxs-lookup"><span data-stu-id="6642e-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="6642e-173"><a id="appendix-a"></a>Bijlage A - uploaden vlucht vertraging gegevens tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="6642e-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="6642e-174">Hallo-gegevensbestand en Hallo HiveQL-scriptbestanden uploaden (Zie [bijlage B](#appendix-b)) vereist een planning.</span><span class="sxs-lookup"><span data-stu-id="6642e-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="6642e-175">Hallo idee is toostore Hallo-gegevensbestanden en Hallo HiveQL bestand voordat u een HDInsight-cluster en Hallo Hive-taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6642e-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="6642e-176">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="6642e-176">You have two options:</span></span>

* <span data-ttu-id="6642e-177">**Gebruik dezelfde hello Azure Storage-account dat wordt gebruikt door Hallo HDInsight-cluster als het standaardbestandssysteem Hallo.**</span><span class="sxs-lookup"><span data-stu-id="6642e-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="6642e-178">Omdat de HDInsight-cluster Hallo Hallo toegangssleutel voor Opslagaccount, hoeft u geen toomake wijzigingen aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="6642e-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="6642e-179">**Gebruik een ander Azure Storage-account van Hallo standaardbestandssysteem voor HDInsight-cluster.**</span><span class="sxs-lookup"><span data-stu-id="6642e-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="6642e-180">Als dit Hallo geval is, moet u Hallo maken deel uit van Hallo Windows PowerShell-script gevonden in wijzigen [maken HDInsight-cluster en voer Hive/Sqoop taken](#runjob) toolink Hallo Storage-account als een aanvullende Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6642e-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="6642e-181">Zie voor instructies [maken Hadoop-clusters in HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="6642e-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="6642e-182">Hallo HDInsight-cluster, vervolgens Hallo-toegangssleutel voor opslagaccount Hallo kent.</span><span class="sxs-lookup"><span data-stu-id="6642e-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="6642e-183">Hallo Blob opslagpad voor Hallo gegevensbestand hard gecodeerd in Hallo HiveQL-scriptbestand is.</span><span class="sxs-lookup"><span data-stu-id="6642e-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="6642e-184">U moet deze dienovereenkomstig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6642e-184">You must update it accordingly.</span></span>

<span data-ttu-id="6642e-185">**toodownload hello vluchtgegevens**</span><span class="sxs-lookup"><span data-stu-id="6642e-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="6642e-186">Te bladeren[onderzoek en beheer-innovatieve technologie, Bureau vervoer statistieken][rita-website].</span><span class="sxs-lookup"><span data-stu-id="6642e-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="6642e-187">Selecteer op Hallo pagina Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="6642e-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="6642e-188">Naam</span><span class="sxs-lookup"><span data-stu-id="6642e-188">Name</span></span></th><th><span data-ttu-id="6642e-189">Waarde</span><span class="sxs-lookup"><span data-stu-id="6642e-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="6642e-190">Filteren van jaar</span><span class="sxs-lookup"><span data-stu-id="6642e-190">Filter Year</span></span></td><td><span data-ttu-id="6642e-191">2013</span><span class="sxs-lookup"><span data-stu-id="6642e-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="6642e-192">Periode filteren</span><span class="sxs-lookup"><span data-stu-id="6642e-192">Filter Period</span></span></td><td><span data-ttu-id="6642e-193">Januari</span><span class="sxs-lookup"><span data-stu-id="6642e-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-194">Velden</span><span class="sxs-lookup"><span data-stu-id="6642e-194">Fields</span></span></td><td><span data-ttu-id="6642e-195">*Jaar*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *oorsprong*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*,  *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (alle andere velden wissen)</span><span class="sxs-lookup"><span data-stu-id="6642e-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="6642e-196">
3.Klik op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="6642e-196">
3. Click **Download**.</span></span>
<span data-ttu-id="6642e-197">4.</span><span class="sxs-lookup"><span data-stu-id="6642e-197">4.</span></span> <span data-ttu-id="6642e-198">Pak Hallo bestand toohello **C:\Tutorials\FlightDelay\2013Data** map.</span><span class="sxs-lookup"><span data-stu-id="6642e-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="6642e-199">Elk bestand is van een CSV-bestand en ongeveer 60GB groot is.</span><span class="sxs-lookup"><span data-stu-id="6642e-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="6642e-200">5.</span><span class="sxs-lookup"><span data-stu-id="6642e-200">5.</span></span> <span data-ttu-id="6642e-201">De naam Hallo bestand toohello van Hallo maand die deze gegevens voor bevat.</span><span class="sxs-lookup"><span data-stu-id="6642e-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="6642e-202">Bijvoorbeeld, Hallo gegevensbestand Hallo januari naam *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="6642e-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="6642e-203">6.</span><span class="sxs-lookup"><span data-stu-id="6642e-203">6.</span></span> <span data-ttu-id="6642e-204">Herhaal stappen 2 en 5 toodownload een bestand voor elke Hallo 12 maanden in 2013.</span><span class="sxs-lookup"><span data-stu-id="6642e-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="6642e-205">U moet minimaal één bestand toorun Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6642e-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="6642e-206">**tooupload hello vlucht vertraging gegevens tooAzure Blob-opslag**</span><span class="sxs-lookup"><span data-stu-id="6642e-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="6642e-207">Bereid Hallo parameters:</span><span class="sxs-lookup"><span data-stu-id="6642e-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="6642e-208">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="6642e-208">Variable Name</span></span></th><th><span data-ttu-id="6642e-209">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6642e-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="6642e-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="6642e-210">$storageAccountName</span></span></td><td><span data-ttu-id="6642e-211">Hallo waar u tooupload Hallo gegevens naar Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6642e-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="6642e-212">$blobContainerName</span></span></td><td><span data-ttu-id="6642e-213">Hallo waar u tooupload Hallo gegevens naar Blob-container.</span><span class="sxs-lookup"><span data-stu-id="6642e-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="6642e-214">Open Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6642e-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="6642e-215">3.</span><span class="sxs-lookup"><span data-stu-id="6642e-215">3.</span></span> <span data-ttu-id="6642e-216">Plak de volgende script in het scriptvenster Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6642e-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="6642e-217">Druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="6642e-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="6642e-218">Als u een andere methode kiest voor het uploaden van bestanden Hallo toouse, zorg Hallo bestandspad wordt flightdelay-zelfstudies-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6642e-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="6642e-219">Hallo-syntaxis voor toegang tot bestanden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="6642e-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="6642e-220">Hallo pad zelfstudies/flightdelay/gegevens is Hallo virtuele map die u hebt gemaakt toen u Hallo bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="6642e-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="6642e-221">Controleer of er 12 bestanden, één voor elke maand.</span><span class="sxs-lookup"><span data-stu-id="6642e-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="6642e-222">Hallo Hive query tooread vanaf de nieuwe locatie hello, moet u bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6642e-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="6642e-223">Hallo container toegang machtiging toobe openbare configureren of binden Hallo Storage account toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6642e-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="6642e-224">Hallo Hive-queryreeks worden anders niet kunnen tooaccess Hallo gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6642e-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="6642e-225"><a id="appendix-b"></a>Bijlage B - maken en uploaden van een HiveQL-script</span><span class="sxs-lookup"><span data-stu-id="6642e-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="6642e-226">Met Azure PowerShell, kunt u meerdere HiveQL-instructies één uitvoeren op een tijd of pakket Hallo instructie van HiveQL in een scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="6642e-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="6642e-227">Deze sectie leest u hoe toocreate HiveQL-script en uploaden Hallo tooAzure Blob-opslag script met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6642e-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="6642e-228">Hive vereist Hallo HiveQL scripts toobe opgeslagen in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6642e-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="6642e-229">Hallo HiveQL-script voert Hallo volgende uit:</span><span class="sxs-lookup"><span data-stu-id="6642e-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="6642e-230">**Hallo delays_raw tabel**, geval Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="6642e-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="6642e-231">**Hallo delays_raw externe Hive-tabel maken** toohello Blob-opslaglocatie met Hallo vlucht vertraging bestanden aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="6642e-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="6642e-232">Deze query geeft aan dat de velden worden gescheiden door ',' en dat de regels worden beëindigd door '\n'.</span><span class="sxs-lookup"><span data-stu-id="6642e-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="6642e-233">Dit is een probleem wanneer veldwaarden komma's bevatten omdat Hive kan geen onderscheid maken tussen een door komma's die een veldscheidingsteken en een die deel uitmaakt van een veldwaarde (die Hallo geval veldwaarden voor de oorsprong is\_STAD\_naam en doel\_ Plaats\_naam).</span><span class="sxs-lookup"><span data-stu-id="6642e-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="6642e-234">tooaddress deze, Hallo query maakt TEMP kolommen toohold gegevens die onjuist is onderverdeeld in kolommen.</span><span class="sxs-lookup"><span data-stu-id="6642e-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="6642e-235">**Hallo vertragingen tabel**, geval Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="6642e-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="6642e-236">**Hallo vertragingen tabel maken**.</span><span class="sxs-lookup"><span data-stu-id="6642e-236">**Create hello delays table**.</span></span> <span data-ttu-id="6642e-237">Is het handig tooclean up Hallo-gegevens voor verdere verwerking.</span><span class="sxs-lookup"><span data-stu-id="6642e-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="6642e-238">Deze query maakt een nieuwe tabel *vertragingen*, uit Hallo delays_raw tabel.</span><span class="sxs-lookup"><span data-stu-id="6642e-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="6642e-239">Opmerking Hallo TEMP kolommen (zoals eerder vermeld) worden niet gekopieerd en die Hallo **subtekenreeks** functie gebruikte tooremove aanhalingstekens Hallo gegevens is.</span><span class="sxs-lookup"><span data-stu-id="6642e-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="6642e-240">**Hallo gemiddelde weer vertraging en groepen Hallo resultaten plaatsnaam berekenen.**</span><span class="sxs-lookup"><span data-stu-id="6642e-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="6642e-241">Dit wordt ook Hallo resultaten tooBlob opslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6642e-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="6642e-242">Houd er rekening mee die query Hallo Hallo gegevens verwijderen van enkele aanhalingstekens en uitsluit rijen waar Hallo waarde voor **weather_delay** is null.</span><span class="sxs-lookup"><span data-stu-id="6642e-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="6642e-243">Dit is nodig omdat Sqoop, die verderop in deze zelfstudie wordt gebruikt, kunnen niet worden verwerkt die waarden probleemloos standaard.</span><span class="sxs-lookup"><span data-stu-id="6642e-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="6642e-244">Zie voor een volledige lijst van Hallo HiveQL opdrachten [Hive Data Definition Language][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="6642e-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="6642e-245">Elke opdracht HiveQL moet eindigen met een puntkomma.</span><span class="sxs-lookup"><span data-stu-id="6642e-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="6642e-246">**een scriptbestand HiveQL toocreate**</span><span class="sxs-lookup"><span data-stu-id="6642e-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="6642e-247">Bereid Hallo parameters:</span><span class="sxs-lookup"><span data-stu-id="6642e-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="6642e-248">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="6642e-248">Variable Name</span></span></th><th><span data-ttu-id="6642e-249">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6642e-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="6642e-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="6642e-250">$storageAccountName</span></span></td><td><span data-ttu-id="6642e-251">Hello Azure Storage-account waar u tooupload hello HiveQL-script op.</span><span class="sxs-lookup"><span data-stu-id="6642e-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="6642e-252">$blobContainerName</span></span></td><td><span data-ttu-id="6642e-253">Hallo Blob-container waar u tooupload hello HiveQL-script op.</span><span class="sxs-lookup"><span data-stu-id="6642e-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="6642e-254">Open Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6642e-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="6642e-255">3.</span><span class="sxs-lookup"><span data-stu-id="6642e-255">3.</span></span> <span data-ttu-id="6642e-256">Kopieer en plak de volgende script in het scriptvenster Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6642e-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="6642e-257">Hier volgen Hallo variabelen in Hallo script gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6642e-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="6642e-258">**$hqlLocalFileName** -Hallo script bestand wordt opgeslagen Hallo HiveQL-script lokaal voordat u dit uploadt tooBlob opslag.</span><span class="sxs-lookup"><span data-stu-id="6642e-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="6642e-259">Dit is de bestandsnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="6642e-259">This is hello file name.</span></span> <span data-ttu-id="6642e-260">de standaardwaarde Hallo is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="6642e-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="6642e-261">**$hqlBlobName** -dit is Hallo HiveQL-script blob bestandsnaam in hello Azure Blob-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6642e-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="6642e-262">de standaardwaarde Hallo is tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="6642e-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="6642e-263">Omdat het Hallo-bestand zal tooAzure Blob-opslag rechtstreeks worden geschreven, is er niet een "/" aan Hallo begin van Hallo blob-naam.</span><span class="sxs-lookup"><span data-stu-id="6642e-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="6642e-264">Als u tooaccess Hallo-bestand van Blob-opslag wilt, moet u tooadd een "/" aan begin Hallo Hallo-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="6642e-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="6642e-265">**$srcDataFolder** en **$dstDataFolder** -= 'flightdelay-zelfstudies/gegevens' = 'flightdelay-zelfstudies/uitvoer'</span><span class="sxs-lookup"><span data-stu-id="6642e-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="6642e-266"><a id="appendix-c"></a>Bijlage C - een Azure SQL database voorbereiden voor Hallo Sqoop taakuitvoer</span><span class="sxs-lookup"><span data-stu-id="6642e-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="6642e-267">**tooprepare hello SQL-database (samenvoegen dit Hello Sqoop script)**</span><span class="sxs-lookup"><span data-stu-id="6642e-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="6642e-268">Bereid Hallo parameters:</span><span class="sxs-lookup"><span data-stu-id="6642e-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="6642e-269">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="6642e-269">Variable Name</span></span></th><th><span data-ttu-id="6642e-270">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6642e-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="6642e-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="6642e-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="6642e-272">Hallo-naam van hello Azure SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="6642e-273">Voer niets toocreate een nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="6642e-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="6642e-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="6642e-275">Hallo aanmeldingsnaam voor hello Azure SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="6642e-276">Als $sqlDatabaseServerName een bestaande server is, zijn Hallo aanmeldingsnaam en wachtwoord bij de aanmelding gebruikte tooauthenticate met Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="6642e-277">Ze zijn anders gebruikte toocreate een nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="6642e-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="6642e-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="6642e-279">Hallo aanmeldingswachtwoord voor hello Azure SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="6642e-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="6642e-281">Deze waarde wordt alleen gebruikt als u een nieuwe Azure-database-server maakt.</span><span class="sxs-lookup"><span data-stu-id="6642e-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="6642e-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="6642e-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="6642e-283">Hallo SQL-database gebruikt toocreate hello AvgDelays tabel voor Hallo Sqoop taak.</span><span class="sxs-lookup"><span data-stu-id="6642e-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="6642e-284">Leeg laat, wordt een database met de naam HDISqoop maken.</span><span class="sxs-lookup"><span data-stu-id="6642e-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="6642e-285">Hallo tabelnaam voor Hallo Sqoop taakuitvoer is AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="6642e-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="6642e-286">Open Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6642e-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="6642e-287">3.</span><span class="sxs-lookup"><span data-stu-id="6642e-287">3.</span></span> <span data-ttu-id="6642e-288">Kopieer en plak de volgende script in het scriptvenster Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6642e-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="6642e-289">Hallo-script gebruikt een representational state transfer (REST)-service, http://bot.whatismyipaddress.com, tooretrieve uw externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6642e-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="6642e-290">Hallo IP-adres wordt gebruikt voor het maken van een firewallregel voor uw SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="6642e-291">Hier volgen een aantal variabelen in Hallo script gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6642e-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="6642e-292">**$ipAddressRestService** -Hallo standaardwaarde is http://bot.whatismyipaddress.com. Het is een openbaar IP-adres REST-service voor het ophalen van het externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6642e-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="6642e-293">U kunt andere services als u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6642e-293">You can use other services if you want.</span></span> <span data-ttu-id="6642e-294">Hallo externe IP-adres opgehaald via Hallo-service worden gebruikte toocreate een firewallregel voor uw Azure SQL database-server, zodat u toegang hebt tot Hallo database vanuit uw werkstation (met behulp van Windows PowerShell-script).</span><span class="sxs-lookup"><span data-stu-id="6642e-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="6642e-295">**$fireWallRuleName** -dit is de naam Hallo Hallo firewallregel voor hello Azure SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6642e-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="6642e-296">Hallo standaardnaam is <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="6642e-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="6642e-297">U kunt deze desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6642e-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="6642e-298">**$sqlDatabaseMaxSizeGB** -deze waarde wordt alleen gebruikt wanneer u een nieuwe Azure SQL database-server maakt.</span><span class="sxs-lookup"><span data-stu-id="6642e-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="6642e-299">Hallo-standaardwaarde is 10GB.</span><span class="sxs-lookup"><span data-stu-id="6642e-299">hello default value is 10GB.</span></span> <span data-ttu-id="6642e-300">10GB is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6642e-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="6642e-301">**$sqlDatabaseName** -deze waarde wordt alleen gebruikt wanneer u een nieuwe Azure SQL database maakt.</span><span class="sxs-lookup"><span data-stu-id="6642e-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="6642e-302">de standaardwaarde Hallo is HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="6642e-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="6642e-303">Als u de naam wijzigt, moet u Hallo Sqoop Windows PowerShell-script dienovereenkomstig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6642e-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="6642e-304">Druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="6642e-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="6642e-305">Hallo-scriptuitvoer valideren.</span><span class="sxs-lookup"><span data-stu-id="6642e-305">Validate hello script output.</span></span> <span data-ttu-id="6642e-306">Zorg ervoor dat het Hallo-script is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6642e-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="6642e-307"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6642e-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="6642e-308">Nu u begrijpt hoe tooupload een bestand tooAzure Blob-opslag, hoe toopopulate een Hive-tabel met behulp van Hallo gegevens uit Azure Blob storage, hoe toorun Hive-query's en hoe toouse Sqoop tooexport gegevens uit HDFS tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6642e-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="6642e-309">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6642e-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="6642e-310">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6642e-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="6642e-311">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6642e-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="6642e-312">[Oozie gebruiken met HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="6642e-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="6642e-313">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="6642e-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="6642e-314">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6642e-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="6642e-315">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6642e-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
