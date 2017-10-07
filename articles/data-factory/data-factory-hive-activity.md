---
title: aaaTransform-gegevens met behulp van Hive-activiteit - Azure | Microsoft Docs
description: Meer informatie over hoe u Hallo Hive-activiteit in een Azure data factory toorun Hive-query's kunt gebruiken op een op-verzoek/uw eigen HDInsight-cluster.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Transformeer gegevens met Hive-activiteit in Azure Data Factory 
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

Hallo HDInsight Hive-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) Hive-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.

> [!NOTE] 
> Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest. 

## <a name="syntax"></a>Syntaxis

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a>Details van de syntaxis
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van de activiteit Hallo |Ja |
| description |Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor |Nee |
| type |HDinsightHive |Ja |
| Invoer |Invoer gebruikt door Hallo Hive-activiteit |Nee |
| uitvoer |Uitvoer geproduceerd door Hallo Hive-activiteit |Ja |
| linkedServiceName |HDInsight-cluster voor verwijzing toohello is geregistreerd als een gekoppelde service in de Data Factory |Ja |
| Script |Hallo Hive-script inline opgeven |Nee |
| scriptpad |Hallo archief Hive-script in een Azure blob storage en geef Hallo pad toohello bestand. Gebruik de eigenschap 'script' of 'scriptPath'. Beide kunnen niet samen worden gebruikt. Hallo-bestandsnaam is hoofdlettergevoelig. |Nee |
| Hiermee worden gedefinieerd |Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Hive-script met behulp van 'hiveconf' |Nee |

## <a name="example"></a>Voorbeeld
Laten we eens een voorbeeld van een game logboeken analytics waar u tooidentify Hallo tijd besteed door gebruikers spelen van games gestart door uw bedrijf. 

Hallo volgende logboek is een game voorbeeldlogboek, komma (`,`) gescheiden en bevat de volgende velden – ProfileID, SessionStart, duur, SrcIPAddress en GameType Hallo.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hallo **Hive-script** tooprocess deze gegevens:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute deze Hive-script in een Data Factory-pijplijn, moet u toodo Hallo volgende

1. Maken van een gekoppelde service tooregister [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). We bellen deze gekoppelde service 'HDInsightLinkedService'.
2. Maak een [gekoppelde service](data-factory-azure-blob-connector.md) tooconfigure Hallo verbinding tooAzure blobopslag Hallo gegevens hosten. We bellen deze gekoppelde service 'StorageLinkedService'
3. Maak [gegevenssets](data-factory-create-datasets.md) wijzen toohello invoer- en Hallo uitvoergegevens. We bellen Hallo invoergegevensset 'HiveSampleIn' en uitvoergegevensset 'HiveSampleOut' Hallo
4. Hallo Hive-query als een bestand tooAzure Blob-opslag geconfigureerd in stap #2 kopiëren. Als opslag voor het hosten van gegevens Hallo Hallo van Hallo een host optreedt voor deze querybestand verschilt, een afzonderlijke gekoppelde Azure Storage-service maken en tooit in Hallo activiteit worden verwezen. Gebruik ** scriptPath ** toospecify Hallo pad toohive query-bestand en **scriptLinkedService** toospecify hello Azure-opslag met Hallo scriptbestand. 
   
   > [!NOTE]
   > U kunt ook Hallo Hive-script inline in de definitie van de activiteit Hallo opgeven met behulp van Hallo **script** eigenschap. We raden deze methode niet als alle speciale tekens in Hallo script binnen Hallo JSON-document moet toobe escape-teken en mag oorzaak opsporen van problemen. Hallo aanbevolen procedure is toofollow stap #4.
   > 
   > 
5. Een pijplijn maken met de Hallo HDInsightHive-activiteit. Hallo activiteit processen/transformaties Hallo-gegevens.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Implementeer Hallo pijplijn. Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie. 
7. Hallo-pipeline met Hallo data factory-controle en beheerweergaven bewaken. Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie. 

## <a name="specifying-parameters-for-a-hive-script"></a>Parameters voor een Hive-script opgeven
In dit voorbeeld game logboeken dagelijks in Azure Blob Storage zijn geconsumeerd en worden opgeslagen in een map die is gepartitioneerd met de datum en tijd. U wilt tooparameterize Hallo Hive-script en Hallo invoermap locatie dynamisch doorgeven tijdens runtime en ook meerdere Hallo uitvoer gepartitioneerd met de datum en tijd.

toouse geparametriseerde Hive-script, doet u Hallo na

* Definieer de parameters Hallo in **definieert**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* In Hallo Hive-Script, verwijzen toohello met behulp van de parameter **${hiveconf:parameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Zie ook
* [Pig-activiteit](data-factory-pig-activity.md)
* [MapReduce-activiteit](data-factory-map-reduce.md)
* [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
* [Spark-programma's aanroepen](data-factory-spark.md)
* [R-scripts aanroepen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

