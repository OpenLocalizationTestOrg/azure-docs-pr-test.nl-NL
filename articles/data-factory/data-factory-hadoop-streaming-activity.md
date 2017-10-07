---
title: aaaTransform gegevens met Hadoop-Streamingactiviteit - Azure | Microsoft Docs
description: Meer informatie over hoe u Hallo Hadoop-Streamingactiviteit in een Azure data factory tootransform gegevens kunt gebruiken met Hadoop-Streaming programma's uitvoeren op een op-verzoek/uw eigen HDInsight-cluster.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Transformeer gegevens met Hadoop-Streamingactiviteit in Azure Data Factory
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

U kunt een Hadoop-Streaming-taak van een Azure Data Factory-pijplijn Hallo HDInsightStreamingActivity activiteit worden aangeroepen. Hallo toont volgende JSON-fragment Hallo-syntaxis voor het gebruik van Hallo HDInsightStreamingActivity in een pijplijn-JSON-bestand. 

Hallo Streaming HDInsight-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) Hadoop-Streaming programma's worden uitgevoerd op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight cluster. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.

> [!NOTE] 
> Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest. 

## <a name="json-sample"></a>JSON-voorbeeld
Hallo HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt). Standaard is de naam van Hallo-container die wordt gebruikt door Hallo HDInsight-cluster Hallo-naam van Hallo cluster zelf. Als de clusternaam van uw myhdicluster is, zou naam van Hallo blob-container die is gekoppeld myhdicluster zijn. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Houd er rekening mee Hallo volgende punten:

1. Set Hallo **linkedServiceName** toohello naam Hallo gekoppelde service die wijst tooyour HDInsight-cluster op welke Hallo streaming mapreduce taak wordt uitgevoerd.
2. Hallo type Hallo activiteit te ingesteld**HDInsightStreaming**.
3. Voor Hallo **mapper** eigenschap Hallo naam opgeven van uitvoerbare toewijzen. In voorbeeld Hallo is cat.exe Hallo mapper uitvoerbare.
4. Voor Hallo **reducer** eigenschap Hallo-naam van de uitvoerbare reducer opgeven. In voorbeeld Hallo is wc.exe hello reducer uitvoerbare.
5. Voor Hallo **invoer** eigenschap type, Hallo invoerbestand (inclusief Hallo locatie) opgeven voor Hallo toewijzen. In Hallo-voorbeeld: ' wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt ': adfsample is Hallo blob-container, gegevens-voorbeeld/Gutenberg Hallo-map en davinci.txt Hallo blob is.
6. Voor Hallo **uitvoer** eigenschap type, Hallo uitvoerbestand (inclusief Hallo locatie) voor Hallo reducer opgeven. Hallo-uitvoer van Hallo Hadoop streamingtaak geschreven toohello locatie die is opgegeven voor deze eigenschap.
7. In Hallo **filePaths** sectie, geeft u Hallo paden voor Hallo toewijzen en reducer uitvoerbare bestanden. In Hallo-voorbeeld: 'adfsample/example/apps/wc.exe' adfsample is Hallo blob-container, voorbeeld/apps Hallo-map en wc.exe Hallo uitvoerbare is.
8. Voor Hallo **fileLinkedService** eigenschap hello Azure Storage gekoppelde service die vertegenwoordigt hello Azure-opslag met Hallo-bestanden die zijn opgegeven in Hallo filePaths sectie opgeven.
9. Voor Hallo **argumenten** eigenschap Hallo-argumenten voor streaming-taak Hallo opgeven.
10. Hallo **getDebugInfo** eigenschap is een optioneel element. Wanneer deze tooFailure is ingesteld, worden alleen op fout Hallo logboeken gedownload. Wanneer deze tooAlways is ingesteld, worden altijd logboeken ongeacht de uitvoeringsstatus van Hallo gedownload.

> [!NOTE]
> In het Hallo-voorbeeld ziet u een uitvoergegevensset voor Hadoop-Streamingactiviteit Hallo voor Hallo opgeven **levert** eigenschap. Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning. U hoeft geen toospecify invoergegevensset voor de activiteit voor Hallo Hallo **invoer** eigenschap.  
> 
> 

## <a name="example"></a>Voorbeeld
Hallo-pijplijn in dit scenario voert Hallo aantal woorden streaming kaart/verminderen programma op Azure HDInsight-cluster. 

### <a name="linked-services"></a>Gekoppelde services
#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
U maakt eerst een gekoppelde service toolink hello Azure Storage dat wordt gebruikt door hello Azure HDInsight-cluster toohello Azure data factory. Als u kopiëren en plakken Hallo code te volgen, vergeet niet tooreplace account naam en een account met Hallo naam en sleutel van uw Azure-opslag. 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Azure gekoppelde HDInsight-service
Vervolgens maakt u een gekoppelde service toolink uw Azure HDInsight-cluster toohello Azure-gegevensfactory. Als kopiëren en plakken van Hallo na code vervangen door de naam van de HDInsight-cluster Hallo-naam van uw HDInsight-cluster en waarden van gebruikersnaam en wachtwoord wijzigen. 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>Gegevenssets
#### <a name="output-dataset"></a>Uitvoergegevensset
Hallo-pijplijn in dit voorbeeld vindt niet alle invoer. U een uitvoergegevensset voor Hallo Streaming HDInsight-activiteit. Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pijplijn
Hallo-pijplijn in dit voorbeeld heeft slechts één activiteit die is van het type: **HDInsightStreaming**. 

Hallo HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt). Standaard is de naam van Hallo-container die wordt gebruikt door Hallo HDInsight-cluster Hallo-naam van Hallo cluster zelf. Als de clusternaam van uw myhdicluster is, zou naam van Hallo blob-container die is gekoppeld myhdicluster zijn.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>Zie ook
* [Hive-activiteit](data-factory-hive-activity.md)
* [Pig-activiteit](data-factory-pig-activity.md)
* [MapReduce-activiteit](data-factory-map-reduce.md)
* [Spark-programma's aanroepen](data-factory-spark.md)
* [R-scripts aanroepen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

