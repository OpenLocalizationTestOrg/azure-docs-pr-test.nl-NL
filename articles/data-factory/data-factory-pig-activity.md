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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="cb5ab-103">Transformeer gegevens met behulp van Pig-activiteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cb5ab-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="cb5ab-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="cb5ab-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="cb5ab-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="cb5ab-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="cb5ab-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="cb5ab-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="cb5ab-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="cb5ab-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="cb5ab-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="cb5ab-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="cb5ab-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="cb5ab-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="cb5ab-114">Hallo HDInsight Pig-activiteit in een Data Factory [pijplijn](data-factory-create-pipelines.md) Pig-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="cb5ab-115">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="cb5ab-116">Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="cb5ab-117">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="cb5ab-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="cb5ab-118">Details van de syntaxis</span><span class="sxs-lookup"><span data-stu-id="cb5ab-118">Syntax details</span></span>
| <span data-ttu-id="cb5ab-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="cb5ab-119">Property</span></span> | <span data-ttu-id="cb5ab-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cb5ab-120">Description</span></span> | <span data-ttu-id="cb5ab-121">Vereist</span><span class="sxs-lookup"><span data-stu-id="cb5ab-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb5ab-122">naam</span><span class="sxs-lookup"><span data-stu-id="cb5ab-122">name</span></span> |<span data-ttu-id="cb5ab-123">Naam van de activiteit Hallo</span><span class="sxs-lookup"><span data-stu-id="cb5ab-123">Name of hello activity</span></span> |<span data-ttu-id="cb5ab-124">Ja</span><span class="sxs-lookup"><span data-stu-id="cb5ab-124">Yes</span></span> |
| <span data-ttu-id="cb5ab-125">description</span><span class="sxs-lookup"><span data-stu-id="cb5ab-125">description</span></span> |<span data-ttu-id="cb5ab-126">Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="cb5ab-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="cb5ab-127">Nee</span><span class="sxs-lookup"><span data-stu-id="cb5ab-127">No</span></span> |
| <span data-ttu-id="cb5ab-128">type</span><span class="sxs-lookup"><span data-stu-id="cb5ab-128">type</span></span> |<span data-ttu-id="cb5ab-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="cb5ab-129">HDinsightPig</span></span> |<span data-ttu-id="cb5ab-130">Ja</span><span class="sxs-lookup"><span data-stu-id="cb5ab-130">Yes</span></span> |
| <span data-ttu-id="cb5ab-131">Invoer</span><span class="sxs-lookup"><span data-stu-id="cb5ab-131">inputs</span></span> |<span data-ttu-id="cb5ab-132">Een of meer invoerwaarden verbruikt door Hallo Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="cb5ab-133">Nee</span><span class="sxs-lookup"><span data-stu-id="cb5ab-133">No</span></span> |
| <span data-ttu-id="cb5ab-134">uitvoer</span><span class="sxs-lookup"><span data-stu-id="cb5ab-134">outputs</span></span> |<span data-ttu-id="cb5ab-135">Een of meer uitvoer geproduceerd door Hallo Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="cb5ab-136">Ja</span><span class="sxs-lookup"><span data-stu-id="cb5ab-136">Yes</span></span> |
| <span data-ttu-id="cb5ab-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="cb5ab-137">linkedServiceName</span></span> |<span data-ttu-id="cb5ab-138">HDInsight-cluster voor verwijzing toohello is geregistreerd als een gekoppelde service in de Data Factory</span><span class="sxs-lookup"><span data-stu-id="cb5ab-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="cb5ab-139">Ja</span><span class="sxs-lookup"><span data-stu-id="cb5ab-139">Yes</span></span> |
| <span data-ttu-id="cb5ab-140">Script</span><span class="sxs-lookup"><span data-stu-id="cb5ab-140">script</span></span> |<span data-ttu-id="cb5ab-141">Hallo Pig-script inline opgeven</span><span class="sxs-lookup"><span data-stu-id="cb5ab-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="cb5ab-142">Nee</span><span class="sxs-lookup"><span data-stu-id="cb5ab-142">No</span></span> |
| <span data-ttu-id="cb5ab-143">scriptpad</span><span class="sxs-lookup"><span data-stu-id="cb5ab-143">script path</span></span> |<span data-ttu-id="cb5ab-144">Hallo Pig-script opslaat in Azure blob storage en geef Hallo pad toohello-bestand.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="cb5ab-145">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="cb5ab-146">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-146">Both cannot be used together.</span></span> <span data-ttu-id="cb5ab-147">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="cb5ab-148">Nee</span><span class="sxs-lookup"><span data-stu-id="cb5ab-148">No</span></span> |
| <span data-ttu-id="cb5ab-149">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="cb5ab-149">defines</span></span> |<span data-ttu-id="cb5ab-150">Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Pig-script</span><span class="sxs-lookup"><span data-stu-id="cb5ab-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="cb5ab-151">Nee</span><span class="sxs-lookup"><span data-stu-id="cb5ab-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="cb5ab-152">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cb5ab-152">Example</span></span>
<span data-ttu-id="cb5ab-153">Laten we eens een voorbeeld van een game logboeken analytics waar u tooidentify Hallo tijd besteed door spelers spelen van games gestart door uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="cb5ab-154">Hallo game voorbeeldlogboek volgende is een bestand gescheiden door een komma (,).</span><span class="sxs-lookup"><span data-stu-id="cb5ab-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="cb5ab-155">Het bevat volgende velden – ProfileID, SessionStart, duur, SrcIPAddress en GameType Hallo.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="cb5ab-156">Hallo **varkens script** tooprocess deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="cb5ab-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="cb5ab-157">Deze Pig-script in een Data Factory-pijplijn tooexecute Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cb5ab-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="cb5ab-158">Maken van een gekoppelde service tooregister [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="cb5ab-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="cb5ab-159">Laten we deze gekoppelde service aanroepen **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="cb5ab-160">Maak een [gekoppelde service](data-factory-azure-blob-connector.md) tooconfigure Hallo verbinding tooAzure blobopslag Hallo gegevens hosten.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="cb5ab-161">Laten we deze gekoppelde service aanroepen **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="cb5ab-162">Maak [gegevenssets](data-factory-create-datasets.md) wijzen toohello invoer- en Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="cb5ab-163">We bellen Hallo invoergegevensset **PigSampleIn** en Hallo uitvoergegevensset **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="cb5ab-164">Hallo Pig query in een bestand hello Azure Blob-opslag geconfigureerd in stap &#2; kopiëren.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="cb5ab-165">Als hello Azure-opslag die als host fungeert voor Hallo gegevens van Hallo een die als host fungeert voor het querybestand hello verschilt, maakt u een afzonderlijke gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="cb5ab-166">Raadpleeg toohello gekoppelde service in Hallo activiteit configuratie.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="cb5ab-167">Gebruik ** scriptPath ** toospecify Hallo pad toopig-scriptbestand en **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cb5ab-168">U kunt ook Hallo Pig-script inline in de definitie van de activiteit Hallo opgeven met behulp van Hallo **script** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="cb5ab-169">Echter raadzaam niet deze benadering als alle speciale tekens in Hallo script moet toobe escape-teken en foutopsporing problemen kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="cb5ab-170">Hallo aanbevolen procedure is toofollow stap #4.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="cb5ab-171">Hallo-pijplijn maken met de Hallo HDInsightPig activiteit.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="cb5ab-172">Deze activiteit verwerkt Hallo invoergegevens door Pig-script uitgevoerd op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="cb5ab-173">Implementeer Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-173">Deploy hello pipeline.</span></span> <span data-ttu-id="cb5ab-174">Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="cb5ab-175">Hallo-pipeline met Hallo data factory-controle en beheerweergaven bewaken.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="cb5ab-176">Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="cb5ab-177">Parameters voor een Pig-script opgeven</span><span class="sxs-lookup"><span data-stu-id="cb5ab-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="cb5ab-178">Overweeg het volgende voorbeeld Hallo: game logboeken zijn geconsumeerd dagelijks in Azure Blob Storage en opgeslagen in een map gepartitioneerde op basis van datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="cb5ab-179">U wilt tooparameterize Hallo Pig-script en Hallo invoermap locatie dynamisch doorgeven tijdens runtime en ook meerdere Hallo uitvoer gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="cb5ab-180">toouse geparametriseerde Pig-script en Voer Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="cb5ab-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="cb5ab-181">Definieer de parameters Hallo in **definieert**.</span><span class="sxs-lookup"><span data-stu-id="cb5ab-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="cb5ab-182">In Hallo Pig-Script, verwijzen toohello parameters met '**$parameterName**, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="cb5ab-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="cb5ab-183">Zie ook</span><span class="sxs-lookup"><span data-stu-id="cb5ab-183">See Also</span></span>
* [<span data-ttu-id="cb5ab-184">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="cb5ab-185">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="cb5ab-186">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="cb5ab-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="cb5ab-187">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="cb5ab-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="cb5ab-188">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="cb5ab-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

