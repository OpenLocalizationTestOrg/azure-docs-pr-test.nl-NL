---
title: aaaBuild uw eerste gegevensfactory (REST) | Microsoft Docs
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
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="099a9-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met de Data Factory-REST API</span><span class="sxs-lookup"><span data-stu-id="099a9-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="099a9-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="099a9-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="099a9-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="099a9-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="099a9-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="099a9-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="099a9-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="099a9-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="099a9-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="099a9-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="099a9-109">REST API</span><span class="sxs-lookup"><span data-stu-id="099a9-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="099a9-110">In dit artikel gebruikt u REST API van Data Factory toocreate uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="099a9-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="099a9-111">toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="099a9-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="099a9-112">Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="099a9-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="099a9-113">Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer.</span><span class="sxs-lookup"><span data-stu-id="099a9-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="099a9-114">Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="099a9-115">In dit artikel omvat niet alle Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="099a9-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="099a9-116">Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over REST API.</span><span class="sxs-lookup"><span data-stu-id="099a9-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="099a9-117">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="099a9-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="099a9-118">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="099a9-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="099a9-119">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="099a9-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="099a9-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="099a9-120">Prerequisites</span></span>
* <span data-ttu-id="099a9-121">Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="099a9-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="099a9-122">Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="099a9-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="099a9-123">U gebruikt Hallo CURL hulpprogramma met REST opdrachten toocreate een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="099a9-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="099a9-124">Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="099a9-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="099a9-125">Maak een webtoepassing met de naam **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="099a9-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="099a9-126">Haal de **client-id** en **geheime sleutel** op.</span><span class="sxs-lookup"><span data-stu-id="099a9-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="099a9-127">Haal de **tenant-id** op.</span><span class="sxs-lookup"><span data-stu-id="099a9-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="099a9-128">Hallo toewijzen **ADFGetStartedApp** toepassing toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="099a9-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="099a9-129">Installeer [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="099a9-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="099a9-130">Start **PowerShell** en Voer Hallo de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="099a9-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="099a9-131">Houd Azure PowerShell open tot Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="099a9-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="099a9-132">Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="099a9-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="099a9-133">Voer **Login-AzureRmAccount** en geef Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="099a9-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="099a9-134">Voer **Get-AzureRmSubscription** tooview alle abonnementen voor dit account Hallo.</span><span class="sxs-lookup"><span data-stu-id="099a9-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="099a9-135">Voer **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect Hallo abonnement dat u wilt dat toowork met.</span><span class="sxs-lookup"><span data-stu-id="099a9-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="099a9-136">Vervang **NameOfAzureSubscription** met Hallo-naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="099a9-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="099a9-137">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="099a9-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="099a9-138">Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="099a9-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="099a9-139">Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="099a9-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="099a9-140">JSON-definities maken</span><span class="sxs-lookup"><span data-stu-id="099a9-140">Create JSON definitions</span></span>
<span data-ttu-id="099a9-141">Maken de volgende JSON-bestanden in Hallo map waar curl.exe zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="099a9-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="099a9-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="099a9-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="099a9-143">Naam moet globaal uniek zijn, zodat u tooprefix-/ achtervoegseltekenreeks ADFCopyTutorialDF toomake kunt deze een unieke naam op.</span><span class="sxs-lookup"><span data-stu-id="099a9-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="099a9-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="099a9-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="099a9-145">Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="099a9-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="099a9-146">toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="099a9-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="099a9-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="099a9-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="099a9-148">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="099a9-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="099a9-149">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="099a9-149">Property</span></span> | <span data-ttu-id="099a9-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="099a9-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="099a9-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="099a9-151">ClusterSize</span></span> |<span data-ttu-id="099a9-152">De grootte van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="099a9-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="099a9-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="099a9-153">TimeToLive</span></span> |<span data-ttu-id="099a9-154">Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="099a9-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="099a9-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="099a9-155">linkedServiceName</span></span> |<span data-ttu-id="099a9-156">Hiermee geeft u op Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="099a9-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="099a9-157">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="099a9-157">Note hello following points:</span></span>

* <span data-ttu-id="099a9-158">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello hierboven JSON.</span><span class="sxs-lookup"><span data-stu-id="099a9-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="099a9-159">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="099a9-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="099a9-160">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="099a9-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="099a9-161">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="099a9-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="099a9-162">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="099a9-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="099a9-163">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="099a9-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="099a9-164">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="099a9-164">This behavior is by design.</span></span> <span data-ttu-id="099a9-165">Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment is verwerkt, tenzij er een bestaand livecluster (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="099a9-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="099a9-166">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="099a9-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="099a9-167">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="099a9-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="099a9-168">Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '.</span><span class="sxs-lookup"><span data-stu-id="099a9-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="099a9-169">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="099a9-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="099a9-170">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="099a9-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="099a9-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="099a9-171">inputdataset.json</span></span>

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

<span data-ttu-id="099a9-172">Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobInput**, die staat voor invoergegevens van een activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="099a9-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="099a9-173">Bovendien wordt hiermee aangegeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="099a9-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="099a9-174">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="099a9-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="099a9-175">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="099a9-175">Property</span></span> | <span data-ttu-id="099a9-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="099a9-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="099a9-177">type</span><span class="sxs-lookup"><span data-stu-id="099a9-177">type</span></span> |<span data-ttu-id="099a9-178">Hallo type eigenschap wordt ingesteld tooAzureBlob omdat de gegevens zich in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="099a9-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="099a9-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="099a9-179">linkedServiceName</span></span> |<span data-ttu-id="099a9-180">verwijst toohello StorageLinkedService die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="099a9-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="099a9-181">fileName</span><span class="sxs-lookup"><span data-stu-id="099a9-181">fileName</span></span> |<span data-ttu-id="099a9-182">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="099a9-182">This property is optional.</span></span> <span data-ttu-id="099a9-183">Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="099a9-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="099a9-184">In dit geval wordt alleen Hallo input.log verwerkt.</span><span class="sxs-lookup"><span data-stu-id="099a9-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="099a9-185">type</span><span class="sxs-lookup"><span data-stu-id="099a9-185">type</span></span> |<span data-ttu-id="099a9-186">Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="099a9-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="099a9-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="099a9-187">columnDelimiter</span></span> |<span data-ttu-id="099a9-188">kolommen in Hallo logboekbestanden worden gescheiden door een kommateken ()</span><span class="sxs-lookup"><span data-stu-id="099a9-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="099a9-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="099a9-189">frequency/interval</span></span> |<span data-ttu-id="099a9-190">frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="099a9-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="099a9-191">external</span><span class="sxs-lookup"><span data-stu-id="099a9-191">external</span></span> |<span data-ttu-id="099a9-192">Deze eigenschap wordt tootrue ingesteld als Hallo invoergegevens niet worden gegenereerd door Hallo Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="099a9-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="099a9-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="099a9-193">outputdataset.json</span></span>

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

<span data-ttu-id="099a9-194">Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobOutput**, die uitvoergegevens voor een activiteit in de pijplijn Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="099a9-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="099a9-195">Bovendien wordt hiermee aangegeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="099a9-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="099a9-196">Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="099a9-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="099a9-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="099a9-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="099a9-198">Vervang **storageaccountname** door de naam van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="099a9-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="099a9-199">In de JSON-codefragment hello maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor Hive tooprocess gegevens op een HDInsight-cluster worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="099a9-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="099a9-200">Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **StorageLinkedService**), en in **script**  map in container Hallo **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="099a9-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="099a9-201">Hallo **definieert** sectie geeft een runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="099a9-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="099a9-202">Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="099a9-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="099a9-203">In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="099a9-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="099a9-204">Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in het voorgaande voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="099a9-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="099a9-205">Globale variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="099a9-205">Set global variables</span></span>
<span data-ttu-id="099a9-206">Uitvoeren in Azure PowerShell Hallo opdrachten na waarbij Hallo waarden vervangt door uw eigen te volgen:</span><span class="sxs-lookup"><span data-stu-id="099a9-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="099a9-207">Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="099a9-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="099a9-208">Verifiëren met AAD</span><span class="sxs-lookup"><span data-stu-id="099a9-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="099a9-209">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="099a9-209">Create data factory</span></span>
<span data-ttu-id="099a9-210">In deze stap maakt u een Azure-gegevensfactory met de naam **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="099a9-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="099a9-211">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="099a9-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="099a9-212">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="099a9-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="099a9-213">Bijvoorbeeld een Kopieeractiviteit toocopy gegevens uit een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens.</span><span class="sxs-lookup"><span data-stu-id="099a9-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="099a9-214">Voer Hallo opdrachten toocreate hello gegevensfactory te volgen:</span><span class="sxs-lookup"><span data-stu-id="099a9-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="099a9-215">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="099a9-216">Bevestig dat Hallo de naam van gegevensfactory Hallo u hier opgeeft (ADFCopyTutorialDF) komt overeen met de naam opgegeven in Hallo Hallo **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="099a9-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-217">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-218">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-218">View hello results.</span></span> <span data-ttu-id="099a9-219">Als Hallo gegevensfactory is gemaakt, ziet u Hallo JSON voor Hallo data factory in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="099a9-220">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="099a9-220">Note hello following points:</span></span>

* <span data-ttu-id="099a9-221">Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="099a9-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="099a9-222">Als er een fout in resultaten Hallo: **Data factory-naam 'FirstDataFactoryREST' is niet beschikbaar**, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="099a9-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="099a9-223">Hallo naam wijzigen (bijvoorbeeld yournameFirstDataFactoryREST) in Hallo **datafactory.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="099a9-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="099a9-224">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="099a9-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="099a9-225">In de eerste opdracht Hallo waar Hallo **$cmd** variabele een waarde is toegewezen, FirstDataFactoryREST vervangen door de nieuwe naam Hallo en het Hallo-opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="099a9-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="099a9-226">Hallo volgende twee opdrachten tooinvoke Hallo REST-API toocreate Hallo data factory en printers Hallo resultaten van Hallo bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="099a9-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="099a9-227">toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe</span><span class="sxs-lookup"><span data-stu-id="099a9-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="099a9-228">Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarom ook openbaar zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="099a9-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="099a9-229">Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="099a9-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="099a9-230">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:</span><span class="sxs-lookup"><span data-stu-id="099a9-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="099a9-231">Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="099a9-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="099a9-232">Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="099a9-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="099a9-233">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="099a9-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="099a9-234">Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst.</span><span class="sxs-lookup"><span data-stu-id="099a9-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="099a9-235">U maakt eerst gekoppelde services toolink gegevens opslaan, definieert u welke invoer en uitvoer gegevenssets toorepresent gegevens in de gekoppelde gegevensopslag/berekeningen tooyour gegevens.</span><span class="sxs-lookup"><span data-stu-id="099a9-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="099a9-236">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="099a9-236">Create linked services</span></span>
<span data-ttu-id="099a9-237">In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="099a9-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="099a9-238">Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="099a9-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="099a9-239">Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="099a9-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="099a9-240">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="099a9-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="099a9-241">In deze stap koppelt u uw Azure Storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="099a9-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="099a9-242">Met deze zelfstudie gebruikt u Hallo dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.</span><span class="sxs-lookup"><span data-stu-id="099a9-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="099a9-243">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-244">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-245">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-245">View hello results.</span></span> <span data-ttu-id="099a9-246">Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="099a9-247">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="099a9-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="099a9-248">In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="099a9-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="099a9-249">Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="099a9-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="099a9-250">U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="099a9-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="099a9-251">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="099a9-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="099a9-252">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-253">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-254">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-254">View hello results.</span></span> <span data-ttu-id="099a9-255">Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="099a9-256">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="099a9-256">Create datasets</span></span>
<span data-ttu-id="099a9-257">In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking.</span><span class="sxs-lookup"><span data-stu-id="099a9-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="099a9-258">Deze gegevenssets verwijzen toohello **StorageLinkedService** u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="099a9-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="099a9-259">Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="099a9-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="099a9-260">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="099a9-260">Create input dataset</span></span>
<span data-ttu-id="099a9-261">In deze stap maakt u Hallo invoergegevensset toorepresent invoergegevens opgeslagen in hello Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="099a9-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="099a9-262">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-263">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-264">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-264">View hello results.</span></span> <span data-ttu-id="099a9-265">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="099a9-266">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="099a9-266">Create output dataset</span></span>
<span data-ttu-id="099a9-267">In deze stap maakt u Hallo gegevensset toorepresent uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="099a9-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="099a9-268">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-269">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-270">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-270">View hello results.</span></span> <span data-ttu-id="099a9-271">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="099a9-272">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="099a9-272">Create pipeline</span></span>
<span data-ttu-id="099a9-273">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="099a9-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="099a9-274">Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="099a9-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="099a9-275">Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="099a9-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="099a9-276">Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="099a9-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="099a9-277">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="099a9-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="099a9-278">Controleer of u Hallo **input.log** bestand in Hallo **adfgetstarted/inputdata** map in hello Azure blob-opslag- en Voer Hallo opdracht toodeploy Hallo pijplijn te volgen.</span><span class="sxs-lookup"><span data-stu-id="099a9-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="099a9-279">Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="099a9-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="099a9-280">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="099a9-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="099a9-281">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="099a9-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="099a9-282">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-282">View hello results.</span></span> <span data-ttu-id="099a9-283">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="099a9-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="099a9-284">U hebt uw eerste pijplijn gemaakt met Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="099a9-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="099a9-285">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="099a9-285">Monitor pipeline</span></span>
<span data-ttu-id="099a9-286">In deze stap gebruikt u REST API van Data Factory toomonitor segmenten wordt geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="099a9-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

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
> <span data-ttu-id="099a9-287">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="099a9-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="099a9-288">Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="099a9-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="099a9-289">Hallo Invoke-Command en uitgevoerd Hallo volgende totdat er Hallo segment **gereed** status of **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="099a9-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="099a9-290">Als Hallo segment status gereed is, Controleer Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="099a9-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="099a9-291">Hallo maken van een HDInsight-cluster op aanvraag duurt normaal gesproken enige tijd.</span><span class="sxs-lookup"><span data-stu-id="099a9-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="099a9-293">Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="099a9-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="099a9-294">Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.</span><span class="sxs-lookup"><span data-stu-id="099a9-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="099a9-295">U kunt ook gebruik van Azure portal toomonitor segmenten en los eventuele problemen.</span><span class="sxs-lookup"><span data-stu-id="099a9-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="099a9-296">Zie voor meer informatie [Pijplijnen bewaken met de Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="099a9-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="099a9-297">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="099a9-297">Summary</span></span>
<span data-ttu-id="099a9-298">In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="099a9-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="099a9-299">U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="099a9-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="099a9-300">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="099a9-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="099a9-301">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="099a9-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="099a9-302">**Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="099a9-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="099a9-303">**Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="099a9-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="099a9-304">Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.</span><span class="sxs-lookup"><span data-stu-id="099a9-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="099a9-305">Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="099a9-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="099a9-306">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="099a9-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="099a9-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="099a9-307">Next steps</span></span>
<span data-ttu-id="099a9-308">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="099a9-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="099a9-309">hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="099a9-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="099a9-310">Zie ook</span><span class="sxs-lookup"><span data-stu-id="099a9-310">See Also</span></span>
| <span data-ttu-id="099a9-311">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="099a9-311">Topic</span></span> | <span data-ttu-id="099a9-312">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="099a9-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="099a9-313">Naslaginformatie over de REST-API voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="099a9-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="099a9-314">Zie de uitgebreide documentatie over Data Factory-cmdlets</span><span class="sxs-lookup"><span data-stu-id="099a9-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="099a9-315">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="099a9-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="099a9-316">In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="099a9-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="099a9-317">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="099a9-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="099a9-318">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="099a9-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="099a9-319">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="099a9-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="099a9-320">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="099a9-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="099a9-321">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="099a9-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="099a9-322">Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="099a9-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
