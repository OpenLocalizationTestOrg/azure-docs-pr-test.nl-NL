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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Zelfstudie: Gebruik Azure Resource Manager sjabloon toocreate een Data Factory-pijplijn toocopy gegevens 
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een Azure data factory. Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Het biedt invoergegevens tooproduce uitvoergegevens niet transformeren. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie. 

> [!NOTE] 
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Vereisten
* Doorloop [overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) en volledige Hallo **vereiste** stappen.
* Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer. In deze zelfstudie gebruikt u PowerShell toodeploy Data Factory-entiteiten. 
* (optioneel) Zie [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn over Azure Resource Manager-sjablonen.

## <a name="in-this-tutorial"></a>In deze zelfstudie
In deze zelfstudie maakt maken u een gegevensfactory met de Hallo Data Factory-entiteiten te volgen:

| Entiteit | Beschrijving |
| --- | --- |
| Een gekoppelde Azure Storage-service |Uw Azure Storage-account toohello data factory gekoppeld. Azure-opslag is brongegevensarchief Hallo en Azure SQL-database is Hallo sink-gegevensopslag voor de kopieeractiviteit Hallo in Hallo zelfstudie. Het specificeert Hallo-opslagaccount waarin de invoergegevens voor de kopieeractiviteit Hallo Hallo. |
| Een gekoppelde Azure SQL Database-service |Uw Azure SQL database toohello data factory gekoppeld. Geeft aan van hello Azure SQL-database die uitvoergegevens Hallo voor de kopieeractiviteit Hallo bevat. |
| Azure Blob-invoergegevensset |Verwijst toohello gekoppelde Azure Storage-service. Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset geeft Hallo-container, map en bestandsnaam in Hallo opslag die Hallo invoergegevens bevat. |
| Azure SQL-uitvoergegevensset |Toohello Azure SQL gekoppelde service verwijst. Hello Azure SQL gekoppelde service verwijst tooan Azure SQL-server en hello Azure SQL-gegevensset bevat Hallo-naam van Hallo tabel waarin Hallo uitvoergegevens. |
| Gegevenspijplijn |Hallo pijplijn heeft een activiteit van Typ Copy waarmee hello Azure blob-gegevensset als invoer en hello Azure SQL-gegevensset als uitvoer. Hallo kopieeractiviteit kopieert gegevens van een tabel van de Azure-blobopslag tooa in hello Azure SQL-database. |

Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md). In deze zelfstudie maakt u een pijplijn met één activiteit (kopiëren).

![Azure Blob-tooAzure SQL-Database kopiëren](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

Hallo volgende sectie bevat Hallo voltooid Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten, zodat u snel via Hallo zelfstudie en test Hallo-sjabloon uitvoeren kunt. toounderstand hoe elke entiteit Data Factory is gedefinieerd, Zie [Data Factory-entiteiten in de sjabloon Hallo](#data-factory-entities-in-the-template) sectie.

## <a name="data-factory-json-template"></a>JSON-sjabloon voor Data Factory
Hallo op het hoogste niveau Resource Manager-sjabloon voor het definiëren van een gegevensfactory is: 

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
Maak een JSON-bestand met de naam **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** map Hello volgende inhoud:

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

## <a name="parameters-json"></a>JSON-bestand met parameters
Maak een JSON-bestand met de naam **ADFCopyTutorialARM Parameters.json** die parameters voor hello Azure Resource Manager-sjabloon bevat. 

> [!IMPORTANT]
> Geef de naam en sleutel van uw Azure Storage-account op voor de parameters storageAccountName en storageAccountKey.  
> 
> Geef de Azure SQL-server, database, gebruiker en het wachtwoord op voor de parameters sqlServerName, databaseName, sqlServerUserName en sqlServerPassword.  

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
> Wellicht hebt u afzonderlijke parameter JSON-bestanden voor ontwikkeling, testen en productieomgevingen die u met gebruiken kunt Hallo dezelfde Data Factory JSON-sjabloon. U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren.  
> 
> 

## <a name="create-data-factory"></a>Een gegevensfactory maken
1. Start **Azure PowerShell** en Voer Hallo de volgende opdracht:
   * Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Voer Hallo na de opdracht toodeploy Data Factory-entiteiten Hallo Resource Manager-sjabloon die u in stap 1 hebt gemaakt.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>De pijplijn bewaken

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met behulp van uw Azure-account.
2. Klik op **gegevensfactory** op Hallo links menu (of) klikt u op **meer services** en klik op **gegevensfactory** onder **INTELLIGENCE en analyse** categorie.
   
    ![Het menu voor gegevensfactory's](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. In Hallo **gegevensfactory** pagina, zoeken en weergeven van uw gegevensfactory (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Naar de gegevensfactory zoeken](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Klik op uw Azure-gegevensfactory. U ziet Hallo startpagina voor Hallo data factory.
   
    ![De startpagina voor de gegevensfactory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Volg de instructies uit [gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor Hallo pijplijn en gegevenssets u in deze zelfstudie hebt gemaakt. Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen.
7. Wanneer een segment is in Hallo **gereed** status, controleren of gegevens Hallo gekopieerde toohello **emp** tabel in hello Azure SQL database.


Zie voor meer informatie over hoe toouse Azure portal-blades toomonitor pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie, [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) .

Zie voor meer informatie over hoe toouse Hallo Monitor & beheren toepassing toomonitor uw gegevens pijplijnen, [bewaken en beheren van de App voor bewaking met Azure Data Factory-pijplijnen](data-factory-monitor-manage-app.md).

## <a name="data-factory-entities-in-hello-template"></a>Data Factory-entiteiten in Hallo-sjabloon
### <a name="define-data-factory"></a>Een gegevensfactory definiëren
U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

Hallo dataFactoryName wordt gedefinieerd als: 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Er is een unieke tekenreeks die is gebaseerd op Hallo resource-ID.  

### <a name="defining-data-factory-entities"></a>Data Factory-entiteiten definiëren
Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo: 

1. [Een gekoppelde Azure Storage-service](#azure-storage-linked-service)
2. [Een gekoppelde Azure SQL-service](#azure-sql-database-linked-service)
3. [De Azure Blob-gegevensset](#azure-blob-dataset)
4. [De Azure SQL-gegevensset](#azure-sql-dataset)
5. [De gegevenspijplijn met een kopieerbewerking](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie. Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service. 

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

Hallo connectionString Hallo storageAccountName en storageAccountKey parameters gebruikt. Hallo-waarden voor deze parameters doorgegeven met behulp van een configuratiebestand. Hallo definitie variabelen ook worden gebruikt: azureStroageLinkedService en dataFactoryName in Hallo sjabloon worden gedefinieerd. 

#### <a name="azure-sql-database-linked-service"></a>Een gekoppelde Azure SQL Database-service
Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). U opgeven hello Azure SQL-servernaam, databasenaam, gebruikersnaam en wachtwoord in deze sectie. Zie [Azure SQL gekoppelde service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL gekoppelde service.  

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

Hallo connectionString gebruikt sqlServerName, databaseName, sqlServerUserName en sqlServerPassword parameters waarvan de waarden worden doorgegeven met behulp van een configuratiebestand. Hallo definitie gebruikt ook Hallo volgende variabelen uit Hallo sjabloon: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>De Azure Blob-gegevensset
Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. In Azure blob-gegevenssetdefinitie geeft u de namen van blob-container, map en -bestand met de invoergegevens Hallo. Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset. 

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

#### <a name="azure-sql-dataset"></a>De Azure SQL-gegevensset
U Hallo naam opgeven van Hallo tabel in hello Azure SQL-database dat gegevens uit Azure Blob storage Hallo Hallo gekopieerd bevat. Zie [eigenschappen van de Azure SQL-gegevensset](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL-gegevensset. 

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

#### <a name="data-pipeline"></a>Gegevenspijplijn
U definiëren een pijplijn waarmee gegevens worden gekopieerd uit hello Azure blob-gegevensset toohello Azure SQL gegevensset. Zie [pijplijn-JSON](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld. 

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

## <a name="reuse-hello-template"></a>Hallo-sjabloon gebruiken
In de zelfstudie hello, moet u een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt. Hallo pijplijn kopieert invoergegevens uit een Azure Storage-account tooan Azure SQL database via parameters opgegeven. toouse Hallo dezelfde sjabloon toodeploy Data Factory-entiteiten toodifferent omgevingen, u een parameterbestand voor elke omgeving maken en deze gebruiken bij het implementeren van toothat-omgeving.     

Voorbeeld:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

U ziet dat de eerste opdracht Hallo maakt gebruik van parameterbestand voor Hallo-ontwikkelomgeving, tweede één voor Hallo testomgeving en derde één voor productie-omgeving Hallo Hallo.  

U kunt ook opnieuw gebruiken Hallo sjabloon tooperform herhaalde taken. Bijvoorbeeld, u toocreate moet veel data Factory met een of meer pijplijnen die implementeren Hallo dezelfde logica, maar elke gegevensfactory maakt gebruik van verschillende accounts voor opslag en SQL-Database. In dit scenario gebruikt u Hallo dezelfde sjabloon in Hallo bestanden dezelfde omgeving (dev-, test- of productie) met de andere parameter toocreate data Factory.   

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.
