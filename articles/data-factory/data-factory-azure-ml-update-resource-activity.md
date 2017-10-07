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
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Azure Machine Learning-modellen Update Resource activiteit bijwerken

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive-activiteit](data-factory-hive-activity.md) 
> * [Pig-activiteit](data-factory-pig-activity.md)
> * [MapReduce-activiteit](data-factory-map-reduce.md)
> * [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
> * [Spark-activiteit](data-factory-spark.md)
> * [Machine Learning-batchuitvoeringsactiviteit](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning-activiteit resources bijwerken](data-factory-azure-ml-update-resource-activity.md)
> * [Opgeslagen procedureactiviteit](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md)
> * [Aangepaste activiteit .NET](data-factory-use-custom-activities.md)

In dit artikel aanvullingen Hallo belangrijkste Azure Data Factory - artikel voor Azure Machine Learning-integratie: [voorspellende pijplijnen met behulp van Azure Machine Learning en Azure Data Factory maken](data-factory-azure-ml-batch-execution-activity.md). Als u dit nog niet hebt gedaan, raadpleegt u de belangrijkste artikel Hallo voordat gelezen in dit artikel. 

## <a name="overview"></a>Overzicht
Na verloop van tijd moeten Hallo voorspellende modellen in hello Azure ML scoreprofiel experimenten toobe retrained met nieuwe invoergegevenssets. Wanneer u klaar bent met de retraining, wilt u tooupdate Hallo score berekenen voor webservice Hello retrained ML-model. Hallo gebruikelijke stappen tooenable retraining en bijwerken van Azure ML-modellen via webservices zijn:

1. Maken van een experiment in [Azure ML Studio](https://studio.azureml.net).
2. Wanneer u tevreden met Hallo model bent, Azure ML Studio toopublish webservices gebruiken voor beide Hallo **trainingsexperiment** en score berekenen /**Voorspellend experiment**.

Hallo beschrijft volgende tabel Hallo-webservices in dit voorbeeld gebruikt.  Zie [Retrain Machine Learning-modellen programmatisch](../machine-learning/machine-learning-retrain-models-programmatically.md) voor meer informatie.

- **Training webservice** - trainingsgegevens ontvangt en getraind modellen produceert. Hallo-uitvoer van Hallo retraining is een .ilearner-bestand in een Azure-blobopslag. Hallo **standaard eindpunt** wordt automatisch gemaakt voor u wanneer u Hallo training publiceert als een webservice experimenteren. U kunt meer eindpunten maken maar Hallo voorbeeld wordt alleen het standaardeindpunt Hallo.
- **Score berekenen voor webservice** - voorbeelden zonder label gegevens ontvangt en voorspellingen maakt. Hallo-uitvoer van de voorspelling kan verschillende vormen, zoals een CSV-bestand of rijen in een Azure SQL database, afhankelijk van de configuratie Hallo van Hallo experiment hebben. Hallo standaardeindpunt wordt automatisch voor u gemaakt wanneer u een Voorspellend experiment Hallo als een webservice publiceert. 

Hallo ziet volgende afbeelding u Hallo relatie tussen de trainings- en eindpunten in de Azure ML score.

![Webservices](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Hallo kunnen worden aangeroepen **training webservice** met behulp van Hallo **Azure ML-Batchuitvoeringsactiviteit**. Aanroepen van een webservice training is hetzelfde als het aanroepen van een Azure ML webservice (score berekenen voor web-service) voor scoreprofiel gegevens. Hallo voorgaande secties behandeld hoe tooinvoke een webservice Azure ML uit een Azure Data Factory pijplijn in detail. 

Hallo kunnen worden aangeroepen **score berekenen voor webservice** met behulp van Hallo **Resourceactiviteit voor Azure ML Update** tooupdate Hallo-webservice met Hallo zojuist getrainde model. Hallo volgen voorbeelden bevatten definities van de gekoppelde service: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Score berekenen voor web-service is een klassieke webservice
Als Hallo score berekenen voor web-service is een **klassieke webservice**, Hallo tweede maken **niet-standaard en bij te werken eindpunt** met behulp van Hallo [Azure-portal](https://manage.windowsazure.com). Zie [eindpunten maken](../machine-learning/machine-learning-create-endpoint.md) artikel voor stappen. Nadat u Hallo niet standaard worden bijgewerkt eindpunt hebt gemaakt, Hallo stappen te volgen:

* Klik op **BATCHUITVOERING** tooget Hallo URI-waarde voor Hallo **mlEndpoint** JSON-eigenschap.
* Klik op **UPDATE RESOURCE** tooget Hallo URI-waarde voor Hallo koppelen **updateResourceEndpoint** JSON-eigenschap. Hallo-API-sleutel is op Hallo eindpunt pagina zelf (in de rechterbenedenhoek Hallo).

![eindpunt bij te werken](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Hallo volgende voorbeeld bevat een voorbeeld JSON-definitie voor Hallo voor met AzureML gekoppelde service. Hallo gekoppelde service gebruikt Hallo apiKey voor authenticatie.  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Score berekenen voor web-service is Azure Resource Manager-webservice 
Als webservice Hallo Hallo nieuw type webservice die een Azure Resource Manager-eindpunt wordt is, hoeft u niet tooadd Hallo tweede **niet-standaard** eindpunt. Hallo **updateResourceEndpoint** in Hallo gekoppelde service van Hallo-indeling is: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

U kunt waarden voor de houders plaats in Hallo-URL krijgen bij het opvragen van de webservice Hallo op Hallo [Azure Machine Learning Web Services-Portal](https://services.azureml.net/). Hallo nieuwe type update resource eindpunt vereist een token van AAD (Azure Active Directory). Geef **servicePrincipalId** en **servicePrincipalKey**in voor met AzureML gekoppelde service. Zie [hoe toocreate service-principal en machtigingen toomanage Azure-resource toewijzen](../azure-resource-manager/resource-group-create-service-principal-portal.md). Hier volgt een voorbeeld van een definitie van AzureML gekoppelde service: 

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

Hallo biedt volgende scenario meer details. Er is een voorbeeld voor retraining en bijwerken van Azure ML-modellen van een Azure Data Factory-pijplijn.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Scenario: retraining en bijwerken van een Azure ML-model
Deze sectie vindt u een voorbeeldpijplijn die gebruikmaakt van Hallo **Azure ML-Batchuitvoering activiteit** tooretrain een model. Hallo pijplijn gebruikt ook Hallo **resourceactiviteit voor Azure ML Update** tooupdate Hallo-model in Hallo score berekenen voor web-service. Hallo bevat ook aan JSON codefragmenten voor alle gekoppelde services, gegevenssets en pijplijn in voorbeeld Hallo Hallo.

Hier volgt de diagramweergave Hallo van Hallo-voorbeeldpijplijn. Zoals u ziet, hello Azure ML-Batchuitvoeringsactiviteit Hallo training invoer- en wordt de uitvoer van een training (iLearner-bestand). Hallo Resourceactiviteit voor Azure ML-Update wordt de uitvoer van deze training en updates Hallo Hallo webservice-eindpunt score-model. Hallo Update Resourceactiviteit produceert geen uitvoer. Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.

![Pipeline-diagram](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Azure Blob-opslag gekoppelde service:
Hello Azure Storage bevat Hallo gegevens te volgen:

* trainingsgegevens. Hallo invoergegevens voor hello Azure ML training-webservice.  
* iLearner-bestand. Hallo de uitvoer van hello Azure ML training-webservice. Dit bestand is ook Hallo invoer toohello resourceactiviteit voor Update.  

Hier volgt Hallo voorbeeld JSON-definitie van Hallo gekoppelde service:

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

### <a name="training-input-dataset"></a>Training invoergegevensset:
Hallo vertegenwoordigt volgende gegevensset Hallo invoer trainingsgegevens voor hello Azure ML training-webservice. Deze gegevensset neemt Hello Azure ML-Batchuitvoering activiteit als invoer.

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

### <a name="training-output-dataset"></a>Uitvoergegevensset voor training:
Hallo vertegenwoordigt volgende gegevensset Hallo uitvoer iLearner-bestand van hello Azure ML training-webservice. Hello Azure ML-Batchuitvoeringsactiviteit produceert deze dataset. Deze gegevensset is ook Hallo invoer toohello resourceactiviteit voor Azure ML-Update.

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Gekoppelde service voor Azure ML training eindpunt
Hallo volgende JSON-codefragment definieert een Azure Machine Learning gekoppelde service die toohello standaardeindpunt van Hallo training webservice verwijst.

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

In **Azure ML Studio**, Hallo volgende tooget waarden voor **mlEndpoint** en **apiKey**:

1. Klik op **WEBSERVICES** op Hallo linkermenu.
2. Klik op Hallo **training webservice** in de lijst Hallo van webservices.
3. Klik op kopiëren naast te**API-sleutel** in het tekstvak. Hallo-sleutel op Hallo Klembord in Hallo Data Factory JSON-editor plakken.
4. In Hallo **Azure ML studio**, klikt u op **BATCHUITVOERING** koppeling.
5. Kopiëren Hallo **aanvraag-URI** van Hallo **aanvragen** sectie en plak deze in Hallo Data Factory JSON-editor.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Gekoppelde Service voor Azure ML bijwerkbare score-eindpunt:
Hallo volgende JSON-codefragment definieert een Azure Machine Learning gekoppelde service die toohello niet standaard worden bijgewerkt eindpunt Hallo score berekenen voor webservice verwijst.  

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

### <a name="placeholder-output-dataset"></a>Tijdelijke aanduiding voor uitvoergegevensset:
Hallo resourceactiviteit voor Azure ML-Update wordt geen uitvoer gegenereerd. Azure Data Factory vereist echter een output dataset toodrive Hallo planning van een pijplijn. Daarom gebruiken we een dummy/tijdelijke aanduiding voor gegevensset in dit voorbeeld.  

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

### <a name="pipeline"></a>Pijplijn
Hallo pipeline heeft twee activiteiten: **AzureMLBatchExecution** en **AzureMLUpdateResource**. Hello Azure ML-Batchuitvoering activiteit duurt Hallo trainingsgegevens als invoer en een iLearner-bestand als uitvoer produceert. Hallo activiteit roept Hallo training webservice (trainingsexperiment weergegeven als een webservice) met Hallo invoer trainen van gegevens en Hallo ilearner-bestand van de webservice Hallo ontvangt. Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.

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
