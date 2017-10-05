---
title: Transformeer gegevens met Hive-activiteit - Azure | Microsoft Docs
description: Meer informatie over hoe u de Hive-activiteit in een Azure data factory kunt gebruiken voor Hive-query's uitvoeren op een op-verzoek/uw eigen HDInsight-cluster.
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="b2f1b-103">Transformeer gegevens met Hive-activiteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2f1b-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b2f1b-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b2f1b-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b2f1b-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b2f1b-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b2f1b-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b2f1b-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b2f1b-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="b2f1b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b2f1b-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b2f1b-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b2f1b-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="b2f1b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b2f1b-114">De HDInsight Hive-activiteit in een Data Factory [pijplijn](data-factory-create-pipelines.md) Hive-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b2f1b-115">In dit artikel is gebaseerd op de [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en de ondersteunde transformatieactiviteiten toont.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="b2f1b-116">Als u niet bekend met Azure Data Factory bent, Lees [Inleiding tot Azure Data Factory](data-factory-introduction.md) en voer de zelfstudie: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="b2f1b-117">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="b2f1b-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="b2f1b-118">Details van de syntaxis</span><span class="sxs-lookup"><span data-stu-id="b2f1b-118">Syntax details</span></span>
| <span data-ttu-id="b2f1b-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b2f1b-119">Property</span></span> | <span data-ttu-id="b2f1b-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b2f1b-120">Description</span></span> | <span data-ttu-id="b2f1b-121">Vereist</span><span class="sxs-lookup"><span data-stu-id="b2f1b-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2f1b-122">naam</span><span class="sxs-lookup"><span data-stu-id="b2f1b-122">name</span></span> |<span data-ttu-id="b2f1b-123">Naam van de activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-123">Name of the activity</span></span> |<span data-ttu-id="b2f1b-124">Ja</span><span class="sxs-lookup"><span data-stu-id="b2f1b-124">Yes</span></span> |
| <span data-ttu-id="b2f1b-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b2f1b-125">description</span></span> |<span data-ttu-id="b2f1b-126">Beschrijving van wat de activiteit wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="b2f1b-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="b2f1b-127">Nee</span><span class="sxs-lookup"><span data-stu-id="b2f1b-127">No</span></span> |
| <span data-ttu-id="b2f1b-128">type</span><span class="sxs-lookup"><span data-stu-id="b2f1b-128">type</span></span> |<span data-ttu-id="b2f1b-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="b2f1b-129">HDinsightHive</span></span> |<span data-ttu-id="b2f1b-130">Ja</span><span class="sxs-lookup"><span data-stu-id="b2f1b-130">Yes</span></span> |
| <span data-ttu-id="b2f1b-131">Invoer</span><span class="sxs-lookup"><span data-stu-id="b2f1b-131">inputs</span></span> |<span data-ttu-id="b2f1b-132">Invoer gebruikt door het Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="b2f1b-133">Nee</span><span class="sxs-lookup"><span data-stu-id="b2f1b-133">No</span></span> |
| <span data-ttu-id="b2f1b-134">uitvoer</span><span class="sxs-lookup"><span data-stu-id="b2f1b-134">outputs</span></span> |<span data-ttu-id="b2f1b-135">Uitvoer geproduceerd door de Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="b2f1b-136">Ja</span><span class="sxs-lookup"><span data-stu-id="b2f1b-136">Yes</span></span> |
| <span data-ttu-id="b2f1b-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b2f1b-137">linkedServiceName</span></span> |<span data-ttu-id="b2f1b-138">Verwijzing naar het HDInsight-cluster dat is geregistreerd als een gekoppelde service in de Data Factory</span><span class="sxs-lookup"><span data-stu-id="b2f1b-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="b2f1b-139">Ja</span><span class="sxs-lookup"><span data-stu-id="b2f1b-139">Yes</span></span> |
| <span data-ttu-id="b2f1b-140">Script</span><span class="sxs-lookup"><span data-stu-id="b2f1b-140">script</span></span> |<span data-ttu-id="b2f1b-141">Geef de inline Hive-script</span><span class="sxs-lookup"><span data-stu-id="b2f1b-141">Specify the Hive script inline</span></span> |<span data-ttu-id="b2f1b-142">Nee</span><span class="sxs-lookup"><span data-stu-id="b2f1b-142">No</span></span> |
| <span data-ttu-id="b2f1b-143">scriptpad</span><span class="sxs-lookup"><span data-stu-id="b2f1b-143">script path</span></span> |<span data-ttu-id="b2f1b-144">Het Hive-script opslaat in Azure blob storage en geef het pad naar het bestand.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="b2f1b-145">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="b2f1b-146">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-146">Both cannot be used together.</span></span> <span data-ttu-id="b2f1b-147">De bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="b2f1b-148">Nee</span><span class="sxs-lookup"><span data-stu-id="b2f1b-148">No</span></span> |
| <span data-ttu-id="b2f1b-149">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="b2f1b-149">defines</span></span> |<span data-ttu-id="b2f1b-150">Geef parameters op als sleutel-waardeparen voor verwijzende binnen het Hive-script met behulp van 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="b2f1b-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="b2f1b-151">Nee</span><span class="sxs-lookup"><span data-stu-id="b2f1b-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="b2f1b-152">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b2f1b-152">Example</span></span>
<span data-ttu-id="b2f1b-153">Laten we eens een voorbeeld van een game logboeken analytics waar u de tijd die door gebruikers spelen van games gestart door uw bedrijf identificeren.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="b2f1b-154">Het volgende logboek is een game voorbeeldlogboek, komma (`,`) gescheiden en bevat de volgende velden: ProfileID, SessionStart, duur, SrcIPAddress en GameType.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="b2f1b-155">De **Hive-script** voor het verwerken van deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="b2f1b-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="b2f1b-156">Voor het uitvoeren van deze Hive-script in een Data Factory-pijplijn, moet u het volgende doen</span><span class="sxs-lookup"><span data-stu-id="b2f1b-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="b2f1b-157">Maken van een gekoppelde service te registreren [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b2f1b-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="b2f1b-158">We bellen deze gekoppelde service 'HDInsightLinkedService'.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="b2f1b-159">Maak een [gekoppelde service](data-factory-azure-blob-connector.md) voor het configureren van de verbinding met Azure-blobopslag die als host fungeert voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="b2f1b-160">We bellen deze gekoppelde service 'StorageLinkedService'</span><span class="sxs-lookup"><span data-stu-id="b2f1b-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="b2f1b-161">Maak [gegevenssets](data-factory-create-datasets.md) die verwijst naar de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="b2f1b-162">We bellen invoergegevensset 'HiveSampleIn' en de uitvoergegevensset 'HiveSampleOut'</span><span class="sxs-lookup"><span data-stu-id="b2f1b-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="b2f1b-163">Kopieer de Hive-query als een bestand naar Azure Blob-opslag geconfigureerd in stap #2.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="b2f1b-164">Als de opslag voor het hosten van de gegevens af van de versie die als host fungeert voor deze query-bestand wijkt, een afzonderlijke gekoppelde Azure Storage-service maken en hiernaar wordt verwezen in de activiteit.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="b2f1b-165">Gebruik ** scriptPath ** om op te geven van het pad voor het hive-query-bestand en **scriptLinkedService** Azure-opslag met het scriptbestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b2f1b-166">U kunt ook de Hive-script inline in de definitie van de activiteit opgeven met behulp van de **script** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="b2f1b-167">We raden niet aan deze methode als alle speciale tekens in het script in de JSON-document moet worden voorafgegaan en foutopsporing problemen kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="b2f1b-168">De aanbevolen procedure is stap #4.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="b2f1b-169">Een pijplijn maken met de HDInsightHive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="b2f1b-170">De activiteit processen/transformaties de gegevens.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="b2f1b-171">Implementeer de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-171">Deploy the pipeline.</span></span> <span data-ttu-id="b2f1b-172">Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="b2f1b-173">De pijplijn met de data factory bewaking en beheer weergaven bewaken.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="b2f1b-174">Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="b2f1b-175">Parameters voor een Hive-script opgeven</span><span class="sxs-lookup"><span data-stu-id="b2f1b-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="b2f1b-176">In dit voorbeeld game logboeken dagelijks in Azure Blob Storage zijn geconsumeerd en worden opgeslagen in een map die is gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="b2f1b-177">U wilt voorzien van het Hive-script en de locatie van de invoer dynamisch doorgeven tijdens runtime en ook produceren de uitvoer die is gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="b2f1b-178">Als u wilt gebruiken met parameters Hive-script, doet u het volgende</span><span class="sxs-lookup"><span data-stu-id="b2f1b-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="b2f1b-179">Definieer de parameters in **definieert**.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="b2f1b-180">In het Hive-Script verwijzen met de parameter via **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="b2f1b-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="b2f1b-181">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b2f1b-181">See Also</span></span>
* [<span data-ttu-id="b2f1b-182">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="b2f1b-183">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="b2f1b-184">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="b2f1b-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="b2f1b-185">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="b2f1b-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="b2f1b-186">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="b2f1b-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

