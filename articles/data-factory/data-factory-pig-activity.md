---
title: Transformeer gegevens met behulp van Pig-activiteit in Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe u kunt de Pig-activiteit in een Azure data factory Pig-scripts uitvoeren op een op-verzoek/uw eigen HDInsight-cluster.
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
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="835f6-103">Transformeer gegevens met behulp van Pig-activiteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="835f6-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="835f6-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="835f6-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="835f6-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="835f6-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="835f6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="835f6-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="835f6-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="835f6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="835f6-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="835f6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="835f6-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="835f6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="835f6-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="835f6-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="835f6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="835f6-114">De HDInsight Pig-activiteit in een Data Factory [pijplijn](data-factory-create-pipelines.md) Pig-query's uitvoert op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="835f6-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="835f6-115">In dit artikel is gebaseerd op de [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en de ondersteunde transformatieactiviteiten toont.</span><span class="sxs-lookup"><span data-stu-id="835f6-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="835f6-116">Als u niet bekend met Azure Data Factory bent, Lees [Inleiding tot Azure Data Factory](data-factory-introduction.md) en voer de zelfstudie: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="835f6-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="835f6-117">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="835f6-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="835f6-118">Details van de syntaxis</span><span class="sxs-lookup"><span data-stu-id="835f6-118">Syntax details</span></span>
| <span data-ttu-id="835f6-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="835f6-119">Property</span></span> | <span data-ttu-id="835f6-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="835f6-120">Description</span></span> | <span data-ttu-id="835f6-121">Vereist</span><span class="sxs-lookup"><span data-stu-id="835f6-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="835f6-122">naam</span><span class="sxs-lookup"><span data-stu-id="835f6-122">name</span></span> |<span data-ttu-id="835f6-123">Naam van de activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-123">Name of the activity</span></span> |<span data-ttu-id="835f6-124">Ja</span><span class="sxs-lookup"><span data-stu-id="835f6-124">Yes</span></span> |
| <span data-ttu-id="835f6-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="835f6-125">description</span></span> |<span data-ttu-id="835f6-126">Beschrijving van wat de activiteit wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="835f6-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="835f6-127">Nee</span><span class="sxs-lookup"><span data-stu-id="835f6-127">No</span></span> |
| <span data-ttu-id="835f6-128">type</span><span class="sxs-lookup"><span data-stu-id="835f6-128">type</span></span> |<span data-ttu-id="835f6-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="835f6-129">HDinsightPig</span></span> |<span data-ttu-id="835f6-130">Ja</span><span class="sxs-lookup"><span data-stu-id="835f6-130">Yes</span></span> |
| <span data-ttu-id="835f6-131">Invoer</span><span class="sxs-lookup"><span data-stu-id="835f6-131">inputs</span></span> |<span data-ttu-id="835f6-132">Een of meer invoerwaarden verbruikt door de activiteit Pig</span><span class="sxs-lookup"><span data-stu-id="835f6-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="835f6-133">Nee</span><span class="sxs-lookup"><span data-stu-id="835f6-133">No</span></span> |
| <span data-ttu-id="835f6-134">uitvoer</span><span class="sxs-lookup"><span data-stu-id="835f6-134">outputs</span></span> |<span data-ttu-id="835f6-135">Een of meer uitvoer geproduceerd door de Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="835f6-136">Ja</span><span class="sxs-lookup"><span data-stu-id="835f6-136">Yes</span></span> |
| <span data-ttu-id="835f6-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="835f6-137">linkedServiceName</span></span> |<span data-ttu-id="835f6-138">Verwijzing naar het HDInsight-cluster dat is geregistreerd als een gekoppelde service in de Data Factory</span><span class="sxs-lookup"><span data-stu-id="835f6-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="835f6-139">Ja</span><span class="sxs-lookup"><span data-stu-id="835f6-139">Yes</span></span> |
| <span data-ttu-id="835f6-140">Script</span><span class="sxs-lookup"><span data-stu-id="835f6-140">script</span></span> |<span data-ttu-id="835f6-141">Geef de inline Pig-script</span><span class="sxs-lookup"><span data-stu-id="835f6-141">Specify the Pig script inline</span></span> |<span data-ttu-id="835f6-142">Nee</span><span class="sxs-lookup"><span data-stu-id="835f6-142">No</span></span> |
| <span data-ttu-id="835f6-143">scriptpad</span><span class="sxs-lookup"><span data-stu-id="835f6-143">script path</span></span> |<span data-ttu-id="835f6-144">De Pig-script opslaat in Azure blob storage en geef het pad naar het bestand.</span><span class="sxs-lookup"><span data-stu-id="835f6-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="835f6-145">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="835f6-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="835f6-146">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="835f6-146">Both cannot be used together.</span></span> <span data-ttu-id="835f6-147">De bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="835f6-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="835f6-148">Nee</span><span class="sxs-lookup"><span data-stu-id="835f6-148">No</span></span> |
| <span data-ttu-id="835f6-149">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="835f6-149">defines</span></span> |<span data-ttu-id="835f6-150">Geef parameters op als sleutel-waardeparen voor verwijzende binnen de Pig-script</span><span class="sxs-lookup"><span data-stu-id="835f6-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="835f6-151">Nee</span><span class="sxs-lookup"><span data-stu-id="835f6-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="835f6-152">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="835f6-152">Example</span></span>
<span data-ttu-id="835f6-153">Laten we eens een voorbeeld van een game logboeken analytics waar u de tijd dat door spelen van games gestart door uw bedrijf spelers besteed identificeren.</span><span class="sxs-lookup"><span data-stu-id="835f6-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="835f6-154">De volgende game voorbeeldlogboek is een bestand gescheiden door een komma (,).</span><span class="sxs-lookup"><span data-stu-id="835f6-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="835f6-155">Het bevat de volgende velden: ProfileID, SessionStart, duur, SrcIPAddress en GameType.</span><span class="sxs-lookup"><span data-stu-id="835f6-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="835f6-156">De **varkens script** voor het verwerken van deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="835f6-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="835f6-157">Voor het uitvoeren van deze Pig-script in een Data Factory-pijplijn, kunt u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="835f6-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="835f6-158">Maken van een gekoppelde service te registreren [uw eigen HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of Configureer [op aanvraag HDInsight berekeningscluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="835f6-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="835f6-159">Laten we deze gekoppelde service aanroepen **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="835f6-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="835f6-160">Maak een [gekoppelde service](data-factory-azure-blob-connector.md) voor het configureren van de verbinding met Azure-blobopslag die als host fungeert voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="835f6-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="835f6-161">Laten we deze gekoppelde service aanroepen **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="835f6-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="835f6-162">Maak [gegevenssets](data-factory-create-datasets.md) die verwijst naar de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="835f6-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="835f6-163">We bellen invoergegevensset **PigSampleIn** en de uitvoergegevensset **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="835f6-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="835f6-164">Kopieer de Pig-query in een bestand met de Azure Blob Storage in stap #2 hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="835f6-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="835f6-165">Als de Azure-opslag die als host fungeert voor de gegevens van de naam die als host fungeert voor het querybestand verschilt, maakt u een afzonderlijke gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="835f6-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="835f6-166">Raadpleeg de gekoppelde service in de configuratie van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="835f6-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="835f6-167">Gebruik ** scriptPath ** om het pad naar scriptbestand pig en **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="835f6-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="835f6-168">U kunt ook de Pig-script inline in de definitie van de activiteit opgeven met behulp van de **script** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="835f6-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="835f6-169">Maar we raden niet aan deze methode als alle speciale tekens in de script moet worden voorafgegaan en foutopsporing problemen kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="835f6-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="835f6-170">De aanbevolen procedure is stap #4.</span><span class="sxs-lookup"><span data-stu-id="835f6-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="835f6-171">De pijplijn maken met de activiteit HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="835f6-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="835f6-172">Deze activiteit wordt de invoergegevens verwerkt door het uitvoeren van Pig-script op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="835f6-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="835f6-173">Implementeer de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="835f6-173">Deploy the pipeline.</span></span> <span data-ttu-id="835f6-174">Zie [pijplijnen maken](data-factory-create-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="835f6-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="835f6-175">De pijplijn met de data factory bewaking en beheer weergaven bewaken.</span><span class="sxs-lookup"><span data-stu-id="835f6-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="835f6-176">Zie [controleren en beheren van de Data Factory-pijplijnen](data-factory-monitor-manage-pipelines.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="835f6-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="835f6-177">Parameters voor een Pig-script opgeven</span><span class="sxs-lookup"><span data-stu-id="835f6-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="835f6-178">Bekijk het volgende voorbeeld: game logboeken zijn geconsumeerd dagelijks in Azure Blob Storage en opgeslagen in een map gepartitioneerde op basis van datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="835f6-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="835f6-179">U wilt voorzien van de Pig-script en de locatie van de invoer dynamisch doorgeven tijdens runtime en ook produceren de uitvoer die is gepartitioneerd met de datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="835f6-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="835f6-180">Als u wilt gebruiken met parameters Pig-script, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="835f6-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="835f6-181">Definieer de parameters in **definieert**.</span><span class="sxs-lookup"><span data-stu-id="835f6-181">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="835f6-182">In de Pig-Script verwijzen naar de parameters met '**$parameterName**, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="835f6-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="835f6-183">Zie ook</span><span class="sxs-lookup"><span data-stu-id="835f6-183">See Also</span></span>
* [<span data-ttu-id="835f6-184">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="835f6-185">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="835f6-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="835f6-186">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="835f6-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="835f6-187">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="835f6-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="835f6-188">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="835f6-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

