---
title: aaaTransform gegevens met behulp van Pig-activiteit in Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe u Hallo Pig-activiteit in een Azure data factory toorun Pig-scripts kunt gebruiken op een op-verzoek/uw eigen HDInsight-cluster.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Transformeer gegevens met behulp van Pig-activiteit in Azure Data Factory
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

Hallo HDInsight Pig-activiteit in een Data Factory [pijplijn](data-factory-create-pipelines.md) Pig-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.

> [!NOTE] 
> Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest. 

## <a name="syntax"></a>Syntaxis

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>Details van de syntaxis
| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam |Naam van de activiteit Hallo |Ja |
| description |Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor |Nee |
| type |HDinsightPig |Ja |
| Invoer |Een of meer invoerwaarden verbruikt door Hallo Pig-activiteit |Nee |
| uitvoer |Een of meer uitvoer geproduceerd door Hallo Pig-activiteit |Ja |
| linkedServiceName |HDInsight-cluster voor verwijzing toohello is geregistreerd als een gekoppelde service in de Data Factory |Ja |
| Script |Hallo Pig-script inline opgeven |Nee |
| scriptpad |Hallo Pig-script opslaat in Azure blob storage en geef Hallo pad toohello-bestand. Gebruik de eigenschap 'script' of 'scriptPath'. Beide kunnen niet samen worden gebruikt. Hallo-bestandsnaam is hoofdlettergevoelig. |Nee |
| Hiermee worden gedefinieerd |Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Pig-script |Nee |

## <a name="example"></a>Voorbeeld
Laten we eens een voorbeeld van een game logboeken analytics waar u tooidentify Hallo tijd besteed door spelers spelen van games gestart door uw bedrijf.

Hallo game voorbeeldlogboek volgende is een bestand gescheiden door een komma (,). Het bevat volgende velden – ProfileID, SessionStart, duur, SrcIPAddress en GameType Hallo.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hallo **varkens script** tooprocess deze gegevens:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

Deze Pig-script in een Data Factory-pijplijn tooexecute Hallo stappen te volgen:

1. Maken van een gekoppelde service tooregister [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Laten we deze gekoppelde service aanroepen **HDInsightLinkedService**.
2. Maak een [gekoppelde service](data-factory-azure-blob-connector.md) tooconfigure Hallo verbinding tooAzure blobopslag Hallo gegevens hosten. Laten we deze gekoppelde service aanroepen **StorageLinkedService**.
3. Maak [gegevenssets](data-factory-create-datasets.md) wijzen toohello invoer- en Hallo uitvoergegevens. We bellen Hallo invoergegevensset **PigSampleIn** en Hallo uitvoergegevensset **PigSampleOut**.
4. Hallo Pig query in een bestand hello Azure Blob-opslag geconfigureerd in stap &#2; kopiëren. Als hello Azure-opslag die als host fungeert voor Hallo gegevens van Hallo een die als host fungeert voor het querybestand hello verschilt, maakt u een afzonderlijke gekoppelde Azure Storage-service. Raadpleeg toohello gekoppelde service in Hallo activiteit configuratie. Gebruik ** scriptPath ** toospecify Hallo pad toopig-scriptbestand en **scriptLinkedService**. 
   
   > [!NOTE]
   > U kunt ook Hallo Pig-script inline in de definitie van de activiteit Hallo opgeven met behulp van Hallo **script** eigenschap. Echter raadzaam niet deze benadering als alle speciale tekens in Hallo script moet toobe escape-teken en foutopsporing problemen kan veroorzaken. Hallo aanbevolen procedure is toofollow stap #4.
   > 
   > 
5. Hallo-pijplijn maken met de Hallo HDInsightPig activiteit. Deze activiteit verwerkt Hallo invoergegevens door Pig-script uitgevoerd op HDInsight-cluster.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Implementeer Hallo pijplijn. Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie. 
7. Hallo-pipeline met Hallo data factory-controle en beheerweergaven bewaken. Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.

## <a name="specifying-parameters-for-a-pig-script"></a>Parameters voor een Pig-script opgeven
Overweeg het volgende voorbeeld Hallo: game logboeken zijn geconsumeerd dagelijks in Azure Blob Storage en opgeslagen in een map gepartitioneerde op basis van datum en tijd. U wilt tooparameterize Hallo Pig-script en Hallo invoermap locatie dynamisch doorgeven tijdens runtime en ook meerdere Hallo uitvoer gepartitioneerd met de datum en tijd.

toouse geparametriseerde Pig-script en Voer Hallo te volgen:

* Definieer de parameters Hallo in **definieert**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* In Hallo Pig-Script, verwijzen toohello parameters met '**$parameterName**, zoals wordt weergegeven in het volgende voorbeeld Hallo:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Zie ook
* [Hive-activiteit](data-factory-hive-activity.md)
* [MapReduce-activiteit](data-factory-map-reduce.md)
* [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
* [Spark-programma's aanroepen](data-factory-spark.md)
* [R-scripts aanroepen](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

