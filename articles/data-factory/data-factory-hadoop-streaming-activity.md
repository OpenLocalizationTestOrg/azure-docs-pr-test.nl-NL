---
title: Transformeer gegevens met Hadoop-Streamingactiviteit - Azure | Microsoft Docs
description: Meer informatie over hoe u de Hadoop-Streamingactiviteit kunt gebruiken in een Azure data factory om gegevens te transformeren met Hadoop-Streaming programma's uitvoeren op een op-verzoek/uw eigen HDInsight-cluster.
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
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="618c8-103">Transformeer gegevens met Hadoop-Streamingactiviteit in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="618c8-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="618c8-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="618c8-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="618c8-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="618c8-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="618c8-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="618c8-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="618c8-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="618c8-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="618c8-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="618c8-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="618c8-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="618c8-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="618c8-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="618c8-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="618c8-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="618c8-114">U kunt de activiteit HDInsightStreamingActivity aanroepen van een Hadoop-Streaming-taak van een Azure Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="618c8-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="618c8-115">De volgende JSON-fragment toont de syntaxis voor het gebruik van de HDInsightStreamingActivity in een pijplijn-JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="618c8-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="618c8-116">De HDInsight Streaming-activiteit in een Data Factory [pijplijn](data-factory-create-pipelines.md) Hadoop-Streaming programma's worden uitgevoerd op [uw eigen](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) of [op aanvraag](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="618c8-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="618c8-117">In dit artikel is gebaseerd op de [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en de ondersteunde transformatieactiviteiten toont.</span><span class="sxs-lookup"><span data-stu-id="618c8-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="618c8-118">Als u niet bekend met Azure Data Factory bent, Lees [Inleiding tot Azure Data Factory](data-factory-introduction.md) en voer de zelfstudie: [bouwen van uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md) voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="618c8-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="618c8-119">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="618c8-119">JSON sample</span></span>
<span data-ttu-id="618c8-120">Het HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="618c8-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="618c8-121">Naam van de container die wordt gebruikt door het HDInsight-cluster is standaard de naam van het cluster zelf.</span><span class="sxs-lookup"><span data-stu-id="618c8-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="618c8-122">Als de clusternaam van uw myhdicluster is, zou de naam van de blob-container die is gekoppeld myhdicluster zijn.</span><span class="sxs-lookup"><span data-stu-id="618c8-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="618c8-123">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="618c8-123">Note the following points:</span></span>

1. <span data-ttu-id="618c8-124">Stel de **linkedServiceName** naar de naam van de gekoppelde service die naar uw HDInsight verwijst-cluster op het streaming mapreduce-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="618c8-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="618c8-125">Het type van de activiteit instellen **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="618c8-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="618c8-126">Voor de **mapper** eigenschap, geef de naam van de uitvoerbare toewijzen.</span><span class="sxs-lookup"><span data-stu-id="618c8-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="618c8-127">In het voorbeeld is cat.exe de uitvoerbare toewijzen.</span><span class="sxs-lookup"><span data-stu-id="618c8-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="618c8-128">Voor de **reducer** eigenschap, de naam van de uitvoerbare reducer opgeven.</span><span class="sxs-lookup"><span data-stu-id="618c8-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="618c8-129">In het voorbeeld is wc.exe de uitvoerbare reducer.</span><span class="sxs-lookup"><span data-stu-id="618c8-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="618c8-130">Voor de **invoer** eigenschap type, geeft u het invoerbestand (inclusief de locatie) voor de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="618c8-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="618c8-131">In het voorbeeld: ' wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt ': adfsample is de blob-container, gegevens-voorbeeld/Gutenberg is de map en davinci.txt is de blob.</span><span class="sxs-lookup"><span data-stu-id="618c8-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="618c8-132">Voor de **uitvoer** eigenschap type, het uitvoerbestand (inclusief de locatie) voor de reducer opgeven.</span><span class="sxs-lookup"><span data-stu-id="618c8-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="618c8-133">De uitvoer van de Hadoop-Streaming-taak wordt geschreven naar de locatie die is opgegeven voor deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="618c8-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="618c8-134">In de **filePaths** sectie, geeft u de paden voor de toewijzing en reducer uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="618c8-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="618c8-135">In het voorbeeld: 'adfsample/example/apps/wc.exe' adfsample is de blob-container, bijvoorbeeld/apps is de map en wc.exe is het uitvoerbare bestand.</span><span class="sxs-lookup"><span data-stu-id="618c8-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="618c8-136">Voor de **fileLinkedService** -eigenschap geeft u de gekoppelde Azure Storage-service die de Azure-opslag met de bestanden die zijn opgegeven in de sectie filePaths vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="618c8-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="618c8-137">Voor de **argumenten** eigenschap, geef de argumenten voor de streaming-taak.</span><span class="sxs-lookup"><span data-stu-id="618c8-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="618c8-138">De **getDebugInfo** eigenschap is een optioneel element.</span><span class="sxs-lookup"><span data-stu-id="618c8-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="618c8-139">Wanneer deze is ingesteld op mislukt, worden de logboeken gedownload alleen bij fouten.</span><span class="sxs-lookup"><span data-stu-id="618c8-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="618c8-140">Wanneer deze is ingesteld op Always, worden altijd logboeken ongeacht de uitvoeringsstatus gedownload.</span><span class="sxs-lookup"><span data-stu-id="618c8-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="618c8-141">In het voorbeeld ziet u een uitvoergegevensset opgeven voor het Hadoop-Streamingactiviteit voor de **levert** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="618c8-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="618c8-142">Deze gegevensset is slechts een dummy gegevensset die is vereist voor het station van de planning van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="618c8-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="618c8-143">U hoeft niet te geven van een invoergegevensset voor de activiteit voor het **invoer** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="618c8-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="618c8-144">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="618c8-144">Example</span></span>
<span data-ttu-id="618c8-145">De pijplijn in dit scenario voert het programma voor streaming kaart/verminderen van aantal woorden in uw Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="618c8-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="618c8-146">Gekoppelde services</span><span class="sxs-lookup"><span data-stu-id="618c8-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="618c8-147">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="618c8-147">Azure Storage linked service</span></span>
<span data-ttu-id="618c8-148">U maakt eerst een gekoppelde service voor het koppelen van de Azure-opslag die wordt gebruikt door de Azure HDInsight-cluster aan het Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="618c8-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="618c8-149">Vergeet niet te vervangen door de naam en sleutel van uw Azure Storage accountnaam en accountsleutel als kopiëren en plakken van de volgende code.</span><span class="sxs-lookup"><span data-stu-id="618c8-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="618c8-150">Azure gekoppelde HDInsight-service</span><span class="sxs-lookup"><span data-stu-id="618c8-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="618c8-151">Maak vervolgens een gekoppelde service voor uw Azure HDInsight-cluster koppelen aan de Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="618c8-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="618c8-152">Als kopiëren en plakken van de volgende code vervangen door de naam van de HDInsight-cluster met de naam van uw HDInsight-cluster en waarden van gebruikersnaam en wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="618c8-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="618c8-153">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="618c8-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="618c8-154">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="618c8-154">Output dataset</span></span>
<span data-ttu-id="618c8-155">De pijplijn in dit voorbeeld vindt niet alle invoer.</span><span class="sxs-lookup"><span data-stu-id="618c8-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="618c8-156">U kunt een uitvoergegevensset opgeven voor de activiteit voor het streamen van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="618c8-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="618c8-157">Deze gegevensset is slechts een dummy gegevensset die is vereist voor het station van de planning van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="618c8-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="618c8-158">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="618c8-158">Pipeline</span></span>
<span data-ttu-id="618c8-159">De pijplijn in dit voorbeeld heeft slechts één activiteit die is van het type: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="618c8-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="618c8-160">Het HDInsight-cluster wordt automatisch gevuld met de voorbeeld-programma's (wc.exe en cat.exe) en gegevens (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="618c8-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="618c8-161">Naam van de container die wordt gebruikt door het HDInsight-cluster is standaard de naam van het cluster zelf.</span><span class="sxs-lookup"><span data-stu-id="618c8-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="618c8-162">Als de clusternaam van uw myhdicluster is, zou de naam van de blob-container die is gekoppeld myhdicluster zijn.</span><span class="sxs-lookup"><span data-stu-id="618c8-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="618c8-163">Zie ook</span><span class="sxs-lookup"><span data-stu-id="618c8-163">See Also</span></span>
* [<span data-ttu-id="618c8-164">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="618c8-165">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="618c8-166">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="618c8-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="618c8-167">Spark-programma's aanroepen</span><span class="sxs-lookup"><span data-stu-id="618c8-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="618c8-168">R-scripts aanroepen</span><span class="sxs-lookup"><span data-stu-id="618c8-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

