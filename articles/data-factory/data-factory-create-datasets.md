---
title: aaaCreate gegevenssets in Azure Data Factory | Microsoft Docs
description: Informatie over hoe toocreate gegevenssets in Azure Data Factory met voorbeelden die gebruikmaken van eigenschappen zoals offset en anchorDateTime.
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
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="288c8-104">Gegevenssets in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="288c8-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="288c8-105">In dit artikel wordt beschreven welke gegevenssets zijn, hoe ze worden gedefinieerd in JSON-indeling, en hoe ze worden gebruikt Azure Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="288c8-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="288c8-106">Het biedt details over elke sectie (bijvoorbeeld, structuur, beschikbaarheid en beleid) in Hallo gegevensset JSON-definitie.</span><span class="sxs-lookup"><span data-stu-id="288c8-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="288c8-107">Hallo artikel biedt ook voorbeelden voor het gebruik van Hallo **offset**, **anchorDateTime**, en **stijl** eigenschappen in de JSON-definitie van een dataset.</span><span class="sxs-lookup"><span data-stu-id="288c8-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="288c8-108">Als u nieuwe tooData Factory, Zie [inleiding tooAzure Data Factory](data-factory-introduction.md) voor een overzicht.</span><span class="sxs-lookup"><span data-stu-id="288c8-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="288c8-109">Als u praktische ervaring met het maken van gegevensfactory niet hebt, kunt u toegang een beter inzicht door Hallo lezen [data transformation zelfstudie](data-factory-build-your-first-pipeline.md) en Hallo [data movement zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="288c8-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="288c8-110">Overview</span></span>
<span data-ttu-id="288c8-111">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="288c8-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="288c8-112">Een **pijplijn** is een logische groepering van **activiteiten** die samen een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="288c8-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="288c8-113">Hallo-activiteiten in een pijplijn definiëren tooperform acties op uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="288c8-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="288c8-114">U kunt bijvoorbeeld een kopie toocopy activiteitsgegevens van een lokale SQL Server tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="288c8-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="288c8-115">Vervolgens kunt u een Hive-activiteit die wordt een Hive-script uitgevoerd op een Azure HDInsight-cluster tooprocess gegevens uit Blob storage tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="288c8-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="288c8-116">Ten slotte kunt u een tweede kopie activiteit toocopy Hallo uitvoer gegevens tooAzure SQL Data Warehouse boven op welke business intelligence (BI) reporting oplossingen zijn gebouwd.</span><span class="sxs-lookup"><span data-stu-id="288c8-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="288c8-117">Zie voor meer informatie over de pijplijnen en activiteiten [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="288c8-118">Een activiteit kan duren voordat de invoer van nul of meer **gegevenssets**, en een of meer uitvoergegevenssets te produceren.</span><span class="sxs-lookup"><span data-stu-id="288c8-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="288c8-119">Een invoergegevensset Hallo invoer voor een activiteit in de pijplijn Hallo vertegenwoordigt, en een uitvoergegevensset Hallo uitvoer voor Hallo activiteit vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="288c8-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="288c8-120">Met gegevenssets worden gegevens binnen andere gegevensarchieven geïdentificeerd, waaronder tabellen, bestanden, mappen en documenten.</span><span class="sxs-lookup"><span data-stu-id="288c8-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="288c8-121">Een Azure Blob-gegevensset bevat bijvoorbeeld Hallo blob-container en map in Blob storage uit welke Hallo pijplijn Hallo gegevens moet lezen.</span><span class="sxs-lookup"><span data-stu-id="288c8-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="288c8-122">Voordat u een gegevensset maakt, maakt u een **gekoppelde service** toolink uw gegevens opslaan toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="288c8-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="288c8-123">Gekoppelde services zijn veel zoals verbindingsreeksen die Hallo verbindingsinformatie die nodig is voor Data Factory tooconnect tooexternal bronnen definiëren.</span><span class="sxs-lookup"><span data-stu-id="288c8-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="288c8-124">Gegevenssets identificeren gegevens in de gegevensarchieven Hallo gekoppeld, zoals SQL-tabellen, bestanden, mappen en documenten.</span><span class="sxs-lookup"><span data-stu-id="288c8-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="288c8-125">Bijvoorbeeld, gekoppelde een Azure Storage service een gegevensfactory storage account toohello.</span><span class="sxs-lookup"><span data-stu-id="288c8-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="288c8-126">Een Azure Blob-gegevensset vertegenwoordigt Hallo blob-container en Hallo-map met de Hallo invoer blobs toobe verwerkt.</span><span class="sxs-lookup"><span data-stu-id="288c8-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="288c8-127">Hier volgt een voorbeeldscenario.</span><span class="sxs-lookup"><span data-stu-id="288c8-127">Here is a sample scenario.</span></span> <span data-ttu-id="288c8-128">toocopy gegevens uit Blob storage tooa SQL-database, hebt u twee gekoppelde services: Azure Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="288c8-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="288c8-129">Vervolgens maakt u twee gegevenssets: Azure Blob-gegevensset (die verwijst naar de toohello gekoppelde Azure Storage-service) en Azure SQL-tabel dataset (die verwijst naar de toohello Azure SQL Database gekoppeld service).</span><span class="sxs-lookup"><span data-stu-id="288c8-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="288c8-130">Hallo Azure Storage en Azure SQL Database, gekoppelde services verbindingstekenreeksen bevatten die Data Factory maakt gebruik van op runtime tooconnect tooyour Azure Storage en Azure SQL Database, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="288c8-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="288c8-131">Hello Azure Blob-gegevensset bevat Hallo blob-container en de blob map Hallo invoer blobs in de Blob-opslag bevat.</span><span class="sxs-lookup"><span data-stu-id="288c8-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="288c8-132">Hello Azure SQL-tabel gegevensset geeft Hallo SQL-tabel in uw SQL-database toowhich Hallo-gegevens is toobe gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="288c8-133">Hallo volgende diagram toont Hallo relaties tussen pipeline, de activiteit, de gegevensset en de gekoppelde service in de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="288c8-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relatie tussen een pijplijn, activiteit, gegevensset, gekoppelde services](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="288c8-135">JSON van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="288c8-135">Dataset JSON</span></span>
<span data-ttu-id="288c8-136">Een gegevensset in Gegevensfactory is gedefinieerd in JSON-indeling als volgt:</span><span class="sxs-lookup"><span data-stu-id="288c8-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="288c8-137">Hallo volgende tabel beschrijft de eigenschappen in Hallo hierboven JSON:</span><span class="sxs-lookup"><span data-stu-id="288c8-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="288c8-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="288c8-138">Property</span></span> | <span data-ttu-id="288c8-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288c8-139">Description</span></span> | <span data-ttu-id="288c8-140">Vereist</span><span class="sxs-lookup"><span data-stu-id="288c8-140">Required</span></span> | <span data-ttu-id="288c8-141">Standaard</span><span class="sxs-lookup"><span data-stu-id="288c8-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="288c8-142">naam</span><span class="sxs-lookup"><span data-stu-id="288c8-142">name</span></span> |<span data-ttu-id="288c8-143">Naam van het Hallo-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="288c8-143">Name of hello dataset.</span></span> <span data-ttu-id="288c8-144">Zie [Azure Data Factory - naamgevingsregels](data-factory-naming-rules.md) voor naamgevingsregels.</span><span class="sxs-lookup"><span data-stu-id="288c8-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="288c8-145">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-145">Yes</span></span> |<span data-ttu-id="288c8-146">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-146">NA</span></span> |
| <span data-ttu-id="288c8-147">type</span><span class="sxs-lookup"><span data-stu-id="288c8-147">type</span></span> |<span data-ttu-id="288c8-148">Type Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="288c8-148">Type of hello dataset.</span></span> <span data-ttu-id="288c8-149">Geef een Hallo die worden ondersteund door de Data Factory (bijvoorbeeld: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="288c8-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="288c8-150">Zie voor meer informatie [gegevensettype](#Type).</span><span class="sxs-lookup"><span data-stu-id="288c8-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="288c8-151">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-151">Yes</span></span> |<span data-ttu-id="288c8-152">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-152">NA</span></span> |
| <span data-ttu-id="288c8-153">structuur</span><span class="sxs-lookup"><span data-stu-id="288c8-153">structure</span></span> |<span data-ttu-id="288c8-154">Schema van Hallo dataset.</span><span class="sxs-lookup"><span data-stu-id="288c8-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="288c8-155">Zie voor meer informatie [gegevenssetstructuur](#Structure).</span><span class="sxs-lookup"><span data-stu-id="288c8-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="288c8-156">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-156">No</span></span> |<span data-ttu-id="288c8-157">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-157">NA</span></span> |
| <span data-ttu-id="288c8-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="288c8-158">typeProperties</span></span> | <span data-ttu-id="288c8-159">Hallo-eigenschappen zijn verschillend voor elk type (bijvoorbeeld: Azure Blob, Azure SQL-tabel).</span><span class="sxs-lookup"><span data-stu-id="288c8-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="288c8-160">Zie voor informatie over de typen Hallo ondersteund en hun eigenschappen, [gegevensettype](#Type).</span><span class="sxs-lookup"><span data-stu-id="288c8-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="288c8-161">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-161">Yes</span></span> |<span data-ttu-id="288c8-162">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-162">NA</span></span> |
| <span data-ttu-id="288c8-163">external</span><span class="sxs-lookup"><span data-stu-id="288c8-163">external</span></span> | <span data-ttu-id="288c8-164">Booleaanse waarde vlag toospecify of een gegevensset wordt expliciet geproduceerd door een data factory-pijplijn of niet.</span><span class="sxs-lookup"><span data-stu-id="288c8-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="288c8-165">Als het Hallo-invoergegevensset voor een activiteit wordt niet door de huidige pipeline Hallo geproduceerd, stelt u deze vlag tootrue.</span><span class="sxs-lookup"><span data-stu-id="288c8-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="288c8-166">Deze vlag tootrue voor invoergegevensset van de eerste activiteit Hallo Hallo in Hallo pijplijn instellen.</span><span class="sxs-lookup"><span data-stu-id="288c8-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="288c8-167">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-167">No</span></span> |<span data-ttu-id="288c8-168">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="288c8-168">false</span></span> |
| <span data-ttu-id="288c8-169">availability</span><span class="sxs-lookup"><span data-stu-id="288c8-169">availability</span></span> | <span data-ttu-id="288c8-170">Hallo venster verwerken (bijvoorbeeld per uur of dagelijks) of model voor Hallo gegevensset productie segmentering Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="288c8-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="288c8-171">Elke eenheid gegevens verbruikt en die wordt geproduceerd door het uitvoeren van een activiteit wordt een gegevenssegment genoemd.</span><span class="sxs-lookup"><span data-stu-id="288c8-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="288c8-172">Als een uitvoergegevensset Hallo beschikbaarheid is set toodaily (frequentie - dag, interval - 1), wordt dagelijks een segment geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="288c8-173">Zie voor meer informatie [gegevensset beschikbaarheid](#Availability).</span><span class="sxs-lookup"><span data-stu-id="288c8-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="288c8-174">Zie voor informatie over Hallo gegevensset segmentering model Hallo [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="288c8-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="288c8-175">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-175">Yes</span></span> |<span data-ttu-id="288c8-176">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-176">NA</span></span> |
| <span data-ttu-id="288c8-177">policy</span><span class="sxs-lookup"><span data-stu-id="288c8-177">policy</span></span> |<span data-ttu-id="288c8-178">Definieert Hallo criteria of Hallo voorwaarde waaraan Hallo gegevensset segmenten moeten voldoen.</span><span class="sxs-lookup"><span data-stu-id="288c8-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="288c8-179">Zie voor meer informatie, Hallo [gegevensset beleid](#Policy) sectie.</span><span class="sxs-lookup"><span data-stu-id="288c8-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="288c8-180">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-180">No</span></span> |<span data-ttu-id="288c8-181">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="288c8-182">Voorbeeld van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="288c8-182">Dataset example</span></span>
<span data-ttu-id="288c8-183">In Hallo voorbeeld te volgen, Hallo gegevensset vertegenwoordigt een tabel met de naam **MyTable** in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="288c8-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="288c8-184">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="288c8-184">Note hello following points:</span></span>

* <span data-ttu-id="288c8-185">**type** tooAzureSqlTable is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="288c8-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="288c8-186">**tableName** tooMyTable is ingesteld door de eigenschap type (specifieke tooAzureSqlTable type).</span><span class="sxs-lookup"><span data-stu-id="288c8-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="288c8-187">**linkedServiceName** tooa gekoppelde service van het type AzureSqlDatabase die is gedefinieerd in de volgende JSON-codefragment Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="288c8-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="288c8-188">**beschikbaarheid frequentie** tooDay, is ingesteld en **interval** too1 is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="288c8-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="288c8-189">Dit betekent dat Hallo gegevensset segment dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="288c8-190">**AzureSqlLinkedService** wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="288c8-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="288c8-191">In Hallo voorafgaand aan JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="288c8-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="288c8-192">**type** tooAzureSqlDatabase is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="288c8-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="288c8-193">**connectionString** type-eigenschap geeft u informatie tooconnect tooa SQL-database.</span><span class="sxs-lookup"><span data-stu-id="288c8-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="288c8-194">Zoals u ziet, hello gekoppelde service definieert hoe tooconnect tooa SQL-database.</span><span class="sxs-lookup"><span data-stu-id="288c8-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="288c8-195">Hallo gegevensset definieert welke tabel wordt gebruikt als invoer en uitvoer van activiteit in een pijplijn Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="288c8-196">Tenzij een gegevensset wordt geproduceerd door de pijplijn hello, moet dit worden gemarkeerd als **externe**.</span><span class="sxs-lookup"><span data-stu-id="288c8-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="288c8-197">Deze instelling geldt doorgaans tooinputs van de eerste activiteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="288c8-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="288c8-198"><a name="Type"></a>Gegevensettype</span><span class="sxs-lookup"><span data-stu-id="288c8-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="288c8-199">Hallo type Hallo dataset is afhankelijk van Hallo-gegevensarchief die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="288c8-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="288c8-200">Zie Hallo volgende tabel voor een lijst met opgeslagen gegevens die door Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="288c8-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="288c8-201">Klik op een data store toolearn hoe toocreate een gekoppelde service en een gegevensset voor dat de gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="288c8-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="288c8-202">Gegevens worden opgeslagen met * on-premises kan worden of op Azure-infrastructuur als een service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="288c8-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="288c8-203">Deze gegevensarchieven moeten u tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="288c8-204">In voorbeeld in de vorige sectie Hallo HALLO hallo type Hallo gegevensset te is ingesteld**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="288c8-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="288c8-205">Op deze manier voor een Azure Blob-gegevensset Hallo type Hallo dataset is ingesteld te**AzureBlob**, zoals weergegeven in de volgende JSON Hallo:</span><span class="sxs-lookup"><span data-stu-id="288c8-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

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

## <span data-ttu-id="288c8-206"><a name="Structure"></a>Structuur van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="288c8-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="288c8-207">Hallo **structuur** sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="288c8-207">hello **structure** section is optional.</span></span> <span data-ttu-id="288c8-208">Hallo-schema van Hallo gegevensset wordt gedefinieerd door dat een verzameling van namen en gegevenstypen van de kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="288c8-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="288c8-209">U Hallo structuur sectie tooprovide type informatie die is gebruikt tooconvert typen en kaart kolommen uit Hallo bron toohello doel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="288c8-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="288c8-210">Hallo voorbeeld te volgen, Hallo gegevensset heeft drie kolommen: `slicetimestamp`, `projectname`, en `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="288c8-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="288c8-211">Zijn van het type String, String en Decimal, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="288c8-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="288c8-212">Elke kolom in het Hallo-structuur bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="288c8-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="288c8-213">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="288c8-213">Property</span></span> | <span data-ttu-id="288c8-214">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288c8-214">Description</span></span> | <span data-ttu-id="288c8-215">Vereist</span><span class="sxs-lookup"><span data-stu-id="288c8-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="288c8-216">naam</span><span class="sxs-lookup"><span data-stu-id="288c8-216">name</span></span> |<span data-ttu-id="288c8-217">Naam van het Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="288c8-217">Name of hello column.</span></span> |<span data-ttu-id="288c8-218">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-218">Yes</span></span> |
| <span data-ttu-id="288c8-219">type</span><span class="sxs-lookup"><span data-stu-id="288c8-219">type</span></span> |<span data-ttu-id="288c8-220">Het gegevenstype van kolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-220">Data type of hello column.</span></span>  |<span data-ttu-id="288c8-221">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-221">No</span></span> |
| <span data-ttu-id="288c8-222">Cultuur</span><span class="sxs-lookup"><span data-stu-id="288c8-222">culture</span></span> |<span data-ttu-id="288c8-223">. NET-gebaseerde cultuur toobe gebruikt wanneer Hallo type een .NET-type is: `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="288c8-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="288c8-224">Hallo standaardwaarde is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="288c8-224">hello default is `en-us`.</span></span> |<span data-ttu-id="288c8-225">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-225">No</span></span> |
| <span data-ttu-id="288c8-226">Indeling</span><span class="sxs-lookup"><span data-stu-id="288c8-226">format</span></span> |<span data-ttu-id="288c8-227">Indeling van tekenreeks toobe gebruikt wanneer Hallo type een .NET-type is: `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="288c8-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="288c8-228">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-228">No</span></span> |

<span data-ttu-id="288c8-229">Hallo volgende richtlijnen te bepalen wanneer tooinclude structuur, gegevens en welke tooinclude in Hallo **structuur** sectie.</span><span class="sxs-lookup"><span data-stu-id="288c8-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="288c8-230">**Voor gestructureerde gegevensbronnen**, Hallo structuur sectie alleen opgeven als u wilt toewijzen bronkolommen kolommen toosink en hun namen zijn niet dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="288c8-231">Dit soort gegevensbron gestructureerde slaat schema en het type informatie samen met de Hallo gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="288c8-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="288c8-232">Voorbeelden van gestructureerde gegevensbronnen zijn SQL Server, Oracle en Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="288c8-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="288c8-233">Als het type informatie is al beschikbaar voor gestructureerde gegevensbronnen, moet u type-informatie niet opnemen wanneer u Hallo structuur sectie opneemt.</span><span class="sxs-lookup"><span data-stu-id="288c8-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="288c8-234">**Voor schema op lezen gegevensbronnen (specifiek Blob-opslag)**, kunt u toostore gegevens zonder schema of het type informatie met Hallo gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="288c8-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="288c8-235">Voor deze typen gegevensbronnen, structuur opnemen wanneer u wilt dat toomap bron kolommen toosink kolommen.</span><span class="sxs-lookup"><span data-stu-id="288c8-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="288c8-236">Structuur wordt ook toevoegen wanneer Hallo gegevensset de invoer voor een kopieeractiviteit vormt en gegevenstypen van de bron-gegevensset geconverteerde toonative typen voor Hallo sink moet.</span><span class="sxs-lookup"><span data-stu-id="288c8-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="288c8-237">Data Factory ondersteunt Hallo waarden voor het ontwikkelen van type-informatie in de structuur te volgen: **Int16, Int32, Int64, Single, Double, Decimal, Byte [], Booleaanse waarde, String, Guid, Datetime, Datetimeoffset en Timespan**.</span><span class="sxs-lookup"><span data-stu-id="288c8-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="288c8-238">Deze waarden zijn Common Language Specification (CLS)-compatibel zijn,. NET-type op basis van waarden.</span><span class="sxs-lookup"><span data-stu-id="288c8-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="288c8-239">Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een brongegevens tooa sink data store opslaan.</span><span class="sxs-lookup"><span data-stu-id="288c8-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="288c8-240">Beschikbaarheid van gegevensset</span><span class="sxs-lookup"><span data-stu-id="288c8-240">Dataset availability</span></span>
<span data-ttu-id="288c8-241">Hallo **beschikbaarheid** onderdeel in een gegevensset gedefinieerd Hallo verwerking venster (bijvoorbeeld elk uur, dagelijks of wekelijks) voor het Hallo-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="288c8-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="288c8-242">Zie voor meer informatie over windows activiteit [planning en uitvoering](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="288c8-243">Hallo beschikbaarheidssectie na bepaalt dat hello uitvoergegevensset wordt ofwel geproduceerd per uur, of het Hallo invoergegevensset per uur beschikbaar is:</span><span class="sxs-lookup"><span data-stu-id="288c8-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="288c8-244">Als Hallo pipeline Hallo begin- en eindtijden te volgen heeft:</span><span class="sxs-lookup"><span data-stu-id="288c8-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="288c8-245">Hallo uitvoergegevensset wordt geproduceerd per uur binnen Hallo pijplijn start- en eindtijd.</span><span class="sxs-lookup"><span data-stu-id="288c8-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="288c8-246">Er zijn daarom vijf gegevensset gegevenssegmenten geproduceerd door deze pipeline, één voor elke activiteitvenster (12: 00 A.M. - 1 uur, 01: 00 - 2 uur, 2 uur - 3 uur, 3 uur - 4 AM, 4 uur - 5 uur).</span><span class="sxs-lookup"><span data-stu-id="288c8-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="288c8-247">Hallo beschrijft volgende tabel eigenschappen die u in de sectie beschikbaarheid Hallo gebruiken kunt:</span><span class="sxs-lookup"><span data-stu-id="288c8-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="288c8-248">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="288c8-248">Property</span></span> | <span data-ttu-id="288c8-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288c8-249">Description</span></span> | <span data-ttu-id="288c8-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="288c8-250">Required</span></span> | <span data-ttu-id="288c8-251">Standaard</span><span class="sxs-lookup"><span data-stu-id="288c8-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="288c8-252">frequency</span><span class="sxs-lookup"><span data-stu-id="288c8-252">frequency</span></span> |<span data-ttu-id="288c8-253">Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.</span><span class="sxs-lookup"><span data-stu-id="288c8-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="288c8-254"><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand</span><span class="sxs-lookup"><span data-stu-id="288c8-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="288c8-255">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-255">Yes</span></span> |<span data-ttu-id="288c8-256">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-256">NA</span></span> |
| <span data-ttu-id="288c8-257">interval</span><span class="sxs-lookup"><span data-stu-id="288c8-257">interval</span></span> |<span data-ttu-id="288c8-258">Hiermee geeft u een vermenigvuldiger voor de frequentie.</span><span class="sxs-lookup"><span data-stu-id="288c8-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="288c8-259">"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="288c8-260">Bijvoorbeeld, als u moet de gegevensset toobe gesegmenteerd op uurbasis hello, u stelt <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="288c8-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="288c8-261">Houd er rekening mee dat als u opgeeft **frequentie** als **minuut**, moet u Hallo interval toono kleiner is dan 15 instellen.</span><span class="sxs-lookup"><span data-stu-id="288c8-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="288c8-262">Ja</span><span class="sxs-lookup"><span data-stu-id="288c8-262">Yes</span></span> |<span data-ttu-id="288c8-263">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-263">NA</span></span> |
| <span data-ttu-id="288c8-264">stijl</span><span class="sxs-lookup"><span data-stu-id="288c8-264">style</span></span> |<span data-ttu-id="288c8-265">Hiermee geeft u op of Hallo segment moet worden geproduceerd op Hallo begin of einde van hello-interval.</span><span class="sxs-lookup"><span data-stu-id="288c8-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="288c8-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="288c8-266">StartOfInterval</span></span></li><li><span data-ttu-id="288c8-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="288c8-267">EndOfInterval</span></span></li></ul><span data-ttu-id="288c8-268">Als **frequentie** te is ingesteld,**maand**, en **stijl** te is ingesteld,**EndOfInterval**, op Hallo laatste dag van de maand Hallo segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="288c8-269">Als **stijl** te is ingesteld,**StartOfInterval**, Hallo segment eerste dag van de maand op Hallo wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="288c8-270">Als **frequentie** te is ingesteld,**dag**, en **stijl** te is ingesteld,**EndOfInterval**, in Hallo afgelopen uur van de dag Hallo Hallo segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="288c8-271">Als **frequentie** te is ingesteld,**uur**, en **stijl** te is ingesteld,**EndOfInterval**, Hallo segment wordt geproduceerd achter Hallo Hallo uur.</span><span class="sxs-lookup"><span data-stu-id="288c8-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="288c8-272">Voor een segment voor 1-2 uur periode Hallo Hallo segment geproduceerd om 2 uur.</span><span class="sxs-lookup"><span data-stu-id="288c8-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="288c8-273">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-273">No</span></span> |<span data-ttu-id="288c8-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="288c8-274">EndOfInterval</span></span> |
| <span data-ttu-id="288c8-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="288c8-275">anchorDateTime</span></span> |<span data-ttu-id="288c8-276">Hallo absolute positie in de tijd die wordt gebruikt door Hallo scheduler toocompute gegevensset segmentgrenzen definieert.</span><span class="sxs-lookup"><span data-stu-id="288c8-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="288c8-277">Let op: als deze propoerty bevat de datumonderdelen die zijn meer granulair Hallo opgegeven frequentie, Hallo gedetailleerdere onderdelen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="288c8-278">Bijvoorbeeld, als hello **interval** is **per uur** (frequentie: uur en interval: 1), en Hallo **anchorDateTime** bevat **minuten en seconden**, vervolgens Hallo minuten en seconden delen van **anchorDateTime** worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="288c8-279">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-279">No</span></span> |<span data-ttu-id="288c8-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="288c8-280">01/01/0001</span></span> |
| <span data-ttu-id="288c8-281">offset</span><span class="sxs-lookup"><span data-stu-id="288c8-281">offset</span></span> |<span data-ttu-id="288c8-282">TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="288c8-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="288c8-283">Houd er rekening mee dat als beide **anchorDateTime** en **offset** zijn opgegeven, Hallo resultaat Hallo gecombineerd shift is.</span><span class="sxs-lookup"><span data-stu-id="288c8-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="288c8-284">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-284">No</span></span> |<span data-ttu-id="288c8-285">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="288c8-286">offset voorbeeld</span><span class="sxs-lookup"><span data-stu-id="288c8-286">offset example</span></span>
<span data-ttu-id="288c8-287">Standaard dagelijks (`"frequency": "Day", "interval": 1`) segmenten beginnen bij 12: 00 A.M. (middernacht) Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="288c8-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="288c8-288">Als u Hallo start tijd toobe 06: 00 UTC-tijd in plaats daarvan wilt, stelt u Hallo zoals weergegeven in het volgende codefragment Hallo offset:</span><span class="sxs-lookup"><span data-stu-id="288c8-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="288c8-289">Voorbeeld van anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="288c8-289">anchorDateTime example</span></span>
<span data-ttu-id="288c8-290">In de Hallo voorbeeld te volgen, wordt de elke 23 uur in Hallo gegevensset wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="288c8-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="288c8-291">Hallo eerste cirkelsegment begint bij Hallo tijd die is opgegeven door **anchorDateTime**, die is ingesteld te`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="288c8-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="288c8-292">Voorbeeld van de offset/style</span><span class="sxs-lookup"><span data-stu-id="288c8-292">offset/style example</span></span>
<span data-ttu-id="288c8-293">Hallo volgende gegevensset is maandelijks, en op Hallo wordt geproduceerd 3rd van elke maand om 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="288c8-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="288c8-294"><a name="Policy"></a>DataSet beleid</span><span class="sxs-lookup"><span data-stu-id="288c8-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="288c8-295">Hallo **beleid** sectie in de definitie van de gegevensset Hallo Hallo criteria bepaalt of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="288c8-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="288c8-296">Van validatiebeleid</span><span class="sxs-lookup"><span data-stu-id="288c8-296">Validation policies</span></span>
| <span data-ttu-id="288c8-297">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="288c8-297">Policy name</span></span> | <span data-ttu-id="288c8-298">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288c8-298">Description</span></span> | <span data-ttu-id="288c8-299">Te worden toegepast</span><span class="sxs-lookup"><span data-stu-id="288c8-299">Applied too</span></span>| <span data-ttu-id="288c8-300">Vereist</span><span class="sxs-lookup"><span data-stu-id="288c8-300">Required</span></span> | <span data-ttu-id="288c8-301">Standaard</span><span class="sxs-lookup"><span data-stu-id="288c8-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="288c8-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="288c8-302">minimumSizeMB</span></span> |<span data-ttu-id="288c8-303">Valideert dat gegevens Hallo in **Azure Blob storage** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="288c8-304">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="288c8-304">Azure Blob storage</span></span> |<span data-ttu-id="288c8-305">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-305">No</span></span> |<span data-ttu-id="288c8-306">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-306">NA</span></span> |
| <span data-ttu-id="288c8-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="288c8-307">minimumRows</span></span> |<span data-ttu-id="288c8-308">Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="288c8-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="288c8-309">Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="288c8-309">Azure SQL database</span></span></li><li><span data-ttu-id="288c8-310">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="288c8-310">Azure table</span></span></li></ul> |<span data-ttu-id="288c8-311">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-311">No</span></span> |<span data-ttu-id="288c8-312">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="288c8-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="288c8-313">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="288c8-313">Examples</span></span>
<span data-ttu-id="288c8-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="288c8-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="288c8-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="288c8-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="288c8-316">Externe gegevenssets</span><span class="sxs-lookup"><span data-stu-id="288c8-316">External datasets</span></span>
<span data-ttu-id="288c8-317">Externe gegevenssets zijn Hallo waarden die niet worden geproduceerd door een actieve pijplijn in Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="288c8-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="288c8-318">Als Hallo dataset is gemarkeerd als **externe**, Hallo **ExternalData** beleid mogelijk gedefinieerde tooinfluence Hallo gedrag van Hallo gegevensset segment beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="288c8-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="288c8-319">Tenzij een gegevensset wordt geproduceerd door Data Factory, moet dit worden gemarkeerd als **externe**.</span><span class="sxs-lookup"><span data-stu-id="288c8-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="288c8-320">Deze instelling geldt doorgaans toohello input van de eerste activiteit in een pijplijn, tenzij activiteit of koppeling van de pijplijn wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="288c8-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="288c8-321">Naam</span><span class="sxs-lookup"><span data-stu-id="288c8-321">Name</span></span> | <span data-ttu-id="288c8-322">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="288c8-322">Description</span></span> | <span data-ttu-id="288c8-323">Vereist</span><span class="sxs-lookup"><span data-stu-id="288c8-323">Required</span></span> | <span data-ttu-id="288c8-324">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="288c8-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="288c8-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="288c8-325">dataDelay</span></span> |<span data-ttu-id="288c8-326">Hallo tijd toodelay Hallo controleren op Hallo beschikbaarheid van de externe gegevens Hallo voor Hallo gegeven segment.</span><span class="sxs-lookup"><span data-stu-id="288c8-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="288c8-327">Bijvoorbeeld, kunt u een controle per uur uitstellen met deze instelling.</span><span class="sxs-lookup"><span data-stu-id="288c8-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="288c8-328">Hallo-instelling is alleen van toepassing toohello huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="288c8-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="288c8-329">Bijvoorbeeld, als het is nu om 13:00 uur en deze waarde 10 minuten is, Hallo validatie wordt gestart om 1:10 uur.</span><span class="sxs-lookup"><span data-stu-id="288c8-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="288c8-330">Houd er rekening mee dat deze instelling heeft geen invloed op segmenten in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="288c8-331">Segmenten met **segment eindtijd** + **dataDelay** < **nu** zonder enige vertraging worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="288c8-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="288c8-332">Tijden groter is dan 23:59 uur moeten worden opgegeven met behulp van Hallo `day.hours:minutes:seconds` indeling.</span><span class="sxs-lookup"><span data-stu-id="288c8-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="288c8-333">Gebruik geen 24:00:00 bijvoorbeeld toospecify 24 uur.</span><span class="sxs-lookup"><span data-stu-id="288c8-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="288c8-334">Gebruik in plaats daarvan 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="288c8-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="288c8-335">Als u 24:00:00, wordt dit beschouwd als 24 dagen (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="288c8-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="288c8-336">Geef 1:04:00:00 voor 1 dag en 4 uur.</span><span class="sxs-lookup"><span data-stu-id="288c8-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="288c8-337">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-337">No</span></span> |<span data-ttu-id="288c8-338">0</span><span class="sxs-lookup"><span data-stu-id="288c8-338">0</span></span> |
| <span data-ttu-id="288c8-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="288c8-339">retryInterval</span></span> |<span data-ttu-id="288c8-340">Hallo wachttijd tussen een fout en Hallo opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="288c8-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="288c8-341">Deze instelling geldt toopresent tijd.</span><span class="sxs-lookup"><span data-stu-id="288c8-341">This setting applies toopresent time.</span></span> <span data-ttu-id="288c8-342">Als de vorige probeer Hallo is mislukt, Hallo volgende probeer is na Hallo **retryInterval** periode.</span><span class="sxs-lookup"><span data-stu-id="288c8-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="288c8-343">Als het nu om 13:00 uur, beginnen we de eerste poging Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="288c8-344">Als Hallo duur toocomplete Hallo eerste validatiecontrole 1 minuut Hallo-bewerking is mislukt is, een nieuwe poging gedaan Hallo is 1:00 + 1 min (duur) + 1 min. (interval voor opnieuw proberen) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="288c8-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="288c8-345">Er is geen vertraging segmenten in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="288c8-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="288c8-346">Hallo opnieuw gebeurt onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="288c8-346">hello retry happens immediately.</span></span> |<span data-ttu-id="288c8-347">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-347">No</span></span> |<span data-ttu-id="288c8-348">00:01:00 (1 minuut)</span><span class="sxs-lookup"><span data-stu-id="288c8-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="288c8-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="288c8-349">retryTimeout</span></span> |<span data-ttu-id="288c8-350">Hallo-out voor nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="288c8-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="288c8-351">Als deze eigenschap is ingesteld too10 minuten, Hallo validatie moet worden voltooid binnen 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="288c8-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="288c8-352">Als het duurt langer dan 10 minuten tooperform Hallo validatie, probeer Hallo time-out.</span><span class="sxs-lookup"><span data-stu-id="288c8-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="288c8-353">Als alle pogingen voor validatie time-out Hallo Hallo segment is gemarkeerd als **time-out**.</span><span class="sxs-lookup"><span data-stu-id="288c8-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="288c8-354">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-354">No</span></span> |<span data-ttu-id="288c8-355">00:10:00 (10 minuten)</span><span class="sxs-lookup"><span data-stu-id="288c8-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="288c8-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="288c8-356">maximumRetry</span></span> |<span data-ttu-id="288c8-357">Hallo aantal keren dat toocheck voor beschikbaarheid Hallo Hallo externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="288c8-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="288c8-358">Hallo maximaal toegestane waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="288c8-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="288c8-359">Nee</span><span class="sxs-lookup"><span data-stu-id="288c8-359">No</span></span> |<span data-ttu-id="288c8-360">3</span><span class="sxs-lookup"><span data-stu-id="288c8-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="288c8-361">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="288c8-361">Create datasets</span></span>
<span data-ttu-id="288c8-362">U kunt de gegevenssets maken met behulp van een van deze hulpprogramma's of de SDK's:</span><span class="sxs-lookup"><span data-stu-id="288c8-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="288c8-363">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="288c8-363">Copy Wizard</span></span> 
- <span data-ttu-id="288c8-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="288c8-364">Azure portal</span></span>
- <span data-ttu-id="288c8-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="288c8-365">Visual Studio</span></span>
- <span data-ttu-id="288c8-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="288c8-366">PowerShell</span></span>
- <span data-ttu-id="288c8-367">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="288c8-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="288c8-368">REST API</span><span class="sxs-lookup"><span data-stu-id="288c8-368">REST API</span></span>
- <span data-ttu-id="288c8-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="288c8-369">.NET API</span></span>

<span data-ttu-id="288c8-370">Zie Hallo-zelfstudies voor stapsgewijze instructies voor het maken van de pijplijnen en gegevenssets met behulp van een van deze hulpprogramma's of de SDK's te volgen:</span><span class="sxs-lookup"><span data-stu-id="288c8-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="288c8-371">Een pijplijn met een transformatieactiviteit voor gegevens bouwen</span><span class="sxs-lookup"><span data-stu-id="288c8-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="288c8-372">Maken van een pijplijn met een activiteit van de verplaatsing van gegevens</span><span class="sxs-lookup"><span data-stu-id="288c8-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="288c8-373">Nadat een pijplijn is gemaakt en geïmplementeerd, kunt u beheren en bewaken van uw pijplijnen met behulp van hello Azure portal-blades of Hallo-app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="288c8-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="288c8-374">Zie de volgende onderwerpen voor stapsgewijze instructies Hallo:</span><span class="sxs-lookup"><span data-stu-id="288c8-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="288c8-375">Bewaken en beheren van pijplijnen via Azure portal-blades</span><span class="sxs-lookup"><span data-stu-id="288c8-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="288c8-376">Bewaken en beheren van pijplijnen met Hallo-app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="288c8-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="288c8-377">Bereik gegevenssets</span><span class="sxs-lookup"><span data-stu-id="288c8-377">Scoped datasets</span></span>
<span data-ttu-id="288c8-378">Kunt u gegevenssets die zich binnen het bereik tooa pijplijn met Hallo **gegevenssets** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="288c8-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="288c8-379">Deze gegevenssets kan alleen worden gebruikt door activiteiten binnen deze pipeline, niet door de activiteiten in andere pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="288c8-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="288c8-380">Hallo volgende voorbeeld definieert een pijplijn met twee gegevenssets (InputDataset rdc en OutputDataset rdc) toobe binnen Hallo pijplijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="288c8-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="288c8-381">Bereik gegevenssets worden alleen ondersteund voor eenmalige pijplijnen (waarbij **pipelineMode** te is ingesteld,**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="288c8-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="288c8-382">Zie [Onetime pijplijn](data-factory-create-pipelines.md#onetime-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="288c8-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="288c8-383">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="288c8-383">Next steps</span></span>
- <span data-ttu-id="288c8-384">Zie voor meer informatie over pijplijnen [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="288c8-385">Zie voor meer informatie over hoe pijplijnen worden gepland en uitgevoerd, [planning en uitvoering in Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="288c8-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
