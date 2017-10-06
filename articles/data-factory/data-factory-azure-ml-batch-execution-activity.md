---
title: voorspellende gegevenspijplijnen aaaCreate met behulp van Azure Data Factory | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate voorspellende pijplijnen met behulp van Azure Data Factory en Azure Machine Learning maken
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="720a8-103">Maak voorspellende pijplijnen met behulp van Azure Machine Learning en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="720a8-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="720a8-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="720a8-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="720a8-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="720a8-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="720a8-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="720a8-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="720a8-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="720a8-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="720a8-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="720a8-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="720a8-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="720a8-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="720a8-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="720a8-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="720a8-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="720a8-114">Inleiding</span><span class="sxs-lookup"><span data-stu-id="720a8-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="720a8-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="720a8-115">Azure Machine Learning</span></span>
<span data-ttu-id="720a8-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Hiermee schakelt u toobuild, testen en implementeren van predictive analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="720a8-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="720a8-117">Het is voltooid uit op hoog niveau oogpunt in drie stappen:</span><span class="sxs-lookup"><span data-stu-id="720a8-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="720a8-118">**Maken van een trainingsexperiment**.</span><span class="sxs-lookup"><span data-stu-id="720a8-118">**Create a training experiment**.</span></span> <span data-ttu-id="720a8-119">U doen deze stap met behulp van hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="720a8-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="720a8-120">Hallo ML studio is een gezamenlijke visual ontwikkelomgeving tootrain te gebruiken en testen van een predictive analytics-model met trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="720a8-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="720a8-121">**Converteert u deze tooa Voorspellend experiment**.</span><span class="sxs-lookup"><span data-stu-id="720a8-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="720a8-122">Nadat uw model is getraind met bestaande gegevens en u klaar toouse bent deze nieuwe gegevens tooscore, bereiden en het stroomlijnen van uw experiment voor score berekenen.</span><span class="sxs-lookup"><span data-stu-id="720a8-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="720a8-123">**Als een webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="720a8-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="720a8-124">U kunt uw scoreprofiel experiment publiceren als een Azure-web-service.</span><span class="sxs-lookup"><span data-stu-id="720a8-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="720a8-125">U kunt tooyour gegevensmodel via deze web service-eindpunt te verzenden en ontvangen resultaat voorspellingen van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="720a8-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="720a8-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="720a8-126">Azure Data Factory</span></span>
<span data-ttu-id="720a8-127">Data Factory is een cloud-gebaseerde gegevens integration-service die ingedeeld en automatiseert Hallo **verkeer** en **transformatie** van gegevens.</span><span class="sxs-lookup"><span data-stu-id="720a8-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="720a8-128">U kunt gegevens integratieoplossingen maken gebruik van Azure Data Factory die kunnen gegevens uit verschillende gegevensarchieven opnemen, transformatieproces Hallo gegevens publiceren Hallo resultaat toohello gegevens gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="720a8-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="720a8-129">Data Factory-service kunt u toocreate gegevenspijplijnen verplaatsen en gegevens transformeren en Voer Hallo pijplijnen volgens een opgegeven schema (elk uur, dagelijks, wekelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="720a8-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="720a8-130">Ook biedt uitgebreide visualisaties toodisplay hello afkomstinformatie en afhankelijkheden tussen uw gegevenspijplijnen en uw gegevenspijplijnen van een één centrale weergave tooeasily baseren problemen bewaken en waarschuwingen voor toepassingsbewaking instellen.</span><span class="sxs-lookup"><span data-stu-id="720a8-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="720a8-131">Zie [inleiding tooAzure Data Factory](data-factory-introduction.md) en [bouwen van uw eerste pijplijn](data-factory-build-your-first-pipeline.md) artikelen tooquickly aan de slag met hello Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="720a8-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="720a8-132">Data Factory en Machine Learning samen</span><span class="sxs-lookup"><span data-stu-id="720a8-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="720a8-133">Azure Data Factory kunt u tooeasily maken pijplijnen die gebruikmaken van een gepubliceerde [Azure Machine Learning] [ azure-machine-learning] voor predictive analytics-webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="720a8-134">Met behulp van Hallo **Batchuitvoeringsactiviteit** in een Azure Data Factory-pijplijn, kunt u een Azure ML web service toomake voorspellingen op Hallo-gegevens in een batch aanroept.</span><span class="sxs-lookup"><span data-stu-id="720a8-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="720a8-135">Zie [aanroepen van een Azure ML-Batchuitvoeringsactiviteit web service gebruikmaakt van Hallo](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="720a8-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="720a8-136">Na verloop van tijd moeten Hallo voorspellende modellen in hello Azure ML scoreprofiel experimenten toobe retrained met nieuwe invoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="720a8-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="720a8-137">U kunt een Azure ML-model van een Data Factory-pijplijn retrain Hallo volgende stappen uit als volgt:</span><span class="sxs-lookup"><span data-stu-id="720a8-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="720a8-138">Hallo trainingsexperiment (geen Voorspellend experiment) publiceren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="720a8-139">Deze stap in hello Azure ML Studio doet u net als tooexpose Voorspellend experiment als een webservice in Hallo voorgaande scenario.</span><span class="sxs-lookup"><span data-stu-id="720a8-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="720a8-140">Hello Azure ML-Batchuitvoeringsactiviteit tooinvoke Hallo-webservice voor Hallo trainingsexperiment gebruiken.</span><span class="sxs-lookup"><span data-stu-id="720a8-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="720a8-141">U kunt in principe hello Azure ML-Batchuitvoering activiteit tooinvoke zowel webservice trainings- en score berekenen voor web-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="720a8-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="720a8-142">Nadat u klaar bent met de retraining, bijwerken Hallo score berekenen voor web-service (Voorspellend experiment weergegeven als een webservice) met Hallo zojuist getrainde model met behulp van Hallo **Azure ML-Resourceactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="720a8-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="720a8-143">Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="720a8-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="720a8-144">Batchuitvoeringsactiviteit met een webservice wordt aangeroepen</span><span class="sxs-lookup"><span data-stu-id="720a8-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="720a8-145">U gebruikt Azure Data Factory tooorchestrate gegevensverplaatsing en verwerking en vervolgens uitvoert met Azure Machine Learning-batchuitvoering.</span><span class="sxs-lookup"><span data-stu-id="720a8-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="720a8-146">Hier volgen op het hoogste niveau Hallo-stappen:</span><span class="sxs-lookup"><span data-stu-id="720a8-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="720a8-147">Maak een Azure Machine Learning gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="720a8-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="720a8-148">U moet Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="720a8-148">You need hello following values:</span></span>

   1. <span data-ttu-id="720a8-149">**URI van de aanvraag** voor Hallo Batch-API voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="720a8-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="720a8-150">U kunt Hallo aanvraag-URI vinden door te klikken op Hallo **BATCHUITVOERING** koppeling op Hallo services webpagina.</span><span class="sxs-lookup"><span data-stu-id="720a8-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="720a8-151">**API-sleutel** voor Hallo gepubliceerd Azure Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="720a8-152">U kunt Hallo API-sleutel vinden door te klikken op Hallo-webservice die u hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="720a8-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="720a8-153">Gebruik Hallo **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Machine Learning-Dashboard](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="720a8-156">Scenario: Experimenten met behulp van Web service invoer/uitvoer die toodata in Azure Blob Storage verwijst</span><span class="sxs-lookup"><span data-stu-id="720a8-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="720a8-157">In dit scenario hello Azure Machine Learning-webservice maakt voorspellingen met gegevens uit een bestand in een Azure blob storage en slaat Hallo voorspelling resultaten in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="720a8-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="720a8-158">Hallo definieert volgende JSON een Data Factory-pijplijn met een AzureMLBatchExecution-activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="720a8-159">Hallo-activiteit heeft Hallo gegevensset **DecisionTreeInputBlob** als invoer en **DecisionTreeResultBlob** als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="720a8-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="720a8-160">Hallo **DecisionTreeInputBlob** is doorgegeven als een webservice van invoer toohello door Hallo met **webServiceInput** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="720a8-161">Hallo **DecisionTreeResultBlob** wordt doorgegeven als uitvoer toohello webservice door met de Hallo **webServiceOutputs** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="720a8-162">Als webservice Hallo meerdere invoer heeft, gebruikt u Hallo **webServiceInputs** in plaats van de eigenschap **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="720a8-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="720a8-163">Zie Hallo [webservice vereist meerdere invoeritems](#web-service-requires-multiple-inputs) sectie voor een voorbeeld van het gebruik van Hallo webServiceInputs eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="720a8-164">Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInput**/**webServiceInputs** en **webServiceOutputs** eigenschappen (in  **typeProperties**) moet ook zijn opgenomen in Hallo activiteit **invoer** en **levert**.</span><span class="sxs-lookup"><span data-stu-id="720a8-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="720a8-165">In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="720a8-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="720a8-166">Hallo namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen moeten exact overeenkomen met Hallo-namen in Hallo experimenten.</span><span class="sxs-lookup"><span data-stu-id="720a8-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="720a8-167">U kunt de aanvraaglading van de steekproef Hallo bekijken op Hallo Batch uitvoering Help-pagina voor uw Azure ML-eindpunt tooverify Hallo verwacht toewijzing.</span><span class="sxs-lookup"><span data-stu-id="720a8-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="720a8-168">Alleen invoer en uitvoer van Hallo AzureMLBatchExecution activiteit kunnen worden doorgegeven als parameters toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="720a8-169">In Hallo hierboven JSON-codefragment is DecisionTreeInputBlob bijvoorbeeld een invoer toohello AzureMLBatchExecution activiteit, die is doorgegeven als een invoer toohello webservice via webServiceInput-parameter.</span><span class="sxs-lookup"><span data-stu-id="720a8-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="720a8-170">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="720a8-170">Example</span></span>
<span data-ttu-id="720a8-171">In dit voorbeeld maakt gebruik van Azure Storage toohold beide Hallo en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="720a8-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="720a8-172">Het is raadzaam dat u Hallo doorloopt [bouwen van uw eerste pijplijn met Data Factory] [ adf-build-1st-pipeline] zelfstudie voordat u verdergaat met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="720a8-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="720a8-173">Hallo Data Factory-Editor toocreate Data Factory-artefacten (gekoppelde services, gegevenssets, pijplijn) in dit voorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="720a8-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="720a8-174">Maak een **gekoppelde service** voor uw **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="720a8-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="720a8-175">Als hello invoer en uitvoer bestanden zich in verschillende storage-accounts, moet u twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="720a8-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="720a8-176">Hier volgt een voorbeeld van JSON:</span><span class="sxs-lookup"><span data-stu-id="720a8-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="720a8-177">Hallo maken **invoer** Azure Data Factory **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="720a8-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="720a8-178">In tegenstelling tot een aantal andere Data Factory-gegevenssets deze gegevenssets, beide moet bevatten **folderPath** en **fileName** waarden.</span><span class="sxs-lookup"><span data-stu-id="720a8-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="720a8-179">U kunt gebruiken partitionering toocause elke batch uitvoering (elke gegevenssegment) tooprocess of unieke invoer produceren en uitvoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="720a8-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="720a8-180">Mogelijk moet u tooinclude sommige upstream-activiteit tootransform Hallo invoer voor Hallo CSV-bestandsindeling en plaats deze in Hallo storage-account voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="720a8-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="720a8-181">In dat geval zou u geen Hallo opgenomen **externe** en **externalData** instellingen die worden weergegeven in de volgende Hallo voorbeeld en uw DecisionTreeInputBlob hello uitvoergegevensset van een andere activiteit zou zijn.</span><span class="sxs-lookup"><span data-stu-id="720a8-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="720a8-182">Uw invoer csv-bestand moet Hallo kolom veldnamenrij hebben.</span><span class="sxs-lookup"><span data-stu-id="720a8-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="720a8-183">Als u van Hallo gebruikmaakt **Kopieeractiviteit** toocreate of verplaatsen Hallo csv in Hallo blob-opslag, moet u Hallo sink-eigenschap instellen **blobWriterAddHeader** te**true**.</span><span class="sxs-lookup"><span data-stu-id="720a8-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="720a8-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="720a8-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="720a8-185">Als Hallo CSV-bestand geen veldnamenrij hello heeft, ziet u mogelijk Hallo volgende fout: **fout in de activiteit: fout bij het lezen van de tekenreeks. Onverwacht token: StartObject. Pad '', regel 1, positie 1**.</span><span class="sxs-lookup"><span data-stu-id="720a8-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="720a8-186">Hallo maken **uitvoer** Azure Data Factory **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="720a8-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="720a8-187">Dit voorbeeld wordt partitionering toocreate een unieke uitvoerpad voor de uitvoering van elk segment.</span><span class="sxs-lookup"><span data-stu-id="720a8-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="720a8-188">Zonder Hallo partitioneren, zou Hallo activiteit Hallo bestand overschreven.</span><span class="sxs-lookup"><span data-stu-id="720a8-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="720a8-189">Maak een **gekoppelde service** van het type: **AzureMLLinkedService**, bieden Hallo API-sleutel en model van de volgende URL.</span><span class="sxs-lookup"><span data-stu-id="720a8-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="720a8-190">Ten slotte schrijft een pijplijn met een **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="720a8-191">Tijdens runtime voert de pijplijn Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="720a8-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="720a8-192">Hallo-locatie van het invoerbestand Hallo krijgt van uw invoer gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="720a8-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="720a8-193">Hello Azure Machine Learning-Batchuitvoering API aanroept</span><span class="sxs-lookup"><span data-stu-id="720a8-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="720a8-194">Kopieën Hallo batch uitvoering uitvoer toohello blob gegeven in de uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="720a8-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="720a8-195">AzureMLBatchExecution activiteit kan hebben nul of meer invoer en uitvoer van een of meer.</span><span class="sxs-lookup"><span data-stu-id="720a8-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="720a8-196">Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="720a8-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="720a8-197">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="720a8-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="720a8-198">Hallo **end** tijd is optioneel.</span><span class="sxs-lookup"><span data-stu-id="720a8-198">hello **end** time is optional.</span></span> <span data-ttu-id="720a8-199">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur.**'</span><span class="sxs-lookup"><span data-stu-id="720a8-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="720a8-200">toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="720a8-201">Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="720a8-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="720a8-202">Invoer voor Hallo AzureMLBatchExecution activiteit opgeven is optioneel.</span><span class="sxs-lookup"><span data-stu-id="720a8-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="720a8-203">Scenario: Experimenten met lezer/schrijver Modules toorefer toodata in verschillende gelijksoortig</span><span class="sxs-lookup"><span data-stu-id="720a8-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="720a8-204">Bij het maken van Azure ML-experimenten een ander gebruikelijk scenario is toouse lezer en -schrijver modules.</span><span class="sxs-lookup"><span data-stu-id="720a8-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="720a8-205">leesmodule Hello gebruikte tooload gegevens in een experiment en Hallo-schrijfmodule toosave gegevens vanuit uw experimenten.</span><span class="sxs-lookup"><span data-stu-id="720a8-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="720a8-206">Zie voor meer informatie over de lezer en -schrijver modules [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="720a8-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="720a8-207">Wanneer u Hallo lezer en -schrijver modules, is het raadzaam om toouse een parameter van de Web service voor elke eigenschap van deze modules lezer/schrijver.</span><span class="sxs-lookup"><span data-stu-id="720a8-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="720a8-208">Deze web-parameters kunnen u tooconfigure Hallo waarden tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="720a8-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="720a8-209">U kunt bijvoorbeeld een experiment maken met een leesmodule die gebruikmaakt van een Azure SQL Database: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="720a8-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="720a8-210">Nadat Hallo web-service is geïmplementeerd, kunt u tooenable Hallo consumenten van Hallo web service toospecify een Azure SQL-Server YYY.database.windows.net aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="720a8-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="720a8-211">Deze waarde toobe geconfigureerd, kunt u een Web service parameter tooallow gebruiken.</span><span class="sxs-lookup"><span data-stu-id="720a8-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="720a8-212">Web service invoer en uitvoer verschillen van de parameters van Web service.</span><span class="sxs-lookup"><span data-stu-id="720a8-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="720a8-213">In het eerste scenario hello, hebt u gezien hoe een invoer en uitvoer voor een webservice Azure ML kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="720a8-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="720a8-214">In dit scenario moet u parameters voor een webservice die overeenkomen met tooproperties lezer/schrijver modules doorgeven.</span><span class="sxs-lookup"><span data-stu-id="720a8-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="720a8-215">We bekijken een scenario voor het gebruik van parameters van Web service.</span><span class="sxs-lookup"><span data-stu-id="720a8-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="720a8-216">U hebt een geïmplementeerde Azure Machine Learning-webservice die gebruikmaakt van een lezer module tooread gegevens uit een van de gegevensbronnen hello wordt ondersteund door Azure Machine Learning (bijvoorbeeld: Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="720a8-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="720a8-217">Nadat de Batchuitvoering hello wordt uitgevoerd, kan Hallo resultaten zijn geschreven met behulp van een module Writer (Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="720a8-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="720a8-218">Er is geen web-service in- en uitgangen zijn gedefinieerd in Hallo experimenten.</span><span class="sxs-lookup"><span data-stu-id="720a8-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="720a8-219">In dit geval is het raadzaam dat u de relevante webserviceparameters voor Hallo lezer en -schrijver modules configureert.</span><span class="sxs-lookup"><span data-stu-id="720a8-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="720a8-220">Deze configuratie kunt Hallo lezer/schrijver modules toobe geconfigureerd wanneer u Hallo AzureMLBatchExecution activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="720a8-221">U Web serviceparameters opgeven in Hallo **globalParameters** sectie in Hallo activiteits-JSON als volgt.</span><span class="sxs-lookup"><span data-stu-id="720a8-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="720a8-222">U kunt ook [Data Factory functies](data-factory-functions-variables.md) in het doorgeven van waarden voor Hallo Web serviceparameters zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="720a8-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="720a8-223">Hallo Web serviceparameters zijn hoofdlettergevoelig, dus zorg ervoor dat Hallo-namen die u opgeeft in de activiteit Hallo JSON overeenkomen Hallo waarden die worden weergegeven door het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="720a8-224">Een lezer module tooread gegevens uit meerdere bestanden in Azure Blob gebruiken</span><span class="sxs-lookup"><span data-stu-id="720a8-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="720a8-225">BIG data pijplijnen met activiteiten zoals Pig en Hive kunt produceren van een of meer uitvoerbestanden zonder extensie.</span><span class="sxs-lookup"><span data-stu-id="720a8-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="720a8-226">Bijvoorbeeld, wanneer u een externe Hive-tabel opgeeft, kunnen de Hallo gegevens voor Hallo externe Hive-tabel worden opgeslagen in Azure blob-opslag Hello naam 000000_0 te volgen.</span><span class="sxs-lookup"><span data-stu-id="720a8-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="720a8-227">U kunt meerdere bestanden Hallo leesmodule in een experiment tooread gebruiken en deze worden gebruikt voor voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="720a8-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="720a8-228">Wanneer u de module reader Hallo in een Azure Machine Learning-experiment, kunt u Azure Blob opgeven als invoer.</span><span class="sxs-lookup"><span data-stu-id="720a8-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="720a8-229">Hallo-bestanden in hello Azure blob-opslag kunnen worden uitvoerbestanden hello (voorbeeld: 000000_0) die worden geproduceerd door een Pig en Hive-script uitgevoerd op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="720a8-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="720a8-230">Hallo leesmodule kunt u tooread-bestanden (met er worden geen extensies) door het configureren van Hallo **toocontainer pad, de map/blob**.</span><span class="sxs-lookup"><span data-stu-id="720a8-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="720a8-231">Hallo **pad toocontainer** punten toohello container en **directory/blob** verwijst toofolder die Hallo bestanden bevat, zoals wordt weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="720a8-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="720a8-232">Hallo sterretje dat wil zeggen, \*) **geeft aan dat alle bestanden in Hallo container of de map Hallo (dat wil zeggen, aggregateddata-gegevens/jaar = maand-2014-6 /\*)** als onderdeel van het Hallo-experiment worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="720a8-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Azure Blob-eigenschappen](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="720a8-234">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="720a8-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="720a8-235">Pijplijn met AzureMLBatchExecution activiteit met de Parameters van Web Service</span><span class="sxs-lookup"><span data-stu-id="720a8-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="720a8-236">In de Hallo hierboven JSON-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="720a8-236">In hello above JSON example:</span></span>

* <span data-ttu-id="720a8-237">Hallo geïmplementeerd in Azure Machine Learning Web service een lezer en een writer module tooread/gegevens schrijven van gebruikt / tooan Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="720a8-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="720a8-238">Deze webservice beschrijft Hallo na vier parameters: servernaam, databasenaam, servergebruikersnaam en wachtwoord voor gebruikersaccount Server-Database.</span><span class="sxs-lookup"><span data-stu-id="720a8-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="720a8-239">Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="720a8-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="720a8-240">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="720a8-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="720a8-241">Hallo **end** tijd is optioneel.</span><span class="sxs-lookup"><span data-stu-id="720a8-241">hello **end** time is optional.</span></span> <span data-ttu-id="720a8-242">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur.**'</span><span class="sxs-lookup"><span data-stu-id="720a8-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="720a8-243">toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="720a8-244">Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="720a8-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="720a8-245">Andere scenario's</span><span class="sxs-lookup"><span data-stu-id="720a8-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="720a8-246">Meerdere invoer is vereist</span><span class="sxs-lookup"><span data-stu-id="720a8-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="720a8-247">Als webservice Hallo meerdere invoer heeft, gebruikt u Hallo **webServiceInputs** in plaats van de eigenschap **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="720a8-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="720a8-248">Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInputs** moet ook zijn opgenomen in Hallo activiteit **invoer**.</span><span class="sxs-lookup"><span data-stu-id="720a8-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="720a8-249">In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="720a8-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="720a8-250">Hallo namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen moeten exact overeenkomen met Hallo-namen in Hallo experimenten.</span><span class="sxs-lookup"><span data-stu-id="720a8-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="720a8-251">U kunt de aanvraaglading van de steekproef Hallo bekijken op Hallo Batch uitvoering Help-pagina voor uw Azure ML-eindpunt tooverify Hallo verwacht toewijzing.</span><span class="sxs-lookup"><span data-stu-id="720a8-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="720a8-252">Web-Service vereist geen invoer</span><span class="sxs-lookup"><span data-stu-id="720a8-252">Web Service does not require an input</span></span>
<span data-ttu-id="720a8-253">Azure ML-batch uitvoering webservices gebruikte toorun geen werkstromen kan worden, bijvoorbeeld R of Python-scripts, kan die niet alle invoer vereisen.</span><span class="sxs-lookup"><span data-stu-id="720a8-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="720a8-254">Of Hallo experiment kan worden geconfigureerd met een lezer-module die u maakt een GlobalParameters niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="720a8-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="720a8-255">In dat geval Hallo AzureMLBatchExecution activiteit zou als volgt geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="720a8-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="720a8-256">Web-Service vereist geen invoer/uitvoer</span><span class="sxs-lookup"><span data-stu-id="720a8-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="720a8-257">Hello Azure ML-batch uitvoering web-service mogelijk geen webservice uitvoer geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="720a8-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="720a8-258">Er is geen webservice invoer of uitvoer in dit voorbeeld, noch een GlobalParameters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="720a8-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="720a8-259">Er is nog steeds een uitvoer die is geconfigureerd op Hallo activiteit zelf, maar er is geen opgegeven als een webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="720a8-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="720a8-260">Web-Service gebruikt en schrijfprogramma en activiteiten bij uitvoering Hallo alleen wanneer andere activiteiten zijn geslaagd</span><span class="sxs-lookup"><span data-stu-id="720a8-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="720a8-261">Hello Azure ML web service lezer en -schrijver modules mogelijk geconfigureerde toorun met of zonder eventuele GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="720a8-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="720a8-262">U kunt echter tooembed service aanroepen in een pijplijn die de gegevensset afhankelijkheden tooinvoke Hallo service gebruikt, alleen wanneer er een upstream-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="720a8-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="720a8-263">U kunt ook een andere actie activeren nadat het Hallo-batchuitvoering is voltooid met deze benadering.</span><span class="sxs-lookup"><span data-stu-id="720a8-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="720a8-264">In dat geval kunt u met behulp van activiteit in- en uitgangen, zonder een van deze als webservice in- of uitgangen Hallo-afhankelijkheden uitdrukken.</span><span class="sxs-lookup"><span data-stu-id="720a8-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="720a8-265">Hallo **takeaways** zijn:</span><span class="sxs-lookup"><span data-stu-id="720a8-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="720a8-266">Als uw experiment-eindpunt maakt gebruik van een webServiceInput: er wordt vertegenwoordigd door een blob-gegevensset en is opgenomen in de activiteitinvoer hello en Hallo webServiceInput eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="720a8-267">Anders is Hallo webServiceInput eigenschap weggelaten.</span><span class="sxs-lookup"><span data-stu-id="720a8-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="720a8-268">Als uw experiment-eindpunt maakt gebruik van webServiceOutput(s): ze worden vertegenwoordigd door de blob-gegevenssets en zijn opgenomen in de uitvoer voor activiteiten hello en in Hallo webServiceOutputs eigenschap.</span><span class="sxs-lookup"><span data-stu-id="720a8-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="720a8-269">Hallo activiteit uitvoer en webServiceOutputs met de naam van elke uitvoer in Hallo experiment Hallo zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="720a8-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="720a8-270">Anders wordt wordt de eigenschap webServiceOutputs hello weggelaten.</span><span class="sxs-lookup"><span data-stu-id="720a8-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="720a8-271">Als uw experiment eindpunt globalParameter(s) beschrijft, wordt verstrekt in de Activiteitseigenschap globalParameters Hallo als sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="720a8-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="720a8-272">Anders wordt wordt de eigenschap globalParameters hello weggelaten.</span><span class="sxs-lookup"><span data-stu-id="720a8-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="720a8-273">Hallo-sleutels zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="720a8-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="720a8-274">[Azure Data Factory-functies](data-factory-functions-variables.md) kan worden gebruikt in Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="720a8-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="720a8-275">Aanvullende gegevenssets kan worden opgenomen in Hallo in- en uitgangen activiteitseigenschappen, zonder waarnaar wordt verwezen in Hallo activiteit typeProperties.</span><span class="sxs-lookup"><span data-stu-id="720a8-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="720a8-276">Deze gegevenssets kan worden uitgevoerd segment afhankelijkheden reguleren maar anders worden genegeerd door Hallo AzureMLBatchExecution activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="720a8-277">Bijwerken van modellen Update Resource activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="720a8-278">Nadat u klaar bent met de retraining, bijwerken Hallo score berekenen voor web-service (Voorspellend experiment weergegeven als een webservice) met Hallo zojuist getrainde model met behulp van Hallo **Azure ML-Resourceactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="720a8-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="720a8-279">Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="720a8-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="720a8-280">Lezer en Writer Modules</span><span class="sxs-lookup"><span data-stu-id="720a8-280">Reader and Writer Modules</span></span>
<span data-ttu-id="720a8-281">Een veelvoorkomend scenario voor het gebruik van parameters voor Web-service is Hallo gebruik van Azure SQL en schrijfprogramma.</span><span class="sxs-lookup"><span data-stu-id="720a8-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="720a8-282">leesmodule Hello is gebruikte tooload gegevens in een experiment van data management-services buiten Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="720a8-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="720a8-283">Hallo-schrijfmodule is toosave gegevens vanuit uw experimenten in beheerservices gegevens buiten Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="720a8-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="720a8-284">Zie voor meer informatie over Azure-Blob/Azure SQL-lezer/schrijver [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="720a8-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="720a8-285">Hallo-voorbeeld in de vorige sectie Hallo gebruikt hello Azure Blob-lezer en Azure Blob-schrijver.</span><span class="sxs-lookup"><span data-stu-id="720a8-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="720a8-286">Deze sectie beschrijft het gebruik van Azure SQL-reader en Azure SQL writer.</span><span class="sxs-lookup"><span data-stu-id="720a8-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="720a8-287">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="720a8-287">Frequently asked questions</span></span>
<span data-ttu-id="720a8-288">**V:** ik heb meerdere bestanden die worden gegenereerd door mijn pijplijnen big data.</span><span class="sxs-lookup"><span data-stu-id="720a8-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="720a8-289">Kan ik Hallo AzureMLBatchExecution activiteit toowork op alle Hallo-bestanden gebruiken?</span><span class="sxs-lookup"><span data-stu-id="720a8-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="720a8-290">**A:** Ja.</span><span class="sxs-lookup"><span data-stu-id="720a8-290">**A:** Yes.</span></span> <span data-ttu-id="720a8-291">Zie Hallo **met een lezer module tooread gegevens uit meerdere bestanden in Azure Blob** sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="720a8-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="720a8-292">Score berekenen voor Azure ML-Batch-activiteit</span><span class="sxs-lookup"><span data-stu-id="720a8-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="720a8-293">Als u van Hallo gebruikmaakt **AzureMLBatchScoring** activiteit toointegrate met Azure Machine Learning, wordt aangeraden dat u Hallo meest recente **AzureMLBatchExecution** activiteit.</span><span class="sxs-lookup"><span data-stu-id="720a8-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="720a8-294">Hallo AzureMLBatchExecution activiteit is geïntroduceerd in Hallo augustus 2015-release van Azure SDK en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="720a8-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="720a8-295">Als u toocontinue hello AzureMLBatchScoring activiteit wilt, blijven lezen via deze sectie.</span><span class="sxs-lookup"><span data-stu-id="720a8-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="720a8-296">Azure ML-Batchscoreberekening activiteit voor het gebruik van Azure Storage voor invoer/uitvoer</span><span class="sxs-lookup"><span data-stu-id="720a8-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="720a8-297">Parameters voor Web-Service</span><span class="sxs-lookup"><span data-stu-id="720a8-297">Web Service Parameters</span></span>
<span data-ttu-id="720a8-298">toospecify waarden voor de Web service-parameters, Voeg een **typeProperties** sectie toohello **AzureMLBatchScoringActivty** sectie in Hallo pijplijn JSON zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="720a8-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="720a8-299">U kunt ook [Data Factory functies](data-factory-functions-variables.md) in het doorgeven van waarden voor Hallo Web serviceparameters zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="720a8-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="720a8-300">Hallo Web serviceparameters zijn hoofdlettergevoelig, dus zorg ervoor dat Hallo-namen die u opgeeft in de activiteit Hallo JSON overeenkomen Hallo waarden die worden weergegeven door het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="720a8-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="720a8-301">Zie ook</span><span class="sxs-lookup"><span data-stu-id="720a8-301">See Also</span></span>
* [<span data-ttu-id="720a8-302">Azure blogbericht: aan de slag met Azure Data Factory en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="720a8-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
