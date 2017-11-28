---
title: Plannen en uitvoeren met Data Factory | Microsoft Docs
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="85497-103">Data Factory plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="85497-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="85497-104">In dit artikel wordt uitleg gegeven over de plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="85497-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="85497-105">In dit artikel wordt ervan uitgegaan dat u van de Data Factory toepassing model concepten basisbeginselen, met inbegrip van activiteiten, pijplijnen, gekoppelde services en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="85497-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="85497-106">Voor de basisconcepten van Azure Data Factory, Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="85497-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="85497-107">Inleiding tot Data Factory</span><span class="sxs-lookup"><span data-stu-id="85497-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="85497-108">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="85497-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="85497-109">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="85497-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="85497-110">Begin- en eindtijden van pijplijn</span><span class="sxs-lookup"><span data-stu-id="85497-110">Start and end times of pipeline</span></span>
<span data-ttu-id="85497-111">Een pijplijn is active alleen tussen de **start** tijd en **end** tijd.</span><span class="sxs-lookup"><span data-stu-id="85497-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="85497-112">Het is niet uitgevoerd vóór de begintijd of na de eindtijd.</span><span class="sxs-lookup"><span data-stu-id="85497-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="85497-113">Als de pijplijn wordt onderbroken, is het niet uitgevoerd ongeacht de begin- en -tijd.</span><span class="sxs-lookup"><span data-stu-id="85497-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="85497-114">Voor een pijplijn om uit te voeren, moet deze niet worden onderbroken.</span><span class="sxs-lookup"><span data-stu-id="85497-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="85497-115">U kunt deze instellingen (start, eindgebruikers, onderbroken) vinden in de definitie van de pijplijn:</span><span class="sxs-lookup"><span data-stu-id="85497-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="85497-116">Zie voor meer informatie deze eigenschappen [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="85497-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="85497-117">Planning voor een activiteit opgeven</span><span class="sxs-lookup"><span data-stu-id="85497-117">Specify schedule for an activity</span></span>
<span data-ttu-id="85497-118">Het is niet de pijplijn die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85497-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="85497-119">De activiteiten in de pijplijn die worden uitgevoerd in de context van de pijplijn is.</span><span class="sxs-lookup"><span data-stu-id="85497-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="85497-120">U kunt een terugkerend schema voor een activiteit opgeven met behulp van de **scheduler** sectie van de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="85497-121">U kunt bijvoorbeeld plannen dat een activiteit per uur als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="85497-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="85497-122">In het volgende diagram ziet opgeven van dat een planning voor een activiteit wordt een reeks van windows met tumbling in de pipeline-begin- en eindtijden.</span><span class="sxs-lookup"><span data-stu-id="85497-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="85497-123">Windows daling zijn een reeks met vaste grootte niet-overlappende, aaneengesloten tijdsintervallen.</span><span class="sxs-lookup"><span data-stu-id="85497-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="85497-124">Deze logische daling vensters voor een activiteit worden genoemd **activiteitsvensters**.</span><span class="sxs-lookup"><span data-stu-id="85497-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Voorbeeld van de activiteit scheduler](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="85497-126">De **scheduler** eigenschap voor een activiteit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="85497-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="85497-127">Als u deze eigenschap opgeeft, moet overeenkomen met de frequentie die u in de definitie van de uitvoergegevensset voor de activiteit opgeeft.</span><span class="sxs-lookup"><span data-stu-id="85497-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="85497-128">Momenteel is de uitvoergegevensset dat wat de planning aanstuurt.</span><span class="sxs-lookup"><span data-stu-id="85497-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="85497-129">Daarom moet u een uitvoergegevensset maken, zelfs als de activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="85497-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="85497-130">Geef de planning voor een gegevensset</span><span class="sxs-lookup"><span data-stu-id="85497-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="85497-131">Een activiteit in een Data Factory-pijplijn kan duren voordat de invoer van nul of meer **gegevenssets** en een of meer uitvoergegevenssets te produceren.</span><span class="sxs-lookup"><span data-stu-id="85497-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="85497-132">Voor een activiteit, kunt u de frequentie waarmee de invoergegevens beschikbaar is of de uitvoergegevens wordt gemaakt met behulp van de **beschikbaarheid** sectie in de definities van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="85497-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="85497-133">**Frequentie** in de **beschikbaarheid** sectie geeft de tijdseenheid.</span><span class="sxs-lookup"><span data-stu-id="85497-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="85497-134">De toegestane waarden voor de frequentie zijn: minuut, uur, dag, Week en maand.</span><span class="sxs-lookup"><span data-stu-id="85497-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="85497-135">De **interval** geeft een vermenigvuldiger voor de frequentie van eigenschap in de beschikbaarheidssectie.</span><span class="sxs-lookup"><span data-stu-id="85497-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="85497-136">Bijvoorbeeld: als de frequentie is ingesteld op dagen en interval is ingesteld op 1 voor een uitvoergegevensset, de uitvoergegevens dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="85497-137">Als u de frequentie als minuut opgeeft, wordt u aangeraden dat u het interval op niet kleiner zijn dan 15 instellen.</span><span class="sxs-lookup"><span data-stu-id="85497-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="85497-138">In het volgende voorbeeld wordt de invoergegevens beschikbaar per uur en de uitvoergegevens per uur wordt geproduceerd (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="85497-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="85497-139">**Invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="85497-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="85497-140">**Uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="85497-140">**Output dataset**</span></span>

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

<span data-ttu-id="85497-141">Op dit moment **uitvoergegevensset stations de planning**.</span><span class="sxs-lookup"><span data-stu-id="85497-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="85497-142">Met andere woorden, wordt de planning die is opgegeven voor de uitvoergegevensset die gebruikt voor het uitvoeren van een activiteit tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="85497-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="85497-143">Daarom moet u een uitvoergegevensset maken, zelfs als de activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="85497-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="85497-144">Als er voor de activiteit geen invoer nodig is, kunt u het maken van de invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="85497-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="85497-145">In de volgende definitie van de pipeline, de **scheduler** eigenschap wordt gebruikt om de planning voor de activiteit te specificeren.</span><span class="sxs-lookup"><span data-stu-id="85497-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="85497-146">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="85497-146">This property is optional.</span></span> <span data-ttu-id="85497-147">Op dit moment wordt de planning voor de uitvoergegevensset opgegeven moet overeenkomen met het schema voor de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="85497-148">In dit voorbeeld wordt de activiteit uitgevoerd per uur tussen de begin- en eindtijden van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="85497-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="85497-149">De uitvoergegevens wordt per uur gemaakt voor drie uur windows (8 AM - 9 uur, 9: 00 uur - 10: 00 uur, en 10: 00 - 11 uur).</span><span class="sxs-lookup"><span data-stu-id="85497-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="85497-150">Elke eenheid van gegevens gebruikt of die wordt geproduceerd door een activiteit die wordt uitgevoerd, heet een **gegevenssegment**.</span><span class="sxs-lookup"><span data-stu-id="85497-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="85497-151">Het volgende diagram toont een voorbeeld van een activiteit met één invoergegevensset en één uitvoergegevensset:</span><span class="sxs-lookup"><span data-stu-id="85497-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Beschikbaarheid scheduler](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="85497-153">Het diagram toont de gegevenssegmenten per uur voor de gegevensset invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="85497-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="85497-154">Het diagram toont de drie invoer segmenten die gereed voor verwerking zijn.</span><span class="sxs-lookup"><span data-stu-id="85497-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="85497-155">De activiteit 10 11 uur wordt uitgevoerd, het opstellen van het segment van de uitvoer 10 11 uur.</span><span class="sxs-lookup"><span data-stu-id="85497-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="85497-156">U hebt toegang tot de tijdsinterval die is gekoppeld aan het huidige segment in de JSON van de gegevensset met behulp van variabelen: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) en [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="85497-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="85497-157">Op deze manier kunt u de tijdsinterval die is gekoppeld aan het venster van een activiteit met de WindowStart en WindowEnd openen.</span><span class="sxs-lookup"><span data-stu-id="85497-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="85497-158">De planning van een activiteit moet overeenkomen met de planning van de uitvoergegevensset voor de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="85497-159">Daarom de SliceStart en SliceEnd waarden zijn hetzelfde als de waarden voor WindowStart en WindowEnd respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="85497-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="85497-160">Zie voor meer informatie over deze variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md#data-factory-system-variables) artikelen.</span><span class="sxs-lookup"><span data-stu-id="85497-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="85497-161">U kunt deze variabelen voor verschillende doeleinden gebruiken in de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="85497-162">Bijvoorbeeld, kunt u gegevens selecteren uit de invoer- en uitvoergegevenssets representatie van time series-gegevens (bijvoorbeeld: 8 uur op 9: 00 uur).</span><span class="sxs-lookup"><span data-stu-id="85497-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="85497-163">Dit voorbeeld wordt tevens **WindowStart** en **WindowEnd** selecteren relevante gegevens voor een activiteit uitvoeren en kopieer het naar een blob met de juiste **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="85497-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="85497-164">De **folderPath** parameters om een afzonderlijke map voor elk uur wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="85497-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="85497-165">In het voorgaande voorbeeld de planning die is opgegeven voor de invoer en uitvoergegevenssets is de dezelfde (elk uur).</span><span class="sxs-lookup"><span data-stu-id="85497-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="85497-166">Als invoergegevensset voor de activiteit beschikbaar op een andere frequentie spreek om de 15 minuten is, de activiteit die deze uitvoergegevensset produceert nog eens per uur uitgevoerd zoals de uitvoergegevensset is wat de activiteitenplanning stations.</span><span class="sxs-lookup"><span data-stu-id="85497-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="85497-167">Zie voor meer informatie [Model gegevenssets frequentie](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="85497-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="85497-168">Beschikbaarheid van de gegevensset en het beleid</span><span class="sxs-lookup"><span data-stu-id="85497-168">Dataset availability and policies</span></span>
<span data-ttu-id="85497-169">U kunt het gebruik van de frequentie en het interval eigenschappen in de beschikbaarheidssectie van de definitie van gegevensset hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="85497-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="85497-170">Er zijn enkele andere eigenschappen die betrekking hebben op de planning en uitvoering van een activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="85497-171">Beschikbaarheid van gegevensset</span><span class="sxs-lookup"><span data-stu-id="85497-171">Dataset availability</span></span> 
<span data-ttu-id="85497-172">De volgende tabel beschrijft de eigenschappen kunt u in de **beschikbaarheid** sectie:</span><span class="sxs-lookup"><span data-stu-id="85497-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="85497-173">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="85497-173">Property</span></span> | <span data-ttu-id="85497-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85497-174">Description</span></span> | <span data-ttu-id="85497-175">Vereist</span><span class="sxs-lookup"><span data-stu-id="85497-175">Required</span></span> | <span data-ttu-id="85497-176">Standaard</span><span class="sxs-lookup"><span data-stu-id="85497-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85497-177">Frequentie</span><span class="sxs-lookup"><span data-stu-id="85497-177">frequency</span></span> |<span data-ttu-id="85497-178">Hiermee geeft u tijdseenheid voor de gegevensset segment productie.</span><span class="sxs-lookup"><span data-stu-id="85497-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="85497-179"><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand</span><span class="sxs-lookup"><span data-stu-id="85497-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="85497-180">Ja</span><span class="sxs-lookup"><span data-stu-id="85497-180">Yes</span></span> |<span data-ttu-id="85497-181">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="85497-181">NA</span></span> |
| <span data-ttu-id="85497-182">Interval</span><span class="sxs-lookup"><span data-stu-id="85497-182">interval</span></span> |<span data-ttu-id="85497-183">Hiermee geeft u een vermenigvuldiger voor de frequentie</span><span class="sxs-lookup"><span data-stu-id="85497-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="85497-184">"Frequentie x-interval" bepaalt hoe vaak het segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="85497-185">Als u de gegevensset worden gesegmenteerd op uurbasis moet, stelt u <b>frequentie</b> naar <b>uur</b>, en <b>interval</b> naar <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="85497-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="85497-186"><b>Opmerking</b>: als u frequentie als minuut opgeeft, raden wij aan dat u het interval aan niet lager zijn dan 15</span><span class="sxs-lookup"><span data-stu-id="85497-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="85497-187">Ja</span><span class="sxs-lookup"><span data-stu-id="85497-187">Yes</span></span> |<span data-ttu-id="85497-188">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="85497-188">NA</span></span> |
| <span data-ttu-id="85497-189">stijl</span><span class="sxs-lookup"><span data-stu-id="85497-189">style</span></span> |<span data-ttu-id="85497-190">Hiermee geeft u op of het segment aan het begin/einde van het interval moet worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="85497-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="85497-191">StartOfInterval</span></span></li><li><span data-ttu-id="85497-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="85497-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="85497-193">Als de frequentie is ingesteld op maand en stijl is ingesteld op EndOfInterval, wordt het segment op de laatste dag van de maand geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="85497-194">Als de stijl is ingesteld op StartOfInterval, wordt het segment op de eerste dag van de maand geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="85497-195">Als de frequentie is ingesteld op de dag en stijl is ingesteld op EndOfInterval, wordt het segment wordt geproduceerd in het afgelopen uur van de dag.</span><span class="sxs-lookup"><span data-stu-id="85497-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="85497-196">Als de frequentie is ingesteld op uur en stijl is ingesteld op EndOfInterval, wordt het segment wordt geproduceerd aan het einde van het uur.</span><span class="sxs-lookup"><span data-stu-id="85497-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="85497-197">Voor een segment 1-2 uur gedurende het segment geproduceerd om 2 uur.</span><span class="sxs-lookup"><span data-stu-id="85497-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="85497-198">Nee</span><span class="sxs-lookup"><span data-stu-id="85497-198">No</span></span> |<span data-ttu-id="85497-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="85497-199">EndOfInterval</span></span> |
| <span data-ttu-id="85497-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="85497-200">anchorDateTime</span></span> |<span data-ttu-id="85497-201">Hiermee definieert u de absolute positie in de tijd die wordt gebruikt door de planner gegevensset segmentgrenzen berekenen.</span><span class="sxs-lookup"><span data-stu-id="85497-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="85497-202"><b>Opmerking</b>: als de AnchorDateTime bevat de datumonderdelen die meer gedetailleerd dan de frequentie zijn, wordt de gedetailleerdere onderdelen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="85497-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="85497-203">Bijvoorbeeld, als de <b>interval</b> is <b>per uur</b> (frequentie: uur en interval: 1) en de <b>AnchorDateTime</b> bevat <b>minuten en seconden</b>, wordt de <b>minuten en seconden</b> delen van de AnchorDateTime worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="85497-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="85497-204">Nee</span><span class="sxs-lookup"><span data-stu-id="85497-204">No</span></span> |<span data-ttu-id="85497-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="85497-205">01/01/0001</span></span> |
| <span data-ttu-id="85497-206">offset</span><span class="sxs-lookup"><span data-stu-id="85497-206">offset</span></span> |<span data-ttu-id="85497-207">TimeSpan waarmee het begin en einde van alle segmenten van de gegevensset zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="85497-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="85497-208"><b>Opmerking</b>: als zowel anchorDateTime als offset worden opgegeven, het resultaat is een gecombineerde verschuiving.</span><span class="sxs-lookup"><span data-stu-id="85497-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="85497-209">Nee</span><span class="sxs-lookup"><span data-stu-id="85497-209">No</span></span> |<span data-ttu-id="85497-210">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="85497-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="85497-211">offset voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85497-211">offset example</span></span>
<span data-ttu-id="85497-212">Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. UTC-tijd (middernacht).</span><span class="sxs-lookup"><span data-stu-id="85497-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="85497-213">Als u de begintijd moet 6 uur UTC-tijd in plaats daarvan wilt, stelt u de verschuiving zoals weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="85497-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="85497-214">Voorbeeld van anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="85497-214">anchorDateTime example</span></span>
<span data-ttu-id="85497-215">In het volgende voorbeeld wordt de elke 23 uur in de gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="85497-216">Het eerste segment wordt gestart op het moment dat is opgegeven door de anchorDateTime die is ingesteld op `2017-04-19T08:00:00` (UTC-tijd).</span><span class="sxs-lookup"><span data-stu-id="85497-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="85497-217">offset/stijl voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85497-217">offset/style Example</span></span>
<span data-ttu-id="85497-218">De volgende gegevensset is een maandelijkse gegevensset en op 3rd van elke maand om 8:00 uur wordt geproduceerd (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="85497-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="85497-219">DataSet beleid</span><span class="sxs-lookup"><span data-stu-id="85497-219">Dataset policy</span></span>
<span data-ttu-id="85497-220">Een dataset kan een validatiebeleid gedefinieerd waarmee wordt aangegeven hoe de gegevens die worden gegenereerd door de uitvoering van een segment kan worden gevalideerd voordat deze gereed voor verbruik is hebben.</span><span class="sxs-lookup"><span data-stu-id="85497-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="85497-221">In dergelijke gevallen dat nadat het segment is uitgevoerd, de status van de uitvoer-segment wordt gewijzigd naar **wachten** met een substatus van **validatie**.</span><span class="sxs-lookup"><span data-stu-id="85497-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="85497-222">Nadat de segmenten zijn geverifieerd, de segment-status gewijzigd in **gereed**.</span><span class="sxs-lookup"><span data-stu-id="85497-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="85497-223">Als een gegevenssegment is geproduceerd, maar zijn niet worden gevalideerd, worden de activiteiten bij uitvoering downstream segmenten die afhankelijk van dit segment zijn niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="85497-224">[Bewaken en beheren van pijplijnen](data-factory-monitor-manage-pipelines.md) bevat informatie over de verschillende toestanden van gegevenssegmenten in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="85497-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="85497-225">De **beleid** sectie in de definitie van gegevensset definieert u de criteria of de conditie van de segmenten van de gegevensset moeten voldoen.</span><span class="sxs-lookup"><span data-stu-id="85497-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="85497-226">De volgende tabel beschrijft de eigenschappen kunt u in de **beleid** sectie:</span><span class="sxs-lookup"><span data-stu-id="85497-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="85497-227">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="85497-227">Policy Name</span></span> | <span data-ttu-id="85497-228">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85497-228">Description</span></span> | <span data-ttu-id="85497-229">Toegepast op</span><span class="sxs-lookup"><span data-stu-id="85497-229">Applied To</span></span> | <span data-ttu-id="85497-230">Vereist</span><span class="sxs-lookup"><span data-stu-id="85497-230">Required</span></span> | <span data-ttu-id="85497-231">Standaard</span><span class="sxs-lookup"><span data-stu-id="85497-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="85497-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="85497-232">minimumSizeMB</span></span> | <span data-ttu-id="85497-233">Valideert dat de gegevens in een **Azure blob** voldoet aan de minimale grootte (in MB).</span><span class="sxs-lookup"><span data-stu-id="85497-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="85497-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="85497-234">Azure Blob</span></span> |<span data-ttu-id="85497-235">Nee</span><span class="sxs-lookup"><span data-stu-id="85497-235">No</span></span> |<span data-ttu-id="85497-236">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="85497-236">NA</span></span> |
| <span data-ttu-id="85497-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="85497-237">minimumRows</span></span> | <span data-ttu-id="85497-238">Valideert dat de gegevens in een **Azure SQL-database** of een **Azure-tabel** het minimum aantal rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="85497-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="85497-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="85497-239">Azure SQL Database</span></span></li><li><span data-ttu-id="85497-240">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="85497-240">Azure Table</span></span></li></ul> |<span data-ttu-id="85497-241">Nee</span><span class="sxs-lookup"><span data-stu-id="85497-241">No</span></span> |<span data-ttu-id="85497-242">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="85497-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="85497-243">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="85497-243">Examples</span></span>
<span data-ttu-id="85497-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="85497-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="85497-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="85497-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="85497-246">Zie voor meer informatie over deze eigenschappen en voorbeelden [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="85497-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="85497-247">Beleidsregels voor activiteiten</span><span class="sxs-lookup"><span data-stu-id="85497-247">Activity policies</span></span>
<span data-ttu-id="85497-248">Beleid geldt voor de run-time-gedrag van een activiteit specifiek wanneer het segment van een tabel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="85497-249">De volgende tabel bevat de details.</span><span class="sxs-lookup"><span data-stu-id="85497-249">The following table provides the details.</span></span>

| <span data-ttu-id="85497-250">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="85497-250">Property</span></span> | <span data-ttu-id="85497-251">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="85497-251">Permitted values</span></span> | <span data-ttu-id="85497-252">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="85497-252">Default Value</span></span> | <span data-ttu-id="85497-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85497-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85497-254">Gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="85497-254">concurrency</span></span> |<span data-ttu-id="85497-255">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="85497-255">Integer</span></span> <br/><br/><span data-ttu-id="85497-256">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="85497-256">Max value: 10</span></span> |<span data-ttu-id="85497-257">1</span><span class="sxs-lookup"><span data-stu-id="85497-257">1</span></span> |<span data-ttu-id="85497-258">Het aantal gelijktijdige uitvoeringen van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="85497-259">Bepaalt het aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten.</span><span class="sxs-lookup"><span data-stu-id="85497-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="85497-260">Bijvoorbeeld, als een activiteit moet doorlopen sneller een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid het verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="85497-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="85497-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="85497-261">executionPriorityOrder</span></span> |<span data-ttu-id="85497-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="85497-262">NewestFirst</span></span><br/><br/><span data-ttu-id="85497-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="85497-263">OldestFirst</span></span> |<span data-ttu-id="85497-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="85497-264">OldestFirst</span></span> |<span data-ttu-id="85497-265">Bepaalt de volgorde van de gegevenssegmenten dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="85497-266">Als er 2 segmenten (één gebeurt om 4 uur en 17: 00 uur een andere één voor één) en beide zijn in behandeling kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85497-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="85497-267">Als u de executionPriorityOrder NewestFirst worden ingesteld, wordt het segment om 17.00 eerst verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="85497-268">Op dezelfde manier als u de executionPriorityORder OldestFIrst worden ingesteld, klikt u vervolgens het segment om 4 uur is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="85497-269">Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="85497-269">retry</span></span> |<span data-ttu-id="85497-270">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="85497-270">Integer</span></span><br/><br/><span data-ttu-id="85497-271">De maximale waarde is 10</span><span class="sxs-lookup"><span data-stu-id="85497-271">Max value can be 10</span></span> |<span data-ttu-id="85497-272">0</span><span class="sxs-lookup"><span data-stu-id="85497-272">0</span></span> |<span data-ttu-id="85497-273">Aantal nieuwe pogingen voordat de verwerking van de gegevens voor het segment is gemarkeerd als mislukt.</span><span class="sxs-lookup"><span data-stu-id="85497-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="85497-274">Uitvoering van de activiteit voor een gegevenssegment wordt herhaald tot maximaal het aantal pogingen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="85497-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="85497-275">De nieuwe poging wordt gedaan zo snel mogelijk na de fout.</span><span class="sxs-lookup"><span data-stu-id="85497-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="85497-276">Time-out</span><span class="sxs-lookup"><span data-stu-id="85497-276">timeout</span></span> |<span data-ttu-id="85497-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="85497-277">TimeSpan</span></span> |<span data-ttu-id="85497-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="85497-278">00:00:00</span></span> |<span data-ttu-id="85497-279">Time-out voor de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-279">Timeout for the activity.</span></span> <span data-ttu-id="85497-280">Voorbeeld: 00:10:00 (impliceert time-out 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="85497-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="85497-281">Als een waarde niet opgegeven is of 0 is, is de time-out van oneindig.</span><span class="sxs-lookup"><span data-stu-id="85497-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="85497-282">Als de verwerkingstijd van de gegevens op een segment de time-outwaarde overschrijdt, deze wordt geannuleerd en wordt geprobeerd om opnieuw te proberen de verwerking.</span><span class="sxs-lookup"><span data-stu-id="85497-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="85497-283">Het aantal nieuwe pogingen, is afhankelijk van de eigenschap probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="85497-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="85497-284">Wanneer een time-out optreedt, wordt de status ingesteld op een time-out opgetreden bij.</span><span class="sxs-lookup"><span data-stu-id="85497-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="85497-285">Vertraging</span><span class="sxs-lookup"><span data-stu-id="85497-285">delay</span></span> |<span data-ttu-id="85497-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="85497-286">TimeSpan</span></span> |<span data-ttu-id="85497-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="85497-287">00:00:00</span></span> |<span data-ttu-id="85497-288">Geef de vertraging optreden voordat de verwerking van het segment wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="85497-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="85497-289">De uitvoering van de activiteit voor een gegevenssegment wordt gestart nadat de vertraging voorbij de verwachte tijd voor uitvoering is.</span><span class="sxs-lookup"><span data-stu-id="85497-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="85497-290">Voorbeeld: 00:10:00 (betekent vertraging van 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="85497-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="85497-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="85497-291">longRetry</span></span> |<span data-ttu-id="85497-292">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="85497-292">Integer</span></span><br/><br/><span data-ttu-id="85497-293">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="85497-293">Max value: 10</span></span> |<span data-ttu-id="85497-294">1</span><span class="sxs-lookup"><span data-stu-id="85497-294">1</span></span> |<span data-ttu-id="85497-295">Het aantal pogingen lang voordat de uitvoering van het segment is mislukt.</span><span class="sxs-lookup"><span data-stu-id="85497-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="85497-296">longRetry pogingen door longRetryInterval gelijkmatig verdeeld.</span><span class="sxs-lookup"><span data-stu-id="85497-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="85497-297">Als u een tijd tussen pogingen opgeven moet, gebruikt u dus longRetry.</span><span class="sxs-lookup"><span data-stu-id="85497-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="85497-298">Als zowel de nieuwe pogingen en de longRetry worden opgegeven, elke poging longRetry bevat nieuwe pogingen en het maximale aantal pogingen is opnieuw * longRetry.</span><span class="sxs-lookup"><span data-stu-id="85497-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="85497-299">Bijvoorbeeld, als we hebben de volgende instellingen in het activiteitenbeleid voor:</span><span class="sxs-lookup"><span data-stu-id="85497-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="85497-300">Probeer: 3</span><span class="sxs-lookup"><span data-stu-id="85497-300">Retry: 3</span></span><br/><span data-ttu-id="85497-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="85497-301">longRetry: 2</span></span><br/><span data-ttu-id="85497-302">longRetryInterval: 01:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="85497-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="85497-303">Wordt ervan uitgegaan dat er is slechts één segment uit te voeren (status Waiting) en de activiteit is uitgevoerd elke keer mislukt.</span><span class="sxs-lookup"><span data-stu-id="85497-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="85497-304">Er zou worden in eerste instantie 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="85497-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="85497-305">De status van het segment is na elke poging probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="85497-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="85497-306">Nadat de eerste 3 pogingen hebben bekeken, zou de status van het segment LongRetry zijn.</span><span class="sxs-lookup"><span data-stu-id="85497-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="85497-307">Na een uur (dat wil zeggen, de longRetryInteval waarde), zou er een andere set 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="85497-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="85497-308">Hierna is de status van het segment zou niet en geen pogingen meer zou worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85497-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="85497-309">Daarom is algemene 6 geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="85497-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="85497-310">Als een uitvoering is voltooid, het segment de status gereed zijn en er worden geen pogingen meer geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="85497-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="85497-311">longRetry kan worden gebruikt in situaties waarbij afhankelijke gegevens aankomen op niet-deterministische tijdstippen of de hele omgeving flaky onder welke gegevensverwerking plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="85497-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="85497-312">In dergelijke gevallen tijd nieuwe pogingen achter elkaar niet kunt doen, en dit na een interval van resultaten in de gewenste uitvoer.</span><span class="sxs-lookup"><span data-stu-id="85497-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="85497-313">Waarschuwing: geen hoge waarden voor de longRetry of longRetryInterval instelt.</span><span class="sxs-lookup"><span data-stu-id="85497-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="85497-314">Hogere waarden dat normaal gesproken andere al problemen.</span><span class="sxs-lookup"><span data-stu-id="85497-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="85497-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="85497-315">longRetryInterval</span></span> |<span data-ttu-id="85497-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="85497-316">TimeSpan</span></span> |<span data-ttu-id="85497-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="85497-317">00:00:00</span></span> |<span data-ttu-id="85497-318">De vertraging tussen pogingen lang</span><span class="sxs-lookup"><span data-stu-id="85497-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="85497-319">Zie voor meer informatie [pijplijnen](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="85497-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="85497-320">Parallelle verwerking van gegevenssegmenten</span><span class="sxs-lookup"><span data-stu-id="85497-320">Parallel processing of data slices</span></span>
<span data-ttu-id="85497-321">U kunt de begindatum van de pijplijn in het verleden instellen.</span><span class="sxs-lookup"><span data-stu-id="85497-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="85497-322">Wanneer u doet dit, wordt Data Factory automatisch berekend (back-opvulling) alle gegevenssegmenten in het verleden en ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="85497-323">Bijvoorbeeld: als u een pijplijn met een begindatum 2017-04-01 maken en de huidige datum 2017-04-10 valt.</span><span class="sxs-lookup"><span data-stu-id="85497-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="85497-324">Als de frequentie van de uitvoergegevensset die dagelijks wordt verwerkt alle segmenten van 2017-04-01 op 2017-04-09 Data Factory-begint onmiddellijk omdat de begindatum in het verleden ligt.</span><span class="sxs-lookup"><span data-stu-id="85497-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="85497-325">Het segment uit 2017-04-10 is niet verwerkt nog omdat de waarde van de eigenschap style in de beschikbaarheidssectie EndOfInterval standaard.</span><span class="sxs-lookup"><span data-stu-id="85497-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="85497-326">Het oudste segment is verwerkt eerst als de standaard waarde van executionPriorityOrder OldestFirst is.</span><span class="sxs-lookup"><span data-stu-id="85497-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="85497-327">Zie voor een beschrijving van de eigenschap style [gegevensset beschikbaarheid](#dataset-availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="85497-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="85497-328">Zie voor een beschrijving van de sectie executionPriorityOrder de [beleidsregels voor activiteiten](#activity-policies) sectie.</span><span class="sxs-lookup"><span data-stu-id="85497-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="85497-329">Kunt u back-gevuld gegevenssegmenten parallel worden verwerkt door in te stellen de **gelijktijdigheid** eigenschap in de **beleid** sectie van de JSON van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="85497-330">Deze eigenschap bepaalt het aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten.</span><span class="sxs-lookup"><span data-stu-id="85497-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="85497-331">De standaardwaarde voor de eigenschap gelijktijdigheid van taken is 1.</span><span class="sxs-lookup"><span data-stu-id="85497-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="85497-332">Daarom is een segment verwerkt op een tijdstip standaard.</span><span class="sxs-lookup"><span data-stu-id="85497-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="85497-333">De maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="85497-333">The maximum value is 10.</span></span> <span data-ttu-id="85497-334">Wanneer een pijplijn moet doorlopen een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid van taken de verwerking van gegevens sneller.</span><span class="sxs-lookup"><span data-stu-id="85497-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="85497-335">Voer een mislukte gegevenssegment</span><span class="sxs-lookup"><span data-stu-id="85497-335">Rerun a failed data slice</span></span>
<span data-ttu-id="85497-336">Wanneer een fout optreedt tijdens het verwerken van een gegevenssegment, vindt u waarom de verwerking van een segment met behulp van Azure portal-blades of Monitor and Manage App is mislukt.</span><span class="sxs-lookup"><span data-stu-id="85497-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="85497-337">Zie [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="85497-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="85497-338">Bekijk het volgende voorbeeld, waarin twee activiteiten.</span><span class="sxs-lookup"><span data-stu-id="85497-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="85497-339">Activiteit1 en activiteit 2.</span><span class="sxs-lookup"><span data-stu-id="85497-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="85497-340">Activiteit1 een segment van Dataset1 verbruikt en een segment van Dataset2 die wordt gebruikt als invoer door activiteit2 voor het produceren van een segment van de laatste gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="85497-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Mislukte segment](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="85497-342">Het diagram toont die uit drie recente segmenten, er is een fout opgetreden bij het opstellen van het segment 9 10 uur voor Dataset2.</span><span class="sxs-lookup"><span data-stu-id="85497-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="85497-343">Data Factory-afhankelijkheid voor de gegevensset van de reeks tijd automatisch worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="85497-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="85497-344">Hierdoor wordt de activiteit die wordt uitgevoerd voor de downstream segment 9-10: 00 uur niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="85497-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="85497-345">Data Factory bewaking en beheer-hulpprogramma's kunnen u inzoomen op de diagnostische logboeken voor het segment de mislukte eenvoudig de hoofdoorzaak voor het probleem te vinden en op te lossen.</span><span class="sxs-lookup"><span data-stu-id="85497-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="85497-346">Nadat u het probleem hebt opgelost, kunt u eenvoudig de activiteit die wordt uitgevoerd om te produceren van het mislukte segment te starten.</span><span class="sxs-lookup"><span data-stu-id="85497-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="85497-347">Zie voor meer informatie over het opnieuw uitvoeren en begrijpen van statusovergangen voor gegevenssegmenten [controleren en beheren met Azure portal-blades pijplijnen](data-factory-monitor-manage-pipelines.md) of [app voor bewaking en beheer](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="85497-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="85497-348">Nadat u het segment 9 10 uur voor opnieuw uitvoeren **Dataset2**, Data Factory begint de uitvoeren voor de afhankelijke segment 9 10 uur op de laatste gegevensset.</span><span class="sxs-lookup"><span data-stu-id="85497-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Mislukte segment opnieuw uitvoeren](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="85497-350">Meerdere activiteiten in een pijplijn</span><span class="sxs-lookup"><span data-stu-id="85497-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="85497-351">U kunt meer dan één activiteit in een pijplijn hebben.</span><span class="sxs-lookup"><span data-stu-id="85497-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="85497-352">Als er meerdere activiteiten in een pijplijn en de uitvoer van een activiteit geen invoer van een andere activiteit is, de activiteiten kunnen parallel worden uitgevoerd als invoergegevens segmenten voor de activiteiten klaar bent.</span><span class="sxs-lookup"><span data-stu-id="85497-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="85497-353">U kunt twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="85497-354">De activiteiten kunnen worden in de dezelfde pijplijn of in verschillende pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="85497-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="85497-355">De tweede activiteit wordt uitgevoerd alleen wanneer de eerste die met succes wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="85497-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="85497-356">Neem bijvoorbeeld het volgende geval waarbij een pijplijn twee activiteiten heeft:</span><span class="sxs-lookup"><span data-stu-id="85497-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="85497-357">A1 activiteit waarvoor externe invoergegevensset D1 en D2 uitvoergegevensset die wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="85497-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="85497-358">Activiteit A2 die invoer uit gegevensset D2 is vereist en produceert uitvoergegevensset D3.</span><span class="sxs-lookup"><span data-stu-id="85497-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="85497-359">In dit scenario zijn activiteiten A1 en A2 in de dezelfde pijplijn.</span><span class="sxs-lookup"><span data-stu-id="85497-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="85497-360">De activiteit A1 wordt uitgevoerd als de externe gegevens beschikbaar is en de frequentie van geplande beschikbaarheid is bereikt.</span><span class="sxs-lookup"><span data-stu-id="85497-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="85497-361">De activiteit A2 wordt uitgevoerd als de geplande segmenten van D2 beschikbaar en de frequentie van geplande beschikbaarheid is bereikt.</span><span class="sxs-lookup"><span data-stu-id="85497-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="85497-362">Als er een fout in een van de segmenten in de gegevensset D2, A2 kan niet worden uitgevoerd voor die segment totdat deze beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="85497-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="85497-363">De diagramweergave met beide activiteiten in de pijplijn voor dezelfde eruit als in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="85497-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Activiteiten in de dezelfde pijplijn-koppeling](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="85497-365">Zoals eerder vermeld, kunnen de activiteiten worden in verschillende pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="85497-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="85497-366">In een dergelijk scenario eruit de diagramweergave als in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="85497-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Koppeling van activiteiten in twee pijplijnen](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="85497-368">Zie de [sequentieel kopiëren](#copy-sequentially) sectie in de bijlage voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="85497-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="85497-369">Model gegevenssets frequentie</span><span class="sxs-lookup"><span data-stu-id="85497-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="85497-370">In de voorbeelden zijn de frequenties voor invoer- en uitvoergegevenssets en het venster van de planning activiteit hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="85497-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="85497-371">Sommige scenario's moet de mogelijkheid om uitvoer met een frequentie afwijken van de frequenties van een of meer invoerwaarden te produceren.</span><span class="sxs-lookup"><span data-stu-id="85497-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="85497-372">Data Factory biedt ondersteuning voor het modelleren van deze scenario's.</span><span class="sxs-lookup"><span data-stu-id="85497-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="85497-373">Voorbeeld 1: Een dagelijkse uitvoer-rapport voor invoergegevens die beschikbaar is om het uur produceren</span><span class="sxs-lookup"><span data-stu-id="85497-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="85497-374">Neem bijvoorbeeld een scenario waarin u hebt ingevoerd meetgegevens van sensoren beschikbaar om het uur in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="85497-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="85497-375">U wilt dat voor het produceren van een dagelijks cumulatieve rapport met statistieken zoals gemiddelde, maximum en minimum voor de dag met [Data Factory hive-activiteit](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="85497-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="85497-376">Hier ziet u hoe u dit scenario met Data Factory kunt model:</span><span class="sxs-lookup"><span data-stu-id="85497-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="85497-377">**Invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="85497-377">**Input dataset**</span></span>

<span data-ttu-id="85497-378">De Uurlijkse invoerbestanden zijn verwijderd in de map voor de opgegeven dag.</span><span class="sxs-lookup"><span data-stu-id="85497-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="85497-379">Beschikbaarheid voor invoer is ingesteld op **uur** (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="85497-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="85497-380">**Uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="85497-380">**Output dataset**</span></span>

<span data-ttu-id="85497-381">Een bestand voor uitvoer wordt elke dag worden gemaakt in de map van de dag.</span><span class="sxs-lookup"><span data-stu-id="85497-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="85497-382">Beschikbaarheid van de uitvoer is ingesteld op **dag** (frequentie: dagen en interval: 1).</span><span class="sxs-lookup"><span data-stu-id="85497-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="85497-383">**Activiteit: hive-activiteit in een pijplijn**</span><span class="sxs-lookup"><span data-stu-id="85497-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="85497-384">Het hive-script ontvangt de juiste *DateTime* informatie als parameters die gebruikmaken van de **WindowStart** variabele, zoals wordt weergegeven in het volgende fragment.</span><span class="sxs-lookup"><span data-stu-id="85497-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="85497-385">Het hive-script gebruikt deze variabele om de gegevens uit de juiste map laden voor de dag en het uitvoeren van de aggregatie voor het genereren van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="85497-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="85497-386">Het volgende diagram toont het scenario uit het oogpunt van een gegevens-afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="85497-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Gegevensafhankelijkheid](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="85497-388">Het segment uitvoer voor elke dag, is afhankelijk van 24 uur segmenten van een invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="85497-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="85497-389">Data Factory berekent automatisch deze afhankelijkheden als u weet de invoergegevens segmenten die in dezelfde periode als het segment uitvoer vallen te produceren.</span><span class="sxs-lookup"><span data-stu-id="85497-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="85497-390">Als een van de 24 invoersegmenten één keer niet beschikbaar is, wacht Data Factory het invoersegment worden gereed is voordat u begint de dagelijkse activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85497-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="85497-391">Voorbeeld 2: Geef afhankelijkheid met expressies en functies van de Data Factory</span><span class="sxs-lookup"><span data-stu-id="85497-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="85497-392">Laten we eens een ander scenario.</span><span class="sxs-lookup"><span data-stu-id="85497-392">Let’s consider another scenario.</span></span> <span data-ttu-id="85497-393">Stel dat u hebt een hive-activiteit die twee invoergegevenssets verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="85497-394">Een van deze nieuwe gegevens dagelijks heeft, maar één van deze nieuwe gegevens worden elke week opgehaald.</span><span class="sxs-lookup"><span data-stu-id="85497-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="85497-395">Stel dat u wilt doen van een join tussen de twee invoeren en uitvoer produceert elke dag.</span><span class="sxs-lookup"><span data-stu-id="85497-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="85497-396">De eenvoudige benadering in welke Data Factory automatisch cijfers uit het recht invoer segmenten worden verwerkt door aan te passen aan de uitvoer van het gegevenssegment tijd periode niet werkt.</span><span class="sxs-lookup"><span data-stu-id="85497-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="85497-397">U moet opgeven dat voor elke activiteit die wordt uitgevoerd, de Data Factory gegevenssegment afgelopen week voor wekelijkse invoergegevensset gebruiken moeten.</span><span class="sxs-lookup"><span data-stu-id="85497-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="85497-398">U Azure Data Factory functies gebruiken zoals wordt weergegeven in het volgende codefragment voor het implementeren van dit probleem.</span><span class="sxs-lookup"><span data-stu-id="85497-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="85497-399">**Input1: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="85497-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="85497-400">De eerste invoer is de blob van Azure wordt dagelijks bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="85497-401">**Input2: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="85497-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="85497-402">Input2 is de Azure blob wekelijks worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="85497-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="85497-403">**Uitvoer: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="85497-403">**Output: Azure blob**</span></span>

<span data-ttu-id="85497-404">Een bestand voor uitvoer wordt elke dag gemaakt in de map voor de dag.</span><span class="sxs-lookup"><span data-stu-id="85497-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="85497-405">Beschikbaarheid van de uitvoer is ingesteld op **dag** (frequentie: dag, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="85497-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="85497-406">**Activiteit: hive-activiteit in een pijplijn**</span><span class="sxs-lookup"><span data-stu-id="85497-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="85497-407">Het hive-activiteit duurt de twee invoeren en een uitvoer-segment wordt geproduceerd elke dag.</span><span class="sxs-lookup"><span data-stu-id="85497-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="85497-408">U kunt elke dag uitvoer segment invoersegment met de vorige week voor wekelijkse invoer als volgt afhankelijk opgeven.</span><span class="sxs-lookup"><span data-stu-id="85497-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="85497-409">Zie [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md) voor een lijst met functies en systeemvariabelen die ondersteuning biedt voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="85497-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="85497-410">Bijlage</span><span class="sxs-lookup"><span data-stu-id="85497-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="85497-411">Voorbeeld: sequentieel kopiëren</span><span class="sxs-lookup"><span data-stu-id="85497-411">Example: copy sequentially</span></span>
<span data-ttu-id="85497-412">Het is mogelijk meerdere kopieerbewerkingen na elkaar uitgevoerd op een manier opeenvolgende/gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="85497-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="85497-413">U wellicht bijvoorbeeld twee kopie activiteiten in een pijplijn met de volgende invoergegevens uitvoergegevenssets (CopyActivity1 en CopyActivity2):</span><span class="sxs-lookup"><span data-stu-id="85497-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="85497-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="85497-414">CopyActivity1</span></span>

<span data-ttu-id="85497-415">Invoer: Dataset.</span><span class="sxs-lookup"><span data-stu-id="85497-415">Input: Dataset.</span></span> <span data-ttu-id="85497-416">Uitvoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="85497-416">Output: Dataset2.</span></span>

<span data-ttu-id="85497-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="85497-417">CopyActivity2</span></span>

<span data-ttu-id="85497-418">Invoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="85497-418">Input: Dataset2.</span></span>  <span data-ttu-id="85497-419">Uitvoer: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="85497-419">Output: Dataset3.</span></span>

<span data-ttu-id="85497-420">CopyActivity2 uitgevoerd alleen als de CopyActivity1 met succes is uitgevoerd en Dataset2 beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="85497-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="85497-421">Hier volgt de JSON van de voorbeeldpijplijn:</span><span class="sxs-lookup"><span data-stu-id="85497-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="85497-422">Merk op dat in het voorbeeld wordt de uitvoergegevensset van de eerste kopieeractiviteit (Dataset2) is opgegeven als invoer voor de tweede activiteit.</span><span class="sxs-lookup"><span data-stu-id="85497-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="85497-423">Daarom de tweede activiteit wordt alleen uitgevoerd als de uitvoergegevensset van de eerste activiteit gereed is.</span><span class="sxs-lookup"><span data-stu-id="85497-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="85497-424">In het voorbeeld kunt CopyActivity2 een andere invoer, zoals Dataset3, maar u Dataset2 opgeven als invoer voor CopyActivity2, zodat de activiteit kan niet worden uitgevoerd totdat CopyActivity1 is voltooid.</span><span class="sxs-lookup"><span data-stu-id="85497-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="85497-425">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="85497-425">For example:</span></span>

<span data-ttu-id="85497-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="85497-426">CopyActivity1</span></span>

<span data-ttu-id="85497-427">Invoer: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="85497-427">Input: Dataset1.</span></span> <span data-ttu-id="85497-428">Uitvoer: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="85497-428">Output: Dataset2.</span></span>

<span data-ttu-id="85497-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="85497-429">CopyActivity2</span></span>

<span data-ttu-id="85497-430">Invoer: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="85497-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="85497-431">Uitvoer: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="85497-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="85497-432">U ziet in het voorbeeld worden twee invoergegevenssets opgegeven voor de kopieeractiviteit van de tweede.</span><span class="sxs-lookup"><span data-stu-id="85497-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="85497-433">Wanneer meerdere invoer zijn opgegeven, wordt alleen de eerste invoer gegevensset wordt gebruikt voor het kopiëren van gegevens, maar andere gegevenssets worden gebruikt als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="85497-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="85497-434">CopyActivity2 zou pas beginnen nadat de volgende voorwaarden wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="85497-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="85497-435">CopyActivity1 is voltooid en Dataset2 is beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="85497-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="85497-436">Deze gegevensset wordt niet gebruikt bij het kopiëren van gegevens naar Dataset4.</span><span class="sxs-lookup"><span data-stu-id="85497-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="85497-437">Deze alleen fungeert als een afhankelijkheid van de planning voor CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="85497-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="85497-438">Dataset3 is beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="85497-438">Dataset3 is available.</span></span> <span data-ttu-id="85497-439">Deze gegevensset vertegenwoordigt de gegevens die worden gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="85497-439">This dataset represents the data that is copied to the destination.</span></span> 