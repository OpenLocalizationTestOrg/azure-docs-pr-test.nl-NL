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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="48d9a-103">Transformeer gegevens met Hive-activiteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="48d9a-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="48d9a-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="48d9a-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="48d9a-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="48d9a-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="48d9a-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="48d9a-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="48d9a-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="48d9a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="48d9a-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="48d9a-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="48d9a-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="48d9a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="48d9a-114">Hallo HDInsight Hive-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) Hive-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48d9a-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="48d9a-115">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.</span><span class="sxs-lookup"><span data-stu-id="48d9a-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="48d9a-116">Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="48d9a-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="48d9a-117">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="48d9a-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="48d9a-118">Details van de syntaxis</span><span class="sxs-lookup"><span data-stu-id="48d9a-118">Syntax details</span></span>
| <span data-ttu-id="48d9a-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="48d9a-119">Property</span></span> | <span data-ttu-id="48d9a-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="48d9a-120">Description</span></span> | <span data-ttu-id="48d9a-121">Vereist</span><span class="sxs-lookup"><span data-stu-id="48d9a-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48d9a-122">naam</span><span class="sxs-lookup"><span data-stu-id="48d9a-122">name</span></span> |<span data-ttu-id="48d9a-123">Naam van de activiteit Hallo</span><span class="sxs-lookup"><span data-stu-id="48d9a-123">Name of hello activity</span></span> |<span data-ttu-id="48d9a-124">Ja</span><span class="sxs-lookup"><span data-stu-id="48d9a-124">Yes</span></span> |
| <span data-ttu-id="48d9a-125">description</span><span class="sxs-lookup"><span data-stu-id="48d9a-125">description</span></span> |<span data-ttu-id="48d9a-126">Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="48d9a-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="48d9a-127">Nee</span><span class="sxs-lookup"><span data-stu-id="48d9a-127">No</span></span> |
| <span data-ttu-id="48d9a-128">type</span><span class="sxs-lookup"><span data-stu-id="48d9a-128">type</span></span> |<span data-ttu-id="48d9a-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="48d9a-129">HDinsightHive</span></span> |<span data-ttu-id="48d9a-130">Ja</span><span class="sxs-lookup"><span data-stu-id="48d9a-130">Yes</span></span> |
| <span data-ttu-id="48d9a-131">Invoer</span><span class="sxs-lookup"><span data-stu-id="48d9a-131">inputs</span></span> |<span data-ttu-id="48d9a-132">Invoer gebruikt door Hallo Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="48d9a-133">Nee</span><span class="sxs-lookup"><span data-stu-id="48d9a-133">No</span></span> |
| <span data-ttu-id="48d9a-134">uitvoer</span><span class="sxs-lookup"><span data-stu-id="48d9a-134">outputs</span></span> |<span data-ttu-id="48d9a-135">Uitvoer geproduceerd door Hallo Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="48d9a-136">Ja</span><span class="sxs-lookup"><span data-stu-id="48d9a-136">Yes</span></span> |
| <span data-ttu-id="48d9a-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="48d9a-137">linkedServiceName</span></span> |<span data-ttu-id="48d9a-138">HDInsight-cluster voor verwijzing toohello is geregistreerd als een gekoppelde service in de Data Factory</span><span class="sxs-lookup"><span data-stu-id="48d9a-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="48d9a-139">Ja</span><span class="sxs-lookup"><span data-stu-id="48d9a-139">Yes</span></span> |
| <span data-ttu-id="48d9a-140">Script</span><span class="sxs-lookup"><span data-stu-id="48d9a-140">script</span></span> |<span data-ttu-id="48d9a-141">Hallo Hive-script inline opgeven</span><span class="sxs-lookup"><span data-stu-id="48d9a-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="48d9a-142">Nee</span><span class="sxs-lookup"><span data-stu-id="48d9a-142">No</span></span> |
| <span data-ttu-id="48d9a-143">scriptpad</span><span class="sxs-lookup"><span data-stu-id="48d9a-143">script path</span></span> |<span data-ttu-id="48d9a-144">Hallo archief Hive-script in een Azure blob storage en geef Hallo pad toohello bestand.</span><span class="sxs-lookup"><span data-stu-id="48d9a-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="48d9a-145">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="48d9a-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="48d9a-146">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48d9a-146">Both cannot be used together.</span></span> <span data-ttu-id="48d9a-147">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="48d9a-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="48d9a-148">Nee</span><span class="sxs-lookup"><span data-stu-id="48d9a-148">No</span></span> |
| <span data-ttu-id="48d9a-149">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="48d9a-149">defines</span></span> |<span data-ttu-id="48d9a-150">Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Hive-script met behulp van 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="48d9a-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="48d9a-151">Nee</span><span class="sxs-lookup"><span data-stu-id="48d9a-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="48d9a-152">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="48d9a-152">Example</span></span>
<span data-ttu-id="48d9a-153">Laten we eens een voorbeeld van een game logboeken analytics waar u tooidentify Hallo tijd besteed door gebruikers spelen van games gestart door uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="48d9a-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="48d9a-154">Hallo volgende logboek is een game voorbeeldlogboek, komma (`,`) gescheiden en bevat de volgende velden – ProfileID, SessionStart, duur, SrcIPAddress en GameType Hallo.</span><span class="sxs-lookup"><span data-stu-id="48d9a-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="48d9a-155">Hallo **Hive-script** tooprocess deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="48d9a-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="48d9a-156">tooexecute deze Hive-script in een Data Factory-pijplijn, moet u toodo Hallo volgende</span><span class="sxs-lookup"><span data-stu-id="48d9a-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="48d9a-157">Maken van een gekoppelde service tooregister [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="48d9a-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="48d9a-158">We bellen deze gekoppelde service 'HDInsightLinkedService'.</span><span class="sxs-lookup"><span data-stu-id="48d9a-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="48d9a-159">Maak een [gekoppelde service](data-factory-azure-blob-connector.md) tooconfigure Hallo verbinding tooAzure blobopslag Hallo gegevens hosten.</span><span class="sxs-lookup"><span data-stu-id="48d9a-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="48d9a-160">We bellen deze gekoppelde service 'StorageLinkedService'</span><span class="sxs-lookup"><span data-stu-id="48d9a-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="48d9a-161">Maak [gegevenssets](data-factory-create-datasets.md) wijzen toohello invoer- en Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="48d9a-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="48d9a-162">We bellen Hallo invoergegevensset 'HiveSampleIn' en uitvoergegevensset 'HiveSampleOut' Hallo</span><span class="sxs-lookup"><span data-stu-id="48d9a-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="48d9a-163">Hallo Hive-query als een bestand tooAzure Blob-opslag geconfigureerd in stap #2 kopiëren.</span><span class="sxs-lookup"><span data-stu-id="48d9a-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="48d9a-164">Als opslag voor het hosten van gegevens Hallo Hallo van Hallo een host optreedt voor deze querybestand verschilt, een afzonderlijke gekoppelde Azure Storage-service maken en tooit in Hallo activiteit worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="48d9a-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="48d9a-165">Gebruik ** scriptPath ** toospecify Hallo pad toohive query-bestand en **scriptLinkedService** toospecify hello Azure-opslag met Hallo scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="48d9a-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="48d9a-166">U kunt ook Hallo Hive-script inline in de definitie van de activiteit Hallo opgeven met behulp van Hallo **script** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="48d9a-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="48d9a-167">We raden deze methode niet als alle speciale tekens in Hallo script binnen Hallo JSON-document moet toobe escape-teken en mag oorzaak opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="48d9a-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="48d9a-168">Hallo aanbevolen procedure is toofollow stap #4.</span><span class="sxs-lookup"><span data-stu-id="48d9a-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="48d9a-169">Een pijplijn maken met de Hallo HDInsightHive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="48d9a-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="48d9a-170">Hallo activiteit processen/transformaties Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="48d9a-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="48d9a-171">Implementeer Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="48d9a-171">Deploy hello pipeline.</span></span> <span data-ttu-id="48d9a-172">Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="48d9a-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="48d9a-173">Hallo-pipeline met Hallo data factory-controle en beheerweergaven bewaken.</span><span class="sxs-lookup"><span data-stu-id="48d9a-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="48d9a-174">Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="48d9a-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="48d9a-175">Parameters voor een Hive-script opgeven</span><span class="sxs-lookup"><span data-stu-id="48d9a-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="48d9a-176">In dit voorbeeld game logboeken dagelijks in Azure Blob Storage zijn geconsumeerd en worden opgeslagen in een map die is gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="48d9a-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="48d9a-177">U wilt tooparameterize Hallo Hive-script en Hallo invoermap locatie dynamisch doorgeven tijdens runtime en ook meerdere Hallo uitvoer gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="48d9a-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="48d9a-178">toouse geparametriseerde Hive-script, doet u Hallo na</span><span class="sxs-lookup"><span data-stu-id="48d9a-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="48d9a-179">Definieer de parameters Hallo in **definieert**.</span><span class="sxs-lookup"><span data-stu-id="48d9a-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="48d9a-180">In Hallo Hive-Script, verwijzen toohello met behulp van de parameter **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="48d9a-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="48d9a-181">Zie ook</span><span class="sxs-lookup"><span data-stu-id="48d9a-181">See Also</span></span>
* [<span data-ttu-id="48d9a-182">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="48d9a-183">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="48d9a-184">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="48d9a-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="48d9a-185">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="48d9a-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="48d9a-186">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="48d9a-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

