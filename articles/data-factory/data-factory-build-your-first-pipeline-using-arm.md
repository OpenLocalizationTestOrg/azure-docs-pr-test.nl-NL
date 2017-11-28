---
title: aaaBuild uw eerste gegevensfactory (Resource Manager-sjabloon) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn op basis van een Azure Resource Manager-sjabloon.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="0f16a-103">Zelfstudie: bouw uw eerste Azure-gegevensfactory op basis van een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0f16a-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f16a-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="0f16a-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="0f16a-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0f16a-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="0f16a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f16a-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="0f16a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f16a-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="0f16a-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0f16a-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="0f16a-109">REST API</span><span class="sxs-lookup"><span data-stu-id="0f16a-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="0f16a-110">In dit artikel gebruikt u een Azure Resource Manager-sjabloon toocreate uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="0f16a-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="0f16a-111">toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="0f16a-112">Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="0f16a-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="0f16a-113">Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer.</span><span class="sxs-lookup"><span data-stu-id="0f16a-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="0f16a-114">Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0f16a-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f16a-115">Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="0f16a-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="0f16a-116">Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0f16a-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="0f16a-117">Hallo-pijplijn in deze zelfstudie is slechts één activiteit van het type: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="0f16a-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="0f16a-118">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="0f16a-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0f16a-119">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="0f16a-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="0f16a-120">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f16a-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0f16a-121">Prerequisites</span></span>
* <span data-ttu-id="0f16a-122">Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="0f16a-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="0f16a-123">Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0f16a-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="0f16a-124">Zie [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn over Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="0f16a-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="0f16a-125">In deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="0f16a-125">In this tutorial</span></span>
| <span data-ttu-id="0f16a-126">Entiteit</span><span class="sxs-lookup"><span data-stu-id="0f16a-126">Entity</span></span> | <span data-ttu-id="0f16a-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0f16a-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f16a-128">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="0f16a-128">Azure Storage linked service</span></span> |<span data-ttu-id="0f16a-129">Uw Azure Storage-account toohello data factory gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0f16a-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="0f16a-130">Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="0f16a-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="0f16a-131">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="0f16a-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="0f16a-132">Een gegevensfactory op aanvraag HDInsight-cluster toohello koppelingen.</span><span class="sxs-lookup"><span data-stu-id="0f16a-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="0f16a-133">Hallo-cluster wordt automatisch gemaakt voor uw tooprocess gegevens en wordt verwijderd nadat het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0f16a-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="0f16a-134">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-134">Azure Blob input dataset</span></span> |<span data-ttu-id="0f16a-135">Verwijst toohello gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="0f16a-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="0f16a-136">Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset geeft Hallo-container, map en bestandsnaam in Hallo opslag die Hallo invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="0f16a-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="0f16a-137">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-137">Azure Blob output dataset</span></span> |<span data-ttu-id="0f16a-138">Verwijst toohello gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="0f16a-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="0f16a-139">Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset bevat Hallo-container, map en bestandsnaam in Hallo opslag van uitvoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="0f16a-140">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="0f16a-140">Data pipeline</span></span> |<span data-ttu-id="0f16a-141">Hallo pijplijn heeft een activiteit van het type HDInsightHive die Hallo invoergegevensset verbruikt en Hallo uitvoergegevensset produceert.</span><span class="sxs-lookup"><span data-stu-id="0f16a-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="0f16a-142">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="0f16a-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0f16a-143">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="0f16a-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0f16a-144">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0f16a-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="0f16a-145">In deze zelfstudie maakt u een pijplijn met één activiteit (Hive-activiteit).</span><span class="sxs-lookup"><span data-stu-id="0f16a-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="0f16a-146">Hallo volgende sectie bevat Hallo voltooid Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten, zodat u snel via Hallo zelfstudie en test Hallo-sjabloon uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="0f16a-147">toounderstand hoe elke entiteit Data Factory is gedefinieerd, Zie [Data Factory-entiteiten in de sjabloon Hallo](#data-factory-entities-in-the-template) sectie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="0f16a-148">JSON-sjabloon voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="0f16a-148">Data Factory JSON template</span></span>
<span data-ttu-id="0f16a-149">Hallo op het hoogste niveau Resource Manager-sjabloon voor het definiëren van een gegevensfactory is:</span><span class="sxs-lookup"><span data-stu-id="0f16a-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
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
<span data-ttu-id="0f16a-150">Maak een JSON-bestand met de naam **ADFTutorialARM.json** in **C:\ADFGetStarted** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="0f16a-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
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
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="0f16a-151">In [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Zelfstudie: met behulp van een Azure Resource Manager-sjabloon een pijplijn maken met een kopieerbewerking) vindt u een ander voorbeeld van een Resource Manager-sjabloon voor het maken van een Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="0f16a-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="0f16a-152">JSON-bestand met parameters</span><span class="sxs-lookup"><span data-stu-id="0f16a-152">Parameters JSON</span></span>
<span data-ttu-id="0f16a-153">Maak een JSON-bestand met de naam **ADFTutorialARM Parameters.json** die parameters voor hello Azure Resource Manager-sjabloon bevat.</span><span class="sxs-lookup"><span data-stu-id="0f16a-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0f16a-154">Geef Hallo naam en sleutel van uw Azure Storage-account voor Hallo **storageAccountName** en **storageAccountKey** parameters in dit parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="0f16a-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="0f16a-155">Wellicht hebt u afzonderlijke parameter JSON-bestanden voor ontwikkeling, testen en productieomgevingen die u met gebruiken kunt Hallo dezelfde Data Factory JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="0f16a-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="0f16a-156">U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="0f16a-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="0f16a-157">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="0f16a-157">Create data factory</span></span>
1. <span data-ttu-id="0f16a-158">Start **Azure PowerShell** en Voer Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0f16a-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="0f16a-159">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0f16a-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="0f16a-160">Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f16a-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="0f16a-161">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f16a-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="0f16a-162">Dit abonnement moet hetzelfde zijn als u die wordt gebruikt bij de Azure-portal Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="0f16a-163">Voer Hallo na de opdracht toodeploy Data Factory-entiteiten Hallo Resource Manager-sjabloon die u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="0f16a-164">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="0f16a-164">Monitor pipeline</span></span>
1. <span data-ttu-id="0f16a-165">Na het aanmelden toohello [Azure-portal](https://portal.azure.com/), klikt u op **Bladeren** en selecteer **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="0f16a-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="0f16a-166">![Bladeren -> Gegevensfactory's](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="0f16a-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="0f16a-167">In Hallo **Gegevensfactory** blade, klikt u op Hallo gegevensfactory (**TutorialFactoryARM**) u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="0f16a-168">In Hallo **Data Factory** blade van uw gegevensfactory klikt u op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="0f16a-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="0f16a-170">In Hallo **diagramweergave**, ziet u een overzicht van Hallo pijplijnen en gegevenssets gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="0f16a-172">Dubbelklik in de diagramweergave hello, op Hallo gegevensset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="0f16a-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="0f16a-173">U ziet dat Hallo-segment dat momenteel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="0f16a-175">Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="0f16a-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="0f16a-176">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="0f16a-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="0f16a-177">Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="0f16a-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="0f16a-179">Wanneer Hallo segment is in **gereed** staat, controleert u Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="0f16a-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="0f16a-180">Zie [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor instructies over hoe toouse hello Azure portal-blades toomonitor Hallo pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="0f16a-181">U kunt uw gegevenspijplijnen ook Monitor and Manage App toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0f16a-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="0f16a-182">Zie [bewaken en beheren van de App voor bewaking met Azure Data Factory-pijplijnen](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="0f16a-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0f16a-183">Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="0f16a-184">Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="0f16a-185">Data Factory-entiteiten in Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0f16a-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="0f16a-186">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="0f16a-186">Define data factory</span></span>
<span data-ttu-id="0f16a-187">U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="0f16a-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="0f16a-188">Hallo dataFactoryName wordt gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="0f16a-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="0f16a-189">Er is een unieke tekenreeks die is gebaseerd op Hallo resource-ID.</span><span class="sxs-lookup"><span data-stu-id="0f16a-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="0f16a-190">Data Factory-entiteiten definiëren</span><span class="sxs-lookup"><span data-stu-id="0f16a-190">Defining Data Factory entities</span></span>
<span data-ttu-id="0f16a-191">Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo:</span><span class="sxs-lookup"><span data-stu-id="0f16a-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="0f16a-192">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="0f16a-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="0f16a-193">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="0f16a-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="0f16a-194">De Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="0f16a-195">De Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="0f16a-196">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="0f16a-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="0f16a-197">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="0f16a-197">Azure Storage linked service</span></span>
<span data-ttu-id="0f16a-198">U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="0f16a-199">Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="0f16a-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="0f16a-200">Hallo **connectionString** maakt gebruik van parameters storageAccountName en storageAccountKey Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="0f16a-201">Hallo-waarden voor deze parameters doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0f16a-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="0f16a-202">Hallo definitie variabelen ook worden gebruikt: azureStroageLinkedService en dataFactoryName in Hallo sjabloon worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0f16a-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="0f16a-203">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="0f16a-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="0f16a-204">Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artikel voor meer informatie over de JSON-eigenschappen die toodefine een gekoppelde HDInsight on demand-service.</span><span class="sxs-lookup"><span data-stu-id="0f16a-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="0f16a-205">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="0f16a-205">Note hello following points:</span></span> 

* <span data-ttu-id="0f16a-206">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello hierboven JSON.</span><span class="sxs-lookup"><span data-stu-id="0f16a-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="0f16a-207">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="0f16a-208">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0f16a-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0f16a-209">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="0f16a-210">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="0f16a-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="0f16a-211">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0f16a-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="0f16a-212">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="0f16a-212">This behavior is by design.</span></span> <span data-ttu-id="0f16a-213">Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment toobe verwerkt moet, tenzij er een bestaand livecluster is (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0f16a-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="0f16a-214">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="0f16a-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0f16a-215">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="0f16a-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="0f16a-216">Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '.</span><span class="sxs-lookup"><span data-stu-id="0f16a-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="0f16a-217">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="0f16a-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="0f16a-218">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="0f16a-219">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-219">Azure blob input dataset</span></span>
<span data-ttu-id="0f16a-220">U opgeven Hallo namen van de blob-container, map en -bestand met de invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="0f16a-221">Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0f16a-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="0f16a-222">Hallo volgende parameters zijn gedefinieerd in de parameter-sjabloon maakt gebruik van deze definitie: blobContainer, inputBlobFolder, en inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="0f16a-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0f16a-223">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="0f16a-223">Azure Blob output dataset</span></span>
<span data-ttu-id="0f16a-224">U opgeven Hallo namen van blob-container en map waarin de uitvoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="0f16a-225">Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0f16a-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
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

<span data-ttu-id="0f16a-226">Hallo na gedefinieerde parameters in Hallo parameter sjabloon maakt gebruik van deze definitie: blobContainer en outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="0f16a-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="0f16a-227">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="0f16a-227">Data pipeline</span></span>
<span data-ttu-id="0f16a-228">U definieert een pijplijn waarmee gegevens worden omgezet door een Hive-script uit te voeren in een Azure HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0f16a-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="0f16a-229">Zie [pijplijn-JSON](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0f16a-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="0f16a-230">Hallo-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="0f16a-230">Reuse hello template</span></span>
<span data-ttu-id="0f16a-231">In de zelfstudie hello, moet u een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f16a-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="0f16a-232">toouse Hallo dezelfde sjabloon toodeploy Data Factory-entiteiten toodifferent omgevingen, u een parameterbestand voor elke omgeving maken en deze gebruiken bij het implementeren van toothat-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0f16a-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="0f16a-233">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0f16a-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="0f16a-234">U ziet dat de eerste opdracht Hallo maakt gebruik van parameterbestand voor Hallo-ontwikkelomgeving, tweede één voor Hallo testomgeving en derde één voor productie-omgeving Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f16a-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="0f16a-235">U kunt ook opnieuw gebruiken Hallo sjabloon tooperform herhaalde taken.</span><span class="sxs-lookup"><span data-stu-id="0f16a-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="0f16a-236">Bijvoorbeeld, u moet toocreate veel data Factory met een of meer pijplijnen die implementeren Hallo dezelfde logica maar elke data factory maakt gebruik van andere Azure storage en Azure SQL Database-accounts.</span><span class="sxs-lookup"><span data-stu-id="0f16a-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="0f16a-237">In dit scenario gebruikt u Hallo dezelfde sjabloon in Hallo bestanden dezelfde omgeving (dev-, test- of productie) met de andere parameter toocreate data Factory.</span><span class="sxs-lookup"><span data-stu-id="0f16a-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="0f16a-238">Resource Manager-sjabloon voor het maken van een gateway</span><span class="sxs-lookup"><span data-stu-id="0f16a-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="0f16a-239">Hier volgt een voorbeeld Resource Manager-sjabloon voor het maken van een logische gateway in Hallo terug.</span><span class="sxs-lookup"><span data-stu-id="0f16a-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="0f16a-240">Een gateway installeren op uw lokale computer of virtuele machine van Azure IaaS en Hallo gateway registreren met behulp van een sleutel Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="0f16a-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="0f16a-241">Zie [Gegevens verplaatsen tussen on-premises en de cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0f16a-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="0f16a-242">Met deze sjabloon maakt u een gegevensfactory met de naam GatewayUsingArmDF, met een gateway met de naam GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="0f16a-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0f16a-243">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0f16a-243">See Also</span></span>
| <span data-ttu-id="0f16a-244">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="0f16a-244">Topic</span></span> | <span data-ttu-id="0f16a-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0f16a-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0f16a-246">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="0f16a-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0f16a-247">In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="0f16a-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0f16a-248">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="0f16a-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0f16a-249">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0f16a-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0f16a-250">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0f16a-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0f16a-251">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="0f16a-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="0f16a-252">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="0f16a-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="0f16a-253">Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="0f16a-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

