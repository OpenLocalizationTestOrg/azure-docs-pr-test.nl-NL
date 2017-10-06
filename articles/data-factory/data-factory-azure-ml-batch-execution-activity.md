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
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Maak voorspellende pijplijnen met behulp van Azure Machine Learning en Azure Data Factory

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

## <a name="introduction"></a>Inleiding

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Hiermee schakelt u toobuild, testen en implementeren van predictive analytics-oplossingen. Het is voltooid uit op hoog niveau oogpunt in drie stappen:

1. **Maken van een trainingsexperiment**. U doen deze stap met behulp van hello Azure ML Studio. Hallo ML studio is een gezamenlijke visual ontwikkelomgeving tootrain te gebruiken en testen van een predictive analytics-model met trainingsgegevens.
2. **Converteert u deze tooa Voorspellend experiment**. Nadat uw model is getraind met bestaande gegevens en u klaar toouse bent deze nieuwe gegevens tooscore, bereiden en het stroomlijnen van uw experiment voor score berekenen.
3. **Als een webservice implementeren**. U kunt uw scoreprofiel experiment publiceren als een Azure-web-service. U kunt tooyour gegevensmodel via deze web service-eindpunt te verzenden en ontvangen resultaat voorspellingen van Hallo-model.  

### <a name="azure-data-factory"></a>Azure Data Factory
Data Factory is een cloud-gebaseerde gegevens integration-service die ingedeeld en automatiseert Hallo **verkeer** en **transformatie** van gegevens. U kunt gegevens integratieoplossingen maken gebruik van Azure Data Factory die kunnen gegevens uit verschillende gegevensarchieven opnemen, transformatieproces Hallo gegevens publiceren Hallo resultaat toohello gegevens gegevensarchieven.

Data Factory-service kunt u toocreate gegevenspijplijnen verplaatsen en gegevens transformeren en Voer Hallo pijplijnen volgens een opgegeven schema (elk uur, dagelijks, wekelijks, enzovoort). Ook biedt uitgebreide visualisaties toodisplay hello afkomstinformatie en afhankelijkheden tussen uw gegevenspijplijnen en uw gegevenspijplijnen van een één centrale weergave tooeasily baseren problemen bewaken en waarschuwingen voor toepassingsbewaking instellen.

Zie [inleiding tooAzure Data Factory](data-factory-introduction.md) en [bouwen van uw eerste pijplijn](data-factory-build-your-first-pipeline.md) artikelen tooquickly aan de slag met hello Azure Data Factory-service.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory en Machine Learning samen
Azure Data Factory kunt u tooeasily maken pijplijnen die gebruikmaken van een gepubliceerde [Azure Machine Learning] [ azure-machine-learning] voor predictive analytics-webservice. Met behulp van Hallo **Batchuitvoeringsactiviteit** in een Azure Data Factory-pijplijn, kunt u een Azure ML web service toomake voorspellingen op Hallo-gegevens in een batch aanroept. Zie [aanroepen van een Azure ML-Batchuitvoeringsactiviteit web service gebruikmaakt van Hallo](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sectie voor meer informatie.

Na verloop van tijd moeten Hallo voorspellende modellen in hello Azure ML scoreprofiel experimenten toobe retrained met nieuwe invoergegevenssets. U kunt een Azure ML-model van een Data Factory-pijplijn retrain Hallo volgende stappen uit als volgt:

1. Hallo trainingsexperiment (geen Voorspellend experiment) publiceren als een webservice. Deze stap in hello Azure ML Studio doet u net als tooexpose Voorspellend experiment als een webservice in Hallo voorgaande scenario.
2. Hello Azure ML-Batchuitvoeringsactiviteit tooinvoke Hallo-webservice voor Hallo trainingsexperiment gebruiken. U kunt in principe hello Azure ML-Batchuitvoering activiteit tooinvoke zowel webservice trainings- en score berekenen voor web-service gebruiken.

Nadat u klaar bent met de retraining, bijwerken Hallo score berekenen voor web-service (Voorspellend experiment weergegeven als een webservice) met Hallo zojuist getrainde model met behulp van Hallo **Azure ML-Resourceactiviteit**. Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Batchuitvoeringsactiviteit met een webservice wordt aangeroepen
U gebruikt Azure Data Factory tooorchestrate gegevensverplaatsing en verwerking en vervolgens uitvoert met Azure Machine Learning-batchuitvoering. Hier volgen op het hoogste niveau Hallo-stappen:

1. Maak een Azure Machine Learning gekoppelde service. U moet Hallo volgende waarden:

   1. **URI van de aanvraag** voor Hallo Batch-API voor uitvoering. U kunt Hallo aanvraag-URI vinden door te klikken op Hallo **BATCHUITVOERING** koppeling op Hallo services webpagina.
   2. **API-sleutel** voor Hallo gepubliceerd Azure Machine Learning-webservice. U kunt Hallo API-sleutel vinden door te klikken op Hallo-webservice die u hebt gepubliceerd.
   3. Gebruik Hallo **AzureMLBatchExecution** activiteit.

      ![Machine Learning-Dashboard](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Scenario: Experimenten met behulp van Web service invoer/uitvoer die toodata in Azure Blob Storage verwijst
In dit scenario hello Azure Machine Learning-webservice maakt voorspellingen met gegevens uit een bestand in een Azure blob storage en slaat Hallo voorspelling resultaten in Hallo blob-opslag. Hallo definieert volgende JSON een Data Factory-pijplijn met een AzureMLBatchExecution-activiteit. Hallo-activiteit heeft Hallo gegevensset **DecisionTreeInputBlob** als invoer en **DecisionTreeResultBlob** als Hallo uitvoer. Hallo **DecisionTreeInputBlob** is doorgegeven als een webservice van invoer toohello door Hallo met **webServiceInput** JSON-eigenschap. Hallo **DecisionTreeResultBlob** wordt doorgegeven als uitvoer toohello webservice door met de Hallo **webServiceOutputs** JSON-eigenschap.  

> [!IMPORTANT]
> Als webservice Hallo meerdere invoer heeft, gebruikt u Hallo **webServiceInputs** in plaats van de eigenschap **webServiceInput**. Zie Hallo [webservice vereist meerdere invoeritems](#web-service-requires-multiple-inputs) sectie voor een voorbeeld van het gebruik van Hallo webServiceInputs eigenschap.
>
> Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInput**/**webServiceInputs** en **webServiceOutputs** eigenschappen (in  **typeProperties**) moet ook zijn opgenomen in Hallo activiteit **invoer** en **levert**.
>
> In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen. Hallo namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen moeten exact overeenkomen met Hallo-namen in Hallo experimenten. U kunt de aanvraaglading van de steekproef Hallo bekijken op Hallo Batch uitvoering Help-pagina voor uw Azure ML-eindpunt tooverify Hallo verwacht toewijzing.
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
> Alleen invoer en uitvoer van Hallo AzureMLBatchExecution activiteit kunnen worden doorgegeven als parameters toohello webservice. In Hallo hierboven JSON-codefragment is DecisionTreeInputBlob bijvoorbeeld een invoer toohello AzureMLBatchExecution activiteit, die is doorgegeven als een invoer toohello webservice via webServiceInput-parameter.   
>
>

### <a name="example"></a>Voorbeeld
In dit voorbeeld maakt gebruik van Azure Storage toohold beide Hallo en uitvoergegevens.

Het is raadzaam dat u Hallo doorloopt [bouwen van uw eerste pijplijn met Data Factory] [ adf-build-1st-pipeline] zelfstudie voordat u verdergaat met het volgende voorbeeld. Hallo Data Factory-Editor toocreate Data Factory-artefacten (gekoppelde services, gegevenssets, pijplijn) in dit voorbeeld gebruiken.   

1. Maak een **gekoppelde service** voor uw **Azure Storage**. Als hello invoer en uitvoer bestanden zich in verschillende storage-accounts, moet u twee gekoppelde services. Hier volgt een voorbeeld van JSON:

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
2. Hallo maken **invoer** Azure Data Factory **gegevensset**. In tegenstelling tot een aantal andere Data Factory-gegevenssets deze gegevenssets, beide moet bevatten **folderPath** en **fileName** waarden. U kunt gebruiken partitionering toocause elke batch uitvoering (elke gegevenssegment) tooprocess of unieke invoer produceren en uitvoerbestanden. Mogelijk moet u tooinclude sommige upstream-activiteit tootransform Hallo invoer voor Hallo CSV-bestandsindeling en plaats deze in Hallo storage-account voor elk segment. In dat geval zou u geen Hallo opgenomen **externe** en **externalData** instellingen die worden weergegeven in de volgende Hallo voorbeeld en uw DecisionTreeInputBlob hello uitvoergegevensset van een andere activiteit zou zijn.

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

    Uw invoer csv-bestand moet Hallo kolom veldnamenrij hebben. Als u van Hallo gebruikmaakt **Kopieeractiviteit** toocreate of verplaatsen Hallo csv in Hallo blob-opslag, moet u Hallo sink-eigenschap instellen **blobWriterAddHeader** te**true**. Bijvoorbeeld:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Als Hallo CSV-bestand geen veldnamenrij hello heeft, ziet u mogelijk Hallo volgende fout: **fout in de activiteit: fout bij het lezen van de tekenreeks. Onverwacht token: StartObject. Pad '', regel 1, positie 1**.
3. Hallo maken **uitvoer** Azure Data Factory **gegevensset**. Dit voorbeeld wordt partitionering toocreate een unieke uitvoerpad voor de uitvoering van elk segment. Zonder Hallo partitioneren, zou Hallo activiteit Hallo bestand overschreven.

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
4. Maak een **gekoppelde service** van het type: **AzureMLLinkedService**, bieden Hallo API-sleutel en model van de volgende URL.

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
5. Ten slotte schrijft een pijplijn met een **AzureMLBatchExecution** activiteit. Tijdens runtime voert de pijplijn Hallo stappen te volgen:

   1. Hallo-locatie van het invoerbestand Hallo krijgt van uw invoer gegevenssets.
   2. Hello Azure Machine Learning-Batchuitvoering API aanroept
   3. Kopieën Hallo batch uitvoering uitvoer toohello blob gegeven in de uitvoergegevensset.

      > [!NOTE]
      > AzureMLBatchExecution activiteit kan hebben nul of meer invoer en uitvoer van een of meer.
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

      Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601). Bijvoorbeeld: 2014-10-14T16:32:41Z. Hallo **end** tijd is optioneel. Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur.**' toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap. Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.

      > [!NOTE]
      > Invoer voor Hallo AzureMLBatchExecution activiteit opgeven is optioneel.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Scenario: Experimenten met lezer/schrijver Modules toorefer toodata in verschillende gelijksoortig
Bij het maken van Azure ML-experimenten een ander gebruikelijk scenario is toouse lezer en -schrijver modules. leesmodule Hello gebruikte tooload gegevens in een experiment en Hallo-schrijfmodule toosave gegevens vanuit uw experimenten. Zie voor meer informatie over de lezer en -schrijver modules [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek.     

Wanneer u Hallo lezer en -schrijver modules, is het raadzaam om toouse een parameter van de Web service voor elke eigenschap van deze modules lezer/schrijver. Deze web-parameters kunnen u tooconfigure Hallo waarden tijdens runtime. U kunt bijvoorbeeld een experiment maken met een leesmodule die gebruikmaakt van een Azure SQL Database: XXX.database.windows.net. Nadat Hallo web-service is geïmplementeerd, kunt u tooenable Hallo consumenten van Hallo web service toospecify een Azure SQL-Server YYY.database.windows.net aangeroepen. Deze waarde toobe geconfigureerd, kunt u een Web service parameter tooallow gebruiken.

> [!NOTE]
> Web service invoer en uitvoer verschillen van de parameters van Web service. In het eerste scenario hello, hebt u gezien hoe een invoer en uitvoer voor een webservice Azure ML kunnen worden opgegeven. In dit scenario moet u parameters voor een webservice die overeenkomen met tooproperties lezer/schrijver modules doorgeven.
>
>

We bekijken een scenario voor het gebruik van parameters van Web service. U hebt een geïmplementeerde Azure Machine Learning-webservice die gebruikmaakt van een lezer module tooread gegevens uit een van de gegevensbronnen hello wordt ondersteund door Azure Machine Learning (bijvoorbeeld: Azure SQL Database). Nadat de Batchuitvoering hello wordt uitgevoerd, kan Hallo resultaten zijn geschreven met behulp van een module Writer (Azure SQL Database).  Er is geen web-service in- en uitgangen zijn gedefinieerd in Hallo experimenten. In dit geval is het raadzaam dat u de relevante webserviceparameters voor Hallo lezer en -schrijver modules configureert. Deze configuratie kunt Hallo lezer/schrijver modules toobe geconfigureerd wanneer u Hallo AzureMLBatchExecution activiteit. U Web serviceparameters opgeven in Hallo **globalParameters** sectie in Hallo activiteits-JSON als volgt.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

U kunt ook [Data Factory functies](data-factory-functions-variables.md) in het doorgeven van waarden voor Hallo Web serviceparameters zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Hallo Web serviceparameters zijn hoofdlettergevoelig, dus zorg ervoor dat Hallo-namen die u opgeeft in de activiteit Hallo JSON overeenkomen Hallo waarden die worden weergegeven door het Hallo-webservice.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Een lezer module tooread gegevens uit meerdere bestanden in Azure Blob gebruiken
BIG data pijplijnen met activiteiten zoals Pig en Hive kunt produceren van een of meer uitvoerbestanden zonder extensie. Bijvoorbeeld, wanneer u een externe Hive-tabel opgeeft, kunnen de Hallo gegevens voor Hallo externe Hive-tabel worden opgeslagen in Azure blob-opslag Hello naam 000000_0 te volgen. U kunt meerdere bestanden Hallo leesmodule in een experiment tooread gebruiken en deze worden gebruikt voor voorspellingen.

Wanneer u de module reader Hallo in een Azure Machine Learning-experiment, kunt u Azure Blob opgeven als invoer. Hallo-bestanden in hello Azure blob-opslag kunnen worden uitvoerbestanden hello (voorbeeld: 000000_0) die worden geproduceerd door een Pig en Hive-script uitgevoerd op HDInsight. Hallo leesmodule kunt u tooread-bestanden (met er worden geen extensies) door het configureren van Hallo **toocontainer pad, de map/blob**. Hallo **pad toocontainer** punten toohello container en **directory/blob** verwijst toofolder die Hallo bestanden bevat, zoals wordt weergegeven in Hallo installatiekopie te volgen. Hallo sterretje dat wil zeggen, \*) **geeft aan dat alle bestanden in Hallo container of de map Hallo (dat wil zeggen, aggregateddata-gegevens/jaar = maand-2014-6 /\*)** als onderdeel van het Hallo-experiment worden gelezen.

![Azure Blob-eigenschappen](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Voorbeeld
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Pijplijn met AzureMLBatchExecution activiteit met de Parameters van Web Service

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

In de Hallo hierboven JSON-voorbeeld:

* Hallo geïmplementeerd in Azure Machine Learning Web service een lezer en een writer module tooread/gegevens schrijven van gebruikt / tooan Azure SQL Database. Deze webservice beschrijft Hallo na vier parameters: servernaam, databasenaam, servergebruikersnaam en wachtwoord voor gebruikersaccount Server-Database.  
* Beide **start** en **end** tijd moeten [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601). Bijvoorbeeld: 2014-10-14T16:32:41Z. Hallo **end** tijd is optioneel. Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur.**' toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap. Zie de [naslaginformatie voor JSON-scriptverwerking](https://msdn.microsoft.com/library/dn835050.aspx) voor meer informatie over de JSON-eigenschappen.

### <a name="other-scenarios"></a>Andere scenario's
#### <a name="web-service-requires-multiple-inputs"></a>Meerdere invoer is vereist
Als webservice Hallo meerdere invoer heeft, gebruikt u Hallo **webServiceInputs** in plaats van de eigenschap **webServiceInput**. Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInputs** moet ook zijn opgenomen in Hallo activiteit **invoer**.

In uw experiment Azure ML web service invoer of uitvoerpoorten en globale parameters standaardnamen hebben ('input1', 'input2') die u kunt aanpassen. Hallo namen die u voor webServiceInputs en webServiceOutputs globalParameters instellingen moeten exact overeenkomen met Hallo-namen in Hallo experimenten. U kunt de aanvraaglading van de steekproef Hallo bekijken op Hallo Batch uitvoering Help-pagina voor uw Azure ML-eindpunt tooverify Hallo verwacht toewijzing.

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

#### <a name="web-service-does-not-require-an-input"></a>Web-Service vereist geen invoer
Azure ML-batch uitvoering webservices gebruikte toorun geen werkstromen kan worden, bijvoorbeeld R of Python-scripts, kan die niet alle invoer vereisen. Of Hallo experiment kan worden geconfigureerd met een lezer-module die u maakt een GlobalParameters niet beschikbaar. In dat geval Hallo AzureMLBatchExecution activiteit zou als volgt geconfigureerd:

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

#### <a name="web-service-does-not-require-an-inputoutput"></a>Web-Service vereist geen invoer/uitvoer
Hello Azure ML-batch uitvoering web-service mogelijk geen webservice uitvoer geconfigureerd. Er is geen webservice invoer of uitvoer in dit voorbeeld, noch een GlobalParameters zijn geconfigureerd. Er is nog steeds een uitvoer die is geconfigureerd op Hallo activiteit zelf, maar er is geen opgegeven als een webServiceOutput.

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web-Service gebruikt en schrijfprogramma en activiteiten bij uitvoering Hallo alleen wanneer andere activiteiten zijn geslaagd
Hello Azure ML web service lezer en -schrijver modules mogelijk geconfigureerde toorun met of zonder eventuele GlobalParameters. U kunt echter tooembed service aanroepen in een pijplijn die de gegevensset afhankelijkheden tooinvoke Hallo service gebruikt, alleen wanneer er een upstream-verwerking is voltooid. U kunt ook een andere actie activeren nadat het Hallo-batchuitvoering is voltooid met deze benadering. In dat geval kunt u met behulp van activiteit in- en uitgangen, zonder een van deze als webservice in- of uitgangen Hallo-afhankelijkheden uitdrukken.

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

Hallo **takeaways** zijn:

* Als uw experiment-eindpunt maakt gebruik van een webServiceInput: er wordt vertegenwoordigd door een blob-gegevensset en is opgenomen in de activiteitinvoer hello en Hallo webServiceInput eigenschap. Anders is Hallo webServiceInput eigenschap weggelaten.
* Als uw experiment-eindpunt maakt gebruik van webServiceOutput(s): ze worden vertegenwoordigd door de blob-gegevenssets en zijn opgenomen in de uitvoer voor activiteiten hello en in Hallo webServiceOutputs eigenschap. Hallo activiteit uitvoer en webServiceOutputs met de naam van elke uitvoer in Hallo experiment Hallo zijn toegewezen. Anders wordt wordt de eigenschap webServiceOutputs hello weggelaten.
* Als uw experiment eindpunt globalParameter(s) beschrijft, wordt verstrekt in de Activiteitseigenschap globalParameters Hallo als sleutel-waardeparen. Anders wordt wordt de eigenschap globalParameters hello weggelaten. Hallo-sleutels zijn hoofdlettergevoelig. [Azure Data Factory-functies](data-factory-functions-variables.md) kan worden gebruikt in Hallo waarden.
* Aanvullende gegevenssets kan worden opgenomen in Hallo in- en uitgangen activiteitseigenschappen, zonder waarnaar wordt verwezen in Hallo activiteit typeProperties. Deze gegevenssets kan worden uitgevoerd segment afhankelijkheden reguleren maar anders worden genegeerd door Hallo AzureMLBatchExecution activiteit.


## <a name="updating-models-using-update-resource-activity"></a>Bijwerken van modellen Update Resource activiteit
Nadat u klaar bent met de retraining, bijwerken Hallo score berekenen voor web-service (Voorspellend experiment weergegeven als een webservice) met Hallo zojuist getrainde model met behulp van Hallo **Azure ML-Resourceactiviteit**. Zie [bijwerken met behulp van de Update Resourceactiviteit modellen](data-factory-azure-ml-update-resource-activity.md) artikel voor meer informatie.

### <a name="reader-and-writer-modules"></a>Lezer en Writer Modules
Een veelvoorkomend scenario voor het gebruik van parameters voor Web-service is Hallo gebruik van Azure SQL en schrijfprogramma. leesmodule Hello is gebruikte tooload gegevens in een experiment van data management-services buiten Azure Machine Learning Studio. Hallo-schrijfmodule is toosave gegevens vanuit uw experimenten in beheerservices gegevens buiten Azure Machine Learning Studio.  

Zie voor meer informatie over Azure-Blob/Azure SQL-lezer/schrijver [lezer](https://msdn.microsoft.com/library/azure/dn905997.aspx) en [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) onderwerpen op MSDN-bibliotheek. Hallo-voorbeeld in de vorige sectie Hallo gebruikt hello Azure Blob-lezer en Azure Blob-schrijver. Deze sectie beschrijft het gebruik van Azure SQL-reader en Azure SQL writer.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
**V:** ik heb meerdere bestanden die worden gegenereerd door mijn pijplijnen big data. Kan ik Hallo AzureMLBatchExecution activiteit toowork op alle Hallo-bestanden gebruiken?

**A:** Ja. Zie Hallo **met een lezer module tooread gegevens uit meerdere bestanden in Azure Blob** sectie voor meer informatie.

## <a name="azure-ml-batch-scoring-activity"></a>Score berekenen voor Azure ML-Batch-activiteit
Als u van Hallo gebruikmaakt **AzureMLBatchScoring** activiteit toointegrate met Azure Machine Learning, wordt aangeraden dat u Hallo meest recente **AzureMLBatchExecution** activiteit.

Hallo AzureMLBatchExecution activiteit is geïntroduceerd in Hallo augustus 2015-release van Azure SDK en Azure PowerShell.

Als u toocontinue hello AzureMLBatchScoring activiteit wilt, blijven lezen via deze sectie.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Azure ML-Batchscoreberekening activiteit voor het gebruik van Azure Storage voor invoer/uitvoer

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

### <a name="web-service-parameters"></a>Parameters voor Web-Service
toospecify waarden voor de Web service-parameters, Voeg een **typeProperties** sectie toohello **AzureMLBatchScoringActivty** sectie in Hallo pijplijn JSON zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
U kunt ook [Data Factory functies](data-factory-functions-variables.md) in het doorgeven van waarden voor Hallo Web serviceparameters zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Hallo Web serviceparameters zijn hoofdlettergevoelig, dus zorg ervoor dat Hallo-namen die u opgeeft in de activiteit Hallo JSON overeenkomen Hallo waarden die worden weergegeven door het Hallo-webservice.
>
>

## <a name="see-also"></a>Zie ook
* [Azure blogbericht: aan de slag met Azure Data Factory en Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
