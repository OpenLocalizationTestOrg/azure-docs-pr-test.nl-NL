---
title: Gegevenssets maken in Azure Data Factory | Microsoft Docs
description: Informatie over het maken van gegevenssets in Azure Data Factory met voorbeelden die gebruikmaken van eigenschappen zoals de offset en anchorDateTime.
keywords: dataset gegevensset voorbeeld maken, voorbeeld van de offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="714f9-104">Gegevenssets in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="714f9-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="714f9-105">In dit artikel wordt beschreven welke gegevenssets zijn, hoe ze worden gedefinieerd in JSON-indeling, en hoe ze worden gebruikt Azure Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="714f9-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="714f9-106">Het biedt details over elke sectie (bijvoorbeeld, structuur, beschikbaarheid en beleid) in de JSON-definitie van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="714f9-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="714f9-107">Het artikel bevat ook voorbeelden voor het gebruik van de **offset**, **anchorDateTime**, en **stijl** eigenschappen in de JSON-definitie van een dataset.</span><span class="sxs-lookup"><span data-stu-id="714f9-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="714f9-108">Als u niet bekend met Data Factory bent, Zie [Inleiding tot Azure Data Factory](data-factory-introduction.md) voor een overzicht.</span><span class="sxs-lookup"><span data-stu-id="714f9-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="714f9-109">Als u praktische ervaring met het maken van gegevensfactory niet hebt, kunt u toegang een beter inzicht in de vorm van de [data transformation zelfstudie](data-factory-build-your-first-pipeline.md) en de [data movement zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="714f9-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="714f9-110">Overview</span></span>
<span data-ttu-id="714f9-111">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="714f9-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="714f9-112">Een **pijplijn** is een logische groepering van **activiteiten** die samen een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="714f9-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="714f9-113">De activiteiten in een pijplijn definiëren acties uitvoeren op uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="714f9-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="714f9-114">Bijvoorbeeld, kunt u een kopieeractiviteit om gegevens te kopiëren van een lokale SQL Server naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="714f9-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="714f9-115">Vervolgens kunt u een Hive-activiteit die wordt uitgevoerd van een Hive-script op een Azure HDInsight-cluster om gegevens te verwerken van Blob-opslag voor het produceren van uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="714f9-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="714f9-116">Ten slotte kunt u een tweede kopieeractiviteit de uitvoergegevens kopiëren naar Azure SQL Data Warehouse boven op welke business intelligence (BI) reporting oplossingen zijn gebouwd.</span><span class="sxs-lookup"><span data-stu-id="714f9-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="714f9-117">Zie voor meer informatie over de pijplijnen en activiteiten [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="714f9-118">Een activiteit kan duren voordat de invoer van nul of meer **gegevenssets**, en een of meer uitvoergegevenssets te produceren.</span><span class="sxs-lookup"><span data-stu-id="714f9-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="714f9-119">Een invoergegevensset staat voor de invoer voor een activiteit in de pijplijn en een uitvoergegevensset voor de uitvoer voor de activiteit.</span><span class="sxs-lookup"><span data-stu-id="714f9-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="714f9-120">Gegevenssets identificeren gegevens binnen andere gegevensarchieven, zoals tabellen, bestanden, mappen en documenten.</span><span class="sxs-lookup"><span data-stu-id="714f9-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="714f9-121">Een Azure Blob-gegevensset geeft bijvoorbeeld de blob-container en map in Blob storage van waaruit de pijplijn de gegevens moet lezen.</span><span class="sxs-lookup"><span data-stu-id="714f9-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="714f9-122">Voordat u een gegevensset maakt, maakt u een **gekoppelde service** uw data store koppelen aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="714f9-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="714f9-123">Gekoppelde services zijn te vergelijken met verbindingsreeksen, die de verbindingsinformatie bevatten die Data Factory nodig heeft om verbinding te maken met externe bronnen.</span><span class="sxs-lookup"><span data-stu-id="714f9-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="714f9-124">Gegevenssets identificeren gegevens binnen de gekoppelde gegevens worden opgeslagen, zoals SQL-tabellen, bestanden, mappen en documenten.</span><span class="sxs-lookup"><span data-stu-id="714f9-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="714f9-125">Bijvoorbeeld, gekoppelde een Azure Storage service een opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="714f9-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="714f9-126">Een Azure Blob-gegevensset vertegenwoordigt de blob-container en de map waarin de invoer blobs moeten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="714f9-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="714f9-127">Hier volgt een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="714f9-127">Here is a sample scenario.</span></span> <span data-ttu-id="714f9-128">Om gegevens te kopiëren van Blob-opslag met een SQL-database, hebt u twee gekoppelde services: Azure Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="714f9-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="714f9-129">Vervolgens maakt u twee gegevenssets: Azure Blob-gegevensset (die verwijst naar de gekoppelde Azure Storage-service) en Azure SQL-tabel dataset (die verwijst naar de service Azure SQL Database gekoppeld).</span><span class="sxs-lookup"><span data-stu-id="714f9-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="714f9-130">De Azure Storage en Azure SQL Database, gekoppelde services bevatten verbindingstekenreeksen die Data Factory tijdens runtime verbinding maakt met uw Azure Storage en Azure SQL Database, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="714f9-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="714f9-131">De Azure Blob-gegevensset bevat de blob-container en de blob-map waarin de invoer blobs in de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="714f9-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="714f9-132">De gegevensset Azure SQL-tabel bevat de SQL-tabel in uw SQL-database die de gegevens wordt worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="714f9-133">Het volgende diagram toont de relaties tussen pipeline, de activiteit, de gegevensset en de gekoppelde service in de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="714f9-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relatie tussen een pijplijn, activiteit, gegevensset, gekoppelde services](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="714f9-135">JSON van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="714f9-135">Dataset JSON</span></span>
<span data-ttu-id="714f9-136">Een gegevensset in Gegevensfactory is gedefinieerd in JSON-indeling als volgt:</span><span class="sxs-lookup"><span data-stu-id="714f9-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="714f9-137">De volgende tabel beschrijft de eigenschappen in de bovenstaande JSON:</span><span class="sxs-lookup"><span data-stu-id="714f9-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="714f9-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="714f9-138">Property</span></span> | <span data-ttu-id="714f9-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="714f9-139">Description</span></span> | <span data-ttu-id="714f9-140">Vereist</span><span class="sxs-lookup"><span data-stu-id="714f9-140">Required</span></span> | <span data-ttu-id="714f9-141">Standaard</span><span class="sxs-lookup"><span data-stu-id="714f9-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="714f9-142">naam</span><span class="sxs-lookup"><span data-stu-id="714f9-142">name</span></span> |<span data-ttu-id="714f9-143">Naam van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="714f9-143">Name of the dataset.</span></span> <span data-ttu-id="714f9-144">Zie [Azure Data Factory - naamgevingsregels](data-factory-naming-rules.md) voor naamgevingsregels.</span><span class="sxs-lookup"><span data-stu-id="714f9-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="714f9-145">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-145">Yes</span></span> |<span data-ttu-id="714f9-146">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-146">NA</span></span> |
| <span data-ttu-id="714f9-147">type</span><span class="sxs-lookup"><span data-stu-id="714f9-147">type</span></span> |<span data-ttu-id="714f9-148">Het type van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="714f9-148">Type of the dataset.</span></span> <span data-ttu-id="714f9-149">Geef een van de typen die door Data Factory worden ondersteund (bijvoorbeeld: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="714f9-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="714f9-150">Zie voor meer informatie [gegevensettype](#Type).</span><span class="sxs-lookup"><span data-stu-id="714f9-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="714f9-151">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-151">Yes</span></span> |<span data-ttu-id="714f9-152">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-152">NA</span></span> |
| <span data-ttu-id="714f9-153">structuur</span><span class="sxs-lookup"><span data-stu-id="714f9-153">structure</span></span> |<span data-ttu-id="714f9-154">Schema voor de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="714f9-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="714f9-155">Zie voor meer informatie [gegevenssetstructuur](#Structure).</span><span class="sxs-lookup"><span data-stu-id="714f9-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="714f9-156">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-156">No</span></span> |<span data-ttu-id="714f9-157">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-157">NA</span></span> |
| <span data-ttu-id="714f9-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="714f9-158">typeProperties</span></span> | <span data-ttu-id="714f9-159">De type-eigenschappen zijn verschillend voor elk type (bijvoorbeeld: Azure Blob, Azure SQL-tabel).</span><span class="sxs-lookup"><span data-stu-id="714f9-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="714f9-160">Zie voor meer informatie over de ondersteunde typen en hun eigenschappen [gegevensettype](#Type).</span><span class="sxs-lookup"><span data-stu-id="714f9-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="714f9-161">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-161">Yes</span></span> |<span data-ttu-id="714f9-162">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-162">NA</span></span> |
| <span data-ttu-id="714f9-163">external</span><span class="sxs-lookup"><span data-stu-id="714f9-163">external</span></span> | <span data-ttu-id="714f9-164">Booleaanse vlag om op te geven of een gegevensset expliciet wordt geproduceerd door een data factory-pijplijn of niet.</span><span class="sxs-lookup"><span data-stu-id="714f9-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="714f9-165">Als de invoergegevensset voor een activiteit niet door de huidige pipeline gemaakt wordt, moet u deze vlag ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="714f9-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="714f9-166">Deze vlag ingesteld op true voor de invoer gegevensset van de eerste activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="714f9-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="714f9-167">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-167">No</span></span> |<span data-ttu-id="714f9-168">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="714f9-168">false</span></span> |
| <span data-ttu-id="714f9-169">availability</span><span class="sxs-lookup"><span data-stu-id="714f9-169">availability</span></span> | <span data-ttu-id="714f9-170">Definieert het venster verwerking (bijvoorbeeld elk uur of dagelijks) of het segmenteringshulplijnen model voor de gegevensset voor productie.</span><span class="sxs-lookup"><span data-stu-id="714f9-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="714f9-171">Elke eenheid gegevens verbruikt en die wordt geproduceerd door het uitvoeren van een activiteit wordt een gegevenssegment genoemd.</span><span class="sxs-lookup"><span data-stu-id="714f9-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="714f9-172">Als de beschikbaarheid van een uitvoergegevensset is ingesteld op dagelijks (frequentie - dag, interval - 1), wordt dagelijks een segment geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="714f9-173">Zie voor meer informatie [gegevensset beschikbaarheid](#Availability).</span><span class="sxs-lookup"><span data-stu-id="714f9-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="714f9-174">Zie voor informatie over de gegevensset segmentering model, de [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="714f9-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="714f9-175">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-175">Yes</span></span> |<span data-ttu-id="714f9-176">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-176">NA</span></span> |
| <span data-ttu-id="714f9-177">Beleid</span><span class="sxs-lookup"><span data-stu-id="714f9-177">policy</span></span> |<span data-ttu-id="714f9-178">Definieert de criteria of de conditie van de segmenten van de gegevensset moeten voldoen.</span><span class="sxs-lookup"><span data-stu-id="714f9-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="714f9-179">Zie voor meer informatie de [gegevensset beleid](#Policy) sectie.</span><span class="sxs-lookup"><span data-stu-id="714f9-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="714f9-180">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-180">No</span></span> |<span data-ttu-id="714f9-181">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="714f9-182">Voorbeeld van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="714f9-182">Dataset example</span></span>
<span data-ttu-id="714f9-183">In het volgende voorbeeld wordt de gegevensset vertegenwoordigt een tabel met de naam **MyTable** in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="714f9-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="714f9-184">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="714f9-184">Note the following points:</span></span>

* <span data-ttu-id="714f9-185">**type** is ingesteld op azuresqltable zijn.</span><span class="sxs-lookup"><span data-stu-id="714f9-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="714f9-186">**tableName** type-eigenschap (die specifiek is voor AzureSqlTable type) is ingesteld op MyTable.</span><span class="sxs-lookup"><span data-stu-id="714f9-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="714f9-187">**linkedServiceName** verwijst naar een gekoppelde service van het type AzureSqlDatabase die is gedefinieerd in het volgende JSON-codefragment.</span><span class="sxs-lookup"><span data-stu-id="714f9-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="714f9-188">**beschikbaarheid frequentie** is ingesteld op dag, en **interval** is ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="714f9-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="714f9-189">Dit betekent dat het segment gegevensset dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="714f9-190">**AzureSqlLinkedService** wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="714f9-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="714f9-191">In het voorgaande JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="714f9-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="714f9-192">**type** is ingesteld op AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="714f9-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="714f9-193">**connectionString** type-eigenschap geeft u informatie voor verbinding met een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="714f9-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="714f9-194">Zoals u ziet, definieert de gekoppelde service verbinding maken met een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="714f9-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="714f9-195">De gegevensset wordt gedefinieerd welke tabel wordt gebruikt als invoer en uitvoer voor de activiteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="714f9-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="714f9-196">Tenzij een gegevensset wordt geproduceerd door de pijplijn, moet dit worden gemarkeerd als **externe**.</span><span class="sxs-lookup"><span data-stu-id="714f9-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="714f9-197">Deze instelling is algemeen van toepassing op invoer van de eerste activiteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="714f9-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="714f9-198"><a name="Type"></a>Gegevensettype</span><span class="sxs-lookup"><span data-stu-id="714f9-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="714f9-199">Het type van de gegevensset is afhankelijk van het gegevensarchief die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="714f9-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="714f9-200">Zie de volgende tabel voor een lijst met opgeslagen gegevens die door Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="714f9-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="714f9-201">Klik op een gegevensarchief voor meer informatie over het maken van een gekoppelde service en een gegevensset voor die gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="714f9-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="714f9-202">Gegevens worden opgeslagen met * on-premises kan worden of op Azure-infrastructuur als een service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="714f9-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="714f9-203">Deze gegevensarchieven moeten u voor het installeren van [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="714f9-204">In het voorbeeld in de vorige sectie, het type van de gegevensset is ingesteld op **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="714f9-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="714f9-205">Op dezelfde manier, het type van de gegevensset voor een Azure Blob-gegevensset is ingesteld op **AzureBlob**, zoals wordt weergegeven in de volgende JSON:</span><span class="sxs-lookup"><span data-stu-id="714f9-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="714f9-206"><a name="Structure"></a>Structuur van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="714f9-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="714f9-207">De **structuur** sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="714f9-207">The **structure** section is optional.</span></span> <span data-ttu-id="714f9-208">Hiermee definieert u het schema van de gegevensset door dat een verzameling van namen en gegevenstypen van de kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="714f9-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="714f9-209">De structuur sectie kunt u type informatie dat wordt gebruikt voor het converteren van de typen en het toewijzen van kolommen van de bron naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="714f9-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="714f9-210">In het volgende voorbeeld wordt de gegevensset heeft drie kolommen: `slicetimestamp`, `projectname`, en `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="714f9-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="714f9-211">Zijn van het type String, String en Decimal, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="714f9-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="714f9-212">Elke kolom in de structuur bevat de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="714f9-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="714f9-213">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="714f9-213">Property</span></span> | <span data-ttu-id="714f9-214">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="714f9-214">Description</span></span> | <span data-ttu-id="714f9-215">Vereist</span><span class="sxs-lookup"><span data-stu-id="714f9-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="714f9-216">naam</span><span class="sxs-lookup"><span data-stu-id="714f9-216">name</span></span> |<span data-ttu-id="714f9-217">De naam van de kolom.</span><span class="sxs-lookup"><span data-stu-id="714f9-217">Name of the column.</span></span> |<span data-ttu-id="714f9-218">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-218">Yes</span></span> |
| <span data-ttu-id="714f9-219">type</span><span class="sxs-lookup"><span data-stu-id="714f9-219">type</span></span> |<span data-ttu-id="714f9-220">Het gegevenstype van de kolom.</span><span class="sxs-lookup"><span data-stu-id="714f9-220">Data type of the column.</span></span>  |<span data-ttu-id="714f9-221">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-221">No</span></span> |
| <span data-ttu-id="714f9-222">Cultuur</span><span class="sxs-lookup"><span data-stu-id="714f9-222">culture</span></span> |<span data-ttu-id="714f9-223">. NET-gebaseerde cultuur moet worden gebruikt wanneer het type een .NET-type is: `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="714f9-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="714f9-224">De standaardwaarde is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="714f9-224">The default is `en-us`.</span></span> |<span data-ttu-id="714f9-225">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-225">No</span></span> |
| <span data-ttu-id="714f9-226">Indeling</span><span class="sxs-lookup"><span data-stu-id="714f9-226">format</span></span> |<span data-ttu-id="714f9-227">Indeling van tekenreeks moet worden gebruikt wanneer het type een .NET-type is: `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="714f9-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="714f9-228">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-228">No</span></span> |

<span data-ttu-id="714f9-229">De volgende richtlijnen te bepalen wanneer gegevens van de structuur en wat u wilt opnemen de **structuur** sectie.</span><span class="sxs-lookup"><span data-stu-id="714f9-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="714f9-230">**Voor gestructureerde gegevensbronnen**, de sectie structuur alleen opgeven als u toewijzen bronkolommen wilt voor het opvangen van kolommen en hun namen niet overeen komen.</span><span class="sxs-lookup"><span data-stu-id="714f9-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="714f9-231">Dit soort gegevensbron gestructureerde slaat schema en het type informatie samen met de gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="714f9-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="714f9-232">Voorbeelden van gestructureerde gegevensbronnen zijn SQL Server, Oracle en Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="714f9-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="714f9-233">Als het type informatie is al beschikbaar voor gestructureerde gegevensbronnen, moet u type-informatie niet opnemen wanneer u de sectie structuur opneemt.</span><span class="sxs-lookup"><span data-stu-id="714f9-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="714f9-234">**Voor schema op lezen gegevensbronnen (specifiek Blob-opslag)**, kunt u gegevens opslaan zonder een schema of het type informatie met de gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="714f9-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="714f9-235">Voor deze typen gegevensbronnen, structuur opnemen wanneer u toewijzen bronkolommen wilt voor het opvangen van kolommen.</span><span class="sxs-lookup"><span data-stu-id="714f9-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="714f9-236">Structuur ook bevatten wanneer de dataset de invoer voor een kopieeractiviteit is en gegevenstypen van de gegevensset bron moeten worden geconverteerd naar native-typen voor de sink.</span><span class="sxs-lookup"><span data-stu-id="714f9-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="714f9-237">Data Factory ondersteunt de volgende waarden voor het type informatie in de structuur: **Int16, Int32, Int64, Single, Double, Decimal, Byte [], Booleaanse waarde, String, Guid, Datetime, Datetimeoffset en Timespan**.</span><span class="sxs-lookup"><span data-stu-id="714f9-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="714f9-238">Deze waarden zijn Common Language Specification (CLS)-compatibel zijn,. NET-type op basis van waarden.</span><span class="sxs-lookup"><span data-stu-id="714f9-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="714f9-239">Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een gegevensopslag bron naar een gegevensarchief sink.</span><span class="sxs-lookup"><span data-stu-id="714f9-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="714f9-240">Beschikbaarheid van gegevensset</span><span class="sxs-lookup"><span data-stu-id="714f9-240">Dataset availability</span></span>
<span data-ttu-id="714f9-241">De **beschikbaarheid** sectie in een gegevensset definieert het venster verwerking (bijvoorbeeld elk uur, dagelijks of wekelijks) voor de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="714f9-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="714f9-242">Zie voor meer informatie over windows activiteit [planning en uitvoering](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="714f9-243">De volgende sectie van de beschikbaarheid geeft aan dat de uitvoergegevensset ofwel per uur wordt geproduceerd, of de invoergegevensset beschikbaar per uur:</span><span class="sxs-lookup"><span data-stu-id="714f9-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="714f9-244">Als de pijplijn de volgende begin- en eindtijden heeft:</span><span class="sxs-lookup"><span data-stu-id="714f9-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="714f9-245">De uitvoergegevensset wordt geproduceerd per uur in de pijplijn start- en eindtijden.</span><span class="sxs-lookup"><span data-stu-id="714f9-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="714f9-246">Er zijn daarom vijf gegevensset gegevenssegmenten geproduceerd door deze pipeline, één voor elke activiteitvenster (12: 00 A.M. - 1 uur, 01: 00 - 2 uur, 2 uur - 3 uur, 3 uur - 4 AM, 4 uur - 5 uur).</span><span class="sxs-lookup"><span data-stu-id="714f9-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="714f9-247">De volgende tabel beschrijft de eigenschappen die u in de beschikbaarheidssectie gebruiken kunt:</span><span class="sxs-lookup"><span data-stu-id="714f9-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="714f9-248">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="714f9-248">Property</span></span> | <span data-ttu-id="714f9-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="714f9-249">Description</span></span> | <span data-ttu-id="714f9-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="714f9-250">Required</span></span> | <span data-ttu-id="714f9-251">Standaard</span><span class="sxs-lookup"><span data-stu-id="714f9-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="714f9-252">Frequentie</span><span class="sxs-lookup"><span data-stu-id="714f9-252">frequency</span></span> |<span data-ttu-id="714f9-253">Hiermee geeft u tijdseenheid voor de gegevensset segment productie.</span><span class="sxs-lookup"><span data-stu-id="714f9-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="714f9-254"><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand</span><span class="sxs-lookup"><span data-stu-id="714f9-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="714f9-255">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-255">Yes</span></span> |<span data-ttu-id="714f9-256">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-256">NA</span></span> |
| <span data-ttu-id="714f9-257">Interval</span><span class="sxs-lookup"><span data-stu-id="714f9-257">interval</span></span> |<span data-ttu-id="714f9-258">Hiermee geeft u een vermenigvuldiger voor de frequentie.</span><span class="sxs-lookup"><span data-stu-id="714f9-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="714f9-259">"Frequentie x-interval" bepaalt hoe vaak het segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="714f9-260">Bijvoorbeeld, als u de gegevensset worden gesegmenteerd op uurbasis moet, u ingesteld <b>frequentie</b> naar <b>uur</b>, en <b>interval</b> naar <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="714f9-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="714f9-261">Houd er rekening mee dat als u opgeeft **frequentie** als **minuut**, moet u het interval instellen op niet kleiner zijn dan 15.</span><span class="sxs-lookup"><span data-stu-id="714f9-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="714f9-262">Ja</span><span class="sxs-lookup"><span data-stu-id="714f9-262">Yes</span></span> |<span data-ttu-id="714f9-263">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-263">NA</span></span> |
| <span data-ttu-id="714f9-264">stijl</span><span class="sxs-lookup"><span data-stu-id="714f9-264">style</span></span> |<span data-ttu-id="714f9-265">Hiermee geeft u op of het segment aan het begin of einde van het interval moet worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="714f9-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="714f9-266">StartOfInterval</span></span></li><li><span data-ttu-id="714f9-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="714f9-267">EndOfInterval</span></span></li></ul><span data-ttu-id="714f9-268">Als **frequentie** is ingesteld op **maand**, en **stijl** is ingesteld op **EndOfInterval**, het segment op de laatste dag van de maand wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="714f9-269">Als **stijl** is ingesteld op **StartOfInterval**, het segment op de eerste dag van de maand wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="714f9-270">Als **frequentie** is ingesteld op **dag**, en **stijl** is ingesteld op **EndOfInterval**, in het afgelopen uur van de dag het segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="714f9-271">Als **frequentie** is ingesteld op **uur**, en **stijl** is ingesteld op **EndOfInterval**, het segment wordt geproduceerd aan het einde van het uur.</span><span class="sxs-lookup"><span data-stu-id="714f9-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="714f9-272">Voor een segment voor de periode van 1-2 uur, het segment geproduceerd om 2 uur.</span><span class="sxs-lookup"><span data-stu-id="714f9-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="714f9-273">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-273">No</span></span> |<span data-ttu-id="714f9-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="714f9-274">EndOfInterval</span></span> |
| <span data-ttu-id="714f9-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="714f9-275">anchorDateTime</span></span> |<span data-ttu-id="714f9-276">Hiermee definieert u de absolute positie in de tijd die wordt gebruikt door de planner gegevensset segmentgrenzen berekenen.</span><span class="sxs-lookup"><span data-stu-id="714f9-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="714f9-277">Houd er rekening mee dat als deze propoerty de onderdelen van de datum die meer gedetailleerd dan de opgegeven frequentie heeft, de gedetailleerdere onderdelen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="714f9-278">Bijvoorbeeld, als de **interval** is **per uur** (frequentie: uur en interval: 1), en de **anchorDateTime** bevat **minuten en seconden**, en vervolgens de minuten en seconden delen van **anchorDateTime** worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="714f9-279">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-279">No</span></span> |<span data-ttu-id="714f9-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="714f9-280">01/01/0001</span></span> |
| <span data-ttu-id="714f9-281">offset</span><span class="sxs-lookup"><span data-stu-id="714f9-281">offset</span></span> |<span data-ttu-id="714f9-282">TimeSpan waarmee het begin en einde van alle segmenten van de gegevensset zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="714f9-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="714f9-283">Houd er rekening mee dat als beide **anchorDateTime** en **offset** zijn opgegeven, wordt het resultaat is een gecombineerde verschuiving.</span><span class="sxs-lookup"><span data-stu-id="714f9-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="714f9-284">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-284">No</span></span> |<span data-ttu-id="714f9-285">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="714f9-286">offset voorbeeld</span><span class="sxs-lookup"><span data-stu-id="714f9-286">offset example</span></span>
<span data-ttu-id="714f9-287">Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. (middernacht) Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="714f9-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="714f9-288">Als u de begintijd moet 6 uur UTC-tijd in plaats daarvan wilt, stelt u de verschuiving zoals weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="714f9-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="714f9-289">Voorbeeld van anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="714f9-289">anchorDateTime example</span></span>
<span data-ttu-id="714f9-290">In het volgende voorbeeld wordt de elke 23 uur in de gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="714f9-291">Het eerste segment wordt gestart op het moment dat is opgegeven door **anchorDateTime**, die is ingesteld op `2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="714f9-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="714f9-292">Voorbeeld van de offset/style</span><span class="sxs-lookup"><span data-stu-id="714f9-292">offset/style example</span></span>
<span data-ttu-id="714f9-293">De volgende gegevensset wordt maandelijks, en op de 3rd van elke maand om 8:00 uur wordt geproduceerd (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="714f9-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="714f9-294"><a name="Policy"></a>DataSet beleid</span><span class="sxs-lookup"><span data-stu-id="714f9-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="714f9-295">De **beleid** sectie in de definitie van de gegevensset definieert u de criteria of de conditie van de segmenten van de gegevensset moeten voldoen.</span><span class="sxs-lookup"><span data-stu-id="714f9-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="714f9-296">Van validatiebeleid</span><span class="sxs-lookup"><span data-stu-id="714f9-296">Validation policies</span></span>
| <span data-ttu-id="714f9-297">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="714f9-297">Policy name</span></span> | <span data-ttu-id="714f9-298">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="714f9-298">Description</span></span> | <span data-ttu-id="714f9-299">Toegepast op</span><span class="sxs-lookup"><span data-stu-id="714f9-299">Applied to</span></span> | <span data-ttu-id="714f9-300">Vereist</span><span class="sxs-lookup"><span data-stu-id="714f9-300">Required</span></span> | <span data-ttu-id="714f9-301">Standaard</span><span class="sxs-lookup"><span data-stu-id="714f9-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="714f9-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="714f9-302">minimumSizeMB</span></span> |<span data-ttu-id="714f9-303">Valideert dat de gegevens in **Azure Blob storage** voldoet aan de minimale grootte (in MB).</span><span class="sxs-lookup"><span data-stu-id="714f9-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="714f9-304">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="714f9-304">Azure Blob storage</span></span> |<span data-ttu-id="714f9-305">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-305">No</span></span> |<span data-ttu-id="714f9-306">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-306">NA</span></span> |
| <span data-ttu-id="714f9-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="714f9-307">minimumRows</span></span> |<span data-ttu-id="714f9-308">Valideert dat de gegevens in een **Azure SQL-database** of een **Azure-tabel** het minimum aantal rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="714f9-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="714f9-309">Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="714f9-309">Azure SQL database</span></span></li><li><span data-ttu-id="714f9-310">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="714f9-310">Azure table</span></span></li></ul> |<span data-ttu-id="714f9-311">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-311">No</span></span> |<span data-ttu-id="714f9-312">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="714f9-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="714f9-313">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="714f9-313">Examples</span></span>
<span data-ttu-id="714f9-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="714f9-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="714f9-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="714f9-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="714f9-316">Externe gegevenssets</span><span class="sxs-lookup"><span data-stu-id="714f9-316">External datasets</span></span>
<span data-ttu-id="714f9-317">Externe gegevenssets zijn degene die niet worden geproduceerd door een actieve pijplijn in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="714f9-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="714f9-318">Als de dataset is gemarkeerd als **externe**, wordt de **ExternalData** beleid invloed op de werking van de beschikbaarheid van gegevensset segment worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="714f9-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="714f9-319">Tenzij een gegevensset wordt geproduceerd door Data Factory, moet dit worden gemarkeerd als **externe**.</span><span class="sxs-lookup"><span data-stu-id="714f9-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="714f9-320">Deze instelling in het algemeen geldt voor de eerste activiteit in een pijplijn-invoer tenzij activiteit of koppeling van de pijplijn wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="714f9-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="714f9-321">Naam</span><span class="sxs-lookup"><span data-stu-id="714f9-321">Name</span></span> | <span data-ttu-id="714f9-322">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="714f9-322">Description</span></span> | <span data-ttu-id="714f9-323">Vereist</span><span class="sxs-lookup"><span data-stu-id="714f9-323">Required</span></span> | <span data-ttu-id="714f9-324">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="714f9-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="714f9-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="714f9-325">dataDelay</span></span> |<span data-ttu-id="714f9-326">De tijd om uit te stellen de controle van de beschikbaarheid van de externe gegevens voor het opgegeven segment.</span><span class="sxs-lookup"><span data-stu-id="714f9-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="714f9-327">Bijvoorbeeld, kunt u een controle per uur uitstellen met deze instelling.</span><span class="sxs-lookup"><span data-stu-id="714f9-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="714f9-328">De instelling is alleen van toepassing op de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="714f9-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="714f9-329">Bijvoorbeeld, als het is nu om 13:00 uur en deze waarde 10 minuten is, begint de validatie om 1:10 uur.</span><span class="sxs-lookup"><span data-stu-id="714f9-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="714f9-330">Houd er rekening mee dat deze instelling heeft geen invloed op segmenten in het verleden.</span><span class="sxs-lookup"><span data-stu-id="714f9-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="714f9-331">Segmenten met **segment eindtijd** + **dataDelay** < **nu** zonder enige vertraging worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="714f9-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="714f9-332">Tijden groter is dan 23:59 uur moeten worden opgegeven met de `day.hours:minutes:seconds` indeling.</span><span class="sxs-lookup"><span data-stu-id="714f9-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="714f9-333">Bijvoorbeeld, als u 24 uur, gebruik geen 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="714f9-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="714f9-334">Gebruik in plaats daarvan 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="714f9-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="714f9-335">Als u 24:00:00, wordt dit beschouwd als 24 dagen (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="714f9-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="714f9-336">Geef 1:04:00:00 voor 1 dag en 4 uur.</span><span class="sxs-lookup"><span data-stu-id="714f9-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="714f9-337">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-337">No</span></span> |<span data-ttu-id="714f9-338">0</span><span class="sxs-lookup"><span data-stu-id="714f9-338">0</span></span> |
| <span data-ttu-id="714f9-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="714f9-339">retryInterval</span></span> |<span data-ttu-id="714f9-340">De wachttijd tussen een fout en het opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="714f9-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="714f9-341">Deze instelling geldt voor de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="714f9-341">This setting applies to present time.</span></span> <span data-ttu-id="714f9-342">Als de vorige is mislukt probeert, de volgende poging is na de **retryInterval** periode.</span><span class="sxs-lookup"><span data-stu-id="714f9-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="714f9-343">Als het nu om 13:00 uur, beginnen we in de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="714f9-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="714f9-344">Als de duur van de eerste validatiecontrole is 1 minuut en de bewerking is mislukt, de volgende poging is 1:00 + 1 min (duur), 1 min. (interval voor opnieuw proberen) + = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="714f9-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="714f9-345">Er is geen vertraging segmenten in het verleden.</span><span class="sxs-lookup"><span data-stu-id="714f9-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="714f9-346">De nieuwe poging gebeurt onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="714f9-346">The retry happens immediately.</span></span> |<span data-ttu-id="714f9-347">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-347">No</span></span> |<span data-ttu-id="714f9-348">00:01:00 (1 minuut)</span><span class="sxs-lookup"><span data-stu-id="714f9-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="714f9-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="714f9-349">retryTimeout</span></span> |<span data-ttu-id="714f9-350">De time-out voor nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="714f9-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="714f9-351">Als deze eigenschap is ingesteld op 10 minuten, moet de validatie binnen 10 minuten worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="714f9-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="714f9-352">Als het duurt langer dan 10 minuten de validatie uitvoeren, wordt de nieuwe poging time-out.</span><span class="sxs-lookup"><span data-stu-id="714f9-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="714f9-353">Als alle pogingen voor de time-out voor de validatie van het segment is gemarkeerd als **time-out**.</span><span class="sxs-lookup"><span data-stu-id="714f9-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="714f9-354">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-354">No</span></span> |<span data-ttu-id="714f9-355">00:10:00 (10 minuten)</span><span class="sxs-lookup"><span data-stu-id="714f9-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="714f9-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="714f9-356">maximumRetry</span></span> |<span data-ttu-id="714f9-357">Het aantal keren om te controleren op de beschikbaarheid van de externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="714f9-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="714f9-358">De maximaal toegestane waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="714f9-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="714f9-359">Nee</span><span class="sxs-lookup"><span data-stu-id="714f9-359">No</span></span> |<span data-ttu-id="714f9-360">3</span><span class="sxs-lookup"><span data-stu-id="714f9-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="714f9-361">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="714f9-361">Create datasets</span></span>
<span data-ttu-id="714f9-362">U kunt de gegevenssets maken met behulp van een van deze hulpprogramma's of de SDK's:</span><span class="sxs-lookup"><span data-stu-id="714f9-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="714f9-363">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="714f9-363">Copy Wizard</span></span> 
- <span data-ttu-id="714f9-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="714f9-364">Azure portal</span></span>
- <span data-ttu-id="714f9-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="714f9-365">Visual Studio</span></span>
- <span data-ttu-id="714f9-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="714f9-366">PowerShell</span></span>
- <span data-ttu-id="714f9-367">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="714f9-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="714f9-368">REST API</span><span class="sxs-lookup"><span data-stu-id="714f9-368">REST API</span></span>
- <span data-ttu-id="714f9-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="714f9-369">.NET API</span></span>

<span data-ttu-id="714f9-370">Zie de volgende zelfstudies voor stapsgewijze instructies voor het maken van de pijplijnen en gegevenssets met behulp van een van deze hulpprogramma's of de SDK's:</span><span class="sxs-lookup"><span data-stu-id="714f9-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="714f9-371">Een pijplijn met een transformatieactiviteit gegevens bouwen</span><span class="sxs-lookup"><span data-stu-id="714f9-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="714f9-372">Maken van een pijplijn met een activiteit van de verplaatsing van gegevens</span><span class="sxs-lookup"><span data-stu-id="714f9-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="714f9-373">Nadat u een pijplijn gemaakt en geïmplementeerd, kunt u deze kunt beheren en uw pijplijnen bewaken met behulp van de Azure portal-blades of de app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="714f9-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="714f9-374">Zie de volgende onderwerpen voor stapsgewijze instructies:</span><span class="sxs-lookup"><span data-stu-id="714f9-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="714f9-375">Bewaken en beheren van pijplijnen via Azure portal-blades</span><span class="sxs-lookup"><span data-stu-id="714f9-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="714f9-376">Bewaken en beheren van pijplijnen met behulp van de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="714f9-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="714f9-377">Bereik gegevenssets</span><span class="sxs-lookup"><span data-stu-id="714f9-377">Scoped datasets</span></span>
<span data-ttu-id="714f9-378">Kunt u gegevenssets die zijn gericht op een pijplijn met behulp van de **gegevenssets** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="714f9-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="714f9-379">Deze gegevenssets kan alleen worden gebruikt door activiteiten binnen deze pipeline, niet door de activiteiten in andere pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="714f9-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="714f9-380">Het volgende voorbeeld definieert een pijplijn met twee gegevenssets (InputDataset rdc en OutputDataset rdc) dat in de pijplijn wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="714f9-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="714f9-381">Bereik gegevenssets worden alleen ondersteund voor eenmalige pijplijnen (waarbij **pipelineMode** is ingesteld op **OneTime**).</span><span class="sxs-lookup"><span data-stu-id="714f9-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="714f9-382">Zie [Onetime pijplijn](data-factory-create-pipelines.md#onetime-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="714f9-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="714f9-383">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="714f9-383">Next steps</span></span>
- <span data-ttu-id="714f9-384">Zie voor meer informatie over pijplijnen [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="714f9-385">Zie voor meer informatie over hoe pijplijnen worden gepland en uitgevoerd, [planning en uitvoering in Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="714f9-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
