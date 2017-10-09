---
title: 'Zelfstudie: een pijplijn maken met het Resource Manager-sjabloon | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met behulp van een Azure Resource Manager-sjabloon. Deze pijplijn kopieert invoergegevens uit een Azure blob storage tooan Azure SQL database.
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="84126-104">Zelfstudie: Gebruik Azure Resource Manager sjabloon toocreate een Data Factory-pijplijn toocopy gegevens</span><span class="sxs-lookup"><span data-stu-id="84126-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84126-105">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="84126-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="84126-106">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="84126-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="84126-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84126-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="84126-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84126-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="84126-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84126-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="84126-110">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="84126-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="84126-111">REST API</span><span class="sxs-lookup"><span data-stu-id="84126-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="84126-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="84126-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="84126-113">Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="84126-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="84126-114">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="84126-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="84126-115">Het biedt invoergegevens tooproduce uitvoergegevens niet transformeren.</span><span class="sxs-lookup"><span data-stu-id="84126-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="84126-116">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="84126-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="84126-117">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="84126-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="84126-118">Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink.</span><span class="sxs-lookup"><span data-stu-id="84126-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="84126-119">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="84126-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="84126-120">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="84126-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="84126-121">Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="84126-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="84126-122">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="84126-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="84126-123">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="84126-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="84126-124">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="84126-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="84126-125">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="84126-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="84126-126">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="84126-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="84126-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="84126-127">Prerequisites</span></span>
* <span data-ttu-id="84126-128">Doorloop [overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="84126-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="84126-129">Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer.</span><span class="sxs-lookup"><span data-stu-id="84126-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="84126-130">In deze zelfstudie gebruikt u PowerShell toodeploy Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="84126-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="84126-131">(optioneel) Zie [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn over Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="84126-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="84126-132">In deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="84126-132">In this tutorial</span></span>
<span data-ttu-id="84126-133">In deze zelfstudie maakt maken u een gegevensfactory met de Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="84126-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="84126-134">Entiteit</span><span class="sxs-lookup"><span data-stu-id="84126-134">Entity</span></span> | <span data-ttu-id="84126-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="84126-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84126-136">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="84126-136">Azure Storage linked service</span></span> |<span data-ttu-id="84126-137">Uw Azure Storage-account toohello data factory gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="84126-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="84126-138">Azure-opslag is brongegevensarchief Hallo en Azure SQL-database is Hallo sink-gegevensopslag voor de kopieeractiviteit Hallo in Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="84126-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="84126-139">Het specificeert Hallo-opslagaccount waarin de invoergegevens voor de kopieeractiviteit Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="84126-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="84126-140">Een gekoppelde Azure SQL Database-service</span><span class="sxs-lookup"><span data-stu-id="84126-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="84126-141">Uw Azure SQL database toohello data factory gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="84126-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="84126-142">Geeft aan van hello Azure SQL-database die uitvoergegevens Hallo voor de kopieeractiviteit Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="84126-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="84126-143">Azure Blob-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-143">Azure Blob input dataset</span></span> |<span data-ttu-id="84126-144">Verwijst toohello gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="84126-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="84126-145">Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset geeft Hallo-container, map en bestandsnaam in Hallo opslag die Hallo invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="84126-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="84126-146">Azure SQL-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-146">Azure SQL output dataset</span></span> |<span data-ttu-id="84126-147">Toohello Azure SQL gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="84126-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="84126-148">Hello Azure SQL gekoppelde service verwijst tooan Azure SQL-server en hello Azure SQL-gegevensset bevat Hallo-naam van Hallo tabel waarin Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="84126-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="84126-149">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="84126-149">Data pipeline</span></span> |<span data-ttu-id="84126-150">Hallo pijplijn heeft een activiteit van Typ Copy waarmee hello Azure blob-gegevensset als invoer en hello Azure SQL-gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="84126-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="84126-151">Hallo kopieeractiviteit kopieert gegevens van een tabel van de Azure-blobopslag tooa in hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="84126-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="84126-152">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="84126-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="84126-153">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="84126-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="84126-154">Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="84126-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="84126-155">In deze zelfstudie maakt u een pijplijn met één activiteit (kopiëren).</span><span class="sxs-lookup"><span data-stu-id="84126-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Azure Blob-tooAzure SQL-Database kopiëren](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="84126-157">Hallo volgende sectie bevat Hallo voltooid Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten, zodat u snel via Hallo zelfstudie en test Hallo-sjabloon uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="84126-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="84126-158">toounderstand hoe elke entiteit Data Factory is gedefinieerd, Zie [Data Factory-entiteiten in de sjabloon Hallo](#data-factory-entities-in-the-template) sectie.</span><span class="sxs-lookup"><span data-stu-id="84126-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="84126-159">JSON-sjabloon voor Data Factory</span><span class="sxs-lookup"><span data-stu-id="84126-159">Data Factory JSON template</span></span>
<span data-ttu-id="84126-160">Hallo op het hoogste niveau Resource Manager-sjabloon voor het definiëren van een gegevensfactory is:</span><span class="sxs-lookup"><span data-stu-id="84126-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="84126-161">Maak een JSON-bestand met de naam **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="84126-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="84126-162">JSON-bestand met parameters</span><span class="sxs-lookup"><span data-stu-id="84126-162">Parameters JSON</span></span>
<span data-ttu-id="84126-163">Maak een JSON-bestand met de naam **ADFCopyTutorialARM Parameters.json** die parameters voor hello Azure Resource Manager-sjabloon bevat.</span><span class="sxs-lookup"><span data-stu-id="84126-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="84126-164">Geef de naam en sleutel van uw Azure Storage-account op voor de parameters storageAccountName en storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="84126-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="84126-165">Geef de Azure SQL-server, database, gebruiker en het wachtwoord op voor de parameters sqlServerName, databaseName, sqlServerUserName en sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="84126-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="84126-166">Wellicht hebt u afzonderlijke parameter JSON-bestanden voor ontwikkeling, testen en productieomgevingen die u met gebruiken kunt Hallo dezelfde Data Factory JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="84126-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="84126-167">U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren.</span><span class="sxs-lookup"><span data-stu-id="84126-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="84126-168">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="84126-168">Create data factory</span></span>
1. <span data-ttu-id="84126-169">Start **Azure PowerShell** en Voer Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="84126-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="84126-170">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="84126-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="84126-171">Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="84126-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="84126-172">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="84126-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="84126-173">Voer Hallo na de opdracht toodeploy Data Factory-entiteiten Hallo Resource Manager-sjabloon die u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84126-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="84126-174">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="84126-174">Monitor pipeline</span></span>

1. <span data-ttu-id="84126-175">Meld u bij toohello [Azure-portal](https://portal.azure.com) met behulp van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="84126-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="84126-176">Klik op **gegevensfactory** op Hallo links menu (of) klikt u op **meer services** en klik op **gegevensfactory** onder **INTELLIGENCE en analyse** categorie.</span><span class="sxs-lookup"><span data-stu-id="84126-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Het menu voor gegevensfactory's](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="84126-178">In Hallo **gegevensfactory** pagina, zoeken en weergeven van uw gegevensfactory (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="84126-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Naar de gegevensfactory zoeken](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="84126-180">Klik op uw Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="84126-180">Click your Azure data factory.</span></span> <span data-ttu-id="84126-181">U ziet Hallo startpagina voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="84126-181">You see hello home page for hello data factory.</span></span>
   
    ![De startpagina voor de gegevensfactory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="84126-183">Volg de instructies uit [gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor Hallo pijplijn en gegevenssets u in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84126-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="84126-184">Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="84126-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="84126-185">Wanneer een segment is in Hallo **gereed** status, controleren of gegevens Hallo gekopieerde toohello **emp** tabel in hello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="84126-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="84126-186">Zie voor meer informatie over hoe toouse Azure portal-blades toomonitor pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie, [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="84126-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="84126-187">Zie voor meer informatie over hoe toouse Hallo Monitor & beheren toepassing toomonitor uw gegevens pijplijnen, [bewaken en beheren van de App voor bewaking met Azure Data Factory-pijplijnen](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="84126-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="84126-188">Data Factory-entiteiten in Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="84126-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="84126-189">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="84126-189">Define data factory</span></span>
<span data-ttu-id="84126-190">U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="84126-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="84126-191">Hallo dataFactoryName wordt gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="84126-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="84126-192">Er is een unieke tekenreeks die is gebaseerd op Hallo resource-ID.</span><span class="sxs-lookup"><span data-stu-id="84126-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="84126-193">Data Factory-entiteiten definiëren</span><span class="sxs-lookup"><span data-stu-id="84126-193">Defining Data Factory entities</span></span>
<span data-ttu-id="84126-194">Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo:</span><span class="sxs-lookup"><span data-stu-id="84126-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="84126-195">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="84126-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="84126-196">Een gekoppelde Azure SQL-service</span><span class="sxs-lookup"><span data-stu-id="84126-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="84126-197">De Azure Blob-gegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="84126-198">De Azure SQL-gegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="84126-199">De gegevenspijplijn met een kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="84126-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="84126-200">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="84126-200">Azure Storage linked service</span></span>
<span data-ttu-id="84126-201">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="84126-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="84126-202">U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="84126-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="84126-203">U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="84126-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="84126-204">Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="84126-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="84126-205">Hallo connectionString Hallo storageAccountName en storageAccountKey parameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="84126-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="84126-206">Hallo-waarden voor deze parameters doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="84126-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="84126-207">Hallo definitie variabelen ook worden gebruikt: azureStroageLinkedService en dataFactoryName in Hallo sjabloon worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="84126-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="84126-208">Een gekoppelde Azure SQL Database-service</span><span class="sxs-lookup"><span data-stu-id="84126-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="84126-209">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="84126-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="84126-210">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="84126-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="84126-211">Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="84126-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="84126-212">U opgeven hello Azure SQL-servernaam, databasenaam, gebruikersnaam en wachtwoord in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="84126-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="84126-213">Zie [Azure SQL gekoppelde service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="84126-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="84126-214">Hallo connectionString gebruikt sqlServerName, databaseName, sqlServerUserName en sqlServerPassword parameters waarvan de waarden worden doorgegeven met behulp van een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="84126-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="84126-215">Hallo definitie gebruikt ook Hallo volgende variabelen uit Hallo sjabloon: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="84126-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="84126-216">De Azure Blob-gegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-216">Azure blob dataset</span></span>
<span data-ttu-id="84126-217">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="84126-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="84126-218">In Azure blob-gegevenssetdefinitie geeft u de namen van blob-container, map en -bestand met de invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="84126-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="84126-219">Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="84126-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="84126-220">De Azure SQL-gegevensset</span><span class="sxs-lookup"><span data-stu-id="84126-220">Azure SQL dataset</span></span>
<span data-ttu-id="84126-221">U Hallo naam opgeven van Hallo tabel in hello Azure SQL-database dat gegevens uit Azure Blob storage Hallo Hallo gekopieerd bevat.</span><span class="sxs-lookup"><span data-stu-id="84126-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="84126-222">Zie [eigenschappen van de Azure SQL-gegevensset](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="84126-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="84126-223">Gegevenspijplijn</span><span class="sxs-lookup"><span data-stu-id="84126-223">Data pipeline</span></span>
<span data-ttu-id="84126-224">U definiëren een pijplijn waarmee gegevens worden gekopieerd uit hello Azure blob-gegevensset toohello Azure SQL gegevensset.</span><span class="sxs-lookup"><span data-stu-id="84126-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="84126-225">Zie [pijplijn-JSON](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="84126-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="84126-226">Hallo-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="84126-226">Reuse hello template</span></span>
<span data-ttu-id="84126-227">In de zelfstudie hello, moet u een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84126-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="84126-228">Hallo pijplijn kopieert invoergegevens uit een Azure Storage-account tooan Azure SQL database via parameters opgegeven.</span><span class="sxs-lookup"><span data-stu-id="84126-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="84126-229">toouse Hallo dezelfde sjabloon toodeploy Data Factory-entiteiten toodifferent omgevingen, u een parameterbestand voor elke omgeving maken en deze gebruiken bij het implementeren van toothat-omgeving.</span><span class="sxs-lookup"><span data-stu-id="84126-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="84126-230">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="84126-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="84126-231">U ziet dat de eerste opdracht Hallo maakt gebruik van parameterbestand voor Hallo-ontwikkelomgeving, tweede één voor Hallo testomgeving en derde één voor productie-omgeving Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="84126-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="84126-232">U kunt ook opnieuw gebruiken Hallo sjabloon tooperform herhaalde taken.</span><span class="sxs-lookup"><span data-stu-id="84126-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="84126-233">Bijvoorbeeld, u toocreate moet veel data Factory met een of meer pijplijnen die implementeren Hallo dezelfde logica, maar elke gegevensfactory maakt gebruik van verschillende accounts voor opslag en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="84126-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="84126-234">In dit scenario gebruikt u Hallo dezelfde sjabloon in Hallo bestanden dezelfde omgeving (dev-, test- of productie) met de andere parameter toocreate data Factory.</span><span class="sxs-lookup"><span data-stu-id="84126-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="84126-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84126-235">Next steps</span></span>
<span data-ttu-id="84126-236">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="84126-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="84126-237">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="84126-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="84126-238">toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="84126-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
