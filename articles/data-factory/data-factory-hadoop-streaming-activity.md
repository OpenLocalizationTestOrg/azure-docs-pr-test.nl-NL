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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="e636d-103">Transformeer gegevens met Hadoop-Streamingactiviteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e636d-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e636d-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e636d-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e636d-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e636d-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="e636d-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e636d-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e636d-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="e636d-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e636d-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="e636d-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e636d-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="e636d-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e636d-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e636d-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="e636d-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="e636d-114">U kunt een Hadoop-Streaming-taak van een Azure Data Factory-pijplijn Hallo HDInsightStreamingActivity activiteit worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e636d-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="e636d-115">Hallo toont volgende JSON-fragment Hallo-syntaxis voor het gebruik van Hallo HDInsightStreamingActivity in een pijplijn-JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="e636d-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="e636d-116">Hallo Streaming HDInsight-activiteit in een Gegevensfactory [pijplijn](data-factory-create-pipelines.md) Hadoop-Streaming programma's worden uitgevoerd op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e636d-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e636d-117">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en activiteiten voor gegevenstransformatie Hallo ondersteund toont.</span><span class="sxs-lookup"><span data-stu-id="e636d-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="e636d-118">Als u nieuwe tooAzure Data Factory, Lees [inleiding tooAzure Data Factory](data-factory-introduction.md) en zelfstudie Hallo: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="e636d-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="e636d-119">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e636d-119">JSON sample</span></span>
<span data-ttu-id="e636d-120">Hallo HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="e636d-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="e636d-121">Standaard is de naam van Hallo-container die wordt gebruikt door Hallo HDInsight-cluster Hallo-naam van Hallo cluster zelf.</span><span class="sxs-lookup"><span data-stu-id="e636d-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="e636d-122">Als de clusternaam van uw myhdicluster is, zou naam van Hallo blob-container die is gekoppeld myhdicluster zijn.</span><span class="sxs-lookup"><span data-stu-id="e636d-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="e636d-123">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="e636d-123">Note hello following points:</span></span>

1. <span data-ttu-id="e636d-124">Set Hallo **linkedServiceName** toohello naam Hallo gekoppelde service die wijst tooyour HDInsight-cluster op welke Hallo streaming mapreduce taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e636d-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="e636d-125">Hallo type Hallo activiteit te ingesteld**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="e636d-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="e636d-126">Voor Hallo **mapper** eigenschap Hallo naam opgeven van uitvoerbare toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e636d-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="e636d-127">In voorbeeld Hallo is cat.exe Hallo mapper uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="e636d-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="e636d-128">Voor Hallo **reducer** eigenschap Hallo-naam van de uitvoerbare reducer opgeven.</span><span class="sxs-lookup"><span data-stu-id="e636d-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="e636d-129">In voorbeeld Hallo is wc.exe hello reducer uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="e636d-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="e636d-130">Voor Hallo **invoer** eigenschap type, Hallo invoerbestand (inclusief Hallo locatie) opgeven voor Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e636d-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="e636d-131">In Hallo-voorbeeld: ' wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt ': adfsample is Hallo blob-container, gegevens-voorbeeld/Gutenberg Hallo-map en davinci.txt Hallo blob is.</span><span class="sxs-lookup"><span data-stu-id="e636d-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="e636d-132">Voor Hallo **uitvoer** eigenschap type, Hallo uitvoerbestand (inclusief Hallo locatie) voor Hallo reducer opgeven.</span><span class="sxs-lookup"><span data-stu-id="e636d-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="e636d-133">Hallo-uitvoer van Hallo Hadoop streamingtaak geschreven toohello locatie die is opgegeven voor deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e636d-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="e636d-134">In Hallo **filePaths** sectie, geeft u Hallo paden voor Hallo toewijzen en reducer uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="e636d-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="e636d-135">In Hallo-voorbeeld: 'adfsample/example/apps/wc.exe' adfsample is Hallo blob-container, voorbeeld/apps Hallo-map en wc.exe Hallo uitvoerbare is.</span><span class="sxs-lookup"><span data-stu-id="e636d-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="e636d-136">Voor Hallo **fileLinkedService** eigenschap hello Azure Storage gekoppelde service die vertegenwoordigt hello Azure-opslag met Hallo-bestanden die zijn opgegeven in Hallo filePaths sectie opgeven.</span><span class="sxs-lookup"><span data-stu-id="e636d-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="e636d-137">Voor Hallo **argumenten** eigenschap Hallo-argumenten voor streaming-taak Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="e636d-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="e636d-138">Hallo **getDebugInfo** eigenschap is een optioneel element.</span><span class="sxs-lookup"><span data-stu-id="e636d-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="e636d-139">Wanneer deze tooFailure is ingesteld, worden alleen op fout Hallo logboeken gedownload.</span><span class="sxs-lookup"><span data-stu-id="e636d-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="e636d-140">Wanneer deze tooAlways is ingesteld, worden altijd logboeken ongeacht de uitvoeringsstatus van Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="e636d-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="e636d-141">In het Hallo-voorbeeld ziet u een uitvoergegevensset voor Hadoop-Streamingactiviteit Hallo voor Hallo opgeven **levert** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e636d-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="e636d-142">Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning.</span><span class="sxs-lookup"><span data-stu-id="e636d-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="e636d-143">U hoeft geen toospecify invoergegevensset voor de activiteit voor Hallo Hallo **invoer** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e636d-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="e636d-144">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e636d-144">Example</span></span>
<span data-ttu-id="e636d-145">Hallo-pijplijn in dit scenario voert Hallo aantal woorden streaming kaart/verminderen programma op Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e636d-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="e636d-146">Gekoppelde services</span><span class="sxs-lookup"><span data-stu-id="e636d-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e636d-147">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="e636d-147">Azure Storage linked service</span></span>
<span data-ttu-id="e636d-148">U maakt eerst een gekoppelde service toolink hello Azure Storage dat wordt gebruikt door hello Azure HDInsight-cluster toohello Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="e636d-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="e636d-149">Als u kopiëren en plakken Hallo code te volgen, vergeet niet tooreplace account naam en een account met Hallo naam en sleutel van uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="e636d-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="e636d-150">Azure gekoppelde HDInsight-service</span><span class="sxs-lookup"><span data-stu-id="e636d-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="e636d-151">Vervolgens maakt u een gekoppelde service toolink uw Azure HDInsight-cluster toohello Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="e636d-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="e636d-152">Als kopiëren en plakken van Hallo na code vervangen door de naam van de HDInsight-cluster Hallo-naam van uw HDInsight-cluster en waarden van gebruikersnaam en wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e636d-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="e636d-153">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="e636d-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="e636d-154">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="e636d-154">Output dataset</span></span>
<span data-ttu-id="e636d-155">Hallo-pijplijn in dit voorbeeld vindt niet alle invoer.</span><span class="sxs-lookup"><span data-stu-id="e636d-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="e636d-156">U een uitvoergegevensset voor Hallo Streaming HDInsight-activiteit.</span><span class="sxs-lookup"><span data-stu-id="e636d-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="e636d-157">Deze gegevensset is slechts een dummy gegevensset die is vereist toodrive Hallo pijplijn planning.</span><span class="sxs-lookup"><span data-stu-id="e636d-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="e636d-158">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="e636d-158">Pipeline</span></span>
<span data-ttu-id="e636d-159">Hallo-pijplijn in dit voorbeeld heeft slechts één activiteit die is van het type: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="e636d-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="e636d-160">Hallo HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="e636d-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="e636d-161">Standaard is de naam van Hallo-container die wordt gebruikt door Hallo HDInsight-cluster Hallo-naam van Hallo cluster zelf.</span><span class="sxs-lookup"><span data-stu-id="e636d-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="e636d-162">Als de clusternaam van uw myhdicluster is, zou naam van Hallo blob-container die is gekoppeld myhdicluster zijn.</span><span class="sxs-lookup"><span data-stu-id="e636d-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="e636d-163">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e636d-163">See Also</span></span>
* [<span data-ttu-id="e636d-164">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="e636d-165">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="e636d-166">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="e636d-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="e636d-167">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="e636d-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="e636d-168">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="e636d-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

