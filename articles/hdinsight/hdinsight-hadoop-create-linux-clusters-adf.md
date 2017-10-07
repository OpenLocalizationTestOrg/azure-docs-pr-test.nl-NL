---
title: aaaCreate op aanvraag Hadoop-clusters met behulp van de Data Factory - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate op aanvraag Hadoop-clusters in HDInsight met behulp van Azure Data Factory.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="6da42-103">Hadoop-clusters op aanvraag maken in HDInsight met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6da42-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="6da42-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is een cloud-gebaseerde gegevens integration-service die ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6da42-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="6da42-105">Dit kan een HDInsight Hadoop-cluster just in time tooprocess een segment invoergegevens maken en Hallo cluster verwijderen als Hallo-verwerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="6da42-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="6da42-106">Enkele van de voordelen van het gebruik van een on-demand HDInsight Hadoop-cluster Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="6da42-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="6da42-107">U alleen betalen voor Hallo tijd taak wordt uitgevoerd op Hallo HDInsight Hadoop-cluster (plus een korte configureerbare niet-actieve tijd).</span><span class="sxs-lookup"><span data-stu-id="6da42-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="6da42-108">Hallo facturering voor HDInsight-clusters worden pro rato per minuut, of u ze worden gebruikt of niet.</span><span class="sxs-lookup"><span data-stu-id="6da42-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="6da42-109">Wanneer u een gekoppelde HDInsight-service op aanvraag in de Data Factory gebruikt, Hallo clusters op aanvraag gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6da42-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="6da42-110">En Hallo clusters worden automatisch verwijderd wanneer Hallo taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="6da42-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="6da42-111">Daarom betaalt u alleen voor actieve tijd en Hallo korte niet-actieve tijd (time to live-instelling) Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="6da42-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="6da42-112">U kunt een werkstroom met behulp van een Data Factory-pijplijn maken.</span><span class="sxs-lookup"><span data-stu-id="6da42-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="6da42-113">U kunt bijvoorbeeld Hallo pijplijn toocopy gegevens uit een lokale SQL Server tooan Azure blob-opslag, gegevens over het installatieproces Hallo door het uitvoeren van een Hive-script en Pig-script op een on-demand HDInsight Hadoop-cluster hebben.</span><span class="sxs-lookup"><span data-stu-id="6da42-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="6da42-114">Kopieer vervolgens Hallo resultaat gegevens tooan Azure SQL Data Warehouse voor BI toepassingen tooconsume.</span><span class="sxs-lookup"><span data-stu-id="6da42-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="6da42-115">U kunt plannen Hallo werkstroom toorun periodiek (elk uur, dagelijks, wekelijks, maandelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="6da42-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="6da42-116">Een gegevensfactory kan één of meer gegevenspijplijnen hebben in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="6da42-117">Een pijplijn gegevens heeft een of meer activiteiten.</span><span class="sxs-lookup"><span data-stu-id="6da42-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="6da42-118">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](../data-factory/data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="6da42-119">U gebruikt data movement activiteiten (momenteel alleen Kopieeractiviteit) toomove gegevens uit een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6da42-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="6da42-120">U gebruikt gegevenstransformatie activiteiten tootransform/proces gegevens.</span><span class="sxs-lookup"><span data-stu-id="6da42-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="6da42-121">HDInsight Hive-activiteit is een van de activiteiten voor gegevenstransformatie hello wordt ondersteund door de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="6da42-122">U Hallo Hive-transformatie-activiteit gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6da42-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="6da42-123">Uw eigen HDInsight Hadoop-cluster of een on-demand HDInsight Hadoop-cluster, kunt u een hive-activiteit toouse configureren.</span><span class="sxs-lookup"><span data-stu-id="6da42-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="6da42-124">In deze zelfstudie is Hallo Hive-activiteit in Hallo data factory-pijplijn geconfigureerde toouse een HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6da42-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="6da42-125">Daarom wanneer Hallo activiteit actief tooprocess een gegevenssegment, is dit wat er gebeurt:</span><span class="sxs-lookup"><span data-stu-id="6da42-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="6da42-126">Een HDInsight Hadoop-cluster wordt automatisch gemaakt voor u just in time tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="6da42-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="6da42-127">Hallo invoergegevens wordt verwerkt door een HiveQL-script uitvoeren op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6da42-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="6da42-128">Hallo HDInsight Hadoop-cluster wordt verwijderd nadat het Hallo-verwerking is voltooid en Hallo cluster Hallo geconfigureerd en de hoeveelheid tijd (timeToLive-instelling) niet actief is.</span><span class="sxs-lookup"><span data-stu-id="6da42-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="6da42-129">Als de volgende gegevenssegment Hallo beschikbaar voor verwerking met van inactiviteit timeToLive is, is hello hetzelfde cluster gebruikte tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="6da42-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="6da42-130">In deze zelfstudie voert Hallo HiveQL-script die zijn gekoppeld aan het hive-activiteit Hallo Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="6da42-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="6da42-131">Maakt een externe tabel waarin verwijzingen Hallo onbewerkte web logboekgegevens opgeslagen in een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="6da42-132">Partities Hallo onbewerkte gegevens op jaar en maand.</span><span class="sxs-lookup"><span data-stu-id="6da42-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="6da42-133">Winkels Hallo gepartitioneerde gegevens in hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="6da42-134">In deze zelfstudie maakt Hallo HiveQL-script die zijn gekoppeld aan het hive-activiteit Hallo een externe tabel waarin verwijzingen Hallo onbewerkte web logboekgegevens opgeslagen in hello Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6da42-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="6da42-135">Hier vindt u voor elke maand Hallo voorbeeld rijen in het invoerbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="6da42-136">Hallo HiveQL-script partities Hallo onbewerkte gegevens op jaar en maand.</span><span class="sxs-lookup"><span data-stu-id="6da42-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="6da42-137">Drie uitvoermappen op basis van de vorige invoer hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6da42-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="6da42-138">Elke map bevat een bestand met vermeldingen van elke maand.</span><span class="sxs-lookup"><span data-stu-id="6da42-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="6da42-139">Zie voor een lijst van activiteiten voor gegevenstransformatie Data Factory in toevoeging tooHive activiteit [transformeren en analyseren met Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6da42-140">U kunt op dit moment alleen HDInsight-cluster versie 3.2 maken uit Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6da42-141">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6da42-141">Prerequisites</span></span>
<span data-ttu-id="6da42-142">Voordat u Hallo-instructies in dit artikel, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="6da42-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="6da42-143">[Azure-abonnement](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6da42-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6da42-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6da42-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="6da42-145">Voorbereiden van de storage-account</span><span class="sxs-lookup"><span data-stu-id="6da42-145">Prepare storage account</span></span>
<span data-ttu-id="6da42-146">U kunt gebruiken om toothree storage-accounts in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="6da42-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="6da42-147">storage-standaardaccount voor Hallo HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="6da42-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="6da42-148">Storage-account voor de invoergegevens Hallo</span><span class="sxs-lookup"><span data-stu-id="6da42-148">storage account for hello input data</span></span>
- <span data-ttu-id="6da42-149">Storage-account voor de uitvoergegevens Hallo</span><span class="sxs-lookup"><span data-stu-id="6da42-149">storage account for hello output data</span></span>

<span data-ttu-id="6da42-150">toosimplify hello zelfstudie maakt u één storage account tooserve Hallo drie doeleinden.</span><span class="sxs-lookup"><span data-stu-id="6da42-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="6da42-151">Hello Azure PowerShell-voorbeeldscript vinden in deze sectie voert Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da42-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="6da42-152">Meld u bij tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6da42-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="6da42-153">Maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6da42-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="6da42-154">Maak een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6da42-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="6da42-155">Een Blob-container in Hallo storage-account maken</span><span class="sxs-lookup"><span data-stu-id="6da42-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="6da42-156">Kopieer Hallo twee bestanden toohello Blob-container te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da42-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="6da42-157">Invoergegevens bestand: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="6da42-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="6da42-158">HiveQL-script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="6da42-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="6da42-159">Beide bestanden worden opgeslagen in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="6da42-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="6da42-160">**tooprepare hello opslag en kopieer Hallo bestanden met Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="6da42-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6da42-161">Geef namen voor hello Azure-resourcegroep en hello Azure storage-account die door het Hallo-script wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6da42-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="6da42-162">Noteer **Resourcegroepnaam**, **opslagaccountnaam**, en **opslagaccountsleutel** output door Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="6da42-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="6da42-163">U moet deze in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="6da42-164">Als u hulp nodig bij Hallo PowerShell-script, Zie [Using hello Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="6da42-165">Als u Azure CLI toouse in plaats daarvan Hallo raadpleegt [bijlage](#appendix) sectie voor hello Azure CLI-script.</span><span class="sxs-lookup"><span data-stu-id="6da42-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="6da42-166">**tooexamine hello storage-account en Hallo inhoud**</span><span class="sxs-lookup"><span data-stu-id="6da42-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="6da42-167">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6da42-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6da42-168">Klik op **resourcegroepen** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="6da42-169">Dubbelklik op Hallo Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="6da42-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="6da42-170">Hallo-filter gebruiken als er te veel resourcegroepen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="6da42-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="6da42-171">Op Hallo **Resources** tegel, wordt er een resource in de lijst, tenzij u de resourcegroep Hallo met andere projecten delen.</span><span class="sxs-lookup"><span data-stu-id="6da42-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="6da42-172">Deze resource is Hallo opslagaccount met de Hallo-naam die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6da42-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="6da42-173">Klik op Hallo opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="6da42-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="6da42-174">Klik op Hallo **Blobs** tegels.</span><span class="sxs-lookup"><span data-stu-id="6da42-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="6da42-175">Klik op Hallo **adfgetstarted** container.</span><span class="sxs-lookup"><span data-stu-id="6da42-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="6da42-176">U ziet twee mappen: **inputdata** en **script**.</span><span class="sxs-lookup"><span data-stu-id="6da42-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="6da42-177">Hallo-map openen en controleer Hallo-bestanden in mappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="6da42-178">Hallo inputdata hello input.log bestand met de invoergegevens bevat en Hallo scriptmap bevat Hallo HiveQL-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="6da42-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="6da42-179">Maak een gegevensfactory met Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="6da42-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="6da42-180">Hallo storage-account, Hallo invoergegevens en Hallo HiveQL-script is voorbereid, bent u klaar toocreate een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="6da42-181">Er zijn verschillende methoden voor het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6da42-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="6da42-182">In deze zelfstudie maakt maken u een gegevensfactory door het implementeren van een Azure Resource Manager-sjabloon met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6da42-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="6da42-183">U kunt ook een Resource Manager-sjabloon implementeren met behulp van [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) en [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="6da42-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="6da42-184">Zie voor andere data factory-aanmaakmethoden [zelfstudie: uw eerste gegevensfactory bouwen](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="6da42-185">Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6da42-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="6da42-186">Hallo-sjabloon bevindt zich op https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="6da42-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="6da42-187">Zie Hallo [Data Factory-entiteiten in de sjabloon Hallo](#data-factory-entities-in-the-template) sectie voor gedetailleerde informatie over entiteiten in Hallo sjabloon worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6da42-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="6da42-188">Selecteer **gebruik bestaande** optie voor Hallo **resourcegroep** -instelling en selecteer Hallo-naam van het Hallo-resourcegroep die u hebt gemaakt in de vorige stap hello (met behulp van PowerShell-script).</span><span class="sxs-lookup"><span data-stu-id="6da42-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="6da42-189">Voer een naam voor de gegevensfactory hello (**Data Factory Name**).</span><span class="sxs-lookup"><span data-stu-id="6da42-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="6da42-190">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="6da42-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="6da42-191">Voer Hallo **opslagaccountnaam** en **opslagaccountsleutel** u in de vorige stap Hallo opgeschreven.</span><span class="sxs-lookup"><span data-stu-id="6da42-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="6da42-192">Selecteer **ik ga akkoord toohello voorwaarden en bepalingen** hierboven vermeld wordt na het lezen van via **voorwaarden en bepalingen**.</span><span class="sxs-lookup"><span data-stu-id="6da42-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="6da42-193">Selecteer **pincode toodashboard** optie.</span><span class="sxs-lookup"><span data-stu-id="6da42-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="6da42-194">Klik op **aankoop/maken**.</span><span class="sxs-lookup"><span data-stu-id="6da42-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="6da42-195">U ziet een tegel op Hallo Dashboard aangeroepen **implementatie van sjabloonimplementatie**.</span><span class="sxs-lookup"><span data-stu-id="6da42-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="6da42-196">Wachten tot Hallo **resourcegroep** blade voor de resourcegroep wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6da42-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="6da42-197">U kunt ook klikken op Hallo tegel als uw groep naam tooopen Hallo resource resourcegroepblade titel.</span><span class="sxs-lookup"><span data-stu-id="6da42-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="6da42-198">Klik op Hallo tegel tooopen Hallo-resourcegroep als Hallo resourcegroepblade nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="6da42-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="6da42-199">Nu u dat één meer data factory-resource weergegeven naast toohello storage account bron ziet.</span><span class="sxs-lookup"><span data-stu-id="6da42-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="6da42-200">Klik op de naam van uw gegevensfactory hello (waarde die u hebt opgegeven voor Hallo **Data Factory Name** parameter).</span><span class="sxs-lookup"><span data-stu-id="6da42-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="6da42-201">Klik op Hallo Hallo Data Factory-Blade **Diagram** tegel.</span><span class="sxs-lookup"><span data-stu-id="6da42-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="6da42-202">Hallo diagram ziet u een activiteit met een invoergegevensset en een uitvoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="6da42-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive-activiteit pipeline-diagram](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="6da42-204">Hallo-namen zijn gedefinieerd in Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6da42-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="6da42-205">Dubbelklik op **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="6da42-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="6da42-206">Op Hallo **onlangs bijgewerkt segmenten**, ziet u een segment.</span><span class="sxs-lookup"><span data-stu-id="6da42-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="6da42-207">Als de status van de Hallo **Bezig**, wacht totdat deze te worden gewijzigd**gereed**.</span><span class="sxs-lookup"><span data-stu-id="6da42-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="6da42-208">Het duurt meestal over **20 minuten** toocreate een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6da42-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="6da42-209">Controleer de Hallo data factory-uitvoer</span><span class="sxs-lookup"><span data-stu-id="6da42-209">Check hello data factory output</span></span>

1. <span data-ttu-id="6da42-210">Gebruik Hallo dezelfde procedure in Hallo laatste sessie toocheck Hallo-containers van de container adfgetstarted Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="6da42-211">Er zijn twee nieuwe containers bovendien ook**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="6da42-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="6da42-212">Een container met de naam die volgt op Hallo patroon: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="6da42-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="6da42-213">Deze container is Hallo standaardcontainer voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6da42-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="6da42-214">adfjobs: deze container is Hallo-container voor Hallo ADF taaklogboeken.</span><span class="sxs-lookup"><span data-stu-id="6da42-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="6da42-215">Hallo data factory-uitvoer wordt opgeslagen in **afgetstarted** zoals u hebt geconfigureerd in Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6da42-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="6da42-216">Klik op **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="6da42-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="6da42-217">Dubbelklik op **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="6da42-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="6da42-218">U ziet een **jaar = 2014** map omdat alle Hallo weblogboeken datum in het jaar 2014.</span><span class="sxs-lookup"><span data-stu-id="6da42-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="6da42-220">Als u de lijst Hallo detailanalyse, ziet u drie mappen voor januari, februari en maart.</span><span class="sxs-lookup"><span data-stu-id="6da42-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="6da42-221">En er is een logboekbestand voor elke maand.</span><span class="sxs-lookup"><span data-stu-id="6da42-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="6da42-223">Data Factory-entiteiten in Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="6da42-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="6da42-224">Hier ziet u hoe Hallo op het hoogste niveau Resource Manager-sjabloon voor een data factory eruit:</span><span class="sxs-lookup"><span data-stu-id="6da42-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="6da42-225">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="6da42-225">Define data factory</span></span>
<span data-ttu-id="6da42-226">U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da42-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="6da42-227">Hallo dataFactoryName is Hallo-naam van gegevensfactory Hallo die u opgeeft wanneer u Hallo sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="6da42-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="6da42-228">Gegevensfactory is momenteel alleen ondersteund in Hallo regio's VS-Oost, VS-West en Noord-Europa.</span><span class="sxs-lookup"><span data-stu-id="6da42-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="6da42-229">Entiteiten in de gegevensfactory Hallo definiëren</span><span class="sxs-lookup"><span data-stu-id="6da42-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="6da42-230">Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo:</span><span class="sxs-lookup"><span data-stu-id="6da42-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="6da42-231">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="6da42-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="6da42-232">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="6da42-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="6da42-233">De Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="6da42-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="6da42-234">De Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="6da42-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="6da42-235">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="6da42-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6da42-236">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="6da42-236">Azure Storage linked service</span></span>
<span data-ttu-id="6da42-237">Hello Azure Storage gekoppelde service uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="6da42-238">In deze zelfstudie wordt hello hetzelfde opslagaccount gebruikt als Hallo HDInsight storage-standaardaccount, invoergegevens opslag- en uitvoer gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="6da42-239">Daarom definieert u slechts één Azure Storage service gekoppelde.</span><span class="sxs-lookup"><span data-stu-id="6da42-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="6da42-240">In de servicedefinitie Hallo gekoppeld geeft u Hallo naam en sleutel van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="6da42-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="6da42-241">Zie [gekoppelde Azure Storage-service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="6da42-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="6da42-242">Hallo **connectionString** maakt gebruik van parameters storageAccountName en storageAccountKey Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="6da42-243">U kunt waarden voor deze parameters opgeven tijdens het Hallo-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="6da42-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="6da42-244">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="6da42-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="6da42-245">In Hallo op aanvraag HDInsight servicedefinitie gekoppeld, u waarden opgeven voor de configuratieparameters die worden gebruikt door Hallo Data Factory-service toocreate een HDInsight Hadoop-cluster tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="6da42-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="6da42-246">Zie [gekoppelde services berekenen](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artikel voor meer informatie over de JSON-eigenschappen die toodefine een gekoppelde HDInsight on demand-service.</span><span class="sxs-lookup"><span data-stu-id="6da42-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="6da42-247">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="6da42-247">Note hello following points:</span></span>

* <span data-ttu-id="6da42-248">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u.</span><span class="sxs-lookup"><span data-stu-id="6da42-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="6da42-249">Hallo HDInsight Hadoop-cluster wordt gemaakt in Hallo dezelfde regio bevinden als Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="6da42-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="6da42-250">Kennisgeving Hallo *timeToLive* instelling.</span><span class="sxs-lookup"><span data-stu-id="6da42-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="6da42-251">Hallo data factory worden Hallo cluster automatisch verwijderd nadat het Hallo-cluster is inactiviteit gedurende 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="6da42-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="6da42-252">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="6da42-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="6da42-253">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6da42-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="6da42-254">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="6da42-254">This behavior is by design.</span></span> <span data-ttu-id="6da42-255">Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment toobe verwerkt moet, tenzij er een bestaand livecluster is (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6da42-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="6da42-256">Zie [Gekoppelde on-demand HDInsight-service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6da42-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6da42-257">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="6da42-258">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="6da42-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="6da42-259">Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '.</span><span class="sxs-lookup"><span data-stu-id="6da42-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="6da42-260">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="6da42-261">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="6da42-261">Azure blob input dataset</span></span>
<span data-ttu-id="6da42-262">In de definitie van de invoergegevensset hello opgeven u Hallo namen van de blob-container, map en -bestand met de invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="6da42-263">Zie [eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="6da42-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="6da42-264">U ziet Hallo specifieke instellingen in de JSON-definitie hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da42-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="6da42-265">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="6da42-265">Azure Blob output dataset</span></span>
<span data-ttu-id="6da42-266">In de gegevenssetdefinitie Hallo-uitvoer geeft u Hallo namen van blob-container en map waarin de uitvoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="6da42-267">Zie [eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="6da42-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="6da42-268">Hallo folderPath geeft Hallo pad toohello map die uitvoergegevens Hallo bevat:</span><span class="sxs-lookup"><span data-stu-id="6da42-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="6da42-269">Hallo [gegevensset beschikbaarheid](../data-factory/data-factory-create-datasets.md#dataset-availability) instelling is als volgt:</span><span class="sxs-lookup"><span data-stu-id="6da42-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="6da42-270">Output dataset beschikbaarheid stations Hallo pijplijn in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="6da42-271">In dit voorbeeld Hallo segment maandelijks geproduceerd op Hallo laatste dag van de maand (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="6da42-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="6da42-272">Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="6da42-273">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="6da42-273">Data pipeline</span></span>
<span data-ttu-id="6da42-274">Definieert u een pijplijn waarmee gegevens worden omgezet door het Hive-script uitvoeren op een on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6da42-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="6da42-275">Zie [pijplijn-JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6da42-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="6da42-276">Hallo pipeline bevat één activiteit, HDInsightHive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="6da42-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="6da42-277">Als zowel begin- en einddatum in januari 2016, gegevens zijn voor slechts één maand (een segment) wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6da42-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="6da42-278">Beide *start* en *end* van Hallo activiteit hebben een datum in het verleden, zodat Hallo Data Factory gegevens Hallo maand onmiddellijk verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6da42-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="6da42-279">Als Hallo end in de toekomst is, wordt een ander segment in de Hallo data factory maakt als Hallo tijd afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="6da42-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="6da42-280">Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="6da42-281">Hallo-zelfstudie opschonen</span><span class="sxs-lookup"><span data-stu-id="6da42-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="6da42-282">Hallo blob-containers gemaakt door on-demand HDInsight-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="6da42-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="6da42-283">Met de gekoppelde HDInsight-service op aanvraag wordt een HDInsight-cluster gemaakt telkens wanneer een segment moet toobe verwerkt, tenzij er een bestaand livecluster (timeToLive); en Hallo cluster wordt verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6da42-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="6da42-284">Voor elk cluster maakt Azure Data Factory een blob-container in hello Azure blob-opslag gebruikt als Hallo stroage standaardaccount voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6da42-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="6da42-285">Hoewel de HDInsight-cluster wordt verwijderd, worden Hallo standaard blob storage-container en Hallo gekoppeld opslagaccount niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6da42-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="6da42-286">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="6da42-286">This behavior is by design.</span></span> <span data-ttu-id="6da42-287">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6da42-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="6da42-288">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="6da42-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="6da42-289">Hallo-namen van deze containers een patroon volgen: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="6da42-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="6da42-290">Hallo verwijderen **adfjobs** en **adfyourdatafactoryname-linkedservicename-datum** mappen.</span><span class="sxs-lookup"><span data-stu-id="6da42-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="6da42-291">Hallo adfjobs container bevat taaklogboeken uit Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6da42-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="6da42-292">Hallo-resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="6da42-292">Delete hello resource group</span></span>
<span data-ttu-id="6da42-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) gebruikte toodeploy is beheren en controleren van uw oplossing als een groep.</span><span class="sxs-lookup"><span data-stu-id="6da42-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="6da42-294">Een resourcegroep verwijdert, worden alle Hallo onderdelen binnen Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="6da42-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="6da42-295">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6da42-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6da42-296">Klik op **resourcegroepen** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="6da42-297">Klik op Hallo Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="6da42-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="6da42-298">Hallo-filter gebruiken als er te veel resourcegroepen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="6da42-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="6da42-299">Hallo-resourcegroep in een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="6da42-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="6da42-300">Op Hallo **Resources** tegel u heeft Hallo storage-standaardaccount en Hallo data factory is vermeld, tenzij u de resourcegroep Hallo met andere projecten delen.</span><span class="sxs-lookup"><span data-stu-id="6da42-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="6da42-301">Klik op **verwijderen** op Hallo Hallo blade bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6da42-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="6da42-302">In dat geval worden Hallo storage-account en Hallo-gegevens die zijn opgeslagen in Hallo storage-account verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6da42-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="6da42-303">Voer Hallo resource group name tooconfirm verwijderen en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="6da42-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="6da42-304">Als u niet dat toodelete Hallo storage-account wilt als u de resourcegroep Hallo verwijdert, overweeg Hallo architectuur volgen door te scheiden Hallo zakelijke gegevens uit Hallo storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="6da42-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="6da42-305">In dit geval u hebt één resourcegroep voor Hallo storage-account met Hallo zakelijke gegevens en andere resourcegroep voor Hallo storage-standaardaccount voor HDInsight gekoppelde service en Hallo data factory Hallo.</span><span class="sxs-lookup"><span data-stu-id="6da42-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="6da42-306">Wanneer u de tweede resourcegroep Hallo verwijdert, heeft deze geen invloed op Hallo zakelijke gegevens storage-account.</span><span class="sxs-lookup"><span data-stu-id="6da42-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="6da42-307">toodo zodat:</span><span class="sxs-lookup"><span data-stu-id="6da42-307">toodo so:</span></span>

* <span data-ttu-id="6da42-308">Hallo volgen op het hoogste niveau resourcegroep toohello samen met de Hallo Microsoft.DataFactory/datafactories resource in de Resource Manager-sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6da42-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="6da42-309">Hiermee maakt u een opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="6da42-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="6da42-310">Een nieuwe gekoppelde servicepunt toohello nieuwe opslagaccount toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6da42-310">Add a new linked service point toohello new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="6da42-311">Hallo HDInsight ondemand gekoppelde service met een extra dependsOn en een additionalLinkedServiceNames configureren:</span><span class="sxs-lookup"><span data-stu-id="6da42-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="6da42-312">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6da42-312">Next steps</span></span>
<span data-ttu-id="6da42-313">In dit artikel hebt u geleerd hoe toouse Azure Data Factory toocreate bellen op HDInsight-cluster tooprocess Hive-taken.</span><span class="sxs-lookup"><span data-stu-id="6da42-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="6da42-314">tooread meer:</span><span class="sxs-lookup"><span data-stu-id="6da42-314">tooread more:</span></span>

* [<span data-ttu-id="6da42-315">Hadoop-zelfstudie: aan de slag met Hadoop op basis van Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6da42-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="6da42-316">Hadoop op basis van Linux-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6da42-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="6da42-317">HDInsight-documentatie</span><span class="sxs-lookup"><span data-stu-id="6da42-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="6da42-318">Data factory-documentatie</span><span class="sxs-lookup"><span data-stu-id="6da42-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="6da42-319">Bijlage</span><span class="sxs-lookup"><span data-stu-id="6da42-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="6da42-320">Azure CLI-script</span><span class="sxs-lookup"><span data-stu-id="6da42-320">Azure CLI script</span></span>
<span data-ttu-id="6da42-321">U kunt Azure CLI gebruiken in plaats van Azure PowerShell toodo Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6da42-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="6da42-322">Azure CLI toouse Azure CLI eerst installeren volgens Hallo instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="6da42-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="6da42-323">Azure CLI tooprepare Hallo opslag gebruiken en het Hallo-bestanden te kopiëren</span><span class="sxs-lookup"><span data-stu-id="6da42-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="6da42-324">Hallo-containernaam is *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="6da42-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="6da42-325">Houd het omdat deze.</span><span class="sxs-lookup"><span data-stu-id="6da42-325">Keep it as it is.</span></span> <span data-ttu-id="6da42-326">Anders moet u tooupdate Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6da42-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="6da42-327">Als u hulp nodig bij dit script CLI, Zie [Using hello Azure CLI met Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6da42-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
