---
title: Maak voorspellende gegevenspijplijnen met behulp van Azure Data Factory | Microsoft Docs
description: Beschrijft hoe u voorspellende pijplijnen met behulp van Azure Data Factory en Azure Machine Learning maken
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="e4099-103">Maak voorspellende pijplijnen met behulp van Azure Machine Learning en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4099-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e4099-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e4099-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e4099-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e4099-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="e4099-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e4099-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e4099-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="e4099-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e4099-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="e4099-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e4099-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="e4099-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e4099-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e4099-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="e4099-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="e4099-114">Inleiding</span><span class="sxs-lookup"><span data-stu-id="e4099-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="e4099-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e4099-115">Azure Machine Learning</span></span>
<span data-ttu-id="e4099-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) kunt u bouwen, testen en implementeren van predictive analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="e4099-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="e4099-117">Het is voltooid uit op hoog niveau oogpunt in drie stappen:</span><span class="sxs-lookup"><span data-stu-id="e4099-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="e4099-118">**Maken van een trainingsexperiment**.</span><span class="sxs-lookup"><span data-stu-id="e4099-118">**Create a training experiment**.</span></span> <span data-ttu-id="e4099-119">U kunt deze stap doen met behulp van de Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="e4099-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="e4099-120">De ML studio is een gezamenlijke visual ontwikkelingsomgeving waarmee u trainen en te testen van een predictive analytics-model met trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="e4099-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="e4099-121">**Converteren naar een Voorspellend experiment**.</span><span class="sxs-lookup"><span data-stu-id="e4099-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="e4099-122">Nadat uw model is getraind met bestaande gegevens en u bent klaar om te gebruiken voor het beoordelen van nieuwe gegevens, kunt u voorbereiden en uw experiment voor score berekenen stroomlijnen.</span><span class="sxs-lookup"><span data-stu-id="e4099-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="e4099-123">**Als een webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="e4099-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="e4099-124">U kunt uw scoreprofiel experiment publiceren als een Azure-web-service.</span><span class="sxs-lookup"><span data-stu-id="e4099-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="e4099-125">U kunt gegevens verzenden naar uw model via deze web service-eindpunt en ontvangen resultaat voorspellingen van het model.</span><span class="sxs-lookup"><span data-stu-id="e4099-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="e4099-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4099-126">Azure Data Factory</span></span>
<span data-ttu-id="e4099-127">Een Data Factory is een cloudgebaseerde gegevensintegratieservice waarmee de **verplaatsing** en **transformatie** van gegevens wordt beheerd en geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="e4099-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="e4099-128">U kunt gegevens integratieoplossingen maken gebruik van Azure Data Factory kunnen opnemen van gegevens uit verschillende gegevensarchieven, transformatieproces de gegevens en de result-gegevens publiceren naar de gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="e4099-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="e4099-129">Met Data Factory-service kunt u gegevenspijplijnen maken die gegevens verplaatsen en transformeren, en de pijplijnen vervolgens uitvoeren volgens een opgegeven schema (per uur, dagelijks, wekelijks enz.).</span><span class="sxs-lookup"><span data-stu-id="e4099-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="e4099-130">U vindt uitgebreide visualisaties om de afkomst en afhankelijkheden tussen uw gegevenspijplijnen weer te geven en al uw gegevenspijplijnen te controleren vanuit één centrale weergave zodat u eenvoudig problemen kunt detecteren en bewakingswaarschuwingen kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="e4099-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="e4099-131">Zie [Inleiding tot Azure Data Factory](data-factory-introduction.md) en [bouwen van uw eerste pijplijn](data-factory-build-your-first-pipeline.md) artikelen die u kunt snel aan de slag met de Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="e4099-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="e4099-132">Data Factory en Machine Learning samen</span><span class="sxs-lookup"><span data-stu-id="e4099-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="e4099-133">Azure Data Factory kunt u gemakkelijk maken pijplijnen die gebruikmaken van een gepubliceerde [Azure Machine Learning] [ azure-machine-learning] voor predictive analytics-webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="e4099-134">Met behulp van de **Batchuitvoeringsactiviteit** in een Azure Data Factory-pijplijn, kunt u een webservice Azure ML zodat voorspellingen op de gegevens in batch aanroept.</span><span class="sxs-lookup"><span data-stu-id="e4099-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="e4099-135">Zie [aanroepen van een Azure ML-webservice met behulp van de Batchuitvoeringsactiviteit](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4099-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="e4099-136">Na verloop van tijd moeten de voorspellende modellen in de Azure ML experimenten score berekenen met behulp van de nieuwe invoergegevenssets worden retrained.</span><span class="sxs-lookup"><span data-stu-id="e4099-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="e4099-137">U kunt een Azure ML-model van een Data Factory-pijplijn retrain als volgt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e4099-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="e4099-138">Publiceer het trainingsexperiment (geen Voorspellend experiment) als een webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="e4099-139">Deze stap in de Azure ML Studio doet u als hiervoor toen u Voorspellend experiment weergeven als een webservice in het voorgaande scenario.</span><span class="sxs-lookup"><span data-stu-id="e4099-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="e4099-140">Gebruik de Azure ML-Batchuitvoeringsactiviteit aanroepen van de webservice voor de trainingsexperiment.</span><span class="sxs-lookup"><span data-stu-id="e4099-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="e4099-141">In principe kunt u de Azure ML-Batchuitvoering activiteit webservice training zowel scoreprofiel webservice aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e4099-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="e4099-142">Nadat u klaar bent met de retraining, de scoreprofiel webservice bijwerken (Voorspellend experiment weergegeven als een webservice) met het nieuwe getrainde model met behulp van de **Azure ML-Resourceactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="e4099-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="e4099-143">Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4099-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="e4099-144">Batchuitvoeringsactiviteit met een webservice wordt aangeroepen</span><span class="sxs-lookup"><span data-stu-id="e4099-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="e4099-145">U Azure Data Factory gebruiken voor het indelen van de verplaatsing van gegevens en verwerking en vervolgens met behulp van Azure Machine Learning-Batchuitvoering uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e4099-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="e4099-146">Hier volgen de stappen op het hoogste niveau:</span><span class="sxs-lookup"><span data-stu-id="e4099-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="e4099-147">Maak een Azure Machine Learning gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="e4099-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="e4099-148">U moet de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="e4099-148">You need the following values:</span></span>

   1. <span data-ttu-id="e4099-149">**URI van de aanvraag** voor de Batchuitvoering API.</span><span class="sxs-lookup"><span data-stu-id="e4099-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="e4099-150">U kunt de aanvraag-URI vinden door te klikken op de **BATCHUITVOERING** koppeling op de webpagina van de services.</span><span class="sxs-lookup"><span data-stu-id="e4099-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="e4099-151">**API-sleutel** voor de gepubliceerde Azure Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="e4099-152">U kunt de API-sleutel vinden door te klikken op de webservice die u hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="e4099-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="e4099-153">Gebruik de **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Machine Learning-Dashboard](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="e4099-156">Scenario: Experimenten met behulp van Web service invoer/uitvoer die naar gegevens in Azure Blob-opslag verwijzen</span><span class="sxs-lookup"><span data-stu-id="e4099-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="e4099-157">In dit scenario wordt de Azure Machine Learning-webservice maakt voorspellingen met gegevens uit een bestand in een Azure blob storage en de resultaten van de voorspelling opslaat in de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="e4099-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="e4099-158">De volgende JSON definieert een Data Factory-pijplijn met een AzureMLBatchExecution-activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="e4099-159">De activiteit heeft de gegevensset **DecisionTreeInputBlob** als invoer en **DecisionTreeResultBlob** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e4099-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="e4099-160">De **DecisionTreeInputBlob** wordt doorgegeven als invoer voor de webservice door met de **webServiceInput** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e4099-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="e4099-161">De **DecisionTreeResultBlob** wordt doorgegeven als uitvoer met de webservice door met de **webServiceOutputs** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e4099-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e4099-162">Als de web-service meerdere invoer heeft, gebruikt u de **webServiceInputs** in plaats van de eigenschap **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="e4099-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="e4099-163">Zie de [webservice vereist meerdere invoeritems](#web-service-requires-multiple-inputs) sectie voor een voorbeeld van het gebruik van de eigenschap webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="e4099-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="e4099-164">Gegevenssets waarnaar wordt verwezen door de **webServiceInput**/**webServiceInputs** en **webServiceOutputs** eigenschappen (in  **typeProperties**) moet ook zijn opgenomen in de activiteit **invoer** en **levert**.</span><span class="sxs-lookup"><span data-stu-id="e4099-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="e4099-165">In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e4099-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="e4099-166">De namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen gebruikt moeten exact overeenkomen met de namen in de experimenten.</span><span class="sxs-lookup"><span data-stu-id="e4099-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="e4099-167">U kunt de nettolading van de voorbeeld-aanvraag bekijken op de pagina Batch-uitvoering Help voor uw Azure ML-eindpunt om te controleren of de verwachte toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e4099-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="e4099-168">Alleen invoer en uitvoer van de activiteit AzureMLBatchExecution kunnen als parameters worden doorgegeven aan de webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="e4099-169">In de bovenstaande JSON-codefragment is DecisionTreeInputBlob bijvoorbeeld invoer voor de activiteit AzureMLBatchExecution, die wordt doorgegeven als invoer voor de webservice via webServiceInput-parameter.</span><span class="sxs-lookup"><span data-stu-id="e4099-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="e4099-170">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e4099-170">Example</span></span>
<span data-ttu-id="e4099-171">Dit voorbeeld wordt een Azure Storage voor de invoer- en gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4099-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="e4099-172">Het is raadzaam dat u doorloopt de [bouwen van uw eerste pijplijn met Data Factory] [ adf-build-1st-pipeline] zelfstudie voordat u verdergaat met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e4099-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="e4099-173">De Data Factory-Editor gebruiken voor het maken van Data Factory-artefacten (gekoppelde services, gegevenssets, pijplijn) in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e4099-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="e4099-174">Maak een **gekoppelde service** voor uw **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="e4099-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="e4099-175">Als de invoer- en -bestanden zich in verschillende storage-accounts, moet u twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="e4099-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="e4099-176">Hier volgt een voorbeeld van JSON:</span><span class="sxs-lookup"><span data-stu-id="e4099-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="e4099-177">Maak de **invoer** Azure Data Factory **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="e4099-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="e4099-178">In tegenstelling tot een aantal andere Data Factory-gegevenssets deze gegevenssets, beide moet bevatten **folderPath** en **fileName** waarden.</span><span class="sxs-lookup"><span data-stu-id="e4099-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="e4099-179">U kunt partitioneren ervoor zorgen dat elke Batchuitvoering (elke gegevenssegment) om te verwerken of produceren unieke invoer en uitvoer van bestanden.</span><span class="sxs-lookup"><span data-stu-id="e4099-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="e4099-180">U moet mogelijk zijn sommige upstream-activiteit voor het transformeren van de invoer naar de CSV-bestandsindeling en plaats deze in het opslagaccount voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="e4099-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="e4099-181">In dat geval u geen omvat de **externe** en **externalData** instellingen die worden weergegeven in het volgende voorbeeld en uw DecisionTreeInputBlob zou de uitvoergegevensbron van een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    <span data-ttu-id="e4099-182">Uw invoer csv-bestand moet de veldnamenrij kolom hebben.</span><span class="sxs-lookup"><span data-stu-id="e4099-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="e4099-183">Als u de **Kopieeractiviteit** als u wilt maken of verplaatsen de csv in de blobopslag, moet u de eigenschap sink instellen **blobWriterAddHeader** naar **true**.</span><span class="sxs-lookup"><span data-stu-id="e4099-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="e4099-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4099-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="e4099-185">Als het csv-bestand is geen de veldnamenrij, ziet u mogelijk de volgende fout: **fout in de activiteit: fout bij het lezen van de tekenreeks. Onverwacht token: StartObject. Pad '', regel 1, positie 1**.</span><span class="sxs-lookup"><span data-stu-id="e4099-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="e4099-186">Maak de **uitvoer** Azure Data Factory **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="e4099-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="e4099-187">In dit voorbeeld gebruikt partitioneren voor een unieke uitvoerpad voor de uitvoering van elk segment maken.</span><span class="sxs-lookup"><span data-stu-id="e4099-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="e4099-188">Zonder de partitionering, zou de activiteit bestand overschreven.</span><span class="sxs-lookup"><span data-stu-id="e4099-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="e4099-189">Maak een **gekoppelde service** van het type: **AzureMLLinkedService**, bieden de API-sleutel en model van de volgende URL.</span><span class="sxs-lookup"><span data-stu-id="e4099-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="e4099-190">Ten slotte schrijft een pijplijn met een **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="e4099-191">Pijplijn voert tijdens runtime, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e4099-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="e4099-192">Hiermee haalt u de locatie van het bestand voor invoer van uw invoer gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="e4099-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="e4099-193">De Batchuitvoering van Azure Machine Learning API aanroept</span><span class="sxs-lookup"><span data-stu-id="e4099-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="e4099-194">De uitvoer van de batch-uitvoering gekopieerd naar de blob die is opgegeven in de uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="e4099-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e4099-195">AzureMLBatchExecution activiteit kan hebben nul of meer invoer en uitvoer van een of meer.</span><span class="sxs-lookup"><span data-stu-id="e4099-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="e4099-196">Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e4099-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e4099-197">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e4099-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="e4099-198">De **end** tijd is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e4099-198">The **end** time is optional.</span></span> <span data-ttu-id="e4099-199">Als u geen waarde voor de **end** eigenschap, wordt berekend als '**start + 48 uur.**'</span><span class="sxs-lookup"><span data-stu-id="e4099-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="e4099-200">Als u de pijplijn voor onbepaalde tijd wilt uitvoeren, geeft u **9999-09-09** op als waarde voor de eigenschap **end**.</span><span class="sxs-lookup"><span data-stu-id="e4099-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="e4099-201">Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e4099-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e4099-202">Invoer voor de AzureMLBatchExecution opgeven is activiteit optioneel.</span><span class="sxs-lookup"><span data-stu-id="e4099-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="e4099-203">Scenario: Experimenten lezer/schrijver-Modules gebruiken om te verwijzen naar gegevens in verschillende gelijksoortig</span><span class="sxs-lookup"><span data-stu-id="e4099-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="e4099-204">Bij het maken van Azure ML-experimenten een ander gebruikelijk scenario is het gebruik van de lezer en -schrijver modules.</span><span class="sxs-lookup"><span data-stu-id="e4099-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="e4099-205">De module reader wordt gebruikt om gegevens te laden in een experiment en de module writer is gegevens van uw experimenten worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e4099-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="e4099-206">Zie voor meer informatie over de lezer en -schrijver modules [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="e4099-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="e4099-207">Wanneer u de lezer en -schrijver modules, is het raadzaam om een Web service-parameter voor elke eigenschap van deze modules lezer/schrijver gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e4099-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="e4099-208">Deze web-parameters kunnen u voor het configureren van de waarden tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="e4099-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="e4099-209">U kunt bijvoorbeeld een experiment maken met een leesmodule die gebruikmaakt van een Azure SQL Database: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="e4099-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="e4099-210">Nadat de web-service is geïmplementeerd, die u wilt inschakelen van de consument van de web-service om op te geven van een Azure SQL-Server YYY.database.windows.net aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e4099-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="e4099-211">Een parameter van Web service kunt u toestaan dat deze waarde moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e4099-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="e4099-212">Web service invoer en uitvoer verschillen van de parameters van Web service.</span><span class="sxs-lookup"><span data-stu-id="e4099-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="e4099-213">In het eerste scenario hebt u gezien hoe een invoer en uitvoer voor een webservice Azure ML kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e4099-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="e4099-214">In dit scenario kunt u parameters voor een webservice die overeenkomen met doorgeven aan de eigenschappen van de lezer/schrijver modules.</span><span class="sxs-lookup"><span data-stu-id="e4099-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="e4099-215">We bekijken een scenario voor het gebruik van parameters van Web service.</span><span class="sxs-lookup"><span data-stu-id="e4099-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="e4099-216">U hebt een geïmplementeerde Azure Machine Learning-webservice die gebruikmaakt van een module reader gegevens lezen uit een van de gegevensbronnen die wordt ondersteund door Azure Machine Learning (bijvoorbeeld: Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="e4099-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="e4099-217">Nadat de batchuitvoering is uitgevoerd, kan de resultaten zijn geschreven met behulp van een module Writer (Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="e4099-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="e4099-218">Er is geen web-service in- en uitgangen zijn gedefinieerd in de experimenten.</span><span class="sxs-lookup"><span data-stu-id="e4099-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="e4099-219">In dit geval is het raadzaam dat u de parameters van de relevante web service voor de lezer en -schrijver modules configureert.</span><span class="sxs-lookup"><span data-stu-id="e4099-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="e4099-220">Deze configuratie kunt de reader/writer modules worden geconfigureerd wanneer u de activiteit AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="e4099-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="e4099-221">U Web serviceparameters opgeven in de **globalParameters** sectie als volgt in de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="e4099-222">U kunt ook [Data Factory functies](data-factory-functions-variables.md) waarden doorgeven voor de Web service-parameters zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4099-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="e4099-223">Parameters van de webservice zijn hoofdlettergevoelig, dus zorg ervoor dat de namen die u opgeeft in de activiteits-JSON overeenkomen met de gegevenstypen die worden weergegeven door de webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="e4099-224">Een module Reader gebruikt om te lezen van gegevens uit meerdere bestanden in Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e4099-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="e4099-225">BIG data pijplijnen met activiteiten zoals Pig en Hive kunt produceren van een of meer uitvoerbestanden zonder extensie.</span><span class="sxs-lookup"><span data-stu-id="e4099-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="e4099-226">Bijvoorbeeld, wanneer u een externe Hive-tabel opgeeft, kan de gegevens voor de externe Hive-tabel kunnen worden opgeslagen in Azure blob storage met de volgende naam 000000_0.</span><span class="sxs-lookup"><span data-stu-id="e4099-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="e4099-227">U kunt de module reader gebruiken in een experiment meerdere bestanden lezen en deze worden gebruikt voor voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="e4099-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="e4099-228">Wanneer u de module reader in een Azure Machine Learning-experiment, kunt u Azure Blob opgeven als invoer.</span><span class="sxs-lookup"><span data-stu-id="e4099-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="e4099-229">De bestanden in Azure blob storage kunnen worden de uitvoerbestanden (voorbeeld: 000000_0) die worden geproduceerd door een Pig en Hive-script uitgevoerd op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4099-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="e4099-230">De module reader kunt u lezen-bestanden (met er worden geen extensies) door het configureren van de **pad naar de container, map/blob**.</span><span class="sxs-lookup"><span data-stu-id="e4099-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="e4099-231">De **pad naar de container** verwijst naar de container en **directory/blob** verwijst naar de map waarin de bestanden, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="e4099-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="e4099-232">Het sterretje dat wil zeggen, \*) **geeft aan dat alle bestanden in de container of de map (dat wil zeggen, aggregateddata-gegevens/jaar = maand-2014-6 /\*)** als onderdeel van het experiment worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="e4099-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Azure Blob-eigenschappen](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="e4099-234">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e4099-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="e4099-235">Pijplijn met AzureMLBatchExecution activiteit met de Parameters van Web Service</span><span class="sxs-lookup"><span data-stu-id="e4099-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="e4099-236">In de bovenstaande JSON-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4099-236">In the above JSON example:</span></span>

* <span data-ttu-id="e4099-237">De geïmplementeerde Azure Machine Learning-webservice maakt gebruik van een lezer en een schrijfmodule tot lezen/schrijven van gegevens van/naar een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e4099-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="e4099-238">Deze webservice beschrijft de volgende vier parameters: servernaam, databasenaam, servergebruikersnaam en wachtwoord voor gebruikersaccount Server-Database.</span><span class="sxs-lookup"><span data-stu-id="e4099-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="e4099-239">Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e4099-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e4099-240">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e4099-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="e4099-241">De **end** tijd is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e4099-241">The **end** time is optional.</span></span> <span data-ttu-id="e4099-242">Als u geen waarde voor de **end** eigenschap, wordt berekend als '**start + 48 uur.**'</span><span class="sxs-lookup"><span data-stu-id="e4099-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="e4099-243">Als u de pijplijn voor onbepaalde tijd wilt uitvoeren, geeft u **9999-09-09** op als waarde voor de eigenschap **end**.</span><span class="sxs-lookup"><span data-stu-id="e4099-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="e4099-244">Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e4099-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="e4099-245">Andere scenario's</span><span class="sxs-lookup"><span data-stu-id="e4099-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="e4099-246">Meerdere invoer is vereist</span><span class="sxs-lookup"><span data-stu-id="e4099-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="e4099-247">Als de web-service meerdere invoer heeft, gebruikt u de **webServiceInputs** in plaats van de eigenschap **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="e4099-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="e4099-248">Gegevenssets waarnaar wordt verwezen door de **webServiceInputs** moet ook zijn opgenomen in de activiteit **invoer**.</span><span class="sxs-lookup"><span data-stu-id="e4099-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="e4099-249">In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e4099-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="e4099-250">De namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen gebruikt moeten exact overeenkomen met de namen in de experimenten.</span><span class="sxs-lookup"><span data-stu-id="e4099-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="e4099-251">U kunt de nettolading van de voorbeeld-aanvraag bekijken op de pagina Batch-uitvoering Help voor uw Azure ML-eindpunt om te controleren of de verwachte toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e4099-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="e4099-252">Web-Service vereist geen invoer</span><span class="sxs-lookup"><span data-stu-id="e4099-252">Web Service does not require an input</span></span>
<span data-ttu-id="e4099-253">Azure ML-batch uitvoering webservices kunnen worden gebruikt voor het uitvoeren van alle werkstromen, voor voorbeeld R- of Python-scripts die niet alle invoer nodig.</span><span class="sxs-lookup"><span data-stu-id="e4099-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="e4099-254">Of het experiment kan worden geconfigureerd met een lezer-module die u maakt een GlobalParameters niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e4099-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="e4099-255">In dat geval wordt de activiteit AzureMLBatchExecution zou als volgt geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="e4099-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="e4099-256">Web-Service vereist geen invoer/uitvoer</span><span class="sxs-lookup"><span data-stu-id="e4099-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="e4099-257">De webservice voor de uitvoering van Azure ML hebben mogelijk niet alle webservice-uitvoer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e4099-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="e4099-258">Er is geen webservice invoer of uitvoer in dit voorbeeld, noch een GlobalParameters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e4099-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="e4099-259">Er is nog steeds een uitvoer die is geconfigureerd op de activiteit zelf, maar er is geen opgegeven als een webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="e4099-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="e4099-260">Web-Service gebruikt lezers en schrijvers en de activiteit wordt uitgevoerd, alleen wanneer andere activiteiten zijn geslaagd</span><span class="sxs-lookup"><span data-stu-id="e4099-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="e4099-261">De Azure ML web service lezer en -schrijver modules kunnen zijn geconfigureerd om te worden uitgevoerd met of zonder eventuele GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="e4099-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="e4099-262">U kunt echter serviceaanroepen insluiten in een pijplijn die gebruikmaakt van gegevensset afhankelijkheden aanroepen van de service alleen wanneer sommige upstream verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e4099-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="e4099-263">Nadat de Batchuitvoering van de is voltooid met deze benadering kunt u ook een andere actie activeren.</span><span class="sxs-lookup"><span data-stu-id="e4099-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="e4099-264">In dat geval kunt u de afhankelijkheden die met behulp van activiteit in- en uitgangen, zonder een van deze als webservice in- of uitgangen uitdrukken.</span><span class="sxs-lookup"><span data-stu-id="e4099-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="e4099-265">De **takeaways** zijn:</span><span class="sxs-lookup"><span data-stu-id="e4099-265">The **takeaways** are:</span></span>

* <span data-ttu-id="e4099-266">Als uw experiment-eindpunt maakt gebruik van een webServiceInput: er wordt vertegenwoordigd door een blob-gegevensset en is opgenomen in de activiteitinvoer en de eigenschap webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="e4099-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="e4099-267">Anders wordt is de eigenschap webServiceInput weggelaten.</span><span class="sxs-lookup"><span data-stu-id="e4099-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="e4099-268">Als uw experiment-eindpunt maakt gebruik van webServiceOutput(s): ze worden vertegenwoordigd door de blob-gegevenssets en zijn opgenomen in de uitvoer voor activiteiten en in de eigenschap webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="e4099-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="e4099-269">Uitvoer van de activiteit en webServiceOutputs zijn toegewezen door de naam van elke uitvoer in het experiment.</span><span class="sxs-lookup"><span data-stu-id="e4099-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="e4099-270">Anders wordt is de eigenschap webServiceOutputs weggelaten.</span><span class="sxs-lookup"><span data-stu-id="e4099-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="e4099-271">Als uw experiment eindpunt globalParameter(s) beschrijft, staan ze vermeld in de eigenschap globalParameters van activiteit als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="e4099-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="e4099-272">Anders wordt is de eigenschap globalParameters weggelaten.</span><span class="sxs-lookup"><span data-stu-id="e4099-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="e4099-273">De sleutels zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="e4099-273">The keys are case-sensitive.</span></span> <span data-ttu-id="e4099-274">[Azure Data Factory-functies](data-factory-functions-variables.md) kan worden gebruikt in de waarden.</span><span class="sxs-lookup"><span data-stu-id="e4099-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="e4099-275">Aanvullende gegevenssets kan worden opgenomen in de eigenschappen van de invoer en uitvoer voor activiteiten, zonder waarnaar wordt verwezen in de activiteit typeProperties.</span><span class="sxs-lookup"><span data-stu-id="e4099-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="e4099-276">Deze gegevenssets kan worden uitgevoerd segment afhankelijkheden reguleren maar anders worden genegeerd door de activiteit AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="e4099-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="e4099-277">Bijwerken van modellen Update Resource activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="e4099-278">Nadat u klaar bent met de retraining, de scoreprofiel webservice bijwerken (Voorspellend experiment weergegeven als een webservice) met het nieuwe getrainde model met behulp van de **Azure ML-Resourceactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="e4099-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="e4099-279">Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4099-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="e4099-280">Lezer en Writer Modules</span><span class="sxs-lookup"><span data-stu-id="e4099-280">Reader and Writer Modules</span></span>
<span data-ttu-id="e4099-281">Een veelvoorkomend scenario voor het gebruik van parameters voor Web-service is het gebruik van Azure SQL en schrijfprogramma.</span><span class="sxs-lookup"><span data-stu-id="e4099-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="e4099-282">De module reader wordt gebruikt voor het laden van gegevens in een experiment van data management-services buiten Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e4099-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="e4099-283">De module writer is het opslaan van gegevens vanuit uw experimenten in beheerservices gegevens buiten Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e4099-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="e4099-284">Zie voor meer informatie over Azure-Blob/Azure SQL-lezer/schrijver [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="e4099-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="e4099-285">Het voorbeeld in de vorige sectie gebruikt de Azure Blob-lezer en Azure Blob-schrijver.</span><span class="sxs-lookup"><span data-stu-id="e4099-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="e4099-286">Deze sectie beschrijft het gebruik van Azure SQL-reader en Azure SQL writer.</span><span class="sxs-lookup"><span data-stu-id="e4099-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="e4099-287">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="e4099-287">Frequently asked questions</span></span>
<span data-ttu-id="e4099-288">**V:** ik heb meerdere bestanden die worden gegenereerd door mijn pijplijnen big data.</span><span class="sxs-lookup"><span data-stu-id="e4099-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="e4099-289">Kan ik de activiteit AzureMLBatchExecution gebruiken om te werken op alle bestanden?</span><span class="sxs-lookup"><span data-stu-id="e4099-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="e4099-290">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="e4099-290">**A:** Yes.</span></span> <span data-ttu-id="e4099-291">Zie de **met behulp van een module Reader gegevens lezen uit meerdere bestanden in Azure Blob** sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4099-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="e4099-292">Score berekenen voor Azure ML-Batch-activiteit</span><span class="sxs-lookup"><span data-stu-id="e4099-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="e4099-293">Als u de **AzureMLBatchScoring** activiteit integreren met Azure Machine Learning, het is raadzaam dat u de meest recente **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="e4099-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="e4099-294">De activiteit AzureMLBatchExecution wordt geïntroduceerd in de augustus 2015-release van Azure SDK en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4099-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="e4099-295">Als u wilt doorgaan met het gebruik van de activiteit AzureMLBatchScoring, blijven lezen via deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e4099-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="e4099-296">Azure ML-Batchscoreberekening activiteit voor het gebruik van Azure Storage voor invoer/uitvoer</span><span class="sxs-lookup"><span data-stu-id="e4099-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="e4099-297">Parameters voor Web-Service</span><span class="sxs-lookup"><span data-stu-id="e4099-297">Web Service Parameters</span></span>
<span data-ttu-id="e4099-298">Waarden voor de Web serviceparameters wilt opgeven, Voeg een **typeProperties** sectie aan de **AzureMLBatchScoringActivty** sectie in de JSON-pijplijn, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4099-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="e4099-299">U kunt ook [Data Factory functies](data-factory-functions-variables.md) waarden doorgeven voor de Web service-parameters zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e4099-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="e4099-300">Parameters van de webservice zijn hoofdlettergevoelig, dus zorg ervoor dat de namen die u opgeeft in de activiteits-JSON overeenkomen met de gegevenstypen die worden weergegeven door de webservice.</span><span class="sxs-lookup"><span data-stu-id="e4099-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="e4099-301">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e4099-301">See Also</span></span>
* [<span data-ttu-id="e4099-302">Azure blogbericht: aan de slag met Azure Data Factory en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e4099-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
