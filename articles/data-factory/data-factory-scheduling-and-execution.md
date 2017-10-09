---
title: aaaScheduling en uitvoering met Data Factory | Microsoft Docs
description: Meer informatie over plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="a4aa7-103">Data Factory plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a4aa7-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="a4aa7-104">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van hello Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="a4aa7-105">In dit artikel wordt ervan uitgegaan dat u van de Data Factory toepassing model concepten basisbeginselen, met inbegrip van activiteiten, pijplijnen, gekoppelde services en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="a4aa7-106">Zie voor de basisconcepten van Azure Data Factory, Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="a4aa7-107">Inleiding tooData Factory</span><span class="sxs-lookup"><span data-stu-id="a4aa7-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="a4aa7-108">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="a4aa7-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="a4aa7-109">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="a4aa7-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="a4aa7-110">Begin- en eindtijden van pijplijn</span><span class="sxs-lookup"><span data-stu-id="a4aa7-110">Start and end times of pipeline</span></span>
<span data-ttu-id="a4aa7-111">Een pijplijn is active alleen tussen de **start** tijd en **end** tijd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="a4aa7-112">Het is niet uitgevoerd vóór de begintijd Hallo of na de eindtijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="a4aa7-113">Als het Hallo-pipeline is onderbroken, is het niet uitgevoerd ongeacht de begin- en -tijd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="a4aa7-114">Voor een toorun pijplijn mag deze niet worden onderbroken.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="a4aa7-115">U vinden deze instellingen (start, eindgebruikers, onderbroken) in de definitie van de pijplijn Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="a4aa7-116">Zie voor meer informatie deze eigenschappen [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="a4aa7-117">Planning voor een activiteit opgeven</span><span class="sxs-lookup"><span data-stu-id="a4aa7-117">Specify schedule for an activity</span></span>
<span data-ttu-id="a4aa7-118">Het is niet Hallo pijplijn die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="a4aa7-119">Het Hallo-activiteiten in Hallo pijplijn die worden uitgevoerd in Hallo is algehele context van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="a4aa7-120">U kunt een terugkerend schema voor een activiteit opgeven met behulp van Hallo **scheduler** sectie van de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="a4aa7-121">Bijvoorbeeld, kunt u plannen een toorun activiteit per uur als volgt:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="a4aa7-122">Zoals u in het volgende diagram hello, opgeven van dat een planning voor een activiteit wordt een reeks van windows met daling in Hallo pipeline-begin- en eindtijden.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="a4aa7-123">Windows daling zijn een reeks met vaste grootte niet-overlappende, aaneengesloten tijdsintervallen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="a4aa7-124">Deze logische daling vensters voor een activiteit worden genoemd **activiteitsvensters**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Voorbeeld van de activiteit scheduler](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="a4aa7-126">Hallo **scheduler** eigenschap voor een activiteit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="a4aa7-127">Als u deze eigenschap opgeeft, moet deze Hallo uitgebracht die u in het Hallo-definitie van de uitvoergegevensset voor de activiteit Hallo opgeeft overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="a4aa7-128">Uitvoergegevensset is momenteel welke stations Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="a4aa7-129">Daarom moet u een uitvoergegevensset maken, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="a4aa7-130">Geef de planning voor een gegevensset</span><span class="sxs-lookup"><span data-stu-id="a4aa7-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="a4aa7-131">Een activiteit in een Data Factory-pijplijn kan duren voordat de invoer van nul of meer **gegevenssets** en een of meer uitvoergegevenssets te produceren.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="a4aa7-132">Voor een activiteit, kunt u Hallo uitgebracht welke Hallo invoergegevens beschikbaar is of uitvoergegevens hello wordt gemaakt met behulp van Hallo **beschikbaarheid** sectie in Hallo gegevensset definities.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="a4aa7-133">**Frequentie** in Hallo **beschikbaarheid** sectie Hallo tijdseenheid geeft.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="a4aa7-134">Hallo toegestane waarden voor de frequentie zijn: minuut, uur, dag, Week en maand.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="a4aa7-135">Hallo **interval** eigenschap in de sectie beschikbaarheid Hallo vermenigvuldigingsfactor voor de frequentie.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="a4aa7-136">Bijvoorbeeld: als Hallo frequentie tooDay is ingesteld en de interval too1 voor een uitvoergegevensset, Hallo uitvoergegevens dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="a4aa7-137">Als u Hallo frequentie als minuut opgeeft, raden wij u Hallo interval toono kleiner is dan 15 instellen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="a4aa7-138">In Hallo voorbeeld te volgen, Hallo invoergegevens beschikbaar per uur en uitvoergegevens Hallo per uur wordt geproduceerd (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="a4aa7-139">**Invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="a4aa7-140">**Uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="a4aa7-141">Op dit moment **output dataset stations Hallo planning**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="a4aa7-142">Met andere woorden, is opgegeven voor de uitvoergegevensset Hallo Hallo-upschema gebruikte toorun een activiteit tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="a4aa7-143">Daarom moet u een uitvoergegevensset maken, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="a4aa7-144">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="a4aa7-145">In de volgende Hallo pipeline-definitie hello **scheduler** eigenschap gebruikte toospecify planning voor Hallo-activiteit is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="a4aa7-146">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-146">This property is optional.</span></span> <span data-ttu-id="a4aa7-147">Op dit moment Hallo-schema voor het Hallo-activiteit moet overeenkomen met opgegeven voor de uitvoergegevensset Hallo Hallo-upschema.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="a4aa7-148">In dit voorbeeld Hallo activiteit wordt uitgevoerd per uur tussen Hallo starten en eindtijden van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="a4aa7-149">Hallo uitvoergegevens wordt per uur gemaakt voor drie uur windows (8 AM - 9 uur, 9: 00 uur - 10: 00 uur, en 10: 00 - 11 uur).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="a4aa7-150">Elke eenheid van gegevens gebruikt of die wordt geproduceerd door een activiteit die wordt uitgevoerd, heet een **gegevenssegment**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="a4aa7-151">Hallo volgende diagram toont een voorbeeld van een activiteit met één invoergegevensset en één uitvoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Beschikbaarheid scheduler](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="a4aa7-153">Hallo diagram toont Hallo per uur in gegevenssegmenten voor Hallo invoer en uitvoer van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="a4aa7-154">Hallo diagram ziet u drie invoer segmenten die gereed voor verwerking zijn.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="a4aa7-155">Hallo 10 11 uur activiteit wordt uitgevoerd, het opstellen van Hallo 10 11 uur uitvoer segment.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="a4aa7-156">U hebt toegang tot Hallo tijdsinterval die is gekoppeld aan het huidige segment Hallo gegevensset JSON Hallo met behulp van variabelen: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) en [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="a4aa7-157">Op deze manier kunt u Hallo tijdsinterval die is gekoppeld aan het venster van een activiteit met behulp van Hallo WindowStart en WindowEnd openen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="a4aa7-158">Hallo-schema van een activiteit moet overeenkomen met de Hallo planning van Hallo uitvoergegevensset voor Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="a4aa7-159">Daarom Hallo SliceStart en SliceEnd waarden zijn Hallo dezelfde als WindowStart en WindowEnd waarden respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="a4aa7-160">Zie voor meer informatie over deze variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md#data-factory-system-variables) artikelen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="a4aa7-161">U kunt deze variabelen voor verschillende doeleinden gebruiken in de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="a4aa7-162">Bijvoorbeeld, kunt u ze tooselect gegevens uit de invoer- en uitvoergegevenssets representatie van time series-gegevens (bijvoorbeeld: 8 AM too9 BEN).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="a4aa7-163">Dit voorbeeld wordt tevens **WindowStart** en **WindowEnd** tooselect relevante gegevens voor een activiteit uitvoeren en kopieer het tooa blob met de juiste Hallo **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="a4aa7-164">Hallo **folderPath** geparameteriseerde toohave van een afzonderlijke map voor elk uur is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="a4aa7-165">In de Hallo voorgaande voorbeeld, Hallo Hallo schema is opgegeven voor de invoer- en uitvoergegevenssets dezelfde (elk uur).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="a4aa7-166">Als invoergegevensset voor activiteit Hallo Hallo beschikbaar op een andere frequentie spreek om de 15 minuten is, uitgevoerd Hallo-activiteit die deze uitvoergegevensset produceert nog eens per uur, zoals Hallo uitvoergegevensset is welke stations Hallo activiteitenplanning.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="a4aa7-167">Zie voor meer informatie [Model gegevenssets frequentie](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="a4aa7-168">Beschikbaarheid van de gegevensset en het beleid</span><span class="sxs-lookup"><span data-stu-id="a4aa7-168">Dataset availability and policies</span></span>
<span data-ttu-id="a4aa7-169">U hebt al gezien Hallo informatie over het gebruik van eigenschappen voor frequentie en het interval in Hallo beschikbaarheidssectie van de definitie van gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="a4aa7-170">Er zijn enkele andere eigenschappen die betrekking hebben op Hallo plannen en uitvoeren van een activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="a4aa7-171">Beschikbaarheid van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a4aa7-171">Dataset availability</span></span> 
<span data-ttu-id="a4aa7-172">Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beschikbaarheid** sectie:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="a4aa7-173">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a4aa7-173">Property</span></span> | <span data-ttu-id="a4aa7-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4aa7-174">Description</span></span> | <span data-ttu-id="a4aa7-175">Vereist</span><span class="sxs-lookup"><span data-stu-id="a4aa7-175">Required</span></span> | <span data-ttu-id="a4aa7-176">Standaard</span><span class="sxs-lookup"><span data-stu-id="a4aa7-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a4aa7-177">frequency</span><span class="sxs-lookup"><span data-stu-id="a4aa7-177">frequency</span></span> |<span data-ttu-id="a4aa7-178">Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="a4aa7-179"><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand</span><span class="sxs-lookup"><span data-stu-id="a4aa7-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="a4aa7-180">Ja</span><span class="sxs-lookup"><span data-stu-id="a4aa7-180">Yes</span></span> |<span data-ttu-id="a4aa7-181">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-181">NA</span></span> |
| <span data-ttu-id="a4aa7-182">interval</span><span class="sxs-lookup"><span data-stu-id="a4aa7-182">interval</span></span> |<span data-ttu-id="a4aa7-183">Hiermee geeft u een vermenigvuldiger voor de frequentie</span><span class="sxs-lookup"><span data-stu-id="a4aa7-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="a4aa7-184">"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="a4aa7-185">Als u de gegevensset toobe gesegmenteerd op uurbasis moet hello, stelt u <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="a4aa7-186"><b>Opmerking</b>: als u de frequentie als minuut opgeeft, raden wij aan dat u Hallo interval toono kleiner is dan 15</span><span class="sxs-lookup"><span data-stu-id="a4aa7-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="a4aa7-187">Ja</span><span class="sxs-lookup"><span data-stu-id="a4aa7-187">Yes</span></span> |<span data-ttu-id="a4aa7-188">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-188">NA</span></span> |
| <span data-ttu-id="a4aa7-189">stijl</span><span class="sxs-lookup"><span data-stu-id="a4aa7-189">style</span></span> |<span data-ttu-id="a4aa7-190">Hiermee geeft u op of Hallo segment Hallo beginnen of eindigen van hello-interval moet worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="a4aa7-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="a4aa7-191">StartOfInterval</span></span></li><li><span data-ttu-id="a4aa7-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a4aa7-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="a4aa7-193">Als de frequentie tooMonth is ingesteld en stijl tooEndOfInterval is ingesteld, wordt Hallo segment op Hallo laatste dag van de maand geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="a4aa7-194">Als Hallo stijl is ingesteld tooStartOfInterval, wordt Hallo segment geproduceerd op Hallo eerste dag van de maand.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="a4aa7-195">Als frequentie tooDay is ingesteld en stijl tooEndOfInterval is ingesteld, wordt in het afgelopen uur van de dag Hallo HALLO hallo segment geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="a4aa7-196">Als frequentie tooHour is ingesteld en stijl tooEndOfInterval is ingesteld, worden Hallo segment wordt geproduceerd achter Hallo Hallo uur.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="a4aa7-197">Voor een segment 1-2 uur gedurende Hallo segment geproduceerd om 2 uur.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="a4aa7-198">Nee</span><span class="sxs-lookup"><span data-stu-id="a4aa7-198">No</span></span> |<span data-ttu-id="a4aa7-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a4aa7-199">EndOfInterval</span></span> |
| <span data-ttu-id="a4aa7-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="a4aa7-200">anchorDateTime</span></span> |<span data-ttu-id="a4aa7-201">Hiermee definieert u Hallo absolute positie in de tijd die wordt gebruikt door de grenzen van scheduler toocompute gegevensset segment.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="a4aa7-202"><b>Opmerking</b>: als Hallo AnchorDateTime bevat de datumonderdelen die meer gedetailleerd dan Hallo frequentie zijn dan hello gedetailleerdere onderdelen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="a4aa7-203">Bijvoorbeeld, als hello <b>interval</b> is <b>per uur</b> (frequentie: uur en interval: 1) en Hallo <b>AnchorDateTime</b> bevat <b>minuten en seconden</b>, vervolgens Hallo <b>minuten en seconden</b> delen van Hallo AnchorDateTime worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="a4aa7-204">Nee</span><span class="sxs-lookup"><span data-stu-id="a4aa7-204">No</span></span> |<span data-ttu-id="a4aa7-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="a4aa7-205">01/01/0001</span></span> |
| <span data-ttu-id="a4aa7-206">offset</span><span class="sxs-lookup"><span data-stu-id="a4aa7-206">offset</span></span> |<span data-ttu-id="a4aa7-207">TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="a4aa7-208"><b>Opmerking</b>: als zowel anchorDateTime als offset worden opgegeven, Hallo resultaat Hallo gecombineerd shift is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="a4aa7-209">Nee</span><span class="sxs-lookup"><span data-stu-id="a4aa7-209">No</span></span> |<span data-ttu-id="a4aa7-210">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="a4aa7-211">offset voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a4aa7-211">offset example</span></span>
<span data-ttu-id="a4aa7-212">Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. UTC-tijd (middernacht).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="a4aa7-213">Als u Hallo start tijd toobe 06: 00 UTC-tijd in plaats daarvan wilt, stelt u Hallo zoals weergegeven in het volgende codefragment Hallo offset:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="a4aa7-214">Voorbeeld van anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="a4aa7-214">anchorDateTime example</span></span>
<span data-ttu-id="a4aa7-215">In de Hallo voorbeeld te volgen, wordt de elke 23 uur in Hallo gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="a4aa7-216">Hallo eerste cirkelsegment begint bij Hallo tijd die is opgegeven door Hallo anchorDateTime die is ingesteld te`2017-04-19T08:00:00` (UTC-tijd).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="a4aa7-217">offset/stijl voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a4aa7-217">offset/style Example</span></span>
<span data-ttu-id="a4aa7-218">Hallo volgende gegevensset is een maandelijkse gegevensset en op 3rd van elke maand om 8:00 uur wordt geproduceerd (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="a4aa7-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="a4aa7-219">DataSet beleid</span><span class="sxs-lookup"><span data-stu-id="a4aa7-219">Dataset policy</span></span>
<span data-ttu-id="a4aa7-220">Een dataset kan een validatiebeleid gedefinieerd waarmee wordt aangegeven hoe Hallo-gegevens die zijn gegenereerd door de uitvoering van een segment kan worden gevalideerd voordat deze gereed voor verbruik is hebben.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="a4aa7-221">In dergelijke gevallen nadat het Hallo-segment is uitgevoerd, Hallo uitvoer segment de status wordt gewijzigd te**wachten** met een substatus van **validatie**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="a4aa7-222">Nadat Hallo segmenten zijn geverifieerd, Hallo segment status verandert te**gereed**.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="a4aa7-223">Als een gegevenssegment is geproduceerd, maar niet gevalideerd hello worden kan, worden de activiteiten bij uitvoering downstream segmenten die afhankelijk van dit segment zijn niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="a4aa7-224">[Bewaken en beheren van pijplijnen](data-factory-monitor-manage-pipelines.md) dekt Hallo verschillende statussen van gegevenssegmenten in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="a4aa7-225">Hallo **beleid** sectie in de definitie van gegevensset definieert Hallo criteria of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="a4aa7-226">Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beleid** sectie:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="a4aa7-227">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="a4aa7-227">Policy Name</span></span> | <span data-ttu-id="a4aa7-228">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4aa7-228">Description</span></span> | <span data-ttu-id="a4aa7-229">Te worden toegepast</span><span class="sxs-lookup"><span data-stu-id="a4aa7-229">Applied too</span></span>| <span data-ttu-id="a4aa7-230">Vereist</span><span class="sxs-lookup"><span data-stu-id="a4aa7-230">Required</span></span> | <span data-ttu-id="a4aa7-231">Standaard</span><span class="sxs-lookup"><span data-stu-id="a4aa7-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a4aa7-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="a4aa7-232">minimumSizeMB</span></span> | <span data-ttu-id="a4aa7-233">Valideert dat Hallo-gegevens in een **Azure blob** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="a4aa7-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a4aa7-234">Azure Blob</span></span> |<span data-ttu-id="a4aa7-235">Nee</span><span class="sxs-lookup"><span data-stu-id="a4aa7-235">No</span></span> |<span data-ttu-id="a4aa7-236">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-236">NA</span></span> |
| <span data-ttu-id="a4aa7-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="a4aa7-237">minimumRows</span></span> | <span data-ttu-id="a4aa7-238">Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="a4aa7-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4aa7-239">Azure SQL Database</span></span></li><li><span data-ttu-id="a4aa7-240">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="a4aa7-240">Azure Table</span></span></li></ul> |<span data-ttu-id="a4aa7-241">Nee</span><span class="sxs-lookup"><span data-stu-id="a4aa7-241">No</span></span> |<span data-ttu-id="a4aa7-242">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="a4aa7-243">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="a4aa7-243">Examples</span></span>
<span data-ttu-id="a4aa7-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="a4aa7-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="a4aa7-246">Zie voor meer informatie over deze eigenschappen en voorbeelden [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="a4aa7-247">Beleidsregels voor activiteiten</span><span class="sxs-lookup"><span data-stu-id="a4aa7-247">Activity policies</span></span>
<span data-ttu-id="a4aa7-248">Beleid geldt voor Hallo run-time gedrag van een activiteit specifiek wanneer Hallo segment van een tabel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="a4aa7-249">Hallo volgende tabel biedt details Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="a4aa7-250">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a4aa7-250">Property</span></span> | <span data-ttu-id="a4aa7-251">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a4aa7-251">Permitted values</span></span> | <span data-ttu-id="a4aa7-252">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="a4aa7-252">Default Value</span></span> | <span data-ttu-id="a4aa7-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4aa7-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a4aa7-254">Gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="a4aa7-254">concurrency</span></span> |<span data-ttu-id="a4aa7-255">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="a4aa7-255">Integer</span></span> <br/><br/><span data-ttu-id="a4aa7-256">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="a4aa7-256">Max value: 10</span></span> |<span data-ttu-id="a4aa7-257">1</span><span class="sxs-lookup"><span data-stu-id="a4aa7-257">1</span></span> |<span data-ttu-id="a4aa7-258">Het aantal gelijktijdige uitvoeringen van Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="a4aa7-259">Bepaalt de Hallo aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="a4aa7-260">Bijvoorbeeld, als een activiteit toogo via moet sneller een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid Hallo gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="a4aa7-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="a4aa7-261">executionPriorityOrder</span></span> |<span data-ttu-id="a4aa7-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="a4aa7-262">NewestFirst</span></span><br/><br/><span data-ttu-id="a4aa7-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="a4aa7-263">OldestFirst</span></span> |<span data-ttu-id="a4aa7-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="a4aa7-264">OldestFirst</span></span> |<span data-ttu-id="a4aa7-265">Hiermee wordt bepaald Hallo ordening van gegevenssegmenten dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="a4aa7-266">Als er 2 segmenten (één gebeurt om 4 uur en 17: 00 uur een andere één voor één) en beide zijn in behandeling kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="a4aa7-267">Als u Hallo executionPriorityOrder toobe NewestFirst instelt, wordt eerst segment hello om 17.00 verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="a4aa7-268">Op dezelfde manier als u Hallo executionPriorityORder toobe OldestFIrst hebt ingesteld, klikt u vervolgens Hallo segment om 4 uur is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="a4aa7-269">retry</span><span class="sxs-lookup"><span data-stu-id="a4aa7-269">retry</span></span> |<span data-ttu-id="a4aa7-270">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="a4aa7-270">Integer</span></span><br/><br/><span data-ttu-id="a4aa7-271">De maximale waarde is 10</span><span class="sxs-lookup"><span data-stu-id="a4aa7-271">Max value can be 10</span></span> |<span data-ttu-id="a4aa7-272">0</span><span class="sxs-lookup"><span data-stu-id="a4aa7-272">0</span></span> |<span data-ttu-id="a4aa7-273">Aantal nieuwe pogingen voordat de gegevensverwerking Hallo voor Hallo segment wordt als mislukt gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="a4aa7-274">Activiteit is uitgevoerd voor een gegevenssegment wordt opnieuw geprobeerd up toohello opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="a4aa7-275">Hallo nieuwe poging wordt gedaan zo snel mogelijk na een storing Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="a4aa7-276">timeout</span><span class="sxs-lookup"><span data-stu-id="a4aa7-276">timeout</span></span> |<span data-ttu-id="a4aa7-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a4aa7-277">TimeSpan</span></span> |<span data-ttu-id="a4aa7-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a4aa7-278">00:00:00</span></span> |<span data-ttu-id="a4aa7-279">Time-out voor Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-279">Timeout for hello activity.</span></span> <span data-ttu-id="a4aa7-280">Voorbeeld: 00:10:00 (impliceert time-out 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="a4aa7-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="a4aa7-281">Als een waarde niet opgegeven is of 0 is, is Hallo time-out oneindig.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="a4aa7-282">Hallo gegevensverwerking tijd op een segment overschrijdt de time-outwaarde Hallo, deze wordt geannuleerd als Hallo-systeem probeert tooretry Hallo verwerking.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="a4aa7-283">Hallo aantal nieuwe pogingen, is afhankelijk van de eigenschap retry Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="a4aa7-284">Wanneer een time-out optreedt, Hallo status tooTimedOut ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="a4aa7-285">Vertraging</span><span class="sxs-lookup"><span data-stu-id="a4aa7-285">delay</span></span> |<span data-ttu-id="a4aa7-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a4aa7-286">TimeSpan</span></span> |<span data-ttu-id="a4aa7-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a4aa7-287">00:00:00</span></span> |<span data-ttu-id="a4aa7-288">Geef Hallo vertraging optreden voordat de verwerking van Hallo segment wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="a4aa7-289">Hallo-uitvoering van de activiteit voor een gegevenssegment wordt gestart nadat Hallo vertraging is verstreken Hallo uitvoeringstijd verwacht.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="a4aa7-290">Voorbeeld: 00:10:00 (betekent vertraging van 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="a4aa7-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="a4aa7-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="a4aa7-291">longRetry</span></span> |<span data-ttu-id="a4aa7-292">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="a4aa7-292">Integer</span></span><br/><br/><span data-ttu-id="a4aa7-293">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="a4aa7-293">Max value: 10</span></span> |<span data-ttu-id="a4aa7-294">1</span><span class="sxs-lookup"><span data-stu-id="a4aa7-294">1</span></span> |<span data-ttu-id="a4aa7-295">Hallo aantal lang pogingen proberen voordat Hallo segment uitvoering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="a4aa7-296">longRetry pogingen door longRetryInterval gelijkmatig verdeeld.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="a4aa7-297">Als u een tijd tussen pogingen toospecify moet, dus longRetry gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="a4aa7-298">Als zowel de nieuwe pogingen en de longRetry worden opgegeven, elke poging longRetry bevat nieuwe pogingen en Hallo kunt u het maximale aantal pogingen is opnieuw * longRetry.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="a4aa7-299">Bijvoorbeeld, als er Hallo instellingen in Hallo activiteit-beleid te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="a4aa7-300">Probeer: 3</span><span class="sxs-lookup"><span data-stu-id="a4aa7-300">Retry: 3</span></span><br/><span data-ttu-id="a4aa7-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="a4aa7-301">longRetry: 2</span></span><br/><span data-ttu-id="a4aa7-302">longRetryInterval: 01:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="a4aa7-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="a4aa7-303">Wordt ervan uitgegaan dat er is slechts één segment tooexecute (status Waiting) en Hallo activiteit is uitgevoerd elke keer mislukt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="a4aa7-304">Er zou worden in eerste instantie 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="a4aa7-305">Na elke poging zijn Hallo segment status probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="a4aa7-306">Nadat de eerste 3 pogingen hebben bekeken, zou Hallo segment status LongRetry zijn.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="a4aa7-307">Na een uur (dat wil zeggen, de longRetryInteval waarde), zou er een andere set 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="a4aa7-308">Hallo segment status zou niet hierna is en geen pogingen meer zou worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="a4aa7-309">Daarom is algemene 6 geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="a4aa7-310">Als een uitvoering is geslaagd, Hallo segment de status gereed zijn en er worden geen pogingen meer geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="a4aa7-311">longRetry kan worden gebruikt in situaties waarbij afhankelijke gegevens aankomen op niet-deterministische tijdstippen of hello algehele omgeving flaky onder welke gegevensverwerking plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="a4aa7-312">In dergelijke gevallen niet pogingen doen achter elkaar kunt en uitvoer doet na een tijd resulteert in het Hallo-interval gewenst.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="a4aa7-313">Waarschuwing: geen hoge waarden voor de longRetry of longRetryInterval instelt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="a4aa7-314">Hogere waarden dat normaal gesproken andere al problemen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="a4aa7-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="a4aa7-315">longRetryInterval</span></span> |<span data-ttu-id="a4aa7-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a4aa7-316">TimeSpan</span></span> |<span data-ttu-id="a4aa7-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a4aa7-317">00:00:00</span></span> |<span data-ttu-id="a4aa7-318">Hallo vertraging tussen pogingen lang</span><span class="sxs-lookup"><span data-stu-id="a4aa7-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="a4aa7-319">Zie voor meer informatie [pijplijnen](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="a4aa7-320">Parallelle verwerking van gegevenssegmenten</span><span class="sxs-lookup"><span data-stu-id="a4aa7-320">Parallel processing of data slices</span></span>
<span data-ttu-id="a4aa7-321">Hallo begindatum voor Hallo pijplijn kunt u instellen in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="a4aa7-322">Wanneer u doet dit, wordt Data Factory automatisch berekend (back-opvulling) alle gegevenssegmenten Hallo afgelopen en ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="a4aa7-323">Bijvoorbeeld: als u een pijplijn met een begindatum 2017-04-01 maken en Hallo de huidige datum 2017-04-10 valt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="a4aa7-324">Als Hallo uitgebracht Hallo uitvoergegevensset dagelijks vervolgens Data Factory wordt gestart voor het verwerken van alle Hallo segmenten van 2017-04-01 is too2017-04-09 onmiddellijk omdat Hallo begindatum in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="a4aa7-325">Hallo-segment van 2017-04-10 is niet verwerkt nog omdat Hallo-waarde van de eigenschap style in de sectie beschikbaarheid Hallo EndOfInterval standaard.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="a4aa7-326">Hallo oudste segment is verwerkt eerst als Hallo standaard waarde van executionPriorityOrder OldestFirst is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="a4aa7-327">Zie voor een beschrijving van de eigenschap style Hallo [gegevensset beschikbaarheid](#dataset-availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="a4aa7-328">Zie voor een beschrijving van Hallo executionPriorityOrder sectie Hallo [beleidsregels voor activiteiten](#activity-policies) sectie.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="a4aa7-329">Kunt u gegevens back gevuld segmenten toobe parallel worden verwerkt door de instelling Hallo **gelijktijdigheid** eigenschap in Hallo **beleid** sectie van de JSON van de Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="a4aa7-330">Deze eigenschap bepaalt het aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="a4aa7-331">de standaardwaarde Hallo voor Hallo gelijktijdigheid eigenschap is 1.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="a4aa7-332">Daarom is een segment verwerkt op een tijdstip standaard.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="a4aa7-333">Hallo maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-333">hello maximum value is 10.</span></span> <span data-ttu-id="a4aa7-334">Wanneer een pijplijn toogo via een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid van taken moet Hallo gegevensverwerking wordt versneld.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="a4aa7-335">Voer een mislukte gegevenssegment</span><span class="sxs-lookup"><span data-stu-id="a4aa7-335">Rerun a failed data slice</span></span>
<span data-ttu-id="a4aa7-336">Wanneer een fout optreedt tijdens het verwerken van een gegevenssegment, vindt u waarom de verwerking van een segment Hallo via Azure portal-blades of Monitor and Manage App is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="a4aa7-337">Zie [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="a4aa7-338">Overweeg het volgende voorbeeld ziet u twee activiteiten Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="a4aa7-339">Activiteit1 en activiteit 2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="a4aa7-340">Activiteit1 een segment van Dataset1 verbruikt en een segment van Dataset2 die wordt gebruikt als invoer door activiteit2 tooproduce een segment Hallo laatste gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Mislukte segment](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="a4aa7-342">Hallo diagram toont die uit drie recente segmenten, er is een fout produceren Hallo 9 10 uur segment voor Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="a4aa7-343">Data Factory-afhankelijkheid voor Hallo time series dataset automatisch worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="a4aa7-344">Hallo activiteit die wordt uitgevoerd voor Hallo 9 10 uur downstream segment worden hierdoor niet gestart.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="a4aa7-345">Data Factory bewaking en beheer-hulpprogramma's kunnen u toodrill in Hallo diagnostische logboeken voor Hallo mislukte segment tooeasily zoeken Hallo hoofdmap voor Hallo probleem veroorzaken en op te lossen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="a4aa7-346">Nadat u Hallo probleem hebt opgelost, kunt u eenvoudig hello activiteit die wordt uitgevoerd tooproduce Hallo mislukte segment te starten.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="a4aa7-347">Voor meer informatie over het toorerun en statusovergangen voor gegevenssegmenten begrijpen, Zie [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="a4aa7-348">Nadat u opnieuw Hallo uitvoeren 9 10 uur segmenteren voor **Dataset2**, Data Factory Hallo uitvoeren voor Hallo 9 10 uur afhankelijke segment op Hallo laatste gegevensset wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Mislukte segment opnieuw uitvoeren](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="a4aa7-350">Meerdere activiteiten in een pijplijn</span><span class="sxs-lookup"><span data-stu-id="a4aa7-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="a4aa7-351">Een pijplijn kan echter meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="a4aa7-352">Als er meerdere activiteiten in een pijplijn en Hallo-uitvoer van een activiteit geen invoer van een andere activiteit is, Hallo activiteiten kunnen parallel worden uitgevoerd als invoer gegevenssegmenten voor Hallo activiteiten klaar bent.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="a4aa7-353">U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a4aa7-354">Hallo-activiteiten kunnen worden ingesteld in Hallo dezelfde pijplijn of in verschillende pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="a4aa7-355">Hallo tweede activiteit wordt uitgevoerd, alleen wanneer hello eerst een succes voltooid wordt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="a4aa7-356">Denk bijvoorbeeld Hallo geval waarbij een pijplijn twee activiteiten heeft te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="a4aa7-357">A1 activiteit waarvoor externe invoergegevensset D1 en D2 uitvoergegevensset die wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="a4aa7-358">Activiteit A2 die invoer uit gegevensset D2 is vereist en produceert uitvoergegevensset D3.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="a4aa7-359">In dit scenario, activiteiten A1 en A2 zijn in Hallo dezelfde pipeline.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="a4aa7-360">Hallo activiteit die a1 wordt uitgevoerd als externe gegevens Hallo beschikbaar is en de frequentie van geplande Hallo beschikbaarheid is bereikt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="a4aa7-361">Hallo activiteit A2 wordt uitgevoerd als hello geplande segmenten van D2 beschikbaar en hello frequentie van geplande beschikbaarheid is bereikt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="a4aa7-362">Als er een fout in een van de segmenten in de gegevensset D2 hello, voert A2 niet voor dat segment totdat deze beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="a4aa7-363">Hallo diagramweergave met beide activiteiten in Hallo dezelfde pijplijn eruit zou Hallo-diagram te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Activiteiten in Hallo-koppeling met dezelfde pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="a4aa7-365">Zoals eerder vermeld, kunnen in verschillende pijplijnen Hallo activiteiten worden.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="a4aa7-366">In een dergelijk scenario eruit Hallo diagramweergave als Hallo-diagram te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Koppeling van activiteiten in twee pijplijnen](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="a4aa7-368">Zie Hallo [sequentieel kopiëren](#copy-sequentially) sectie in het Hallo-bijlage voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="a4aa7-369">Model gegevenssets frequentie</span><span class="sxs-lookup"><span data-stu-id="a4aa7-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="a4aa7-370">In de voorbeelden van Hallo zijn Hallo frequenties voor invoer en uitvoer gegevenssets en Hallo activiteit Planningsvenster Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="a4aa7-371">Sommige scenario's moet Hallo mogelijkheid tooproduce uitvoer met een frequentie anders dan Hallo frequenties van een of meer invoerwaarden.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="a4aa7-372">Data Factory biedt ondersteuning voor het modelleren van deze scenario's.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="a4aa7-373">Voorbeeld 1: Een dagelijkse uitvoer-rapport voor invoergegevens die beschikbaar is om het uur produceren</span><span class="sxs-lookup"><span data-stu-id="a4aa7-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="a4aa7-374">Neem bijvoorbeeld een scenario waarin u hebt ingevoerd meetgegevens van sensoren beschikbaar om het uur in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="a4aa7-375">Gewenste tooproduce een dagelijkse cumulatieve rapport met statistieken zoals gemiddelde, maximum en minimum voor Hallo dag met [Data Factory hive-activiteit](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="a4aa7-376">Hier ziet u hoe u dit scenario met Data Factory kunt model:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="a4aa7-377">**Invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-377">**Input dataset**</span></span>

<span data-ttu-id="a4aa7-378">Hallo invoer per uur bestanden worden verwijderd in de map Hallo voor Hallo opgegeven dag.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="a4aa7-379">Beschikbaarheid voor invoer is ingesteld op **uur** (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="a4aa7-380">**Uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-380">**Output dataset**</span></span>

<span data-ttu-id="a4aa7-381">Een bestand voor uitvoer wordt elke dag in van de dag van het Hallo-map gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="a4aa7-382">Beschikbaarheid van de uitvoer is ingesteld op **dag** (frequentie: dagen en interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a4aa7-383">**Activiteit: hive-activiteit in een pijplijn**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="a4aa7-384">Hallo hive-script ontvangt Hallo juiste *DateTime* informatie als parameters die gebruikmaken van Hallo **WindowStart** variabele, zoals wordt weergegeven in het volgende codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="a4aa7-385">Hallo hive-script gebruikt deze variabele tooload Hallo gegevens uit de juiste map Hallo voor Hallo dag en Voer Hallo aggregatie toogenerate Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="a4aa7-386">Hallo toont volgende diagram Hallo scenario uit het oogpunt van een gegevens-afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Gegevensafhankelijkheid](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="a4aa7-388">Hallo uitvoer segment voor elke dag, is afhankelijk van 24 uur segmenten van een invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="a4aa7-389">Berekent de Data Factory deze afhankelijkheden automatisch door uitzoeken Hallo invoergegevens segmenten die in Hallo vallen dezelfde periode zoals Hallo uitvoer segment toobe geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="a4aa7-390">Als een van de invoersegmenten één keer Hallo 24 niet beschikbaar is, wacht de Data Factory Hallo invoersegment toobe gereed is voordat u begint Hallo dagelijkse activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="a4aa7-391">Voorbeeld 2: Geef afhankelijkheid met expressies en functies van de Data Factory</span><span class="sxs-lookup"><span data-stu-id="a4aa7-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="a4aa7-392">Laten we eens een ander scenario.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-392">Let’s consider another scenario.</span></span> <span data-ttu-id="a4aa7-393">Stel dat u hebt een hive-activiteit die twee invoergegevenssets verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="a4aa7-394">Een van deze nieuwe gegevens dagelijks heeft, maar één van deze nieuwe gegevens worden elke week opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="a4aa7-395">Stel dat u deze wilde toodo een join tussen de twee invoeren Hallo en elke dag wordt een uitvoer geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="a4aa7-396">Hallo eenvoudige benadering waarin cijfers Data Factory automatisch uit de juiste invoerwaarden Hallo segmenten tooprocess door toohello uitvoer gegevens segmenttijd periode niet werkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="a4aa7-397">U moet opgeven dat voor elke activiteit die wordt uitgevoerd, Hallo Data Factory gegevenssegment afgelopen week voor wekelijkse invoergegevensset Hallo gebruiken moet.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="a4aa7-398">U Azure Data Factory-functies, zoals wordt weergegeven in het volgende codefragment tooimplement Hallo dit gedrag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="a4aa7-399">**Input1: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="a4aa7-400">eerste invoer Hello wordt hello Azure blob wordt dagelijks bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a4aa7-401">**Input2: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="a4aa7-402">Input2 is hello Azure blob wekelijks worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="a4aa7-403">**Uitvoer: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-403">**Output: Azure blob**</span></span>

<span data-ttu-id="a4aa7-404">Een bestand voor uitvoer wordt elke dag gemaakt in de map Hallo Hallo dag.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="a4aa7-405">Beschikbaarheid van de uitvoer is ingesteld, te**dag** (frequentie: dag, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a4aa7-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a4aa7-406">**Activiteit: hive-activiteit in een pijplijn**</span><span class="sxs-lookup"><span data-stu-id="a4aa7-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="a4aa7-407">Hallo hive-activiteit duurt Hallo twee invoeritems en een uitvoer-segment wordt geproduceerd elke dag.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="a4aa7-408">U kunt opgeven dat elke dag uitvoer segment toodepend op Hallo invoersegment met de vorige week voor wekelijkse invoer als volgt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="a4aa7-409">Zie [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md) voor een lijst met functies en systeemvariabelen die ondersteuning biedt voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="a4aa7-410">Bijlage</span><span class="sxs-lookup"><span data-stu-id="a4aa7-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="a4aa7-411">Voorbeeld: sequentieel kopiëren</span><span class="sxs-lookup"><span data-stu-id="a4aa7-411">Example: copy sequentially</span></span>
<span data-ttu-id="a4aa7-412">Het is mogelijk toorun meerdere kopieerbewerkingen achter elkaar op een manier opeenvolgende/gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="a4aa7-413">U wellicht bijvoorbeeld twee kopiëren gegevens activiteiten in een pijplijn (CopyActivity1 en CopyActivity2) met Hallo na invoer uitvoergegevenssets:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="a4aa7-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="a4aa7-414">CopyActivity1</span></span>

<span data-ttu-id="a4aa7-415">Invoer: Dataset.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-415">Input: Dataset.</span></span> <span data-ttu-id="a4aa7-416">Uitvoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-416">Output: Dataset2.</span></span>

<span data-ttu-id="a4aa7-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="a4aa7-417">CopyActivity2</span></span>

<span data-ttu-id="a4aa7-418">Invoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-418">Input: Dataset2.</span></span>  <span data-ttu-id="a4aa7-419">Uitvoer: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-419">Output: Dataset3.</span></span>

<span data-ttu-id="a4aa7-420">CopyActivity2 uitgevoerd alleen als Hallo CopyActivity1 met succes is uitgevoerd en Dataset2 beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="a4aa7-421">Hier volgt Hallo voorbeeldpijplijn JSON:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="a4aa7-422">U ziet dat de uitvoergegevensset Hallo Hallo eerste kopieeractiviteit (Dataset2) in Hallo bijvoorbeeld is opgegeven als invoer voor de tweede activiteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="a4aa7-423">Daarom Hallo tweede activiteit wordt alleen uitgevoerd als Hallo uitvoergegevensset van de eerste activiteit Hallo gereed is.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="a4aa7-424">In voorbeeld Hallo kunt CopyActivity2 een andere invoer, zoals Dataset3, maar u Dataset2 opgeven als een invoer tooCopyActivity2 zodat Hallo activiteit kan niet worden uitgevoerd totdat CopyActivity1 is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="a4aa7-425">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-425">For example:</span></span>

<span data-ttu-id="a4aa7-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="a4aa7-426">CopyActivity1</span></span>

<span data-ttu-id="a4aa7-427">Invoer: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-427">Input: Dataset1.</span></span> <span data-ttu-id="a4aa7-428">Uitvoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-428">Output: Dataset2.</span></span>

<span data-ttu-id="a4aa7-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="a4aa7-429">CopyActivity2</span></span>

<span data-ttu-id="a4aa7-430">Invoer: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="a4aa7-431">Uitvoer: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="a4aa7-432">U ziet in Hallo voorbeeld worden twee invoergegevenssets opgegeven voor de tweede kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="a4aa7-433">Wanneer meerdere invoer zijn opgegeven, wordt alleen Hallo eerste invoergegevensset wordt gebruikt voor het kopiëren van gegevens, maar andere gegevenssets worden gebruikt als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="a4aa7-434">CopyActivity2 zou pas beginnen nadat hello volgende voorwaarden wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="a4aa7-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="a4aa7-435">CopyActivity1 is voltooid en Dataset2 is beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="a4aa7-436">Deze gegevensset wordt niet gebruikt bij het kopiëren van gegevens tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="a4aa7-437">Deze alleen fungeert als een afhankelijkheid van de planning voor CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="a4aa7-438">Dataset3 is beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-438">Dataset3 is available.</span></span> <span data-ttu-id="a4aa7-439">Deze gegevensset vertegenwoordigt Hallo-gegevens die gekopieerde toohello doel.</span><span class="sxs-lookup"><span data-stu-id="a4aa7-439">This dataset represents hello data that is copied toohello destination.</span></span> 
