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
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="3325b-103">Aanroepen van MapReduce-programma's uit Data Factory</span><span class="sxs-lookup"><span data-stu-id="3325b-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="3325b-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="3325b-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="3325b-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="3325b-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="3325b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="3325b-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="3325b-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="3325b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="3325b-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="3325b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="3325b-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="3325b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="3325b-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="3325b-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="3325b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="3325b-114">Hallo HDInsight MapReduce-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) MapReduce-programma's worden uitgevoerd op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3325b-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3325b-115">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.</span><span class="sxs-lookup"><span data-stu-id="3325b-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="3325b-116">Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="3325b-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="3325b-117">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3325b-117">Introduction</span></span>
<span data-ttu-id="3325b-118">Een pijplijn in een Azure data factory verwerkt gegevens in gekoppelde storage-services met behulp van gekoppelde compute services.</span><span class="sxs-lookup"><span data-stu-id="3325b-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="3325b-119">Het bevat een reeks activiteiten, waarbij elke activiteit uitvoert voor een specifieke verwerking.</span><span class="sxs-lookup"><span data-stu-id="3325b-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="3325b-120">In dit artikel wordt beschreven hoe Hallo HDInsight MapReduce-activiteit.</span><span class="sxs-lookup"><span data-stu-id="3325b-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="3325b-121">Zie [Pig](data-factory-pig-activity.md) en [Hive](data-factory-hive-activity.md) voor meer informatie over het uitvoeren van Pig/Hive scripts op een Windows, Linux-gebaseerde HDInsight-cluster van een pijplijn met behulp van HDInsight Pig en Hive-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="3325b-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="3325b-122">JSON voor HDInsight MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="3325b-123">In de JSON-definitie voor HDInsight-activiteit Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="3325b-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="3325b-124">Set Hallo **type** Hallo **activiteit** te**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3325b-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="3325b-125">Hallo naam opgeven van de klasse Hallo voor **className** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3325b-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="3325b-126">Geef Hallo pad toohello JAR-bestand inclusief de bestandsnaam Hallo voor **jarFilePath** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3325b-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="3325b-127">Geef Hallo gekoppelde service die toohello Azure Blob Storage met Hallo JAR-bestand voor verwijst **jarLinkedService** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3325b-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="3325b-128">Geef geen argumenten voor Hallo MapReduce-programma in Hallo **argumenten** sectie.</span><span class="sxs-lookup"><span data-stu-id="3325b-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="3325b-129">Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework.</span><span class="sxs-lookup"><span data-stu-id="3325b-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="3325b-130">toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden).</span><span class="sxs-lookup"><span data-stu-id="3325b-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

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
<span data-ttu-id="3325b-131">U kunt Hallo HDInsight MapReduce-activiteit toorun elk MapReduce jar-bestand op een HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3325b-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="3325b-132">Volgende voorbeeld JSON-definitie van een pijplijn, Hallo HDInsight-activiteit is geconfigureerd in Hallo toorun een Mahout JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="3325b-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="3325b-133">Voorbeeld op GitHub</span><span class="sxs-lookup"><span data-stu-id="3325b-133">Sample on GitHub</span></span>
<span data-ttu-id="3325b-134">U kunt een voorbeeld voor het gebruik van HDInsight MapReduce-activiteit Hallo downloaden van: [Data Factory-voorbeelden op GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="3325b-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="3325b-135">Hallo Word-Count-programma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3325b-135">Running hello Word Count program</span></span>
<span data-ttu-id="3325b-136">Hallo pijplijn in dit voorbeeld Hallo aantal woorden kaart/verminderen programma op Azure HDInsight-cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3325b-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="3325b-137">Gekoppelde Services</span><span class="sxs-lookup"><span data-stu-id="3325b-137">Linked Services</span></span>
<span data-ttu-id="3325b-138">U maakt eerst een gekoppelde service toolink hello Azure Storage dat wordt gebruikt door hello Azure HDInsight-cluster toohello Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="3325b-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="3325b-139">Als kopiëren en plakken van Hallo na code vergeet niet tooreplace **accountnaam** en **accountsleutel** met Hallo naam en sleutel van uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="3325b-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="3325b-140">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="3325b-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="3325b-141">Azure gekoppelde HDInsight-service</span><span class="sxs-lookup"><span data-stu-id="3325b-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="3325b-142">Vervolgens maakt u een gekoppelde service toolink uw Azure HDInsight-cluster toohello Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="3325b-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="3325b-143">Als kopiëren en plakken van Hallo na code vervangt **de naam van de HDInsight-cluster** met Hallo-naam van uw HDInsight-cluster en de wijziging waarden gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3325b-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="3325b-144">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="3325b-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="3325b-145">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="3325b-145">Output dataset</span></span>
<span data-ttu-id="3325b-146">Hallo-pijplijn in dit voorbeeld vindt niet alle invoer.</span><span class="sxs-lookup"><span data-stu-id="3325b-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="3325b-147">U een uitvoergegevensset voor Hallo HDInsight MapReduce-activiteit.</span><span class="sxs-lookup"><span data-stu-id="3325b-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="3325b-148">Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning.</span><span class="sxs-lookup"><span data-stu-id="3325b-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="3325b-149">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="3325b-149">Pipeline</span></span>
<span data-ttu-id="3325b-150">Hallo-pijplijn in dit voorbeeld heeft slechts één activiteit die is van het type: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="3325b-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="3325b-151">Enkele belangrijke eigenschappen van de Hallo in Hallo JSON zijn:</span><span class="sxs-lookup"><span data-stu-id="3325b-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="3325b-152">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3325b-152">Property</span></span> | <span data-ttu-id="3325b-153">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3325b-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="3325b-154">type</span><span class="sxs-lookup"><span data-stu-id="3325b-154">type</span></span> |<span data-ttu-id="3325b-155">Hallo-type te moet worden ingesteld**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="3325b-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="3325b-156">className</span><span class="sxs-lookup"><span data-stu-id="3325b-156">className</span></span> |<span data-ttu-id="3325b-157">Naam van de klasse Hallo is: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="3325b-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="3325b-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="3325b-158">jarFilePath</span></span> |<span data-ttu-id="3325b-159">Pad toohello jar-bestand met Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="3325b-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="3325b-160">Als kopiëren en plakken van Hallo na code vergeet niet toochange Hallo-naam van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3325b-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="3325b-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="3325b-161">jarLinkedService</span></span> |<span data-ttu-id="3325b-162">Gekoppelde Azure Storage-service die Hallo jar-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="3325b-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="3325b-163">Deze gekoppelde service verwijst toohello opslag die is gekoppeld aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3325b-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="3325b-164">Argumenten</span><span class="sxs-lookup"><span data-stu-id="3325b-164">arguments</span></span> |<span data-ttu-id="3325b-165">Hallo wordcount wordt gehouden met twee argumenten, invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3325b-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="3325b-166">Hallo-bestand voor invoer is Hallo davinci.txt bestand.</span><span class="sxs-lookup"><span data-stu-id="3325b-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="3325b-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="3325b-167">frequency/interval</span></span> |<span data-ttu-id="3325b-168">Hallo-waarden voor deze eigenschappen overeen Hallo uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="3325b-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="3325b-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3325b-169">linkedServiceName</span></span> |<span data-ttu-id="3325b-170">verwijst toohello gekoppelde HDInsight-service u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3325b-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

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

## <a name="run-spark-programs"></a><span data-ttu-id="3325b-171">Spark-programma's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3325b-171">Run Spark programs</span></span>
<span data-ttu-id="3325b-172">U kunt de MapReduce-activiteit toorun Spark programma's op uw HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3325b-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="3325b-173">Zie [Spark-programma's aanroepen vanuit Azure Data Factory](data-factory-spark.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3325b-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="3325b-174">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3325b-174">See Also</span></span>
* [<span data-ttu-id="3325b-175">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="3325b-176">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="3325b-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="3325b-177">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="3325b-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="3325b-178">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="3325b-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="3325b-179">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="3325b-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

