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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Zelfstudie: bouw uw eerste Azure-gegevensfactory op basis van een Azure Resource Manager-sjabloon
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

In dit artikel gebruikt u een Azure Resource Manager-sjabloon toocreate uw eerste Azure-gegevensfactory. toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.

Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**. Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer. Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven. 

> [!NOTE]
> Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Hallo-pijplijn in deze zelfstudie is slechts één activiteit van het type: HDInsightHive. Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie. 

## <a name="prerequisites"></a>Vereisten
* Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.
* Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer.
* Zie [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn over Azure Resource Manager-sjablonen. 

## <a name="in-this-tutorial"></a>In deze zelfstudie
| Entiteit | Beschrijving |
| --- | --- |
| Een gekoppelde Azure Storage-service |Uw Azure Storage-account toohello data factory gekoppeld. Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account. |
| Een gekoppelde HDInsight-service op aanvraag |Een gegevensfactory op aanvraag HDInsight-cluster toohello koppelingen. Hallo-cluster wordt automatisch gemaakt voor uw tooprocess gegevens en wordt verwijderd nadat het Hallo-verwerking is voltooid. |
| Azure Blob-invoergegevensset |Verwijst toohello gekoppelde Azure Storage-service. Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset geeft Hallo-container, map en bestandsnaam in Hallo opslag die Hallo invoergegevens bevat. |
| Azure Blob-uitvoergegevensset |Verwijst toohello gekoppelde Azure Storage-service. Hallo gekoppelde service verwijst tooan Azure Storage-account en hello Azure Blob-gegevensset bevat Hallo-container, map en bestandsnaam in Hallo opslag van uitvoergegevens Hallo. |
| Gegevenspijplijn |Hallo pijplijn heeft een activiteit van het type HDInsightHive die Hallo invoergegevensset verbruikt en Hallo uitvoergegevensset produceert. |

Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md). In deze zelfstudie maakt u een pijplijn met één activiteit (Hive-activiteit).

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
Maak een JSON-bestand met de naam **ADFTutorialARM.json** in **C:\ADFGetStarted** map Hello volgende inhoud:

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
> In [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Zelfstudie: met behulp van een Azure Resource Manager-sjabloon een pijplijn maken met een kopieerbewerking) vindt u een ander voorbeeld van een Resource Manager-sjabloon voor het maken van een Azure-gegevensfactory.  
> 
> 

## <a name="parameters-json"></a>JSON-bestand met parameters
Maak een JSON-bestand met de naam **ADFTutorialARM Parameters.json** die parameters voor hello Azure Resource Manager-sjabloon bevat.  

> [!IMPORTANT]
> Geef Hallo naam en sleutel van uw Azure Storage-account voor Hallo **storageAccountName** en **storageAccountKey** parameters in dit parameterbestand. 
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
   * Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd. Dit abonnement moet hetzelfde zijn als u die wordt gebruikt bij de Azure-portal Hallo HALLO hallo.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Voer Hallo na de opdracht toodeploy Data Factory-entiteiten Hallo Resource Manager-sjabloon die u in stap 1 hebt gemaakt. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>De pijplijn bewaken
1. Na het aanmelden toohello [Azure-portal](https://portal.azure.com/), klikt u op **Bladeren** en selecteer **gegevensfactory**.
     ![Bladeren -> Gegevensfactory's](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. In Hallo **Gegevensfactory** blade, klikt u op Hallo gegevensfactory (**TutorialFactoryARM**) u hebt gemaakt.    
3. In Hallo **Data Factory** blade van uw gegevensfactory klikt u op **Diagram**.

     ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. In Hallo **diagramweergave**, ziet u een overzicht van Hallo pijplijnen en gegevenssets gebruikt in deze zelfstudie.
   
   ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Dubbelklik in de diagramweergave hello, op Hallo gegevensset **AzureBlobOutput**. U ziet dat Hallo-segment dat momenteel wordt verwerkt.
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status. Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten). Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Wanneer Hallo segment is in **gereed** staat, controleert u Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.  

Zie [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor instructies over hoe toouse hello Azure portal-blades toomonitor Hallo pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie.

U kunt uw gegevenspijplijnen ook Monitor and Manage App toomonitor. Zie [bewaken en beheren van de App voor bewaking met Azure Data Factory-pijplijnen](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van de toepassing hello. 

> [!IMPORTANT]
> Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt. Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.
> 
> 

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
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Er is een unieke tekenreeks die is gebaseerd op Hallo resource-ID.  

### <a name="defining-data-factory-entities"></a>Data Factory-entiteiten definiëren
Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo: 

* [Een gekoppelde Azure Storage-service](#azure-storage-linked-service)
* [Een gekoppelde HDInsight-service op aanvraag](#hdinsight-on-demand-linked-service)
* [De Azure Blob-invoergegevensset](#azure-blob-input-dataset)
* [De Azure Blob-uitvoergegevensset](#azure-blob-output-dataset)
* [De gegevenspijplijn met een kopieerbewerking](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie. Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service. 

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
Hallo **connectionString** maakt gebruik van parameters storageAccountName en storageAccountKey Hallo. Hallo-waarden voor deze parameters doorgegeven met behulp van een configuratiebestand. Hallo definitie variabelen ook worden gebruikt: azureStroageLinkedService en dataFactoryName in Hallo sjabloon worden gedefinieerd. 

#### <a name="hdinsight-on-demand-linked-service"></a>Een gekoppelde HDInsight-service op aanvraag
Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artikel voor meer informatie over de JSON-eigenschappen die toodefine een gekoppelde HDInsight on demand-service.  

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
Houd er rekening mee Hallo volgende punten: 

* Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello hierboven JSON. Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie. 
* U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.
* Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment toobe verwerkt moet, tenzij er een bestaand livecluster is (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.
  
    Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.

#### <a name="azure-blob-input-dataset"></a>Azure Blob-invoergegevensset
U opgeven Hallo namen van de blob-container, map en -bestand met de invoergegevens Hallo. Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset. 

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
Hallo volgende parameters zijn gedefinieerd in de parameter-sjabloon maakt gebruik van deze definitie: blobContainer, inputBlobFolder, en inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset
U opgeven Hallo namen van blob-container en map waarin de uitvoergegevens Hallo. Zie [eigenschappen van de Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.  

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

Hallo na gedefinieerde parameters in Hallo parameter sjabloon maakt gebruik van deze definitie: blobContainer en outputBlobFolder. 

#### <a name="data-pipeline"></a>Gegevenspijplijn
U definieert een pijplijn waarmee gegevens worden omgezet door een Hive-script uit te voeren in een Azure HDInsight-cluster op aanvraag. Zie [pijplijn-JSON](data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld. 

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

## <a name="reuse-hello-template"></a>Hallo-sjabloon gebruiken
In de zelfstudie hello, moet u een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt. toouse Hallo dezelfde sjabloon toodeploy Data Factory-entiteiten toodifferent omgevingen, u een parameterbestand voor elke omgeving maken en deze gebruiken bij het implementeren van toothat-omgeving.     

Voorbeeld:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
U ziet dat de eerste opdracht Hallo maakt gebruik van parameterbestand voor Hallo-ontwikkelomgeving, tweede één voor Hallo testomgeving en derde één voor productie-omgeving Hallo Hallo.  

U kunt ook opnieuw gebruiken Hallo sjabloon tooperform herhaalde taken. Bijvoorbeeld, u moet toocreate veel data Factory met een of meer pijplijnen die implementeren Hallo dezelfde logica maar elke data factory maakt gebruik van andere Azure storage en Azure SQL Database-accounts. In dit scenario gebruikt u Hallo dezelfde sjabloon in Hallo bestanden dezelfde omgeving (dev-, test- of productie) met de andere parameter toocreate data Factory. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Resource Manager-sjabloon voor het maken van een gateway
Hier volgt een voorbeeld Resource Manager-sjabloon voor het maken van een logische gateway in Hallo terug. Een gateway installeren op uw lokale computer of virtuele machine van Azure IaaS en Hallo gateway registreren met behulp van een sleutel Data Factory-service. Zie [Gegevens verplaatsen tussen on-premises en de cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie.

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
Met deze sjabloon maakt u een gegevensfactory met de naam GatewayUsingArmDF, met een gateway met de naam GatewayUsingARM. 

## <a name="see-also"></a>Zie ook
| Onderwerp | Beschrijving |
|:--- |:--- |
| [Pijplijnen](data-factory-create-pipelines.md) |In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf. |
| [Gegevenssets](data-factory-create-datasets.md) |Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory. |
| [Plannen en uitvoeren](data-factory-scheduling-and-execution.md) |Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel. |
| [Pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) |Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App. |

