---
title: Uw eerste gegevensfactory bouwen (Resource Manager-sjabloon) | Microsoft Docs
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="eb3df-103">Zelfstudie: bouw uw eerste Azure-gegevensfactory op basis van een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="eb3df-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb3df-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="eb3df-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="eb3df-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="eb3df-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="eb3df-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb3df-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="eb3df-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb3df-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="eb3df-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="eb3df-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="eb3df-109">REST API</span><span class="sxs-lookup"><span data-stu-id="eb3df-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="eb3df-110">In dit artikel gebruikt u een Azure Resource Manager-sjabloon om uw eerste Azure-gegevensfactory te maken.</span><span class="sxs-lookup"><span data-stu-id="eb3df-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="eb3df-111">Als u de zelfstudie wilt volgen met andere hulpprogramma's/SDK's, selecteert u een van de opties uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="eb3df-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="eb3df-112">De pijplijn in deze zelfstudie heeft één activiteit: **HDInsight-componentactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="eb3df-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="eb3df-113">Deze activiteit voert een Hive-script uit op een Azure HDInsight-cluster dat invoergegevens transformeert om uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="eb3df-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="eb3df-114">De pijplijn is gepland on één keer per maand tussen de opgegeven begin- en eindtijd te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eb3df-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb3df-115">Met de gegevenspijplijn in deze zelfstudie worden invoergegevens getransformeerd in uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="eb3df-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="eb3df-116">Zie [Zelfstudie: gegevens kopiëren van Blob Storage naar SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor informatie over het kopiëren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="eb3df-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="eb3df-117">De pijplijn in deze zelfstudie heeft maar één activiteit van het type: HDInsight-componentactiviteit.</span><span class="sxs-lookup"><span data-stu-id="eb3df-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="eb3df-118">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="eb3df-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="eb3df-119">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="eb3df-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="eb3df-120">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb3df-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb3df-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eb3df-121">Prerequisites</span></span>
* <span data-ttu-id="eb3df-122">Lees het artikel [Overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="eb3df-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="eb3df-123">Volg de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/overview) om de meest recente versie van Azure PowerShell te installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="eb3df-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="eb3df-124">Zie [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) (Azure Resource Manager-sjablonen samenstellen) voor meer informatie over Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="eb3df-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="eb3df-125">In deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="eb3df-125">In this tutorial</span></span>
| <span data-ttu-id="eb3df-126">Entiteit</span><span class="sxs-lookup"><span data-stu-id="eb3df-126">Entity</span></span> | <span data-ttu-id="eb3df-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="eb3df-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb3df-128">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="eb3df-128">Azure Storage linked service</span></span> |<span data-ttu-id="eb3df-129">Koppelt uw Azure Storage-account aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="eb3df-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="eb3df-130">Het Azure Storage-account bevat de in- en uitvoergegevens van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="eb3df-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="eb3df-131">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="eb3df-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="eb3df-132">Koppelt een HDInsight-cluster op aanvraag aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="eb3df-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="eb3df-133">Het cluster wordt automatisch voor u gemaakt om gegevens te verwerken en wordt verwijderd nadat de verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eb3df-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="eb3df-134">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-134">Azure Blob input dataset</span></span> |<span data-ttu-id="eb3df-135">Verwijst naar de gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="eb3df-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="eb3df-136">De gekoppelde service verwijst naar een Azure Storage-account en in de Azure Blob-gegevensset vindt u de container, map en bestandsnaam in de opslag die de invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="eb3df-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="eb3df-137">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-137">Azure Blob output dataset</span></span> |<span data-ttu-id="eb3df-138">Verwijst naar de gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="eb3df-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="eb3df-139">De gekoppelde service verwijst naar een Azure Storage-account en in de Azure Blob-gegevensset vindt u de container, map en bestandsnaam in de opslag die de uitvoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="eb3df-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="eb3df-140">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="eb3df-140">Data pipeline</span></span> |<span data-ttu-id="eb3df-141">De gegevenspijplijn bevat één activiteit van het type HDInsightHive die de invoergegevensset gebruikt en de uitvoergegevensset produceert.</span><span class="sxs-lookup"><span data-stu-id="eb3df-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="eb3df-142">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="eb3df-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="eb3df-143">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="eb3df-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="eb3df-144">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="eb3df-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="eb3df-145">In deze zelfstudie maakt u een pijplijn met één activiteit (Hive-activiteit).</span><span class="sxs-lookup"><span data-stu-id="eb3df-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="eb3df-146">In de volgende sectie vindt u de volledige Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten zodat u de zelfstudie snel kunt doorlopen en de sjabloon kunt testen.</span><span class="sxs-lookup"><span data-stu-id="eb3df-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="eb3df-147">Raadpleeg de sectie [Data Factory-entiteiten in de sjabloon](#data-factory-entities-in-the-template) om te lezen hoe elke Data Factory-entiteit wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eb3df-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="eb3df-148">JSON-sjabloon voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="eb3df-148">Data Factory JSON template</span></span>
<span data-ttu-id="eb3df-149">De Resource Manager-sjabloon op het hoogste niveau voor het definiëren van een gegevensfactory is als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb3df-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="eb3df-150">Maak een JSON-bestand met de naam **ADFTutorialARM.json** in de map **C:\ADFGetStarted**. Geef het bestand de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="eb3df-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="eb3df-151">In [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Zelfstudie: met behulp van een Azure Resource Manager-sjabloon een pijplijn maken met een kopieerbewerking) vindt u een ander voorbeeld van een Resource Manager-sjabloon voor het maken van een Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="eb3df-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="eb3df-152">JSON-bestand met parameters</span><span class="sxs-lookup"><span data-stu-id="eb3df-152">Parameters JSON</span></span>
<span data-ttu-id="eb3df-153">Maak een JSON-bestand met de naam **ADFTutorialARM-Parameters.json** dat parameters voor de Azure Resource Manager-sjabloon bevat.</span><span class="sxs-lookup"><span data-stu-id="eb3df-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="eb3df-154">Geef de naam en sleutel van uw Azure Storage-account op voor de parameters **storageAccountName** en **storageAccountKey** in dit parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="eb3df-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="eb3df-155">Mogelijk beschikt u over afzonderlijke JSON-bestanden met parameters voor ontwikkel-, test- en productieomgevingen die u met dezelfde JSON-sjabloon voor Data Factory kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb3df-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="eb3df-156">U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="eb3df-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="eb3df-157">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="eb3df-157">Create data factory</span></span>
1. <span data-ttu-id="eb3df-158">Open **Azure PowerShell** en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="eb3df-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="eb3df-159">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eb3df-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="eb3df-160">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="eb3df-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="eb3df-161">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="eb3df-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="eb3df-162">Dit moet hetzelfde abonnement zijn als het abonnement dat u in de Azure Portal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="eb3df-163">Voer de volgende opdracht uit om Data Factory-entiteiten te implementeren met behulp van het Resource Manager-sjabloon dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="eb3df-164">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="eb3df-164">Monitor pipeline</span></span>
1. <span data-ttu-id="eb3df-165">Wanneer u zich hebt aangemeld bij [Azure Portal](https://portal.azure.com/), klikt u op **Bladeren** en selecteert u **Gegevensfactory’s**.</span><span class="sxs-lookup"><span data-stu-id="eb3df-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="eb3df-166">![Bladeren -> Gegevensfactory's](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="eb3df-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="eb3df-167">Klik op de blade **Gegevensfactory’s** op de gegevensfactory (**TutorialFactoryARM**) die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="eb3df-168">Klik op de blade **Gegevensfactory** van uw gegevensfactory op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="eb3df-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="eb3df-170">In de **diagramweergave** ziet u een overzicht van de pijplijnen en gegevenssets die voor deze zelfstudie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="eb3df-172">Dubbelklik in de diagramweergave op de gegevensset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="eb3df-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="eb3df-173">U ziet het segment dat momenteel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-173">You see that the slice that is currently being processed.</span></span>
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="eb3df-175">Als het verwerken is voltooid, ziet u dat het segment de status **Gereed** heeft.</span><span class="sxs-lookup"><span data-stu-id="eb3df-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="eb3df-176">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="eb3df-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="eb3df-177">Daarom kunt u ervan uitgaan dat het **ongeveer 30 minuten** duurt voordat het segment in de pijplijn is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="eb3df-179">Wanneer het segment de status **Gereed** heeft, controleert u de map **partitioneddata** in de container **adfgetstarted** in uw blobopslag voor de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="eb3df-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="eb3df-180">Zie [Gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor instructies over het gebruik van Azure Portal-blades om de pijplijn en gegevenssets te bewaken die u tijdens deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="eb3df-181">U kunt ook de app voor bewaking en beheer gebruiken om uw gegevenspijplijnen te bewaken.</span><span class="sxs-lookup"><span data-stu-id="eb3df-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="eb3df-182">Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb3df-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="eb3df-183">Het invoerbestand wordt verwijderd zodra het segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="eb3df-184">Als u het segment dus opnieuw wilt uitvoeren of als u de zelfstudie opnieuw wilt doorlopen, uploadt u het invoerbestand (input.log) naar de map met invoergegevens van de container adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="eb3df-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="eb3df-185">Data Factory-entiteiten in de sjabloon</span><span class="sxs-lookup"><span data-stu-id="eb3df-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="eb3df-186">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="eb3df-186">Define data factory</span></span>
<span data-ttu-id="eb3df-187">U definieert een gegevensfactory in de Resource Manager-sjabloon zoals in het volgende voorbeeld wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="eb3df-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="eb3df-188">De variabele dataFactoryName wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="eb3df-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="eb3df-189">Het is een unieke tekenreeks op basis van de resourcegroep-id.</span><span class="sxs-lookup"><span data-stu-id="eb3df-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="eb3df-190">Data Factory-entiteiten definiëren</span><span class="sxs-lookup"><span data-stu-id="eb3df-190">Defining Data Factory entities</span></span>
<span data-ttu-id="eb3df-191">De volgende Data Factory-entiteiten worden in de JSON-sjabloon gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="eb3df-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="eb3df-192">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="eb3df-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="eb3df-193">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="eb3df-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="eb3df-194">De Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="eb3df-195">De Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="eb3df-196">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="eb3df-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="eb3df-197">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="eb3df-197">Azure Storage linked service</span></span>
<span data-ttu-id="eb3df-198">In deze sectie geeft u de naam en sleutel van uw Azure Storage-account op.</span><span class="sxs-lookup"><span data-stu-id="eb3df-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="eb3df-199">Zie [Een gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="eb3df-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="eb3df-200">De tekenreeks **connectionString** maakt gebruik van de parameters storageAccountName en storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="eb3df-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="eb3df-201">De waarden voor deze parameters worden doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="eb3df-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="eb3df-202">De definitie maakt ook gebruik van variabelen: azureStorageLinkedService en dataFactoryName die zijn gedefinieerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="eb3df-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="eb3df-203">Een gekoppelde HDInsight-service op aanvraag</span><span class="sxs-lookup"><span data-stu-id="eb3df-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="eb3df-204">Zie het artikel [Compute linked services (Gekoppelde services verwerken)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde HDInsight-service op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="eb3df-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="eb3df-205">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="eb3df-205">Note the following points:</span></span> 

* <span data-ttu-id="eb3df-206">Met de bovenstaande JSON maakt Data Factory voor u een HDInsight-cluster **op basis van Linux**.</span><span class="sxs-lookup"><span data-stu-id="eb3df-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="eb3df-207">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb3df-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="eb3df-208">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="eb3df-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="eb3df-209">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb3df-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="eb3df-210">Het HDInsight-cluster maakt een **standaardcontainer** in de blobopslag die u hebt opgegeven in de JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="eb3df-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="eb3df-211">HDInsight verwijdert deze container niet wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="eb3df-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="eb3df-212">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="eb3df-212">This behavior is by design.</span></span> <span data-ttu-id="eb3df-213">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment moet worden verwerkt, tenzij er een bestaand livecluster is (**timeToLive**). Het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="eb3df-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="eb3df-214">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="eb3df-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="eb3df-215">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="eb3df-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="eb3df-216">De namen van deze containers worden als volgt opgebouwd: adf**naamvanuwgegevensfactory**-**naamvangekoppeldeservice**-datum-/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="eb3df-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="eb3df-217">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om containers in uw Azure-blobopslag te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="eb3df-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="eb3df-218">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb3df-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="eb3df-219">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-219">Azure blob input dataset</span></span>
<span data-ttu-id="eb3df-220">U geeft de namen van de blobcontainer, map en het bestand met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="eb3df-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="eb3df-221">Zie [Eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="eb3df-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="eb3df-222">Deze definitie maakt gebruik van de volgende parameters die in de parametersjabloon zijn gedefinieerd: blobContainer, inputBlobFolder en inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="eb3df-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="eb3df-223">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="eb3df-223">Azure Blob output dataset</span></span>
<span data-ttu-id="eb3df-224">U geeft de namen van de blobcontainer en de map met de uitvoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="eb3df-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="eb3df-225">Zie [Eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="eb3df-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="eb3df-226">Deze definitie maakt gebruik van de volgende parameters die in de parametersjabloon zijn gedefinieerd: blobContainer en outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="eb3df-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="eb3df-227">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="eb3df-227">Data pipeline</span></span>
<span data-ttu-id="eb3df-228">U definieert een pijplijn waarmee gegevens worden omgezet door een Hive-script uit te voeren in een Azure HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="eb3df-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="eb3df-229">Zie [JSON-bestand voor een pijplijn](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt voor het definiëren van een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="eb3df-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="eb3df-230">De sjabloon hergebruiken</span><span class="sxs-lookup"><span data-stu-id="eb3df-230">Reuse the template</span></span>
<span data-ttu-id="eb3df-231">U hebt in de zelfstudie een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb3df-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="eb3df-232">Als u dezelfde sjabloon wilt gebruiken voor het implementeren van Data Factory-entiteiten in verschillende omgevingen, maakt u een parameterbestand voor elke omgeving en gebruikt u dit bij het implementeren in die omgeving.</span><span class="sxs-lookup"><span data-stu-id="eb3df-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="eb3df-233">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eb3df-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="eb3df-234">De eerste opdracht maakt gebruik van het parameterbestand voor de ontwikkelomgeving, de tweede voor de testomgeving en de derde voor de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="eb3df-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="eb3df-235">U kunt de sjabloon ook hergebruiken om herhaalde taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="eb3df-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="eb3df-236">U moet bijvoorbeeld veel gegevensfactory's maken met een of meer pijplijnen die dezelfde logica implementeren, maar elke gegevensfactory maakt gebruik van andere Azure Storage- en Azure SQL Database-accounts.</span><span class="sxs-lookup"><span data-stu-id="eb3df-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="eb3df-237">In dit scenario gebruikt u dezelfde sjabloon in dezelfde omgeving (voor het ontwikkelen, testen of de productie) met andere parameterbestanden om de gegevensfactory's te maken.</span><span class="sxs-lookup"><span data-stu-id="eb3df-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="eb3df-238">Resource Manager-sjabloon voor het maken van een gateway</span><span class="sxs-lookup"><span data-stu-id="eb3df-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="eb3df-239">Hier volgt een Resource Manager-voorbeeldsjabloon voor het op de achtergrond maken van een logische gateway.</span><span class="sxs-lookup"><span data-stu-id="eb3df-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="eb3df-240">Installeer een gateway op uw on-premises computer of virtuele Azure IaaS-machine en registreer de gateway met een sleutel bij de Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="eb3df-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="eb3df-241">Zie [Gegevens verplaatsen tussen on-premises en de cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb3df-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="eb3df-242">Met deze sjabloon maakt u een gegevensfactory met de naam GatewayUsingArmDF, met een gateway met de naam GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="eb3df-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="eb3df-243">Zie ook</span><span class="sxs-lookup"><span data-stu-id="eb3df-243">See Also</span></span>
| <span data-ttu-id="eb3df-244">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="eb3df-244">Topic</span></span> | <span data-ttu-id="eb3df-245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="eb3df-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="eb3df-246">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="eb3df-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="eb3df-247">Met behulp van dit artikel krijgt u inzicht in de pijplijnen en activiteiten in Azure Data Factory en in de wijze waarop u deze kunt gebruiken om end-to-end gegevensgestuurde werkstromen te maken voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="eb3df-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="eb3df-248">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="eb3df-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="eb3df-249">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="eb3df-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="eb3df-250">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="eb3df-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="eb3df-251">In dit artikel wordt uitleg gegeven over de plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="eb3df-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="eb3df-252">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="eb3df-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="eb3df-253">In dit artikel wordt beschreven hoe u pijplijnen bewaakt en beheert en hoe u fouten hierin oplost met de app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="eb3df-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

