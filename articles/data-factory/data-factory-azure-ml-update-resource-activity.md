---
title: Machine Learning-modellen aaaUpdate met behulp van Azure Data Factory | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate voorspellende pijplijnen met behulp van Azure Data Factory en Azure Machine Learning maken
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="3a9d6-103">Azure Machine Learning-modellen Update Resource activiteit bijwerken</span><span class="sxs-lookup"><span data-stu-id="3a9d6-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="3a9d6-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="3a9d6-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="3a9d6-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="3a9d6-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="3a9d6-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="3a9d6-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="3a9d6-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="3a9d6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="3a9d6-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="3a9d6-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="3a9d6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="3a9d6-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="3a9d6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="3a9d6-114">In dit artikel aanvullingen Hallo belangrijkste Azure Data Factory - artikel voor Azure Machine Learning-integratie: [voorspellende pijplijnen met behulp van Azure Machine Learning en Azure Data Factory maken](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="3a9d6-115">Als u dit nog niet hebt gedaan, raadpleegt u de belangrijkste artikel Hallo voordat gelezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="3a9d6-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3a9d6-116">Overview</span></span>
<span data-ttu-id="3a9d6-117">Na verloop van tijd moeten Hallo voorspellende modellen in hello Azure ML scoreprofiel experimenten toobe retrained met nieuwe invoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="3a9d6-118">Wanneer u klaar bent met de retraining, wilt u tooupdate Hallo score berekenen voor webservice Hello retrained ML-model.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="3a9d6-119">Hallo gebruikelijke stappen tooenable retraining en bijwerken van Azure ML-modellen via webservices zijn:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="3a9d6-120">Maken van een experiment in [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="3a9d6-121">Wanneer u tevreden met Hallo model bent, Azure ML Studio toopublish webservices gebruiken voor beide Hallo **trainingsexperiment** en score berekenen /**Voorspellend experiment**.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="3a9d6-122">Hallo beschrijft volgende tabel Hallo-webservices in dit voorbeeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="3a9d6-123">Zie [Retrain Machine Learning-modellen programmatisch](../machine-learning/machine-learning-retrain-models-programmatically.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="3a9d6-124">**Training webservice** - trainingsgegevens ontvangt en getraind modellen produceert.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="3a9d6-125">Hallo-uitvoer van Hallo retraining is een .ilearner-bestand in een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="3a9d6-126">Hallo **standaard eindpunt** wordt automatisch gemaakt voor u wanneer u Hallo training publiceert als een webservice experimenteren.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="3a9d6-127">U kunt meer eindpunten maken maar Hallo voorbeeld wordt alleen het standaardeindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="3a9d6-128">**Score berekenen voor webservice** - voorbeelden zonder label gegevens ontvangt en voorspellingen maakt.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="3a9d6-129">Hallo-uitvoer van de voorspelling kan verschillende vormen, zoals een CSV-bestand of rijen in een Azure SQL database, afhankelijk van de configuratie Hallo van Hallo experiment hebben.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="3a9d6-130">Hallo standaardeindpunt wordt automatisch voor u gemaakt wanneer u een Voorspellend experiment Hallo als een webservice publiceert.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="3a9d6-131">Hallo ziet volgende afbeelding u Hallo relatie tussen de trainings- en eindpunten in de Azure ML score.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![Webservices](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="3a9d6-133">Hallo kunnen worden aangeroepen **training webservice** met behulp van Hallo **Azure ML-Batchuitvoeringsactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="3a9d6-134">Aanroepen van een webservice training is hetzelfde als het aanroepen van een Azure ML webservice (score berekenen voor web-service) voor scoreprofiel gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="3a9d6-135">Hallo voorgaande secties behandeld hoe tooinvoke een webservice Azure ML uit een Azure Data Factory pijplijn in detail.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="3a9d6-136">Hallo kunnen worden aangeroepen **score berekenen voor webservice** met behulp van Hallo **Resourceactiviteit voor Azure ML Update** tooupdate Hallo-webservice met Hallo zojuist getrainde model.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="3a9d6-137">Hallo volgen voorbeelden bevatten definities van de gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="3a9d6-138">Score berekenen voor web-service is een klassieke webservice</span><span class="sxs-lookup"><span data-stu-id="3a9d6-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="3a9d6-139">Als Hallo score berekenen voor web-service is een **klassieke webservice**, Hallo tweede maken **niet-standaard en bij te werken eindpunt** met behulp van Hallo [Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="3a9d6-140">Zie [eindpunten maken](../machine-learning/machine-learning-create-endpoint.md) artikel voor stappen.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="3a9d6-141">Nadat u Hallo niet standaard worden bijgewerkt eindpunt hebt gemaakt, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="3a9d6-142">Klik op **BATCHUITVOERING** tooget Hallo URI-waarde voor Hallo **mlEndpoint** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="3a9d6-143">Klik op **UPDATE RESOURCE** tooget Hallo URI-waarde voor Hallo koppelen **updateResourceEndpoint** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="3a9d6-144">Hallo-API-sleutel is op Hallo eindpunt pagina zelf (in de rechterbenedenhoek Hallo).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![eindpunt bij te werken](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="3a9d6-146">Hallo volgende voorbeeld bevat een voorbeeld JSON-definitie voor Hallo voor met AzureML gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="3a9d6-147">Hallo gekoppelde service gebruikt Hallo apiKey voor authenticatie.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-147">hello linked service uses hello apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="3a9d6-148">Score berekenen voor web-service is Azure Resource Manager-webservice</span><span class="sxs-lookup"><span data-stu-id="3a9d6-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="3a9d6-149">Als webservice Hallo Hallo nieuw type webservice die een Azure Resource Manager-eindpunt wordt is, hoeft u niet tooadd Hallo tweede **niet-standaard** eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="3a9d6-150">Hallo **updateResourceEndpoint** in Hallo gekoppelde service van Hallo-indeling is:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="3a9d6-151">U kunt waarden voor de houders plaats in Hallo-URL krijgen bij het opvragen van de webservice Hallo op Hallo [Azure Machine Learning Web Services-Portal](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="3a9d6-152">Hallo nieuwe type update resource eindpunt vereist een token van AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="3a9d6-153">Geef **servicePrincipalId** en **servicePrincipalKey**in voor met AzureML gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="3a9d6-154">Zie [hoe toocreate service-principal en machtigingen toomanage Azure-resource toewijzen](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="3a9d6-155">Hier volgt een voorbeeld van een definitie van AzureML gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="3a9d6-156">Hallo biedt volgende scenario meer details.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-156">hello following scenario provides more details.</span></span> <span data-ttu-id="3a9d6-157">Er is een voorbeeld voor retraining en bijwerken van Azure ML-modellen van een Azure Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="3a9d6-158">Scenario: retraining en bijwerken van een Azure ML-model</span><span class="sxs-lookup"><span data-stu-id="3a9d6-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="3a9d6-159">Deze sectie vindt u een voorbeeldpijplijn die gebruikmaakt van Hallo **Azure ML-Batchuitvoering activiteit** tooretrain een model.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="3a9d6-160">Hallo pijplijn gebruikt ook Hallo **resourceactiviteit voor Azure ML Update** tooupdate Hallo-model in Hallo score berekenen voor web-service.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="3a9d6-161">Hallo bevat ook aan JSON codefragmenten voor alle gekoppelde services, gegevenssets en pijplijn in voorbeeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="3a9d6-162">Hier volgt de diagramweergave Hallo van Hallo-voorbeeldpijplijn.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="3a9d6-163">Zoals u ziet, hello Azure ML-Batchuitvoeringsactiviteit Hallo training invoer- en wordt de uitvoer van een training (iLearner-bestand).</span><span class="sxs-lookup"><span data-stu-id="3a9d6-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="3a9d6-164">Hallo Resourceactiviteit voor Azure ML-Update wordt de uitvoer van deze training en updates Hallo Hallo webservice-eindpunt score-model.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="3a9d6-165">Hallo Update Resourceactiviteit produceert geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="3a9d6-166">Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![Pipeline-diagram](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="3a9d6-168">Azure Blob-opslag gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="3a9d6-169">Hello Azure Storage bevat Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="3a9d6-170">trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-170">training data.</span></span> <span data-ttu-id="3a9d6-171">Hallo invoergegevens voor hello Azure ML training-webservice.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="3a9d6-172">iLearner-bestand.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-172">iLearner file.</span></span> <span data-ttu-id="3a9d6-173">Hallo de uitvoer van hello Azure ML training-webservice.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="3a9d6-174">Dit bestand is ook Hallo invoer toohello resourceactiviteit voor Update.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="3a9d6-175">Hier volgt Hallo voorbeeld JSON-definitie van Hallo gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-175">Here is hello sample JSON definition of hello linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="3a9d6-176">Training invoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-176">Training input dataset:</span></span>
<span data-ttu-id="3a9d6-177">Hallo vertegenwoordigt volgende gegevensset Hallo invoer trainingsgegevens voor hello Azure ML training-webservice.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="3a9d6-178">Deze gegevensset neemt Hello Azure ML-Batchuitvoering activiteit als invoer.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a><span data-ttu-id="3a9d6-179">Uitvoergegevensset voor training:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-179">Training output dataset:</span></span>
<span data-ttu-id="3a9d6-180">Hallo vertegenwoordigt volgende gegevensset Hallo uitvoer iLearner-bestand van hello Azure ML training-webservice.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="3a9d6-181">Hello Azure ML-Batchuitvoeringsactiviteit produceert deze dataset.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="3a9d6-182">Deze gegevensset is ook Hallo invoer toohello resourceactiviteit voor Azure ML-Update.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="3a9d6-183">Gekoppelde service voor Azure ML training eindpunt</span><span class="sxs-lookup"><span data-stu-id="3a9d6-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="3a9d6-184">Hallo volgende JSON-codefragment definieert een Azure Machine Learning gekoppelde service die toohello standaardeindpunt van Hallo training webservice verwijst.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="3a9d6-185">In **Azure ML Studio**, Hallo volgende tooget waarden voor **mlEndpoint** en **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="3a9d6-186">Klik op **WEBSERVICES** op Hallo linkermenu.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="3a9d6-187">Klik op Hallo **training webservice** in de lijst Hallo van webservices.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="3a9d6-188">Klik op kopiëren naast te**API-sleutel** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="3a9d6-189">Hallo-sleutel op Hallo Klembord in Hallo Data Factory JSON-editor plakken.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="3a9d6-190">In Hallo **Azure ML studio**, klikt u op **BATCHUITVOERING** koppeling.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="3a9d6-191">Kopiëren Hallo **aanvraag-URI** van Hallo **aanvragen** sectie en plak deze in Hallo Data Factory JSON-editor.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="3a9d6-192">Gekoppelde Service voor Azure ML bijwerkbare score-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="3a9d6-193">Hallo volgende JSON-codefragment definieert een Azure Machine Learning gekoppelde service die toohello niet standaard worden bijgewerkt eindpunt Hallo score berekenen voor webservice verwijst.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="3a9d6-194">Tijdelijke aanduiding voor uitvoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="3a9d6-194">Placeholder output dataset:</span></span>
<span data-ttu-id="3a9d6-195">Hallo resourceactiviteit voor Azure ML-Update wordt geen uitvoer gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="3a9d6-196">Azure Data Factory vereist echter een output dataset toodrive Hallo planning van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="3a9d6-197">Daarom gebruiken we een dummy/tijdelijke aanduiding voor gegevensset in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="3a9d6-198">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="3a9d6-198">Pipeline</span></span>
<span data-ttu-id="3a9d6-199">Hallo pipeline heeft twee activiteiten: **AzureMLBatchExecution** en **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="3a9d6-200">Hello Azure ML-Batchuitvoering activiteit duurt Hallo trainingsgegevens als invoer en een iLearner-bestand als uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="3a9d6-201">Hallo activiteit roept Hallo training webservice (trainingsexperiment weergegeven als een webservice) met Hallo invoer trainen van gegevens en Hallo ilearner-bestand van de webservice Hallo ontvangt.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="3a9d6-202">Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3a9d6-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![Pipeline-diagram](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
