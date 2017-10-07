---
title: aaaInvoke MapReduce-programma van Azure Data Factory
description: Meer informatie over hoe tooprocess gegevens door MapReduce-programma's uitvoeren op een Azure HDInsight-cluster van een Azure data factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Aanroepen van MapReduce-programma's uit Data Factory
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

Hallo HDInsight MapReduce-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) MapReduce-programma's worden uitgevoerd op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.

> [!NOTE] 
> Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.  

## <a name="introduction"></a>Inleiding
Een pijplijn in een Azure data factory verwerkt gegevens in gekoppelde storage-services met behulp van gekoppelde compute services. Het bevat een reeks activiteiten, waarbij elke activiteit uitvoert voor een specifieke verwerking. In dit artikel wordt beschreven hoe Hallo HDInsight MapReduce-activiteit.

Zie [Pig](data-factory-pig-activity.md) en [Hive](data-factory-hive-activity.md) voor meer informatie over het uitvoeren van Pig/Hive scripts op een Windows, Linux-gebaseerde HDInsight-cluster van een pijplijn met behulp van HDInsight Pig en Hive-activiteiten. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON voor HDInsight MapReduce-activiteit
In de JSON-definitie voor HDInsight-activiteit Hallo Hallo: 

1. Set Hallo **type** Hallo **activiteit** te**HDInsight**.
2. Hallo naam opgeven van de klasse Hallo voor **className** eigenschap.
3. Geef Hallo pad toohello JAR-bestand inclusief de bestandsnaam Hallo voor **jarFilePath** eigenschap.
4. Geef Hallo gekoppelde service die toohello Azure Blob Storage met Hallo JAR-bestand voor verwijst **jarLinkedService** eigenschap.   
5. Geef geen argumenten voor Hallo MapReduce-programma in Hallo **argumenten** sectie. Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework. toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
U kunt Hallo HDInsight MapReduce-activiteit toorun elk MapReduce jar-bestand op een HDInsight-cluster gebruiken. Volgende voorbeeld JSON-definitie van een pijplijn, Hallo HDInsight-activiteit is geconfigureerd in Hallo toorun een Mahout JAR-bestand.

## <a name="sample-on-github"></a>Voorbeeld op GitHub
U kunt een voorbeeld voor het gebruik van HDInsight MapReduce-activiteit Hallo downloaden van: [Data Factory-voorbeelden op GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Hallo Word-Count-programma uitvoeren
Hallo pijplijn in dit voorbeeld Hallo aantal woorden kaart/verminderen programma op Azure HDInsight-cluster wordt uitgevoerd.   

### <a name="linked-services"></a>Gekoppelde Services
U maakt eerst een gekoppelde service toolink hello Azure Storage dat wordt gebruikt door hello Azure HDInsight-cluster toohello Azure data factory. Als kopiëren en plakken van Hallo na code vergeet niet tooreplace **accountnaam** en **accountsleutel** met Hallo naam en sleutel van uw Azure-opslag. 

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service

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
Vervolgens maakt u een gekoppelde service toolink uw Azure HDInsight-cluster toohello Azure-gegevensfactory. Als kopiëren en plakken van Hallo na code vervangt **de naam van de HDInsight-cluster** met Hallo-naam van uw HDInsight-cluster en de wijziging waarden gebruikersnaam en wachtwoord.   

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
Hallo-pijplijn in dit voorbeeld vindt niet alle invoer. U een uitvoergegevensset voor Hallo HDInsight MapReduce-activiteit. Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Pijplijn
Hallo-pijplijn in dit voorbeeld heeft slechts één activiteit die is van het type: HDInsightMapReduce. Enkele belangrijke eigenschappen van de Hallo in Hallo JSON zijn: 

| Eigenschap | Opmerkingen |
|:--- |:--- |
| type |Hallo-type te moet worden ingesteld**HDInsightMapReduce**. |
| className |Naam van de klasse Hallo is: **wordcount** |
| jarFilePath |Pad toohello jar-bestand met Hallo-klasse. Als kopiëren en plakken van Hallo na code vergeet niet toochange Hallo-naam van Hallo-cluster. |
| jarLinkedService |Gekoppelde Azure Storage-service die Hallo jar-bestand bevat. Deze gekoppelde service verwijst toohello opslag die is gekoppeld aan Hallo HDInsight-cluster. |
| Argumenten |Hallo wordcount wordt gehouden met twee argumenten, invoer en uitvoer. Hallo-bestand voor invoer is Hallo davinci.txt bestand. |
| frequency/interval |Hallo-waarden voor deze eigenschappen overeen Hallo uitvoergegevensset. |
| linkedServiceName |verwijst toohello gekoppelde HDInsight-service u eerder hebt gemaakt. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Spark-programma's uitvoeren
U kunt de MapReduce-activiteit toorun Spark programma's op uw HDInsight Spark-cluster. Zie [Spark-programma's aanroepen vanuit Azure Data Factory](data-factory-spark.md) voor meer informatie.  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Zie ook
* [Hive-activiteit](data-factory-hive-activity.md)
* [Pig-activiteit](data-factory-pig-activity.md)
* [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
* [Spark-programma's aanroepen](data-factory-spark.md)
* [R-scripts aanroepen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

