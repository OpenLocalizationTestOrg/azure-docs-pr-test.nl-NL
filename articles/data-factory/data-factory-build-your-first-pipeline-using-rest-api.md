---
title: Uw eerste gegevensfactory bouwen (REST) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van de Data Factory-REST API.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: b0c237667f1f55298df20ab0f525202aa1b42e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="fc576-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met de Data Factory-REST API</span><span class="sxs-lookup"><span data-stu-id="fc576-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc576-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="fc576-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="fc576-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc576-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="fc576-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc576-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="fc576-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc576-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="fc576-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="fc576-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="fc576-109">REST API</span><span class="sxs-lookup"><span data-stu-id="fc576-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="fc576-110">In dit artikel gebruikt u de Data Factory-REST API voor het maken van uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="fc576-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="fc576-111">Als u de zelfstudie wilt volgen met andere hulpprogramma's/SDK's, selecteert u een van de opties uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="fc576-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="fc576-112">De pijplijn in deze zelfstudie heeft één activiteit: **HDInsight-componentactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="fc576-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="fc576-113">Deze activiteit voert een Hive-script uit op een Azure HDInsight-cluster dat invoergegevens transformeert om uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="fc576-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="fc576-114">De pijplijn is gepland on één keer per maand tussen de opgegeven begin- en eindtijd te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc576-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="fc576-115">Dit artikel omvat niet alles over de REST API.</span><span class="sxs-lookup"><span data-stu-id="fc576-115">This article does not cover all the REST API.</span></span> <span data-ttu-id="fc576-116">Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over REST API.</span><span class="sxs-lookup"><span data-stu-id="fc576-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="fc576-117">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="fc576-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fc576-118">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="fc576-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="fc576-119">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc576-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fc576-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fc576-120">Prerequisites</span></span>
* <span data-ttu-id="fc576-121">Lees het artikel [Overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="fc576-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="fc576-122">Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fc576-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="fc576-123">U kunt in het hulpprogramma CURL REST-opdrachten gebruiken om een gegevensfactory te maken.</span><span class="sxs-lookup"><span data-stu-id="fc576-123">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="fc576-124">Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="fc576-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="fc576-125">Maak een webtoepassing met de naam **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc576-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="fc576-126">Haal de **client-id** en **geheime sleutel** op.</span><span class="sxs-lookup"><span data-stu-id="fc576-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="fc576-127">Haal de **tenant-id** op.</span><span class="sxs-lookup"><span data-stu-id="fc576-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="fc576-128">Wijs de **ADFGetStartedApp**-toepassing toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="fc576-128">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="fc576-129">Installeer [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc576-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fc576-130">Start **PowerShell** en voer de volgende opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="fc576-130">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="fc576-131">Houd Azure PowerShell open tot het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="fc576-131">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="fc576-132">Als u het programma sluit en opnieuw opent, moet u de opdrachten opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fc576-132">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="fc576-133">Voer **Login-AzureRmAccount** uit en geef de gebruikersnaam en het wachtwoord op die u gebruikt om u aan te melden bij de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fc576-133">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="fc576-134">Voer **Get-AzureRmSubscription** uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="fc576-134">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="fc576-135">Voer **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set AzureRmContext** uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="fc576-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="fc576-136">Vervang **NameOfAzureSubscription** door de naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fc576-136">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="fc576-137">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door de volgende opdracht uit te voeren in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fc576-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="fc576-138">Voor sommige van de stappen in deze zelfstudie wordt ervan uitgegaan dat u de resourcegroep met de naam ADFTutorialResourceGroup gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fc576-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="fc576-139">Als u een andere resourcegroep gebruikt, moet u voor deze zelfstudie de naam van uw resourcegroep gebruiken in plaats van ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="fc576-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="fc576-140">JSON-definities maken</span><span class="sxs-lookup"><span data-stu-id="fc576-140">Create JSON definitions</span></span>
<span data-ttu-id="fc576-141">Maak de volgende JSON-bestanden in de map waar curl.exe staat.</span><span class="sxs-lookup"><span data-stu-id="fc576-141">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="fc576-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="fc576-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc576-143">Naam moet uniek zijn, dus het is raadzaam om voor- en/of achtervoegsels te gebruiken bij ADFCopyTutorialDF, zodat het een unieke naam wordt.</span><span class="sxs-lookup"><span data-stu-id="fc576-143">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="fc576-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fc576-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc576-145">Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="fc576-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="fc576-146">Raadpleeg de informatie over het weergeven, kopiëren en opnieuw genereren van toegangssleutels voor opslag in [Uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account) als u meer wilt weten over het verkrijgen van een toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="fc576-146">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="fc576-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fc576-147">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="fc576-148">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fc576-148">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="fc576-149">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="fc576-149">Property</span></span> | <span data-ttu-id="fc576-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fc576-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fc576-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="fc576-151">ClusterSize</span></span> |<span data-ttu-id="fc576-152">Grootte van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc576-152">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="fc576-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="fc576-153">TimeToLive</span></span> |<span data-ttu-id="fc576-154">Geeft aan hoelang het HDInsight-cluster inactief moet zijn voordat het wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fc576-154">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="fc576-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fc576-155">linkedServiceName</span></span> |<span data-ttu-id="fc576-156">Geeft het opslagaccount aan dat wordt gebruikt voor het opslaan van de logboeken die door HDInsight worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="fc576-156">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="fc576-157">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="fc576-157">Note the following points:</span></span>

* <span data-ttu-id="fc576-158">Met de bovenstaande JSON maakt Data Factory voor u een HDInsight-cluster **op basis van Linux**.</span><span class="sxs-lookup"><span data-stu-id="fc576-158">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="fc576-159">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc576-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="fc576-160">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc576-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fc576-161">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc576-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="fc576-162">Het HDInsight-cluster maakt een **standaardcontainer** in de blobopslag die u hebt opgegeven in de JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="fc576-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="fc576-163">HDInsight verwijdert deze container niet wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fc576-163">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="fc576-164">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="fc576-164">This behavior is by design.</span></span> <span data-ttu-id="fc576-165">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**). Het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fc576-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="fc576-166">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="fc576-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="fc576-167">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="fc576-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="fc576-168">De namen van deze containers worden als volgt opgebouwd: adf**naamvanuwgegevensfactory**-**naamvangekoppeldeservice**-datum-/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="fc576-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="fc576-169">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om containers in uw Azure-blobopslag te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fc576-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="fc576-170">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc576-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="fc576-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fc576-171">inputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

<span data-ttu-id="fc576-172">Met de JSON wordt een gegevensset gedefinieerd met de naam **AzureBlobInput**. Deze bevat de invoergegevens voor een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="fc576-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="fc576-173">Bovendien wordt hiermee aangegeven dat de invoergegevens zich bevinden in de blobcontainer met de naam **adfgetstarted** en in de map met de naam **inputdata**</span><span class="sxs-lookup"><span data-stu-id="fc576-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="fc576-174">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fc576-174">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="fc576-175">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="fc576-175">Property</span></span> | <span data-ttu-id="fc576-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fc576-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fc576-177">type</span><span class="sxs-lookup"><span data-stu-id="fc576-177">type</span></span> |<span data-ttu-id="fc576-178">De eigenschap type wordt ingesteld op AzureBlob, omdat de gegevens zich in de Azure-blobopslag bevinden.</span><span class="sxs-lookup"><span data-stu-id="fc576-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="fc576-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fc576-179">linkedServiceName</span></span> |<span data-ttu-id="fc576-180">Deze eigenschap verwijst naar de StorageLinkedService die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fc576-180">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="fc576-181">fileName</span><span class="sxs-lookup"><span data-stu-id="fc576-181">fileName</span></span> |<span data-ttu-id="fc576-182">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="fc576-182">This property is optional.</span></span> <span data-ttu-id="fc576-183">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath gekozen.</span><span class="sxs-lookup"><span data-stu-id="fc576-183">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="fc576-184">In dit geval wordt alleen input.log verwerkt.</span><span class="sxs-lookup"><span data-stu-id="fc576-184">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="fc576-185">type</span><span class="sxs-lookup"><span data-stu-id="fc576-185">type</span></span> |<span data-ttu-id="fc576-186">Omdat de logboekbestanden tekstbestanden zijn, gebruiken we TextFormat.</span><span class="sxs-lookup"><span data-stu-id="fc576-186">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="fc576-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fc576-187">columnDelimiter</span></span> |<span data-ttu-id="fc576-188">Kolommen in de logboekbestanden worden gescheiden door een komma (,)</span><span class="sxs-lookup"><span data-stu-id="fc576-188">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="fc576-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="fc576-189">frequency/interval</span></span> |<span data-ttu-id="fc576-190">Als frequency wordt ingesteld op Month en de interval 1 is, betekent dat dat de invoersegmenten één keer per maand beschikbaar worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fc576-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="fc576-191">external</span><span class="sxs-lookup"><span data-stu-id="fc576-191">external</span></span> |<span data-ttu-id="fc576-192">Deze eigenschap wordt ingesteld op true als de invoergegevens niet worden gegenereerd door de Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="fc576-192">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="fc576-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fc576-193">outputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="fc576-194">Met de JSON wordt een gegevensset gedefinieerd met de naam **AzureBlobOutput**. Deze bevat de uitvoergegevens voor een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="fc576-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="fc576-195">Bovendien wordt hiermee aangegeven dat de resultaten worden opgeslagen in de blobcontainer met de naam **adfgetstarted** en in de map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="fc576-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="fc576-196">In het gedeelte **availability** wordt opgegeven dat de uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="fc576-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="fc576-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="fc576-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc576-198">Vervang **storageaccountname** door de naam van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="fc576-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="fc576-199">In het JSON-fragment maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik wordt gemaakt van Hive om gegevens in een HDInsight-cluster te verwerken.</span><span class="sxs-lookup"><span data-stu-id="fc576-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="fc576-200">Het Hive-scriptbestand **partitionweblogs.hql** wordt opgeslagen in het Azure-opslagaccount (opgegeven door de scriptLinkedService met de naam **StorageLinkedService**) en in de map **script** van de container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="fc576-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="fc576-201">In het gedeelte **defines** worden de runtime-instellingen aangegeven die als Hive-configuratiewaarden worden doorgegeven aan het Hive-script (bijvoorbeeld ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="fc576-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="fc576-202">Met de eigenschappen **start** en **end** van de pijplijn wordt opgegeven in welke periode de pijplijn actief is.</span><span class="sxs-lookup"><span data-stu-id="fc576-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="fc576-203">In de activiteits-JSON geeft u op dat het Hive-script wordt uitgevoerd in de berekening die is opgegeven door de **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fc576-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="fc576-204">Zie 'Pijplijn JSON' in [Pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in het voorgaande voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fc576-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="fc576-205">Globale variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="fc576-205">Set global variables</span></span>
<span data-ttu-id="fc576-206">Voer in Azure PowerShell de volgende opdrachten uit nadat u de waarden hebt vervangen door uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="fc576-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc576-207">Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="fc576-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="fc576-208">Verifiëren met AAD</span><span class="sxs-lookup"><span data-stu-id="fc576-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="fc576-209">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="fc576-209">Create data factory</span></span>
<span data-ttu-id="fc576-210">In deze stap maakt u een Azure-gegevensfactory met de naam **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="fc576-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="fc576-211">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="fc576-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fc576-212">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="fc576-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fc576-213">Bijvoorbeeld een kopieeractiviteit om gegevens van een bron- naar een doelgegevensopslagplaats te kopiëren en een HDInsight Hive-activiteit om een Hive-script uit te voeren voor het transformeren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="fc576-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span></span> <span data-ttu-id="fc576-214">Voer de volgende opdracht uit om de gegevensfactory te maken:</span><span class="sxs-lookup"><span data-stu-id="fc576-214">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="fc576-215">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-215">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="fc576-216">Bevestig dat de naam van de gegevensfactory die u hier opgeeft (ADFCopyTutorialDF) overeenkomt met de naam die is opgegeven in de **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="fc576-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-217">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-217">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-218">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-218">View the results.</span></span> <span data-ttu-id="fc576-219">Als de gegevensfactory is gemaakt, ziet u de JSON voor de gegevensfactory in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="fc576-220">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="fc576-220">Note the following points:</span></span>

* <span data-ttu-id="fc576-221">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="fc576-221">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="fc576-222">Als u de fout **Naam gegevensfactory FirstDataFactoryREST is niet beschikbaar** in de resultaten ziet, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc576-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="fc576-223">Wijzig de naam (bijvoorbeeld uwnaamFirstDataFactoryREST) in het bestand **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="fc576-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="fc576-224">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="fc576-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="fc576-225">In de eerste opdracht waar aan de **$cmd**-variabele een waarde is toegewezen, vervangt u FirstDataFactoryREST door de nieuwe naam en voert u de opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="fc576-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="fc576-226">Voer de volgende twee opdrachten uit voor het aanroepen van de REST API om de gegevensfactory te maken en de resultaten van de bewerking af te drukken.</span><span class="sxs-lookup"><span data-stu-id="fc576-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="fc576-227">Als u Data Factory-exemplaren wilt maken, moet u bijdrager/beheerder zijn van het Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="fc576-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="fc576-228">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als DNS-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="fc576-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="fc576-229">Als u de foutmelding **Dit abonnement is niet geregistreerd voor gebruik van de naamruimte Microsoft.DataFactory** ontvangt, voert u een van de volgende stappen uit en probeert u opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="fc576-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="fc576-230">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-provider te registreren:</span><span class="sxs-lookup"><span data-stu-id="fc576-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="fc576-231">U kunt de volgende opdracht uitvoeren om te bevestigen dat de Data Factory-provider is geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="fc576-231">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fc576-232">Meld u bij de [Azure Portal](https://portal.azure.com) aan met behulp van het Azure-abonnement en navigeer naar een Data Factory-blade of maak een gegevensfactory in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fc576-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="fc576-233">Door deze actie wordt de provider automatisch voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="fc576-233">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="fc576-234">Voordat u een pijplijn maakt, moet u eerst enkele Data Factory-entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="fc576-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="fc576-235">U maakt eerst gekoppelde services om gegevensopslag/berekeningen te koppelen aan uw gegevensopslag, vervolgens definieert u welke invoer- en uitvoergegevenssets de gegevens in de gekoppelde gegevensopslag vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="fc576-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fc576-236">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="fc576-236">Create linked services</span></span>
<span data-ttu-id="fc576-237">In deze stap koppelt u uw Azure Storage-account en een on-demand Azure HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="fc576-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="fc576-238">Het Azure Storage-account bevat de in- en uitvoergegevens van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fc576-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="fc576-239">De gekoppelde HDInsight-service wordt gebruikt om een Hive-script uit te voeren dat is opgegeven in de activiteit van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fc576-239">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="fc576-240">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="fc576-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="fc576-241">In deze stap koppelt u uw Azure Storage-account aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="fc576-241">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="fc576-242">Bij deze zelfstudie gebruikt u hetzelfde Azure Storage-account om invoer- en uitvoergegevens en het HQL-scriptbestand op te slaan.</span><span class="sxs-lookup"><span data-stu-id="fc576-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="fc576-243">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-243">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-244">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-244">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-245">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-245">View the results.</span></span> <span data-ttu-id="fc576-246">Als de gekoppelde service is gemaakt, ziet u de JSON voor de gekoppelde service in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="fc576-247">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="fc576-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="fc576-248">In deze stap koppelt u een on-demand HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="fc576-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="fc576-249">Het HDInsight-cluster wordt automatisch gemaakt tijdens runtime en wordt verwijderd wanneer het verwerken is voltooid en het cluster gedurende een opgegeven tijdsperiode niet actief is geweest.</span><span class="sxs-lookup"><span data-stu-id="fc576-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="fc576-250">U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc576-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fc576-251">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc576-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="fc576-252">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-252">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-253">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-253">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-254">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-254">View the results.</span></span> <span data-ttu-id="fc576-255">Als de gekoppelde service is gemaakt, ziet u de JSON voor de gekoppelde service in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="fc576-256">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="fc576-256">Create datasets</span></span>
<span data-ttu-id="fc576-257">In deze stap maakt u gegevenssets die de invoer- en uitvoergegevens voor Hive-verwerking vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="fc576-257">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="fc576-258">Deze gegevenssets verwijzen naar de **StorageLinkedService** die u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fc576-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="fc576-259">De gekoppelde service verwijst naar een Azure-opslagaccount en in de gegevenssets vindt u de container, map en bestandsnaam in de opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="fc576-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="fc576-260">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="fc576-260">Create input dataset</span></span>
<span data-ttu-id="fc576-261">In deze stap maakt u de invoergegevensset die staat voor invoergegevens die worden opgeslagen in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="fc576-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="fc576-262">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-262">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-263">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-263">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-264">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-264">View the results.</span></span> <span data-ttu-id="fc576-265">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="fc576-266">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="fc576-266">Create output dataset</span></span>
<span data-ttu-id="fc576-267">In deze stap maakt u de uitvoergegevensset die staat voor uitvoergegevens die worden opgeslagen in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="fc576-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="fc576-268">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-268">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-269">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-269">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-270">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-270">View the results.</span></span> <span data-ttu-id="fc576-271">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="fc576-272">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="fc576-272">Create pipeline</span></span>
<span data-ttu-id="fc576-273">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="fc576-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="fc576-274">Het invoersegment wordt elke maand beschikbaar gesteld (frequentie: Maand, interval: 1), evenals het uitvoersegment. Ook de plannereigenschap van de activiteit wordt op maandelijks ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fc576-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="fc576-275">De instellingen voor de uitvoergegevensset en de activiteitenplanner moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="fc576-275">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="fc576-276">Op dit moment wordt de planning gebaseerd op de uitvoergegevensset. Daarom moet u ook een uitvoergegevensset maken als er tijdens de activiteit geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="fc576-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="fc576-277">Als er voor de activiteit geen invoer nodig is, kunt u het maken van de invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="fc576-277">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="fc576-278">Controleer of u het bestand **input.log** ziet in de map **adfgetstarted/inputdata** in de Azure-blobopslag en voer de volgende opdracht uit om de pijplijn te implementeren.</span><span class="sxs-lookup"><span data-stu-id="fc576-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="fc576-279">Aangezien de tijden voor **start** en **end** in het verleden vallen en **isPaused** is ingesteld op false, wordt de pijplijn (activiteit in de pijplijn) direct na het implementeren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc576-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="fc576-280">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc576-280">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc576-281">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc576-281">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc576-282">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="fc576-282">View the results.</span></span> <span data-ttu-id="fc576-283">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc576-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="fc576-284">U hebt uw eerste pijplijn gemaakt met Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="fc576-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="fc576-285">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="fc576-285">Monitor pipeline</span></span>
<span data-ttu-id="fc576-286">In deze stap gebruikt u Data Factory-REST API voor het bewaken van segmenten die worden geproduceerd door de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="fc576-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="fc576-287">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="fc576-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="fc576-288">Daarom kunt u ervan uitgaan dat het **ongeveer 30 minuten** duurt voordat het segment in de pijplijn is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="fc576-288">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
>

<span data-ttu-id="fc576-289">Voer de Invoke-Command en de volgende uit totdat u het segment in de status **Gereed** of **Mislukt** ziet.</span><span class="sxs-lookup"><span data-stu-id="fc576-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="fc576-290">Wanneer het segment de status Gereed heeft, controleert u de map **partitioneddata** in de container **adfgetstarted** in uw blobopslag voor de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="fc576-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="fc576-291">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd.</span><span class="sxs-lookup"><span data-stu-id="fc576-291">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="fc576-293">Het invoerbestand wordt verwijderd zodra het segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="fc576-293">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="fc576-294">Als u het segment dus opnieuw wilt uitvoeren of als u de zelfstudie opnieuw wilt doorlopen, uploadt u het invoerbestand (input.log) naar de map met invoergegevens van de container adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="fc576-294">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

<span data-ttu-id="fc576-295">U kunt ook Azure Portal gebruiken voor het bewaken van segmenten en om eventuele problemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="fc576-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="fc576-296">Zie voor meer informatie [Pijplijnen bewaken met de Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fc576-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="fc576-297">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="fc576-297">Summary</span></span>
<span data-ttu-id="fc576-298">In deze zelfstudie hebt u een Azure-gegevensfactory gemaakt voor het verwerken van gegevens. Dit hebt u gedaan door Hive-script uit te voeren op een HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc576-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="fc576-299">U hebt in de Azure Portal de Data Factory-editor gebruikt om de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="fc576-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="fc576-300">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fc576-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fc576-301">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="fc576-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="fc576-302">Een gekoppelde **Azure Storage**-service om te koppelen aan de Azure-blobopslag die de invoer-/uitvoerbestanden van de gegevensfactory bevat.</span><span class="sxs-lookup"><span data-stu-id="fc576-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="fc576-303">Een gekoppelde on-demand **Azure HDInsight**-service om te koppelen aan een on-demand HDInsight Hadoop-cluster van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="fc576-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="fc576-304">Azure Data Factory maakt op tijd een HDInsight Hadoop-cluster om invoergegevens te verwerken en uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="fc576-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="fc576-305">U hebt twee **gegevenssets** gemaakt, waarin de invoer- en uitvoergegevens van de HDInsight Hive-activiteit in de pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fc576-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="fc576-306">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="fc576-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc576-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc576-307">Next steps</span></span>
<span data-ttu-id="fc576-308">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc576-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="fc576-309">Zie [Zelfstudie: gegevens van een Azure-blob kopiëren naar Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor meer informatie over het gebruiken van een kopieeractiviteit om gegevens van een Azure-blob te kopiëren naar Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fc576-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fc576-310">Zie ook</span><span class="sxs-lookup"><span data-stu-id="fc576-310">See Also</span></span>
| <span data-ttu-id="fc576-311">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="fc576-311">Topic</span></span> | <span data-ttu-id="fc576-312">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fc576-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="fc576-313">Naslaginformatie over de REST-API voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc576-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="fc576-314">Zie de uitgebreide documentatie over Data Factory-cmdlets</span><span class="sxs-lookup"><span data-stu-id="fc576-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="fc576-315">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="fc576-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="fc576-316">Met behulp van dit artikel krijgt u inzicht in de pijplijnen en activiteiten in Azure Data Factory en in de wijze waarop u deze kunt gebruiken om end-to-end gegevensgestuurde werkstromen te maken voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="fc576-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="fc576-317">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="fc576-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="fc576-318">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fc576-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="fc576-319">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fc576-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="fc576-320">In dit artikel wordt uitleg gegeven over de plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="fc576-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="fc576-321">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="fc576-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="fc576-322">In dit artikel wordt beschreven hoe u pijplijnen bewaakt en beheert en hoe u fouten hierin oplost met de app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="fc576-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
