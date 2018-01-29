---
title: Een Azure Data Factory maken op basis van een Resource Manager-sjabloon | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn op basis van een Azure Resource Manager-sjabloon.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/22/2018
ms.author: spelluru
ms.openlocfilehash: 5008d8f0ce36f09ff26bf10fadbf14da6b474ea9
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/25/2018
---
# <a name="tutorial-create-an-azure-data-factory-using-azure-resource-manager-template"></a>Zelfstudie: een Azure Data Factory maken op basis van een Azure Resource Manager-sjabloon
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versie 1 - Algemene beschikbaarheid](v1/data-factory-build-your-first-pipeline-using-arm.md)
> * [Versie 2 - Preview](quickstart-create-data-factory-resource-manager-template.md) 

In deze QuickStart wordt beschreven hoe u een Azure Resource Manager-sjabloon gebruikt om een Azure Data Factory te maken. Met de pijplijn die u in deze data factory maakt, worden gegevens **gekopieerd** van één map naar een andere map in een Azure Blob Storage. Zie [Zelfstudie: Gegevens transformeren met Spark](transform-data-using-spark.md) voor meer informatie over het **transformeren** van gegevens met Azure Data Factory. 

> [!NOTE]
> Dit artikel is van toepassing op versie 2 van Data Factory, dat zich momenteel in de previewfase bevindt. Als u versie 1 van de Data Factory-service gebruikt, die algemeen beschikbaar is, raadpleegt u [Uw eerste data factory maken met versie 1 van Data Factory](v1/data-factory-build-your-first-pipeline-using-arm.md).
>
> Dit artikel is geen gedetailleerde introductie tot de Data Factory-service. Zie [Inleiding tot Azure Data Factory](introduction.md) voor een inleiding tot Azure Data Factory-service.

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="azure-powershell"></a>Azure PowerShell
Installeer de nieuwste Azure PowerShell-modules met de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/install-azurerm-ps).

## <a name="resource-manager-templates"></a>Resource Manager-sjablonen
Zie [Azure Resource Manager-sjablonen maken](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over Azure Resource Manager-sjablonen. 

In de volgende sectie vindt u de volledige Resource Manager-sjabloon voor het definiëren van Data Factory-entiteiten zodat u de zelfstudie snel kunt doorlopen en de sjabloon kunt testen. Raadpleeg de sectie [Data Factory-entiteiten in de sjabloon](#data-factory-entities-in-the-template) om te lezen hoe elke Data Factory-entiteit wordt gedefinieerd.

## <a name="data-factory-json"></a>JSON van data factory 
Maak een JSON-bestand met de naam **ADFTutorialARM.json** in de map **C:\ADFTutorial** en voeg de volgende inhoud toe:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "dataFactoryName": {
            "type": "string",
            "metadata": {
                "description": "Name of the data factory. Must be globally unique."
            }
        },
        "dataFactoryLocation": {
            "type": "string",
            "allowedValues": [
                "East US",
                "East US 2",
                "West Europe"
            ],
            "defaultValue": "East US",
            "metadata": {
                "description": "Location of the data factory. Currently, only East US, East US 2, and West Europe are supported. "
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Azure storage account that contains the input/output data."
            }
        },
        "storageAccountKey": {
            "type": "securestring",
            "metadata": {
                "description": "Key for the Azure storage account."
            }
        },
        "blobContainer": {
            "type": "string",
            "metadata": {
                "description": "Name of the blob container in the Azure Storage account."
            }
        },
        "inputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that has the input file."
            }
        },
        "inputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the input file/blob."
            }
        },
        "outputBlobFolder": {
            "type": "string",
            "metadata": {
                "description": "The folder in the blob container that will hold the transformed data."
            }
        },
        "outputBlobName": {
            "type": "string",
            "metadata": {
                "description": "Name of the output file/blob."
            }
        },
        "triggerStartTime": {
            "type": "string",
            "metadata": {
                "description": "Start time for the trigger."
            }
        },
        "triggerEndTime": {
            "type": "string",
            "metadata": {
                "description": "End time for the trigger."
            }
        }
    },
    "variables": {
        "azureStorageLinkedServiceName": "ArmtemplateStorageLinkedService",
        "inputDatasetName": "ArmtemplateTestDatasetIn",
        "outputDatasetName": "ArmtemplateTestDatasetOut",
        "pipelineName": "ArmtemplateSampleCopyPipeline",
        "triggerName": "ArmTemplateTestTrigger"
    },
    "resources": [{
        "name": "[parameters('dataFactoryName')]",
        "apiVersion": "2017-09-01-preview",
        "type": "Microsoft.DataFactory/factories",
        "location": "[parameters('dataFactoryLocation')]",
        "properties": {
            "loggingStorageAccountName": "[parameters('storageAccountName')]",
            "loggingStorageAccountKey": "[parameters('storageAccountKey')]"
        },
        "resources": [{
                "type": "linkedservices",
                "name": "[variables('azureStorageLinkedServiceName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureStorage",
                    "description": "Azure Storage linked service",
                    "typeProperties": {
                        "connectionString": {
                            "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                            "type": "SecureString"
                        }
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('inputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
                        "fileName": "[parameters('inputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "datasets",
                "name": "[variables('outputDatasetName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "AzureBlob",
                    "typeProperties": {
                        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
                        "fileName": "[parameters('outputBlobName')]"
                    },
                    "linkedServiceName": {
                        "referenceName": "[variables('azureStorageLinkedServiceName')]",
                        "type": "LinkedServiceReference"
                    }
                }
            },
            {
                "type": "pipelines",
                "name": "[variables('pipelineName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "activities": [{
                        "type": "Copy",
                        "typeProperties": {
                            "source": {
                                "type": "BlobSource"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "name": "MyCopyActivity",
                        "inputs": [{
                            "referenceName": "[variables('inputDatasetName')]",
                            "type": "DatasetReference"
                        }],
                        "outputs": [{
                            "referenceName": "[variables('outputDatasetName')]",
                            "type": "DatasetReference"
                        }]
                    }]
                }
            },
            {
                "type": "triggers",
                "name": "[variables('triggerName')]",
                "dependsOn": [
                    "[parameters('dataFactoryName')]",
                    "[variables('azureStorageLinkedServiceName')]",
                    "[variables('inputDatasetName')]",
                    "[variables('outputDatasetName')]",
                    "[variables('pipelineName')]"
                ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "ScheduleTrigger",
                    "typeProperties": {
                        "recurrence": {
                            "frequency": "Hour",
                            "interval": 1,
                            "startTime": "[parameters('triggerStartTime')]",
                            "endTime": "[parameters('triggerEndTime')]",
                            "timeZone": "UTC"
                        }
                    },
                    "pipelines": [{
                        "pipelineReference": {
                            "type": "PipelineReference",
                            "referenceName": "ArmtemplateSampleCopyPipeline"
                        },
                        "parameters": {}
                    }]
                }
            }
        ]
    }]
}
```

## <a name="parameters-json"></a>JSON-bestand met parameters
Maak een JSON-bestand met de naam **ADFTutorialARM-Parameters.json** dat parameters voor de Azure Resource Manager-sjabloon bevat.  

> [!IMPORTANT]
> - Geef de naam en sleutel van uw Azure Storage-account op voor de parameters **storageAccountName** en **storageAccountKey** in dit parameterbestand. U hebt de container adftutorial gemaakt en het voorbeeldbestand (emp.txt) geüpload naar de invoermap in deze Azure-blobopslag. 
> - Geef een wereldwijd unieke naam voor de data factory op voor de parameter **dataFactoryName**. Bijvoorbeeld: ARMTutorialFactoryJohnDoe11282017. 
> - Geef voor **triggerStartTime** de huidige dag op in de notatie: `2017-11-28T00:00:00`.
> - Geef voor **triggerEndTime** de volgende dag op in de notatie: `2017-11-29T00:00:00`. U kunt ook de huidige UTC-tijd controleren en de volgende een of twee uur opgeven als eindtijd. Als de huidige UTC-tijd bijvoorbeeld 1:32 AM is, geeft u `2017-11-29:03:00:00` op als eindtijd. In dit geval voert de trigger de pijplijn tweemaal uit (om 2 uur en om 3 uur).

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "dataFactoryName": {
      "value": "<datafactoryname>"
    },    
    "dataFactoryLocation": {
      "value": "East US"
    },
    "storageAccountName": {
      "value": "<yourstroageaccountname>"
    },
    "storageAccountKey": {
      "value": "<yourstorageaccountkey>"
    },
    "blobContainer": {
      "value": "adftutorial"
    },
    "inputBlobFolder": {
      "value": "input"
    },
    "inputBlobName": {
      "value": "emp.txt"
    },
    "outputBlobFolder": {
      "value": "output"
    },
    "outputBlobName": {
      "value": "emp.txt"
    },
    "triggerStartTime": {
        "value": "2017-11-28T00:00:00. Set to today"
    },
    "triggerEndTime": {
        "value": "2017-11-29T00:00:00. Set to tomorrow"
    }
  }
}
```

> [!IMPORTANT]
> Mogelijk beschikt u over afzonderlijke JSON-bestanden met parameters voor ontwikkel-, test- en productieomgevingen die u met dezelfde JSON-sjabloon voor Data Factory kunt gebruiken. U kunt met behulp van een Power Shell-script het implementeren van Data Factory-entiteiten in deze omgevingen automatiseren. 

## <a name="deploy-data-factory-entities"></a>Data Factory-entiteiten implementeren 
Voer de volgende opdracht uit in PowerShell om Data Factory-entiteiten te implementeren met behulp van de Resource Manager-sjabloon die u eerder in deze QuickStart hebt gemaakt. 

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFTutorial\ADFTutorialARM.json -TemplateParameterFile C:\ADFTutorial\ADFTutorialARM-Parameters.json
```

De uitvoer ziet eruit als in het volgende voorbeeld: 

```
DeploymentName          : MyARMDeployment
ResourceGroupName       : ADFTutorialResourceGroup
ProvisioningState       : Succeeded
Timestamp               : 11/29/2017 3:11:13 AM
Mode                    : Incremental
TemplateLink            :
Parameters              :
                          Name                 Type            Value
                          ===============      ============    ==========
                          dataFactoryName      String          <data factory name>
                          dataFactoryLocation  String          East US
                          storageAccountName   String          <storage account name>
                          storageAccountKey    SecureString
                          blobContainer        String          adftutorial
                          inputBlobFolder      String          input
                          inputBlobName        String          emp.txt
                          outputBlobFolder     String          output
                          outputBlobName       String          emp.txt
                          triggerStartTime     String          11/29/2017 12:00:00 AM
                          triggerEndTime       String          11/29/2017 4:00:00 AM

Outputs                 :
DeploymentDebugLogLevel :
```

## <a name="start-the-trigger"></a>De trigger starten

De sjabloon implementeert de volgende Data Factory-entiteiten: 

- Een gekoppelde Azure Storage-service
- Azure Blob-gegevenssets (invoer en uitvoer)
- Pijplijn met een kopieeractiviteit
- Trigger om de pijplijn te activeren

De geïmplementeerde trigger is gestopt. Een van de manieren om de trigger te starten, is met de PowerShell-cmdlet **Start-AzureRmDataFactoryV2Trigger**. De volgende procedure bevat gedetailleerde stappen: 

1. Maak in het PowerShell-venster een variabele voor de naam van de resourcegroep. Kopieer de volgende opdracht naar het PowerShell-venster en druk op ENTER. Als u de naam van een andere resourcegroep hebt opgegeven voor de opdracht New-AzureRmResourceGroupDeployment, moet u de waarde hier bijwerken. 

    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ``` 
1. Maak een variabele voor de naam van de data factory. Geef dezelfde naam op die u hebt opgegeven in het bestand ADFTutorialARM-Parameters.json.   

    ```powershell
    $dataFactoryName = "<yourdatafactoryname>"
    ```
3. Stel een variabele in voor de naam van de trigger. De naam van de trigger is via code vastgelegd in het Resource Manager-sjabloonbestand (ADFTutorialARM.json).

    ```powershell
    $triggerName = "ArmTemplateTestTrigger"
    ```
4. Haal de **status van de trigger** op door de volgende PowerShell-opdracht uit te voeren nadat u de naam van uw data factory en trigger hebt opgegeven:

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

    Hier volgt een voorbeeld van uitvoer: 

    ```json
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Stopped
    ```
    
    Zoals u ziet, is de runtimestatus van de trigger **Gestopt**. 
5. **Start de trigger**. De trigger voert de pijplijn die in de sjabloon is gedefinieerd, uit op het hele uur. Dat wil zeggen dat als u deze opdracht uitvoert om 14:25 uur, de trigger de pijplijn voor het eerst uitvoert om 15:00 uur. Vervolgens wordt de pijplijn elk uur uitgevoerd totdat de opgegeven eindtijd voor de trigger is bereikt. 

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    Hier volgt een voorbeeld van uitvoer: 
    
    ```
    Confirm
    Are you sure you want to start trigger 'ArmTemplateTestTrigger' in data factory 'ARMFactory1128'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    True
    ```
6. Controleer of de trigger is gestart door de opdracht Get-AzureRmDataFactoryV2Trigger nogmaals uit te voeren.  

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -TriggerName $triggerName
    ```
    
    Hier volgt een voorbeeld van uitvoer:
    
    ```
    TriggerName       : ArmTemplateTestTrigger
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ARMFactory1128
    Properties        : Microsoft.Azure.Management.DataFactory.Models.ScheduleTrigger
    RuntimeState      : Started
    ```

## <a name="monitor-the-pipeline"></a>De pijplijn bewaken
1. Nadat u zich hebt aangemeld bij [Azure Portal](https://portal.azure.com/), klikt u op **Meer services**, zoekt u met een trefwoord zoals **data fa**, en selecteert u **Gegevensfabrieken**.

    ![Door het menu met data factory's bladeren](media/quickstart-create-data-factory-resource-manager-template/browse-data-factories-menu.png)
2. Klik op de pagina **Data factory's** op de data factory die u hebt gemaakt. Filter de lijst zo nodig op de naam van uw data factory.  

    ![Data factory selecteren](media/quickstart-create-data-factory-resource-manager-template/select-data-factory.png)
3. Klik op de pagina Data factory op de tegel **Controleren en beheren**. 

    ![De tegel Controleren en beheren](media/quickstart-create-data-factory-resource-manager-template/monitor-manage-tile.png)
4. De **toepassing voor gegevensintegratie** moet worden geopend op een afzonderlijk tabblad in de webbrowser. Als het controletabblad niet actief is, schakelt u over naar het **controletabblad**. U ziet dat de uitvoering van de pijplijn is geactiveerd door een **geplande trigger**. 

    ![De uitvoering van de pijplijn controleren](media/quickstart-create-data-factory-resource-manager-template/monitor-pipeline-run.png)    

    > [!IMPORTANT]
    > Zoals u ziet, wordt de pijplijn alleen uitgevoerd op het hele uur (bijvoorbeeld om 4:00 uur, 5:00 uur, 6:00 uur enz.). Klik op **Vernieuwen** op de werkbalk om de lijst te vernieuwen wanneer het volgende uur wordt bereikt. 
5. Klik op de koppeling in de kolom **Acties**. 

    ![Koppeling voor pijplijnacties](media/quickstart-create-data-factory-resource-manager-template/pipeline-actions-link.png)
6. U ziet de uitvoering van de activiteiten die zijn gekoppeld aan de pijplijnuitvoering. In deze QuickStart heeft de pijplijn slechts één activiteit en wel van het type Kopiëren. Daarom ziet u een uitvoering voor die activiteit. 

    ![Uitvoering van activiteiten](media/quickstart-create-data-factory-resource-manager-template/activity-runs.png)
1. Klik op de koppeling onder de kolom **Uitvoer**. U ziet de uitvoer van de kopieerbewerking in het venster **Uitvoer**. Klik op de knop Maximaliseren om de volledige uitvoer te bekijken. U kunt het gemaximaliseerde uitvoervenster sluiten. 

    ![Uitvoervenster](media/quickstart-create-data-factory-resource-manager-template/output-window.png)
7. Stop de trigger zodra u ziet dat de uitvoering is geslaagd/mislukt. De trigger voert de pijplijn eenmaal per uur uit. Bij elke uitvoering kopieert de pijplijn hetzelfde bestand uit de invoermap naar de uitvoermap. Als u de trigger wilt stoppen, voert u de volgende opdracht uit in het PowerShell-venster. 
    
    ```powershell
    Stop-AzureRmDataFactoryV2Trigger -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $triggerName
    ```

[!INCLUDE [data-factory-quickstart-verify-output-cleanup.md](../../includes/data-factory-quickstart-verify-output-cleanup.md)] 

## <a name="json-definitions-for-entities"></a>JSON-definities voor entiteiten
De volgende Data Factory-entiteiten worden in de JSON-sjabloon gedefinieerd: 

- [Een gekoppelde Azure Storage-service](#azure-storage-linked-service)
- [De Azure Blob-invoergegevensset](#azure-blob-input-dataset)
- [Azure Blob-uitvoergegevensset](#azure-blob-output-dataset)
- [De gegevenspijplijn met een kopieerbewerking](#data-pipeline)
- [Trigger](#trigger)

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
De AzureStorageLinkedService koppelt uw Azure-opslagaccount aan de gegevensfactory. U hebt een container gemaakt en gegevens naar dit opslagaccount geüpload als onderdeel van de vereisten. In deze sectie geeft u de naam en sleutel van uw Azure Storage-account op. Zie [Een gekoppelde Azure Storage-service](connector-azure-blob-storage.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure Storage-service. 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": {
                "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]",
                "type": "SecureString"
            }
        }
    }
}
```

De tekenreeks connectionString maakt gebruik van de parameters storageAccountName en storageAccountKey. De waarden voor deze parameters worden doorgegeven met behulp van een configuratiebestand. De definitie maakt ook gebruik van variabelen: azureStorageLinkedService en dataFactoryName die zijn gedefinieerd in de sjabloon. 

#### <a name="azure-blob-input-dataset"></a>Azure Blob-invoergegevensset
De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount. In de gegevenssetdefinitie van de Azure-blob geeft u de namen op van de blobcontainer, map en het bestand met de invoergegevens op. Zie [Eigenschappen van de Azure Blob-gegevensset](connector-azure-blob-storage.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset. 

```json
{
    "type": "datasets",
    "name": "[variables('inputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'), '/')]",
        "fileName": "[parameters('inputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
},

```

#### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset
U geeft de naam op van de map in de Azure-blobopslag die de gekopieerde gegevens uit de invoermap bevat. Zie [Eigenschappen van de Azure Blob-gegevensset](connector-azure-blob-storage.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een Azure Blob-gegevensset. 

```json
{
    "type": "datasets",
    "name": "[variables('outputDatasetName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
        "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'), '/')]",
        "fileName": "[parameters('outputBlobName')]"
    },
    "linkedServiceName": {
        "referenceName": "[variables('azureStorageLinkedServiceName')]",
        "type": "LinkedServiceReference"
    }
    }
}
```

#### <a name="data-pipeline"></a>Gegevenspijplijn
U definieert een pijplijn waarmee gegevens uit de ene Azure Blob-gegevensset naar de andere Azure Blob-gegevensset worden gekopieerd. Zie [JSON-bestand voor een pijplijn](concepts-pipelines-activities.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt voor het definiëren van een pijplijn in dit voorbeeld. 

```json
{
    "type": "pipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
    "[parameters('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]",
    "[variables('inputDatasetName')]",
    "[variables('outputDatasetName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
    "activities": [
        {
        "type": "Copy",
        "typeProperties": {
            "source": {
            "type": "BlobSource"
            },
            "sink": {
            "type": "BlobSink"
            }
        },
        "name": "MyCopyActivity",
        "inputs": [
            {
            "referenceName": "[variables('inputDatasetName')]",
            "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
            "referenceName": "[variables('outputDatasetName')]",
            "type": "DatasetReference"
            }
        ]
        }
    ]
    }
}
```

#### <a name="trigger"></a>Trigger
U definieert een trigger die de pijplijn eenmaal per uur uitvoert. De geïmplementeerde trigger is gestopt. Start de trigger via de cmdlet **Start-AzureRmDataFactoryV2Trigger**. Zie het artikel [Pijplijnen uitvoeren en triggers](concepts-pipeline-execution-triggers.md#triggers) voor meer informatie over triggers. 

```json
{
    "type": "triggers",
    "name": "[variables('triggerName')]",
    "dependsOn": [
        "[parameters('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('inputDatasetName')]",
        "[variables('outputDatasetName')]",
        "[variables('pipelineName')]"
    ],
    "apiVersion": "2017-09-01-preview",
    "properties": {
        "type": "ScheduleTrigger",
        "typeProperties": {
            "recurrence": {
                "frequency": "Hour",
                "interval": 1,
                "startTime": "2017-11-28T00:00:00",
                "endTime": "2017-11-29T00:00:00",
                "timeZone": "UTC"               
            }
        },
        "pipelines": [{
            "pipelineReference": {
                "type": "PipelineReference",
                "referenceName": "ArmtemplateSampleCopyPipeline"
            },
            "parameters": {}
        }]
    }
}
```

## <a name="reuse-the-template"></a>De sjabloon hergebruiken
U hebt in de zelfstudie een sjabloon voor het definiëren van Data Factory-entiteiten en een sjabloon voor het doorgeven van waarden voor parameters gemaakt. Als u dezelfde sjabloon wilt gebruiken voor het implementeren van Data Factory-entiteiten in verschillende omgevingen, maakt u een parameterbestand voor elke omgeving en gebruikt u dit bij het implementeren in die omgeving.     

Voorbeeld:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
De eerste opdracht maakt gebruik van het parameterbestand voor de ontwikkelomgeving, de tweede voor de testomgeving en de derde voor de productieomgeving.  

U kunt de sjabloon ook hergebruiken om herhaalde taken uit te voeren. U kunt bijvoorbeeld veel data factory's maken met een of meer pijplijnen die dezelfde logica implementeren, waarbij elke data factory echter gebruikmaakt van andere Azure Storage-accounts. In dit scenario gebruikt u dezelfde sjabloon in dezelfde omgeving (voor het ontwikkelen, testen of de productie) met andere parameterbestanden om de gegevensfactory's te maken. 


## <a name="next-steps"></a>Volgende stappen
Met de pijplijn in dit voorbeeld worden gegevens gekopieerd van de ene locatie naar een andere locatie in een Azure Blob-opslag. Doorloop de [zelfstudies](tutorial-copy-data-dot-net.md) voor meer informatie over het gebruiken van Data Factory in andere scenario's. 
