---
title: Op aanvraag met behulp van de Data Factory - Azure HDInsight Hadoop-clusters maken | Microsoft Docs
description: Informatie over het maken van op aanvraag Hadoop-clusters in HDInsight met behulp van Azure Data Factory.
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
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="ebd73-103">Hadoop-clusters op aanvraag maken in HDInsight met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ebd73-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ebd73-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is een cloud-gebaseerde gegevens integration-service die ingedeeld en automatiseert de verplaatsing en transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebd73-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="ebd73-105">Deze kunt maken van een HDInsight Hadoop-cluster just-in-time voor het verwerken van een segment invoergegevens en verwijderen van het cluster wanneer het verwerken voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ebd73-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="ebd73-106">Enkele van de voordelen van het gebruik van een on-demand HDInsight Hadoop-cluster zijn:</span><span class="sxs-lookup"><span data-stu-id="ebd73-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="ebd73-107">U alleen betalen voor de taak tijd wordt uitgevoerd op de HDInsight Hadoop-cluster (plus een korte configureerbare niet-actieve tijd).</span><span class="sxs-lookup"><span data-stu-id="ebd73-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="ebd73-108">De facturering voor HDInsight-clusters worden pro rato per minuut, of u ze worden gebruikt of niet.</span><span class="sxs-lookup"><span data-stu-id="ebd73-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="ebd73-109">Wanneer u een gekoppelde HDInsight-service op aanvraag in de Data Factory gebruikt, kan de clusters op aanvraag worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="ebd73-110">En de clusters worden automatisch verwijderd wanneer de taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="ebd73-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="ebd73-111">Daarom betaalt u alleen voor de taak met de tijd en de korte niet-actieve tijd (time to live-instelling).</span><span class="sxs-lookup"><span data-stu-id="ebd73-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="ebd73-112">U kunt een werkstroom met behulp van een Data Factory-pijplijn maken.</span><span class="sxs-lookup"><span data-stu-id="ebd73-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="ebd73-113">U kunt bijvoorbeeld de pijplijn gegevens kopiëren van een lokale SQL Server naar een Azure blob storage, de gegevens worden verwerkt door het uitvoeren van een Hive-script en Pig-script op een on-demand HDInsight Hadoop-cluster hebben.</span><span class="sxs-lookup"><span data-stu-id="ebd73-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ebd73-114">Kopieer vervolgens de resultaatgegevens naar een Azure SQL Data Warehouse voor BI-toepassingen om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebd73-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="ebd73-115">U kunt plannen dat de werkstroom periodiek wordt uitgevoerd (elk uur, dagelijks, wekelijks, maandelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="ebd73-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="ebd73-116">Een gegevensfactory kan één of meer gegevenspijplijnen hebben in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="ebd73-117">Een pijplijn gegevens heeft een of meer activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ebd73-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="ebd73-118">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](../data-factory/data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="ebd73-119">Activiteiten voor gegevensverplaatsing (momenteel alleen Kopieeractiviteit) kunt u gegevens uit een gegevensopslag bron verplaatsen naar een doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ebd73-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="ebd73-120">Kunt u activiteiten voor gegevenstransformatie transformatieproces gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebd73-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="ebd73-121">HDInsight Hive-activiteit is een van de activiteiten voor gegevenstransformatie ondersteund door Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="ebd73-122">U kunt de Hive-transformatie-activiteit gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ebd73-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="ebd73-123">U kunt een hive-activiteit voor het gebruik van uw eigen HDInsight Hadoop-cluster of een on-demand HDInsight Hadoop-cluster configureren.</span><span class="sxs-lookup"><span data-stu-id="ebd73-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ebd73-124">In deze zelfstudie wordt de Hive-activiteit in de data factory-pijplijn geconfigureerd voor gebruik van een HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="ebd73-125">Wanneer de activiteit wordt uitgevoerd voor het verwerken van een gegevenssegment, dus hier wat er gebeurt:</span><span class="sxs-lookup"><span data-stu-id="ebd73-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="ebd73-126">Een HDInsight Hadoop-cluster wordt automatisch gemaakt voor u just-in-time voor het verwerken van het segment.</span><span class="sxs-lookup"><span data-stu-id="ebd73-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="ebd73-127">De ingevoerde gegevens worden verwerkt door een HiveQL-script uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="ebd73-128">De HDInsight Hadoop-cluster wordt verwijderd nadat de verwerking voltooid is en het cluster niet actief voor de geconfigureerde hoeveelheid tijd (timeToLive-instelling is).</span><span class="sxs-lookup"><span data-stu-id="ebd73-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="ebd73-129">Als het volgende gegevenssegment voor verwerking met binnen deze timeToLive niet-actieve tijd beschikbaar is, wordt hetzelfde cluster wordt gebruikt voor het verwerken van het segment.</span><span class="sxs-lookup"><span data-stu-id="ebd73-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="ebd73-130">In deze zelfstudie maakt voert het HiveQL-script dat is gekoppeld aan het hive-activiteit de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="ebd73-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="ebd73-131">Maakt een externe tabel die verwijst naar de onbewerkte web logboekgegevens opgeslagen in een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="ebd73-132">De onbewerkte gegevens partitioneert op jaar en maand.</span><span class="sxs-lookup"><span data-stu-id="ebd73-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="ebd73-133">De gepartitioneerde-gegevens opslaat in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ebd73-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="ebd73-134">In deze zelfstudie maakt het HiveQL-script dat is gekoppeld aan het hive-activiteit een externe tabel die verwijst naar de onbewerkte web logboekgegevens opgeslagen in de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ebd73-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="ebd73-135">Hier ziet u de voorbeeldrijen per maand in het invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ebd73-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="ebd73-136">Het HiveQL-script partities van de onbewerkte gegevens op jaar en maand.</span><span class="sxs-lookup"><span data-stu-id="ebd73-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="ebd73-137">Drie uitvoermappen op basis van de vorige invoer wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="ebd73-138">Elke map bevat een bestand met vermeldingen van elke maand.</span><span class="sxs-lookup"><span data-stu-id="ebd73-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="ebd73-139">Zie voor een lijst van activiteiten voor gegevenstransformatie Data Factory naast het Hive-activiteit [transformeren en analyseren met Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ebd73-140">U kunt op dit moment alleen HDInsight-cluster versie 3.2 maken uit Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebd73-141">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ebd73-141">Prerequisites</span></span>
<span data-ttu-id="ebd73-142">Voordat u de instructies in dit artikel, hebt u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ebd73-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="ebd73-143">[Azure-abonnement](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ebd73-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="ebd73-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebd73-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="ebd73-145">Voorbereiden van de storage-account</span><span class="sxs-lookup"><span data-stu-id="ebd73-145">Prepare storage account</span></span>
<span data-ttu-id="ebd73-146">In dit scenario kunt u maximaal drie storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="ebd73-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="ebd73-147">storage-standaardaccount voor het HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="ebd73-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="ebd73-148">Storage-account voor de invoergegevens</span><span class="sxs-lookup"><span data-stu-id="ebd73-148">storage account for the input data</span></span>
- <span data-ttu-id="ebd73-149">Storage-account voor de uitvoergegevens</span><span class="sxs-lookup"><span data-stu-id="ebd73-149">storage account for the output data</span></span>

<span data-ttu-id="ebd73-150">Om te vereenvoudigen de zelfstudie, kunt u één opslagaccount voor de drie doeleinden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="ebd73-151">De Azure PowerShell-voorbeeldscript vinden in deze sectie voert de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="ebd73-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="ebd73-152">Aanmelden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd73-152">Log in to Azure.</span></span>
2. <span data-ttu-id="ebd73-153">Maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ebd73-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="ebd73-154">Maak een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="ebd73-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="ebd73-155">Een Blob-container in het opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="ebd73-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="ebd73-156">Kopieer de volgende twee bestanden naar de Blob-container:</span><span class="sxs-lookup"><span data-stu-id="ebd73-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="ebd73-157">Invoergegevens bestand: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="ebd73-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="ebd73-158">HiveQL-script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="ebd73-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="ebd73-159">Beide bestanden worden opgeslagen in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="ebd73-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="ebd73-160">**Voor het voorbereiden van de opslag en kopieer de bestanden met Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="ebd73-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ebd73-161">Geef namen voor de Azure-resourcegroep en de Azure storage-account die door het script wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="ebd73-162">Noteer **Resourcegroepnaam**, **opslagaccountnaam**, en **opslagaccountsleutel** output door het script.</span><span class="sxs-lookup"><span data-stu-id="ebd73-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="ebd73-163">U moet deze in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="ebd73-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="ebd73-164">Als u hulp nodig bij het PowerShell-script, Zie [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="ebd73-165">Als u Azure CLI gebruiken in plaats daarvan, Zie de [bijlage](#appendix) sectie voor het script voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ebd73-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="ebd73-166">**Het opslagaccount en de inhoud te onderzoeken**</span><span class="sxs-lookup"><span data-stu-id="ebd73-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="ebd73-167">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebd73-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ebd73-168">Klik op **resourcegroepen** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="ebd73-169">Dubbelklik op de Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="ebd73-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="ebd73-170">Het filter gebruiken als er te veel resourcegroepen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ebd73-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="ebd73-171">Op de **Resources** tegel, wordt er een resource in de lijst, tenzij u de resourcegroep met andere projecten delen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="ebd73-172">Deze resource is het opslagaccount met de naam die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ebd73-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="ebd73-173">Klik op de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ebd73-173">Click the storage account name.</span></span>
5. <span data-ttu-id="ebd73-174">Klik op de **Blobs** tegels.</span><span class="sxs-lookup"><span data-stu-id="ebd73-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="ebd73-175">Klik op de **adfgetstarted** container.</span><span class="sxs-lookup"><span data-stu-id="ebd73-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="ebd73-176">U ziet twee mappen: **inputdata** en **script**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="ebd73-177">Open de map en controleert u de bestanden in de mappen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="ebd73-178">De invoergegevens bevat het bestand input.log met invoergegevens en de scriptmap bevat het bestand HiveQL-script.</span><span class="sxs-lookup"><span data-stu-id="ebd73-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="ebd73-179">Maak een gegevensfactory met Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="ebd73-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="ebd73-180">Met de storage-account, de invoergegevens en het HiveQL-script dat is voorbereid, bent u klaar voor het maken van een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="ebd73-181">Er zijn verschillende methoden voor het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="ebd73-182">In deze zelfstudie maakt maken u een gegevensfactory door het implementeren van een Azure Resource Manager-sjabloon met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ebd73-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="ebd73-183">U kunt ook een Resource Manager-sjabloon implementeren met behulp van [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) en [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="ebd73-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="ebd73-184">Zie voor andere data factory-aanmaakmethoden [zelfstudie: uw eerste gegevensfactory bouwen](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="ebd73-185">Klik op de volgende afbeelding om u aan te melden bij Azure en de Resource Manager-sjabloon in Azure Portal te openen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="ebd73-186">De sjabloon bevindt zich op https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="ebd73-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="ebd73-187">Zie de [Data Factory-entiteiten in de sjabloon](#data-factory-entities-in-the-template) sectie voor gedetailleerde informatie over entiteiten gedefinieerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ebd73-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="ebd73-188">Selecteer **gebruik bestaande** optie voor de **resourcegroep** instelling en selecteer de naam van de resourcegroep die u hebt gemaakt in de vorige stap (met behulp van PowerShell-script).</span><span class="sxs-lookup"><span data-stu-id="ebd73-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="ebd73-189">Voer een naam voor de gegevensfactory (**Data Factory Name**).</span><span class="sxs-lookup"><span data-stu-id="ebd73-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="ebd73-190">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="ebd73-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="ebd73-191">Voer de **opslagaccountnaam** en **opslagaccountsleutel** u in de vorige stap hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="ebd73-192">Selecteer **ik ga akkoord met de voorwaarden en bepalingen** hierboven vermeld wordt na het lezen van via **voorwaarden en bepalingen**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="ebd73-193">Selecteer **vastmaken aan dashboard** optie.</span><span class="sxs-lookup"><span data-stu-id="ebd73-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="ebd73-194">Klik op **aankoop/maken**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="ebd73-195">U ziet een tegel op het Dashboard aangeroepen **implementatie van sjabloonimplementatie**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="ebd73-196">Wacht totdat de **resourcegroep** blade voor de resourcegroep wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ebd73-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="ebd73-197">U kunt ook klikken op de tegel met de titel als de naam van uw resources te openen van de blade met resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="ebd73-198">Klik op de tegel om te openen van de resourcegroep als de resourcegroepblade nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="ebd73-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="ebd73-199">U ziet nu één meer data factory resource vermeld naast de opslagbronnen-account.</span><span class="sxs-lookup"><span data-stu-id="ebd73-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="ebd73-200">Klik op de naam van uw gegevensfactory (waarde als u hebt opgegeven voor de **Data Factory Name** parameter).</span><span class="sxs-lookup"><span data-stu-id="ebd73-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="ebd73-201">Klik in de Data Factory-blade op de **Diagram** tegel.</span><span class="sxs-lookup"><span data-stu-id="ebd73-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="ebd73-202">Het diagram ziet u een activiteit met een invoergegevensset en een uitvoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="ebd73-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive-activiteit pipeline-diagram](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="ebd73-204">De namen zijn gedefinieerd in het Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ebd73-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="ebd73-205">Dubbelklik op **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="ebd73-206">Op de **onlangs bijgewerkt segmenten**, ziet u een segment.</span><span class="sxs-lookup"><span data-stu-id="ebd73-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="ebd73-207">Als de status **Bezig**, wacht u totdat deze is gewijzigd in **gereed**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="ebd73-208">Het duurt meestal over **20 minuten** om een HDInsight-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="ebd73-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="ebd73-209">Controleer de uitvoer van de data factory</span><span class="sxs-lookup"><span data-stu-id="ebd73-209">Check the data factory output</span></span>

1. <span data-ttu-id="ebd73-210">Gebruik dezelfde procedure in de laatste sessie om te controleren van de containers van de container adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="ebd73-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="ebd73-211">Er zijn twee nieuwe containers naast **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="ebd73-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="ebd73-212">Een container met de naam die voldoet aan het patroon: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="ebd73-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="ebd73-213">Deze container is de standaardcontainer voor het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="ebd73-214">adfjobs: deze container is de container voor de logboeken van de ADF-taak.</span><span class="sxs-lookup"><span data-stu-id="ebd73-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="ebd73-215">De data factory-uitvoer wordt opgeslagen in **afgetstarted** zoals u in de Resource Manager-sjabloon hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="ebd73-216">Klik op **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="ebd73-217">Dubbelklik op **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="ebd73-218">U ziet een **jaar = 2014** map omdat alle weblogboeken datum in het jaar 2014.</span><span class="sxs-lookup"><span data-stu-id="ebd73-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="ebd73-220">Als u de lijst detailanalyse, ziet u drie mappen voor januari, februari en maart.</span><span class="sxs-lookup"><span data-stu-id="ebd73-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="ebd73-221">En er is een logboekbestand voor elke maand.</span><span class="sxs-lookup"><span data-stu-id="ebd73-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="ebd73-223">Data Factory-entiteiten in de sjabloon</span><span class="sxs-lookup"><span data-stu-id="ebd73-223">Data Factory entities in the template</span></span>
<span data-ttu-id="ebd73-224">Hier ziet u hoe de op het hoogste niveau Resource Manager-sjabloon voor een data factory eruit:</span><span class="sxs-lookup"><span data-stu-id="ebd73-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="ebd73-225">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="ebd73-225">Define data factory</span></span>
<span data-ttu-id="ebd73-226">U definieert een gegevensfactory in de Resource Manager-sjabloon zoals in het volgende voorbeeld wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ebd73-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="ebd73-227">De dataFactoryName is de naam van de gegevensfactory die u opgeeft wanneer u de sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="ebd73-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="ebd73-228">Gegevensfactory is momenteel alleen ondersteund in de regio's VS-Oost, VS-West en Noord-Europa.</span><span class="sxs-lookup"><span data-stu-id="ebd73-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="ebd73-229">Entiteiten in de gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="ebd73-229">Defining entities within the data factory</span></span>
<span data-ttu-id="ebd73-230">De volgende Data Factory-entiteiten worden in de JSON-sjabloon gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="ebd73-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="ebd73-231">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="ebd73-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="ebd73-232">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="ebd73-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="ebd73-233">De Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="ebd73-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="ebd73-234">De Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="ebd73-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="ebd73-235">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="ebd73-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ebd73-236">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="ebd73-236">Azure Storage linked service</span></span>
<span data-ttu-id="ebd73-237">De gekoppelde Azure Storage-service koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="ebd73-238">In deze zelfstudie wordt hetzelfde opslagaccount gebruikt als de storage-standaardaccount HDInsight, invoergegevens-opslag- en uitvoer gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="ebd73-239">Daarom definieert u slechts één Azure Storage service gekoppelde.</span><span class="sxs-lookup"><span data-stu-id="ebd73-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="ebd73-240">In de definitie van de gekoppelde service geeft u de naam en sleutel van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="ebd73-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="ebd73-241">Zie [Een gekoppelde Azure Storage-service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="ebd73-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

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
<span data-ttu-id="ebd73-242">De tekenreeks **connectionString** maakt gebruik van de parameters storageAccountName en storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="ebd73-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="ebd73-243">U kunt waarden voor deze parameters opgeven tijdens de implementatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ebd73-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="ebd73-244">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="ebd73-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="ebd73-245">In de definitie op aanvraag een gekoppelde HDInsight-service geeft u waarden voor de configuratieparameters die worden gebruikt door de Data Factory-service voor het maken van een HDInsight Hadoop-cluster tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ebd73-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="ebd73-246">Zie het artikel [Compute linked services (Gekoppelde services verwerken)](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde HDInsight-service op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="ebd73-247">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="ebd73-247">Note the following points:</span></span>

* <span data-ttu-id="ebd73-248">De Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u.</span><span class="sxs-lookup"><span data-stu-id="ebd73-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="ebd73-249">De HDInsight Hadoop-cluster wordt gemaakt in dezelfde regio bevinden als het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ebd73-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="ebd73-250">U ziet de *timeToLive* instelling.</span><span class="sxs-lookup"><span data-stu-id="ebd73-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="ebd73-251">De gegevensfactory wordt het cluster automatisch verwijderd nadat het cluster is inactiviteit gedurende 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="ebd73-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="ebd73-252">Het HDInsight-cluster maakt een **standaardcontainer** in de blobopslag die u hebt opgegeven in de JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="ebd73-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="ebd73-253">HDInsight verwijdert deze container niet wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="ebd73-254">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="ebd73-254">This behavior is by design.</span></span> <span data-ttu-id="ebd73-255">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment moet worden verwerkt, tenzij er een bestaand livecluster is (**timeToLive**). Het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ebd73-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="ebd73-256">Zie [Gekoppelde on-demand HDInsight-service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebd73-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebd73-257">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="ebd73-258">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="ebd73-259">De namen van deze containers worden als volgt opgebouwd: adf**naamvanuwgegevensfactory**-**naamvangekoppeldeservice**-datum-/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="ebd73-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="ebd73-260">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om containers in uw Azure-blobopslag te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="ebd73-261">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="ebd73-261">Azure blob input dataset</span></span>
<span data-ttu-id="ebd73-262">In de definitie van de invoergegevensset geeft u de namen van de blob-container, map en -bestand dat de invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="ebd73-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="ebd73-263">Zie [Eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ebd73-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

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

<span data-ttu-id="ebd73-264">U ziet de volgende specifieke instellingen in de JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="ebd73-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ebd73-265">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="ebd73-265">Azure Blob output dataset</span></span>
<span data-ttu-id="ebd73-266">In de definitie van de uitvoer-gegevensset geeft u de namen van blob-container en map die uitvoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="ebd73-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="ebd73-267">Zie [Eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ebd73-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="ebd73-268">FolderPath geeft het pad naar de map die uitvoergegevens bevat:</span><span class="sxs-lookup"><span data-stu-id="ebd73-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="ebd73-269">De [gegevensset beschikbaarheid](../data-factory/data-factory-create-datasets.md#dataset-availability) instelling is als volgt:</span><span class="sxs-lookup"><span data-stu-id="ebd73-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="ebd73-270">In Azure Data Factory-uitvoer gegevensset beschikbaarheid stations de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="ebd73-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="ebd73-271">In dit voorbeeld wordt maandelijks op de laatste dag van de maand (EndOfInterval) het segment geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="ebd73-272">Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="ebd73-273">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="ebd73-273">Data pipeline</span></span>
<span data-ttu-id="ebd73-274">Definieert u een pijplijn waarmee gegevens worden omgezet door het Hive-script uitvoeren op een on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="ebd73-275">Zie [JSON-bestand voor een pijplijn](../data-factory/data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt voor het definiëren van een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ebd73-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

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

<span data-ttu-id="ebd73-276">De pijplijn bevat één activiteit, HDInsightHive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="ebd73-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="ebd73-277">Als zowel begin- en einddatum in januari 2016, gegevens zijn voor slechts één maand (een segment) wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="ebd73-278">Beide *start* en *end* hebben van de activiteit een datum in het verleden, zodat de Data Factory gegevens voor de maand onmiddellijk verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ebd73-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="ebd73-279">Als het end in de toekomst is, wordt een ander segment in de data factory maakt wanneer dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="ebd73-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="ebd73-280">Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="ebd73-281">De zelfstudie opschonen</span><span class="sxs-lookup"><span data-stu-id="ebd73-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="ebd73-282">De blob-containers die is gemaakt door on-demand HDInsight-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="ebd73-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="ebd73-283">Met de gekoppelde HDInsight-service op aanvraag wordt een HDInsight-cluster gemaakt telkens wanneer een segment moet worden verwerkt, tenzij er een bestaand livecluster (timeToLive); en het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ebd73-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="ebd73-284">Voor elk cluster maakt Azure Data Factory een blob-container in Azure blob storage gebruikt als het standaardaccount voor stroage voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="ebd73-285">Hoewel de HDInsight-cluster wordt verwijderd, worden de standaard blob storage-container en het bijbehorende opslagaccount niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="ebd73-286">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="ebd73-286">This behavior is by design.</span></span> <span data-ttu-id="ebd73-287">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="ebd73-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="ebd73-288">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="ebd73-289">De namen van deze containers volgen een patroon: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="ebd73-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="ebd73-290">Verwijder de **adfjobs** en **adfyourdatafactoryname-linkedservicename-datum** mappen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="ebd73-291">De container adfjobs bevat taaklogboeken uit Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ebd73-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="ebd73-292">De resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="ebd73-292">Delete the resource group</span></span>
<span data-ttu-id="ebd73-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wordt gebruikt om te implementeren, beheren en bewaken van uw oplossing als een groep.</span><span class="sxs-lookup"><span data-stu-id="ebd73-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="ebd73-294">Een resourcegroep verwijdert, worden de onderdelen binnen de groep.</span><span class="sxs-lookup"><span data-stu-id="ebd73-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="ebd73-295">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebd73-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ebd73-296">Klik op **resourcegroepen** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="ebd73-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="ebd73-297">Klik op de Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="ebd73-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="ebd73-298">Het filter gebruiken als er te veel resourcegroepen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ebd73-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="ebd73-299">De resourcegroep in een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="ebd73-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="ebd73-300">Op de **Resources** tegel u heeft het standaardopslagaccount en de gegevensfactory weergegeven tenzij u de resourcegroep met andere projecten delen.</span><span class="sxs-lookup"><span data-stu-id="ebd73-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="ebd73-301">Klik op **verwijderen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="ebd73-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="ebd73-302">In dat geval worden de storage-account en de gegevens die zijn opgeslagen in het opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ebd73-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="ebd73-303">Voer de naam van de resourcegroep verwijderen bevestigen en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ebd73-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="ebd73-304">Als u niet dat het storage-account wordt verwijderd wilt wanneer u de resourcegroep verwijdert, kunt u de volgende architectuur door te scheiden van de bedrijfsgegevens van het standaardopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ebd73-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="ebd73-305">In dit geval hebt u een resourcegroep voor het opslagaccount met de zakelijke gegevens en de andere resourcegroep voor het standaardopslagaccount voor HDInsight-service en de data factory gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ebd73-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="ebd73-306">Wanneer u de tweede resourcegroep verwijdert, heeft deze geen gevolgen voor de zakelijke gegevens storage-account.</span><span class="sxs-lookup"><span data-stu-id="ebd73-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="ebd73-307">Dit doet u als volgt:</span><span class="sxs-lookup"><span data-stu-id="ebd73-307">To do so:</span></span>

* <span data-ttu-id="ebd73-308">Voeg het volgende toe aan de site op het hoogste resourcegroep samen met de Microsoft.DataFactory/datafactories resource in het Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ebd73-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="ebd73-309">Hiermee maakt u een opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="ebd73-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="ebd73-310">Een nieuw gekoppelde service-punt aan het nieuwe opslagaccount toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ebd73-310">Add a new linked service point to the new storage account:</span></span>

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
* <span data-ttu-id="ebd73-311">De service van HDInsight ondemand gekoppeld met een extra dependsOn en een additionalLinkedServiceNames configureren:</span><span class="sxs-lookup"><span data-stu-id="ebd73-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="ebd73-312">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebd73-312">Next steps</span></span>
<span data-ttu-id="ebd73-313">In dit artikel hebt u geleerd hoe Azure Data Factory gebruiken voor het maken van HDInsight-cluster op aanvraag voor het verwerken van Hive-taken.</span><span class="sxs-lookup"><span data-stu-id="ebd73-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="ebd73-314">Voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="ebd73-314">To read more:</span></span>

* [<span data-ttu-id="ebd73-315">Hadoop-zelfstudie: aan de slag met Hadoop op basis van Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebd73-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="ebd73-316">Hadoop op basis van Linux-clusters maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebd73-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="ebd73-317">HDInsight-documentatie</span><span class="sxs-lookup"><span data-stu-id="ebd73-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="ebd73-318">Data factory-documentatie</span><span class="sxs-lookup"><span data-stu-id="ebd73-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="ebd73-319">Bijlage</span><span class="sxs-lookup"><span data-stu-id="ebd73-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="ebd73-320">Azure CLI-script</span><span class="sxs-lookup"><span data-stu-id="ebd73-320">Azure CLI script</span></span>
<span data-ttu-id="ebd73-321">U kunt Azure CLI gebruiken in plaats van de zelfstudie wilt met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebd73-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="ebd73-322">Voor het gebruik van Azure CLI, moet u eerst Azure CLI installeren volgens de volgende instructies:</span><span class="sxs-lookup"><span data-stu-id="ebd73-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="ebd73-323">Azure CLI gebruiken voor het voorbereiden van de opslag en kopieer de bestanden</span><span class="sxs-lookup"><span data-stu-id="ebd73-323">Use Azure CLI to prepare the storage and copy the files</span></span>

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

<span data-ttu-id="ebd73-324">De containernaam van de is *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="ebd73-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="ebd73-325">Houd het omdat deze.</span><span class="sxs-lookup"><span data-stu-id="ebd73-325">Keep it as it is.</span></span> <span data-ttu-id="ebd73-326">Anders moet u de sjabloon van de Resource Manager bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ebd73-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="ebd73-327">Als u hulp nodig bij dit script CLI, Zie [met de Azure CLI met Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebd73-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
