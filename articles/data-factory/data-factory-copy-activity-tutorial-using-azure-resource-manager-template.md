---
title: 'Zelfstudie: een pijplijn maken met het Resource Manager-sjabloon | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met behulp van een Azure Resource Manager-sjabloon. Met deze pijplijn worden gegevens vanuit een Azure-blobopslag gekopieerd naar een Azure SQL-database.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="96172-104">Zelfstudie: een Azure Resource Manager-sjabloon gebruiken voor het maken van een Data Factory-pijplijn om gegevens te kopiëren</span><span class="sxs-lookup"><span data-stu-id="96172-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96172-105">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="96172-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="96172-106">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="96172-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="96172-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="96172-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="96172-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96172-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="96172-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96172-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="96172-110">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="96172-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="96172-111">REST API</span><span class="sxs-lookup"><span data-stu-id="96172-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="96172-112">.NET-API</span><span class="sxs-lookup"><span data-stu-id="96172-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="96172-113">In deze zelfstudie wordt uitgelegd hoe u een Azure Resource Manager-sjabloon maakt om een Azure-gegevensfactory te maken.</span><span class="sxs-lookup"><span data-stu-id="96172-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="96172-114">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="96172-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="96172-115">Er worden geen invoergegevens mee getransformeerd in uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="96172-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="96172-116">Zie [Zelfstudie: een pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="96172-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="96172-117">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="96172-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="96172-118">De kopieeractiviteit in Data Factory kopieert gegevens uit een ondersteund gegevensarchief naar een ondersteund sinkgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="96172-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="96172-119">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="96172-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="96172-120">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="96172-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="96172-121">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="96172-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="96172-122">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="96172-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="96172-123">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="96172-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="96172-124">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="96172-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="96172-125">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="96172-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="96172-126">Zie [Zelfstudie: een pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="96172-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="96172-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="96172-127">Prerequisites</span></span>
* <span data-ttu-id="96172-128">Neem [Overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) door en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="96172-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="96172-129">Volg de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/overview) om de meest recente versie van Azure PowerShell te installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="96172-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="96172-130">In deze zelfstudie gebruikt u PowerShell om Data Factory-entiteiten te implementeren.</span><span class="sxs-lookup"><span data-stu-id="96172-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="96172-131">Zie [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) (Azure Resource Manager-sjablonen samenstellen) voor meer informatie over Azure Resource Manager-sjablonen (optioneel).</span><span class="sxs-lookup"><span data-stu-id="96172-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="96172-132">In deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="96172-132">In this tutorial</span></span>
<span data-ttu-id="96172-133">In deze zelfstudie maakt u een gegevensfactory met de volgende Data Factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="96172-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="96172-134">Entiteit</span><span class="sxs-lookup"><span data-stu-id="96172-134">Entity</span></span> | <span data-ttu-id="96172-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="96172-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96172-136">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="96172-136">Azure Storage linked service</span></span> |<span data-ttu-id="96172-137">Koppelt uw Azure Storage-account aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="96172-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="96172-138">Azure Storage is de brongegevensopslag en Azure SQL Database de opvanggegevensopslag voor de kopieerbewerking in de handleiding.</span><span class="sxs-lookup"><span data-stu-id="96172-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="96172-139">Het geeft de opslagaccount aan die de invoergegevens voor de kopieerbewerking bevat.</span><span class="sxs-lookup"><span data-stu-id="96172-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="96172-140">Een gekoppelde Azure SQL Database-service</span><span class="sxs-lookup"><span data-stu-id="96172-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="96172-141">Koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="96172-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="96172-142">Het geeft de Azure SQL-database aan die de uitvoergegevens voor de kopieerbewerking bevat.</span><span class="sxs-lookup"><span data-stu-id="96172-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="96172-143">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-143">Azure Blob input dataset</span></span> |<span data-ttu-id="96172-144">Verwijst naar de gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="96172-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="96172-145">De gekoppelde service verwijst naar een Azure Storage-account en in de Azure Blob-gegevensset vindt u de container, map en bestandsnaam in de opslag die de invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="96172-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="96172-146">Azure SQL-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-146">Azure SQL output dataset</span></span> |<span data-ttu-id="96172-147">Verwijst naar de gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="96172-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="96172-148">De gekoppelde Azure SQL-service verwijst naar een Azure SQL-server en de Azure SQL-gegevensset bevat de naam van de tabel met de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="96172-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="96172-149">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="96172-149">Data pipeline</span></span> |<span data-ttu-id="96172-150">De pijplijn heeft één activiteit van het type Kopiëren waarbij de Azure Blob-gegevensset als invoer en de Azure SQL-gegevensset als uitvoer wordt genomen.</span><span class="sxs-lookup"><span data-stu-id="96172-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="96172-151">Met de kopieerbewerking worden gegevens van een Azure-blob naar een tabel in de Azure SQL-database gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="96172-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="96172-152">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="96172-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="96172-153">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="96172-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="96172-154">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="96172-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="96172-155">In deze zelfstudie maakt u een pijplijn met één activiteit (kopiëren).</span><span class="sxs-lookup"><span data-stu-id="96172-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Een Azure Blob-gegevensset kopiëren naar Azure SQL Database](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="96172-157">In de volgende sectie vindt u de volledige Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten zodat u de zelfstudie snel kunt doorlopen en de sjabloon kunt testen.</span><span class="sxs-lookup"><span data-stu-id="96172-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="96172-158">Raadpleeg de sectie [Data Factory-entiteiten in de sjabloon](#data-factory-entities-in-the-template) om te lezen hoe elke Data Factory-entiteit wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="96172-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="96172-159">JSON-sjabloon voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="96172-159">Data Factory JSON template</span></span>
<span data-ttu-id="96172-160">De Resource Manager-sjabloon op het hoogste niveau voor het definiëren van een gegevensfactory is als volgt:</span><span class="sxs-lookup"><span data-stu-id="96172-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="96172-161">Maak een JSON-bestand met de naam **ADFCopyTutorialARM.json** in de map **C:\ADFGetStarted**. Geef het bestand de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="96172-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="96172-162">JSON-bestand met parameters</span><span class="sxs-lookup"><span data-stu-id="96172-162">Parameters JSON</span></span>
<span data-ttu-id="96172-163">Maak een JSON-bestand met de naam **ADFCopyTutorialARM-Parameters.json** dat parameters voor de Azure Resource Manager-sjabloon bevat.</span><span class="sxs-lookup"><span data-stu-id="96172-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="96172-164">Geef de naam en sleutel van uw Azure Storage-account op voor de parameters storageAccountName en storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="96172-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="96172-165">Geef de Azure SQL-server, database, gebruiker en het wachtwoord op voor de parameters sqlServerName, databaseName, sqlServerUserName en sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="96172-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="96172-166">Mogelijk beschikt u over afzonderlijke JSON-bestanden met parameters voor ontwikkel-, test- en productieomgevingen die u met dezelfde JSON-sjabloon voor Data Factory kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96172-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="96172-167">U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="96172-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="96172-168">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="96172-168">Create data factory</span></span>
1. <span data-ttu-id="96172-169">Open **Azure PowerShell** en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="96172-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="96172-170">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="96172-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="96172-171">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="96172-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="96172-172">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="96172-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="96172-173">Voer de volgende opdracht uit om Data Factory-entiteiten te implementeren met behulp van het Resource Manager-sjabloon dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96172-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="96172-174">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="96172-174">Monitor pipeline</span></span>

1. <span data-ttu-id="96172-175">Meld u met uw Azure-account aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96172-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="96172-176">Klik in het linkermenu op **Gegevensfactory's** (of) klik op **Meer services** en vervolgens op **Gegevensfactory's** onder de categorie **Informatie en analytische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="96172-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Het menu voor gegevensfactory's](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="96172-178">Zoek uw gegevenfactory (AzureBlobToAzureSQLDatabaseDF) op de pagina **Gegevensfactory's** op.</span><span class="sxs-lookup"><span data-stu-id="96172-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Naar de gegevensfactory zoeken](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="96172-180">Klik op uw Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="96172-180">Click your Azure data factory.</span></span> <span data-ttu-id="96172-181">De startpagina voor de gegevensfactory wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="96172-181">You see the home page for the data factory.</span></span>
   
    ![De startpagina voor de gegevensfactory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="96172-183">Volg de instructies in [Gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) voor het bewaken van de pijplijn en gegevenssets die u tijdens deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96172-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="96172-184">Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="96172-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="96172-185">Wanneer een segment de status **Gereed** heeft, controleert u of de gegevens naar de tabel **emp** in de Azure SQL-database zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="96172-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="96172-186">Zie [Gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor meer informatie over het gebruik van Azure Portal voor het bewaken van de pijplijn en gegevenssets te bewaken die u tijdens deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96172-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="96172-187">Zie [Azure Data Factory-pijplijnen bewaken en beheren met de Controle-app](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van de app Controleren en beheren voor het bewaken van uw gegevenspijplijnen.</span><span class="sxs-lookup"><span data-stu-id="96172-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="96172-188">Data Factory-entiteiten in de sjabloon</span><span class="sxs-lookup"><span data-stu-id="96172-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="96172-189">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="96172-189">Define data factory</span></span>
<span data-ttu-id="96172-190">U definieert een gegevensfactory in de Resource Manager-sjabloon zoals in het volgende voorbeeld wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="96172-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="96172-191">De variabele dataFactoryName wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="96172-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="96172-192">Het is een unieke tekenreeks op basis van de resourcegroep-id.</span><span class="sxs-lookup"><span data-stu-id="96172-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="96172-193">Data Factory-entiteiten definiëren</span><span class="sxs-lookup"><span data-stu-id="96172-193">Defining Data Factory entities</span></span>
<span data-ttu-id="96172-194">De volgende Data Factory-entiteiten worden in de JSON-sjabloon gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="96172-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="96172-195">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="96172-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="96172-196">Een gekoppelde Azure SQL-service</span><span class="sxs-lookup"><span data-stu-id="96172-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="96172-197">De Azure Blob-gegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="96172-198">De Azure SQL-gegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="96172-199">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="96172-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="96172-200">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="96172-200">Azure Storage linked service</span></span>
<span data-ttu-id="96172-201">De AzureStorageLinkedService koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="96172-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="96172-202">U hebt een container gemaakt en gegevens naar dit opslagaccount geüpload als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="96172-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="96172-203">In deze sectie geeft u de naam en sleutel van uw Azure Storage-account op.</span><span class="sxs-lookup"><span data-stu-id="96172-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="96172-204">Zie [Een gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="96172-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="96172-205">De tekenreeks connectionString maakt gebruik van de parameters storageAccountName en storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="96172-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="96172-206">De waarden voor deze parameters worden doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="96172-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="96172-207">De definitie maakt ook gebruik van variabelen: azureStorageLinkedService en dataFactoryName die zijn gedefinieerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="96172-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="96172-208">Een gekoppelde Azure SQL Database-service</span><span class="sxs-lookup"><span data-stu-id="96172-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="96172-209">De AzureSqlLinkedService koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="96172-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="96172-210">De gegevens die worden gekopieerd uit de blobopslag worden opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="96172-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="96172-211">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u de emp-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96172-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="96172-212">U geeft in deze sectie de Azure SQL-servernaam, -databasenaam, -gebruikersnaam en -wachtwoord op.</span><span class="sxs-lookup"><span data-stu-id="96172-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="96172-213">Zie [Een gekoppelde Azure SQL-service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="96172-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="96172-214">De tekenreeks connectionString maakt gebruik van de parameters sqlServerName, databaseName, sqlServerUserName en sqlServerPassword waarvan de waarden worden doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="96172-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="96172-215">De definitie maakt ook gebruik van de volgende variabelen uit de sjabloon: azureSqlLinkedServiceName en dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="96172-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="96172-216">De Azure Blob-gegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-216">Azure blob dataset</span></span>
<span data-ttu-id="96172-217">De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="96172-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="96172-218">In de gegevenssetdefinitie van de Azure-blob geeft u de namen op van de blobcontainer, map en het bestand met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="96172-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="96172-219">Zie [Eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="96172-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="96172-220">De Azure SQL-gegevensset</span><span class="sxs-lookup"><span data-stu-id="96172-220">Azure SQL dataset</span></span>
<span data-ttu-id="96172-221">U geeft de naam op van de tabel in de Azure SQL-database die de gekopieerde gegevens uit de Azure Blob-opslag bevat.</span><span class="sxs-lookup"><span data-stu-id="96172-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="96172-222">Zie [Eigenschappen van de Azure SQL-gegevensset](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure SQL-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="96172-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="96172-223">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="96172-223">Data pipeline</span></span>
<span data-ttu-id="96172-224">U definieert een pijplijn waarmee gegevens uit de Azure Blob-gegevensset naar de Azure SQL-gegevensset worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="96172-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="96172-225">Zie [JSON-bestand voor een pijplijn](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt voor het definiëren van een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="96172-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="96172-226">De sjabloon hergebruiken</span><span class="sxs-lookup"><span data-stu-id="96172-226">Reuse the template</span></span>
<span data-ttu-id="96172-227">U hebt in de zelfstudie een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96172-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="96172-228">Met de pijplijn worden gegevens gekopieerd van een Azure Storage-account naar een Azure SQL-database die zijn opgegeven via parameters.</span><span class="sxs-lookup"><span data-stu-id="96172-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="96172-229">Als u dezelfde sjabloon wilt gebruiken voor het implementeren van Data Factory-entiteiten in verschillende omgevingen, maakt u een parameterbestand voor elke omgeving en gebruikt u dit bij het implementeren in die omgeving.</span><span class="sxs-lookup"><span data-stu-id="96172-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="96172-230">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="96172-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="96172-231">De eerste opdracht maakt gebruik van het parameterbestand voor de ontwikkelomgeving, de tweede voor de testomgeving en de derde voor de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="96172-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="96172-232">U kunt de sjabloon ook hergebruiken om herhaalde taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="96172-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="96172-233">U moet bijvoorbeeld veel gegevensfactory's maken met een of meer pijplijnen die dezelfde logica implementeren, maar elke gegevensfactory maakt gebruik van andere Storage- en SQL Database-accounts.</span><span class="sxs-lookup"><span data-stu-id="96172-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="96172-234">In dit scenario gebruikt u dezelfde sjabloon in dezelfde omgeving (voor het ontwikkelen, testen of de productie) met andere parameterbestanden om de gegevensfactory's te maken.</span><span class="sxs-lookup"><span data-stu-id="96172-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="96172-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96172-235">Next steps</span></span>
<span data-ttu-id="96172-236">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="96172-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="96172-237">De volgende tabel bevat een lijst met gegevensarchieven die worden ondersteund als bron en doel voor de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="96172-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="96172-238">Klik op de koppeling voor de gegevensopslag in de tabel voor meer informatie over het kopiëren van gegevens naar/uit een gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="96172-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
